# Data Safety Architecture

## Overview

This document describes how the system ensures data is never lost, never corrupted, and always recoverable. It covers encryption in memory before writing, atomic file operations, the separation of keys from data, portability of notebooks and the application itself, and the permanent erasure mechanism. The design prioritises safety over convenience, explicitness over automation, and verifiability over opacity.

---

## 1. Encryption in Memory Before Write

### 1.1 When Encryption Happens

Encryption occurs only at the moment of writing to disk. Data is held in memory as plaintext while the user is working. This is necessary because the user needs to read and edit the content. The key is also held in memory while the notebook is unlocked.

When a note is edited:

1. The note content is in memory as plaintext.
2. The user saves. The content is written to a temporary file.
3. The temporary file is encrypted using the notebook's key.
4. The encrypted temporary file is renamed to the final file.

The key is cleared from memory when the notebook is locked. The content is cleared from memory when the notebook is locked or when the application exits.

### 1.2 Why Not Encrypt in Memory

Encrypting in memory would require keeping the encrypted data alongside the plaintext or re‑encrypting on every access. It would add complexity without adding safety. The threat model assumes that if an attacker has access to memory, they also have access to the key. Keeping the key in memory is the necessary risk. The lock button is the explicit control to clear that risk when the notebook is not in use.

---

## 2. Atomic Writes

### 2.1 The Problem

Writing directly to a file risks partial writes. If the system crashes during the write, the file may be left half‑written, corrupted, or empty. This is unacceptable for data that must never be lost.

### 2.2 The Solution

Every JSON file is written using an atomic pattern:

1. Write to a temporary file in the same directory (`file.json.tmp`).
2. Call `os.fsync()` to force the data to disk.
3. Rename the temporary file to the final name (`file.json`).

On Unix systems, rename is atomic. If the system crashes during the write, the temporary file may be incomplete, but the original file remains untouched. If the system crashes during the rename, the file either has the old content or the new content. There is no intermediate state.

This pattern is used for `structure.json`, `notes.json`, `files.json`, the registry, and the session storage.

### 2.3 Recovery

After a crash, the system starts with the files as they were before the interrupted write. No recovery action is needed. The temporary files are left behind and are ignored.

---

## 3. Separation of Keys from Data

### 3.1 Where Keys Are Stored

Keys are stored in `config/.session_storage.enc`. This file is encrypted with a key derived from the machine's hardware fingerprint. It is separate from the notebooks themselves.

### 3.2 Why Separate

If a notebook folder is copied to another machine, the keys do not go with it. The encrypted data is useless without the key. The key must be re‑entered on the new machine. This is intentional. It prevents unauthorised decryption of copied data.

If the session storage is lost, the keys are lost. The encrypted notebooks become unreadable unless the user re‑enters the passwords. This is a trade‑off: convenience on one machine, security across machines.

### 3.3 Portability of Notebooks

A notebook folder can be copied, moved, or synced to any location. It contains only encrypted data. The key is not inside. The folder can be backed up, shared, or stored in the cloud without exposing the content.

To open the notebook on another machine, the user must enter the password. The key is derived again and stored on the new machine. The notebook travels. The keys do not.

---

## 4. Application Portability

### 4.1 No Installation

The application is distributed as a folder. It contains:

- The Python source or compiled executable.
- The `assets` folder with bundled cryptography and cffi.
- A `config.json` for user preferences.

The user copies the folder. It runs. No installation. No registry entries. No system dependencies beyond Python and Git (which are widely available).

### 4.2 Data Location

All user data is stored inside the same folder:

- `config/` – session storage, system fingerprint, Git accounts.
- `notebooks_root/` – notebooks and registry.
- `.recovery/` – recovery files from unsaved edits.

The entire folder can be backed up by copying it. It can be moved to another machine and run. The user's notebooks and settings move with it. The only thing that does not move is the session storage, which is tied to the machine's hardware. This is by design.

### 4.3 No External Dependencies

The application bundles its own cryptography and cffi. It does not require the user to install them. It does not require internet to install them. It does not require root or admin privileges. It runs from the folder. It is portable.

---

## 5. Permanent Erasure with git‑filter‑repo

### 5.1 Two‑Tier Deletion

- **Forget (soft delete).** The item is removed from the current view. The Git history remains. The item can be restored.
- **Erase (hard delete).** The item is removed from Git history. It cannot be restored. A tombstone commit remains to mark the erasure.

### 5.2 How Erasure Works

The system uses a customised version of `git-filter-repo`, imported as a module, not called as a subprocess.

For a single item:

1. The system finds all commits that mention the UUID.
2. It runs `UUIDEraseFilter`, which removes those commits and strips the UUID from file content.
3. It adds a tombstone commit with `type: ERASED`.

For an entire notebook:

1. The system collects all UUIDs in the notebook and its descendants.
2. It runs `NotebookEraseFilter`, which removes every commit that mentions any of those UUIDs.
3. It deletes the notebook folder.

The erasure is irreversible. The user must confirm by typing "erase" before the operation proceeds.

### 5.3 Why git‑filter‑repo Is Embedded

The tool is embedded as a module so that it can be extended with custom filters and called programmatically. The system does not rely on the user having it installed. It does not spawn a subprocess. The erasure is integrated into the application, not a separate script.

---

## 6. Recovery from Crash

### 6.1 During Editing

When an external editor is open, a background thread saves the content every 30 seconds to a recovery file. The recovery file is named with the note's UUID and title. It is stored in `.recovery/` inside the application folder.

If the editor crashes, the system closes, or the machine loses power, the recovery file remains.

### 6.2 On Next Open

When the notebook is opened, the system scans `.recovery/` for files matching the UUIDs of notes in the notebook. For each match:

- If the note exists, the recovery content is compared to the saved content. If newer, it is restored.
- If the note does not exist, the recovery content is used to create a new note.

The recovery file is deleted after restoration. The user does not need to know that recovery happened.

---

## 7. Integrity Checks

### 7.1 Registry

The registry is the source of truth for which notebooks exist and where they are located. It is encrypted for encrypted notebooks. The system checks on startup that the paths in the registry exist. If a path is missing, the notebook is marked as missing but not removed. The user can later re‑import it.

### 7.2 Session Storage

The session storage file is encrypted with the machine's fingerprint. On startup, the system attempts to decrypt it. If decryption fails (different machine or corrupted file), the system starts with an empty session storage. The user must re‑enter passwords.

### 7.3 Notebook Structure

Each notebook's `structure.json` is read on unlock. If it is corrupted (unreadable JSON or missing UUIDs), the notebook cannot be unlocked. The user must restore from backup or Git history.

---

## 8. Design Principles

- **Atomicity.** Every write is atomic. No partial writes. No corruption.
- **Separation.** Keys are separate from data. Notebooks are portable. Keys are not.
- **Explicitness.** The lock button is explicit. Erasure requires confirmation. Recovery is silent but present.
- **Verifiability.** The registry is the source of truth. Git is the history. The user can inspect both.
- **Portability.** The application runs from a folder. Notebooks run from a folder. No installation. No system dependencies.

---

## 9. Limitations

- **No automatic backup.** The system does not back up data. The user must copy the folder.
- **No conflict resolution.** If the same notebook is modified in two locations, manual merge is required.
- **Keys are single‑machine.** Moving notebooks to another machine requires re‑entering passwords.
- **Erasure is irreversible.** Once erased, data cannot be recovered. The user confirms.
- **Git required for history.** Without Git, resurrection, timeline, and activity are disabled. The core remains.

---

## 10. Summary

Data is encrypted only when written to disk. Writes are atomic. Keys are stored separately from notebooks. Notebooks are portable; keys are not. The application is portable; it runs from a folder with no installation. Deleted items are soft‑deleted (restorable) or hard‑erased (with tombstone) using an embedded `git-filter-repo`. Recovery from crash is automatic. The system does not lose data unless the user explicitly erases it. It does not corrupt data. It does not require external tools. It is designed for safety, portability, and verifiability.
