# Encryption System Documentation

## Overview

The Terminal Notes encryption system is built on AES-256-GCM with per-notebook keys derived from a user password and the notebook folder name. Keys are stored permanently on the local machine using hardware-bound encryption, enabling password-less unlocking on the same system while maintaining security across machines.

All encrypted data includes a magic header (`TN_ENC`) for immediate verification. The system is fully transparent: reading and writing JSON files automatically encrypts or decrypts when a crypto key is provided.

## Key Derivation

Each notebook gets its own unique encryption key derived from two inputs:

- **User password** – supplied by the user when creating an encrypted notebook.
- **Folder name** – the actual name of the notebook folder on disk (e.g., `"my-notes-20260323120000"`).

The derivation uses:

```
key = SHA-256(password + ":" + folder_name)
```

This ties the key to both the password and the exact folder name. **Renaming the folder will break decryption** – a warning is shown during creation.

## Encryption Algorithm

- **Cipher**: AES-256-GCM (Galois/Counter Mode with authentication)
- **Key size**: 256 bits
- **Nonce**: 12 random bytes (generated per encryption)
- **Authentication**: Integrated, prevents tampering

The encryption process:

1. Prepend the magic header `b"TN_ENC"` to the plaintext.
2. Generate a random 12‑byte nonce.
3. Encrypt with AES-256-GCM, producing ciphertext.
4. Return `nonce + ciphertext`.

Decryption:

1. Split the first 12 bytes as nonce.
2. Decrypt the remainder.
3. Verify that the plaintext starts with `b"TN_ENC"`.
4. Remove the header and decode to UTF-8.

If the magic header is missing, decryption raises an error – this immediately detects wrong keys or corrupted data.

## Permanent Key Storage

Keys are stored permanently in the `config/.session_storage.enc` file. This file is encrypted with a key derived from the machine’s hardware fingerprint (system UUID, DMI product UUID, etc.), making it impossible to copy keys to another computer.

The storage class `SecureSessionStorage` provides:

- `store_session_key(folder_name, crypto)` – saves the key after verifying it works.
- `retrieve_session_key(folder_name)` – retrieves the key if it exists and passes verification.
- `remove_session_key(folder_name)` – removes the key (used when unregistering a notebook).

Key retrieval includes a verification step: the stored key is used to encrypt and decrypt a test string. If the test fails, the key is considered invalid and removed.

## Integration with File Operations

All JSON file reads and writes go through two central functions in `notebook_operations.py`:

- `read_json(filepath, crypto=None)` – reads a file, decrypts if crypto is provided, and returns the parsed dictionary.
- `write_json(filepath, data, crypto=None)` – writes a dictionary as JSON, encrypts if crypto is provided, and performs an atomic rename.

This design ensures that encryption is transparent: code that handles notebooks never needs to know whether a file is encrypted.

## Integration with Git History

Git stores encrypted files as binary blobs. When reading historical versions (e.g., via `git show`), the same crypto key is used to decrypt the content because the key depends only on the password and the folder name – both remain constant across commits.

The `TimelineEngine` and `GitHistoryMiner` therefore accept a `crypto` parameter and use `read_json`/`read_bytes` to reconstruct historical items.

## Lock/Unlock Mechanism

A notebook’s lock state is tracked both in memory and in the registry.

- **Locked**: The notebook object has `custom_path = None` and `_crypto = None`. The registry entry has `locked = True`.
- **Unlocked**: The notebook object has `custom_path` set and `_crypto` holds the key. The registry entry has `locked = False`.

When the user presses the lock button:

- **If locked**: The app prompts for the password, derives the key, decrypts the registry entry to obtain the actual folder path, loads the notebook, updates the registry to `locked=False`, and keeps the key in memory.
- **If unlocked**: The app clears the in‑memory key and `custom_path`, updates the registry to `locked=True`, and removes the key from the session.

**The key is never stored in permanent storage unless the user explicitly unlocks.** After the first successful unlock, the key is stored permanently so that future restarts can auto‑load unlocked notebooks, but the lock button always asks for a password again (security boundary).

## Registry Encryption

The registry file (`notebooks_registry.json`) stores metadata for each notebook. For encrypted notebooks, the entry is encrypted using the notebook’s own crypto key and stored as a hex‑encoded string. This means the registry cannot be read without the key.

However, to locate the notebook folder before unlocking, the registry entry must be decryptable. Therefore the unlock flow first prompts for the password, derives the key, and then decrypts the entry to obtain the path. This ensures that even if the notebook is in a custom location, the correct folder is found.

## Security Considerations

- **Password never stored** – only the derived key is stored, encrypted with the hardware fingerprint.
- **Keys are hardware‑bound** – they cannot be used on another machine.
- **Folder name is part of the key** – renaming a notebook folder makes it inaccessible.
- **Magic header prevents accidental decryption** – wrong keys fail instantly.
- **Atomic file writes** – temporary file + rename prevents corruption.
- **Keys cleared from memory on lock** – no lingering keys after locking.

## Usage Examples

### Creating an encrypted notebook

```python
notebook = manager.create_notebook("My Notes", encrypt=True)
# user is prompted for password
```

### Unlocking a notebook (from the UI)

```python
# UI calls lock handler, which prompts for password, derives key,
# decrypts registry, finds path, loads notebook.
```

### Reading an encrypted JSON file

```python
data = read_json("structure.json", crypto)
```

### Writing an encrypted JSON file

```python
write_json("notes.json", notes_map, crypto)
```

### Retrieving a stored key

```python
crypto = Crypto.retrieve_for_folder("my-notes-20260323120000")
```

### Storing a key permanently

```python
crypto = Crypto(password, folder_name)
# the constructor automatically calls _store_key_permanently()
```

## Summary

The encryption system is built on industry‑standard AES‑256‑GCM with a unique design that ties keys to the notebook folder name and stores them permanently using hardware‑derived encryption. All file operations are unified through `read_json`/`write_json`, making encryption transparent to the rest of the application. The lock/unlock mechanism provides explicit control, and the registry is encrypted to protect metadata.
