# Comparative Analysis: Terminal Notes vs. Contemporary Note‑Taking Applications (April 2026)

## 1. Introduction

This document compares Terminal Notes against twelve widely used note‑taking and knowledge management applications. The analysis focuses on features fundamental to a writing environment: permanence, versioning, encryption, portability, deployment flexibility, and cognitive alignment.

Data for other applications is drawn from official documentation, release notes, and authoritative third‑party sources as of April 2026. Terminal Notes is described as implemented in the source code of this repository.

This is an observational document. It records what exists. It does not advertise. It does not claim superiority. It simply presents a comparison based on publicly available information.

---

## 2. Feature Comparison Matrix

| Feature | Terminal Notes | Notion | Apple Notes | Evernote | Google Keep | OneNote | Obsidian | Standard Notes | Joplin | Notesnook | SimpleNote | AppFlowy | SiYuan |
|---------|----------------|--------|-------------|----------|-------------|---------|----------|----------------|--------|-----------|-----------|----------|--------|
| **Data Permanence** |
| Permanent item identifier | ✓ (UUID) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Deleted items recoverable | ✓ (forever) | 30‑day trash | 30‑day trash | 30‑day trash | N/A | Limited | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Resurrection from history | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **Versioning & History** |
| Item‑level timeline | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Activity view across hierarchy | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Git as primary storage | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Change statistics per edit | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **Encryption & Security** |
| End‑to‑end encryption | ✓ (AES-256-GCM) | ✗ (in‑transit only) | ✗ (on‑device) | ✗ (in‑transit) | ✗ | ✗ (in‑transit) | ✗ | ✓ (XChaCha20-Poly1305) | ✓ (AES-256) | ✓ (XChaCha20-Poly1305) | ✗ | ✗ | ✗ |
| Hardware‑bound keys | ✓ (system fingerprint) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Dual‑factor (password + phrase) | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Lock button flushes memory | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Permanent erasure with audit | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Recovery phrase (never stored) | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Password change without re-encryption | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **Portability & Deployment** |
| Single‑folder portable | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| No installation required | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (minimal) | ✗ | ✗ |
| Runs from USB / external drive | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Docker / container support | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ |
| Self‑hosting | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ | ✓ | ✓ | ✗ | ✓ | ✓ |
| Notebook import from any location | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Notebook creation in any location | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **Sync & Backup** |
| Free encrypted sync | ✓ (via Git remote) | ✗ | ✗ | ✗ | ✗ | ✗ | Limited | ✗ | ✗ (cloud required) | ✗ (subscription) | ✓ | ✗ | ✗ |
| Public repo safe (encrypted) | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Per‑notebook backup | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **Interface & Experience** |
| Terminal UI | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Data as UI (numbers as commands) | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Fish‑eye path navigation | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Jump navigation (j1, j2, jb) | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| No app name / branding | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Zero configuration | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **Search** |
| Action filters (created*, deleted*) | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Type filters (note*, file*, sub*) | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Time filters (today*, yesterday*, thisweek*) | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Date range (date* DD‑MM‑YYYY) | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Order‑free query | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Semantic / natural language search | ✗ | ✓ | ✓ (iOS 26) | ✓ (v11) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **Hierarchy** |
| Infinite subnotebook depth | ✓ | ✓ | ✓ | ✓ | ✗ | ✓ | ✗ | ✗ | ✓ | ✓ | ✗ | ✓ | ✓ |
| Recursive activity view | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Path display with truncation | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **Data Integrity** |
| Atomic writes | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Crash recovery | ✓ | ✗ | ✗ | ✗ | ✗ | ✓ (iOS 2026) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Autosave | ✓ (every 30s) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Other** |
| Mobile app | ✗ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Web clipper | ✗ | ✗ | ✗ | ✓ | ✗ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| AI features | ✗ | ✓ (Custom Agents) | ✓ (AI Search) | ✓ (AI Assistant) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Prior art disclosures | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |

---

## 3. Detailed Analysis

### 3.1 Data Permanence and Resurrection

**Terminal Notes** implements UUID‑based identification. Each item receives a permanent identifier at creation. Deleted items remain in Git history and can be restored. The resurrection engine reconstructs items from historical commits.

**Other surveyed applications**:
- Notion, Apple Notes, Evernote, and OneNote provide trash bins with retention periods (typically 30 days).
- Standard Notes does not offer recovery for deleted notes.
- Obsidian's file‑level versioning depends on external Git plugins; resurrection is not a built‑in feature.
- Joplin 3.6.3 added a delete revisions API, but this is intended for API use, not user‑facing resurrection with full content recovery.

### 3.2 Versioning and History

**Terminal Notes** provides per‑item timeline showing commits affecting a note, with change statistics (+X/-Y) for each edit. Activity view aggregates changes across a notebook and all its descendants.

**Other surveyed applications**:
- Notion offers revision history but not per‑item granular change statistics.
- Obsidian's versioning depends on external Git plugins without integrated change statistics.
- No surveyed application provides hierarchical activity view across subnotebooks.

### 3.3 Encryption and Security

**Terminal Notes** uses AES‑256‑GCM. Keys are derived from password and folder name. Keys are stored encrypted with a system‑specific hardware fingerprint. The lock button clears keys from memory and unloads notebook structure. Password changes do not require re‑encrypting the notebook. Recovery phrases (6, 8, 12, 24 words, or user‑provided text) are not stored. Dual‑factor (password + phrase) is required for decryption.

**Other surveyed applications**:
- **Standard Notes** uses XChaCha20‑Poly1305 with PBKDF2. Keys are not hardware‑bound. Recovery requires a paid subscription.
- **Joplin** supports AES‑256 end‑to‑end encryption, but local data is not encrypted at rest; documentation recommends disk encryption.
- **Notesnook** uses XChaCha20‑Poly1305 with Argon2. Local encryption requires a Pro subscription.
- **Bitwarden** (password manager, not a note app) increased minimum PBKDF2 iterations to 600,000 and added item archiving. It does not offer hardware binding or phrase recovery.
- **1Password** uses AES‑256 with PBKDF2 and a Secret Key. The Secret Key is required daily, not only for recovery.

None of these applications implement hardware‑bound keys, dual‑factor with redundant recovery (password OR phrase), password change without re‑encryption, or a lock button that explicitly flushes memory.

### 3.4 Portability and Deployment

**Terminal Notes** runs from a single folder. No installation is required. Dependencies (cryptography libraries) are bundled. The application runs on any platform with Python, including Docker, Raspberry Pi, and USB drives. Notebooks can be imported from or created in any accessible filesystem location. A single executable output (via PyInstaller) includes all dependencies.

**Other surveyed applications**:
- **Simplenote** is free and cross‑platform but requires installation.
- **Joplin** offers self‑hosting via Nextcloud, WebDAV, Dropbox, or FTP, but requires installation and configuration.
- **AppFlowy** and **SiYuan** support Docker self‑hosting but not single‑folder portability.
- **Obsidian** supports third‑party sync but requires installation and configuration.

None of these applications offer single‑folder portability with bundled dependencies, no installation requirement, and the ability to import or create notebooks in any user‑chosen location.

### 3.5 Search Capabilities

**Terminal Notes** supports:
- Action wildcards: `created*`, `deleted*`, `updated*`, `renamed*`, `restored*`, `erased*`
- Type wildcards: `note*`, `file*`, `sub*`
- Time filters: `today*`, `yesterday*`, `thisweek*`, `lastweek*`
- Date ranges: `date* DD‑MM‑YYYY`
- Scope filters: `in*`, `g*`
- Order‑free query composition

**Other surveyed applications**:
- **Notion** offers natural language AI search via Custom Agents.
- **Apple Notes** added AI‑powered natural language search in iOS 26.
- **Evernote v11** introduced semantic search.

None of these applications offer action‑based, type‑based, or time‑based filters combined with order‑free syntax.

### 3.6 User Interface and Cognitive Load

**Terminal Notes** aims to minimize cognitive load through:
- Numbers on displayed items, commands on numbers
- All available commands visible in footer
- Path truncation to 4‑7 segments
- Jump navigation by position (`j1`, `j2`, `jb`)
- No modal dialogs
- No application name or branding in the interface

**Other surveyed applications**:
- **Apple Notes** introduced an Adaptive Toolbar in iOS 26 that shows relevant tools based on context.
- **Obsidian** offers distraction‑free mode and supports networked thinking.

None of these applications combine spatial navigation, fish‑eye path display, jump navigation, visible commands, and zero branding into a single integrated interface.

---

## 4. Feature Summary

The following capabilities are present in Terminal Notes and not observed in the surveyed applications:

| Capability | Description |
|------------|-------------|
| UUID permanence | Items retain identity across renames, moves, deletions, and restorations |
| Resurrection | Deleted items remain searchable and restorable indefinitely |
| Per‑item timeline | Complete history of each note with change statistics |
| Hierarchical activity view | Changes across a notebook and all descendants |
| Git as primary storage | Every change is a commit; Git acts as a temporal database |
| Hardware‑bound encryption | Keys tied to machine fingerprint |
| Dual‑factor (password + phrase) | Both required for decryption; phrase not stored |
| Lock button as memory flush | Explicit key clearing and structure unloading |
| Password change without re‑encryption | Instant, regardless of notebook size |
| Recovery phrase only | Works on any machine; no cloud, email, or central authority |
| Data as UI | Numbers on data; commands on numbers |
| Portable folder | Single folder, no installation, bundled dependencies |
| Notebook import from any location | Import from any accessible filesystem path |
| Notebook creation in any location | Create in any user‑chosen directory |
| Search with action, type, time filters | Order‑free query language |
| Fish‑eye path navigation | Always shows 4‑7 segments |
| No app name / branding | Application does not announce itself |
| Atomic writes | Guarantee of no file corruption |
| Prior art disclosures | Concepts published to prevent patenting |

---

## 5. Deployment Flexibility

| Deployment Method | Terminal Notes | Other Applications |
|-------------------|----------------|---------------------|
| Run from USB drive | Yes (single folder, no installation) | No (installation required) |
| Run from any filesystem location | Yes (any path, any drive) | No (installation‑dependent) |
| Docker container | Yes (multi‑user, SSH, three modes) | AppFlowy, SiYuan only |
| Raspberry Pi / ARM | Yes (Python everywhere) | Limited |
| Network share / NAS | Yes (copy folder, run) | No |
| Multiple copies on same machine | Yes (isolated folders) | No (single installation) |

**Notebook import from any location**: Terminal Notes can import notebooks from any filesystem path, including USB drives, network shares, cloud‑synced folders, and external drives.

**Notebook creation in any location**: When creating a new notebook, the user can choose any directory. The notebook is created as a self‑contained folder.

---

## 6. Cognitive Alignment

The following alignments with established cognitive principles were observed in Terminal Notes:

| Principle | Implementation |
|-----------|----------------|
| **Spatial memory** (Tversky, 1992) | Relative numbers, not absolute paths; jump navigation by position |
| **Working memory** (Miller, 1956) | Fish‑eye path display shows 4‑7 segments |
| **Recognition over recall** (Norman, 1988) | All commands visible in footer |
| **Affordance** (Gibson, 1979) | Numbers invite pressing; commands invite typing |
| **Progressive disclosure** (Norman, 1988) | Basic navigation first; advanced discovered through use |
| **Fish‑eye view** (Furnas, 1986) | Context + focus display with truncated ancestors |
| **Cognitive load** (Sweller, 1988) | No path memorization; no command recall |
| **Flow** (Csikszentmihalyi, 1990) | Navigation becomes automatic; interface does not interrupt |

These principles were not consulted during development. They were identified afterward.

---

## 7. GDPR Compliance

Terminal Notes exhibits the following compliance characteristics:

| Article | Requirement | Status |
|---------|-------------|--------|
| **5(1)(a)** | Lawfulness, fairness, transparency | No telemetry, no tracking |
| **5(1)(b)** | Purpose limitation | Only purpose: store notes |
| **5(1)(c)** | Data minimization | Only note content and timestamps |
| **5(1)(f)** | Integrity and confidentiality | AES-256-GCM, hardware binding |
| **17** | Right to erasure | Hard delete with git-filter-repo |
| **20** | Right to portability | JSON format, copy folder |
| **32** | Security of processing | AES-256-GCM, no network |
| **33** | Breach notification | Not applicable (no servers, no breach possible) |
| **35** | DPIA | Not applicable (no high-risk processing) |

The application contains no analytics code, no network transmission code, and no server components.

---

## 8. Conclusion

Terminal Notes implements a set of features that distinguish it from the surveyed applications. These include UUID‑based permanence, resurrection from history, per‑item timeline, hierarchical activity view, Git as primary storage, hardware‑bound encryption, dual‑factor authentication, instant password changes, phrase recovery without cloud, data‑as‑UI, portable folder deployment, flexible notebook import/creation, advanced search filters, fish‑eye path navigation, and zero branding.

The surveyed applications excel in areas such as mobile experience, collaboration, AI assistance, and task management. Terminal Notes does not implement these features.

The comparison is based on publicly available information as of April 2026. Feature availability may change.

---

**Document Date:** April 2026  
**Repository:** github.com/sys-ronin/terminal-notes
sys_ronin
