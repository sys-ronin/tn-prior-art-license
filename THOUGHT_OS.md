===============================================================================
                             THOUGHT OS
            An Environment Where Thinking Is the Only Interface
===============================================================================

===============================================================================
                                OVERVIEW
===============================================================================

This document describes a different way of understanding Terminal Notes.

Not as an application.
Not as a tool.
Not as software at all.

But as an environment—a space where thinking happens,
and the only thing visible is what you're thinking about.

The computer becomes a peripheral.
The terminal becomes a window.
The mind remains the center.

This is not a claim.
This is an observation.
The system exists. This describes what it is.

===============================================================================
                          THE OPERATING SYSTEM ANALOGY
===============================================================================

Every computer has an operating system.
It manages hardware. It runs programs. It provides interfaces.

Thought OS does the same—for thought.

┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│  Traditional OS                   Thought OS                                │
│  ───────────────────────          ───────────────────────                   │
│  Hard Disk Drive                  Git (storage through time)                │
│  File System                      JSON (organization)                       │
│  Directory structure              Notebook hierarchy (UUID-addressed)       │
│  Inodes                           UUIDs (permanent identity)                │
│  RAM                              Navigation stack (working memory)         │
│  Process scheduler                Command parser (intention router)         │
│  Kernel                           Core logic (UUID permanence)              │
│  System calls                     Single-key commands (c,v,e,d,j,s,t,a,b,q)│
│  File handles                     UUID references                           │
│  Journaling filesystem            Atomic writes (.tmp → rename)             │
│  File system repair               Git fsck / recovery system                │
│  Recycle bin                      Soft delete (searchable in history)       │
│  Secure erase                     Hard delete with filter-repo              │
│  System restore                   Timeline reconstruction                   │
│  Crash recovery                   Autosave + UUID-keyed recovery            │
│  Remote desktop                   SSH access                                │
│  Portable apps                    Docker deployment                         │
│  Display                          Terminal (the invisible window)           │
│  Multi-user support               Filesystem isolation + SSH users          │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

Each component maps because the functions are the same.
The implementation differs. The purpose does not.

===============================================================================
                    WHERE TECHNOLOGY AND THOUGHT MEET
===============================================================================

At the boundary between the terminal and the mind,
something interesting happens.

The terminal presents:
- Numbers: [1] [2] [3]
- Letters: C V D S J T A B Q
- A cursor: >

The mind interprets:
- Numbers as locations ("that thing I was just looking at")
- Letters as intentions ("I want to create something new")
- The cursor as readiness ("I can write now")

NO TRANSLATION LAYER:

The mind does not think:
    "I need to press the key that corresponds to the create command"
It thinks:
    "I want to create something"
And the finger presses 'c'.

The gap between intention and action is one keystroke.
That is the entire interface.

NO ABSTRACTION:

The numbers on the screen ARE the items.
Not representations of the items. The items themselves.
When you press 'v1', you are not "selecting item number one".
You are reaching for the thing itself.

This is not metaphor.
This is how the system is built.
The data IS the interface.
The numbers ARE the commands.

===============================================================================
                            GIT AS STORAGE THROUGH TIME
===============================================================================

A hard disk stores files.
Git stores changes through time.

In Thought OS, Git serves as the permanent storage layer.

WHAT IT PROVIDES:
- Every state preserved forever
- Any point in time retrievable
- Deleted items still accessible
- Complete history without overhead
- Parent/root UUIDs in every commit
- Structured messages: "CREATED NOTE: title | in notebook"

WHY THIS MATTERS:

Human memory is temporal.
We remember not just what, but when.
Git provides that dimension for digital thought.

A NOTE FROM TODAY AND A NOTE FROM LAST YEAR
are equally present. Time is not a barrier.
It is a dimension of the storage itself.

WHEN YOU SEARCH:
    s deleted* meeting
Git returns UUIDs from commits containing "DELETED" and "meeting".
The system reconstructs those items.
They appear alongside current items.
No distinction. No hierarchy. All writing is equally present.

This is not a feature.
This is how memory works.

===============================================================================
                            JSON AS ORGANIZATION
===============================================================================

A file system organizes data into hierarchies.
Directories contain files. Files contain content.

In Thought OS, JSON files provide this organization.

THE THREE-FILE ARCHITECTURE:

structure.json
    The hierarchy. Notebooks inside notebooks.
    UUIDs as identifiers. Parent-child as relationships.
    No content. Pure structure. Pure relationship.

notes.json
    Content for regular thoughts.
    UUID-keyed for direct access.
    Plain text. Human-readable. Forever accessible.

files.json
    Content for code, data, anything structured.
    UUID-keyed with extension tracking (80+ formats).
    Preserves syntax context for editing.

WHY THIS MATTERS:

JSON is not a proprietary format.
It is text. It will be readable as long as text exists.
The organization of your thoughts outlives any software.

THE THREE-FILE SEPARATION WAS NOT DESIGNED FOR GIT.
It was designed for clarity.
Git happened to work perfectly with it.
This is not foresight. This is luck from building cleanly.

===============================================================================
                            UUID AS PERMANENT IDENTITY
===============================================================================

In file systems, inodes identify files permanently.
A file can be renamed, moved, linked—
the inode remains, tracking the content through changes.

In Thought OS, UUIDs serve this function.

WHAT IT PROVIDES:
- Every item receives an ID at creation
- That ID never changes
- Renames don't affect it
- Moves don't affect it
- Deletions don't erase it from history
- Parent UUIDs track lineage
- Root UUIDs track origin

WHY THIS MATTERS:

You can find something by what it was,
even if its name changed.
You can track an idea across its entire lifetime,
even if you moved it, renamed it, or forgot about it.

Identity is permanent. Only location changes.

WHEN YOU RESTORE A DELETED ITEM:
The system finds its UUID in Git history.
Extracts its content from the commit before deletion.
Places it back in its original location (parent UUID).
The UUID never changed. The item never really left.
It was just waiting to be found.

===============================================================================
                            STACK AS WORKING MEMORY
===============================================================================

RAM holds what you're actively working on.
It is fast, ephemeral, and limited.

In Thought OS, the navigation stack serves this function.

WHAT IT PROVIDES:
- Current location always known
- Session history preserved
- Back navigation without thinking
- Jump back to previous contexts (jb)
- O(1) access to any visible location (j1/j2/j3)

WHY THIS MATTERS:

You don't need to remember where you've been.
The system remembers for you.
You can focus on where you're going.

THE STACK IS INVISIBLE:
You never see it. You never manage it.
You just press 'b' and you're back where you were.
Like memory, it works until you think about it.

===============================================================================
                            COMMANDS AS INTENTIONS
===============================================================================

System calls translate user intentions into kernel operations.
They are few, consistent, and well-defined.

In Thought OS, single-key commands serve this function.

THE COMMAND SET:

c (create)     → bring a new thought into existence
v (view)       → examine a thought
e (edit)       → refine a thought
d (delete)     → remove from current view
r (rename)     → change a thought's name
j (jump)       → move to another location (j1/j2/j3/jb)
s (search)     → find across all time (with type/action filters)
t (timeline)   → see how a thought evolved
a (activity)   → see all changes across the system
x (export)     → extract a file note to the filesystem
b (back)       → return to previous context
q (quit)       → leave the environment

WHY THIS MATTERS:

Each command maps directly to an intention.
No menus to navigate. No modes to remember.
The gap between thinking and doing is one keystroke.

Commands become reflexes.
Reflexes become automatic.
The interface disappears.

===============================================================================
                            SEARCH AS REMEMBERING
===============================================================================

Search is not a feature.
Search is how memory works when you can't quite recall.

THE SYNTAX EMERGED FROM USAGE:
    s meeting              → find everything about meetings
    s .py                  → find all Python files
    s deleted* old-project → find deleted items about old-project
    s file* config         → find all config files
    s created* note* today → find notes created today

ANY ORDER:
    s deleted* note* meeting
    s note* deleted* meeting
    s meeting note* deleted*

All produce the same result.
The parser does not care about order.
It extracts what it recognizes and searches for the rest.

WHAT IT FINDS:
- Current items (live search)
- Deleted items (reconstructed from Git)
- Renamed items (UUID-tracked across name changes)

All merged. All deduplicated by UUID. All sorted by date.
All presented as one list. No indication of state.
Deleted items appear alongside current items.
Because in memory, they are the same.

THIS IS NOT A DESIGN DECISION:
This is what happened when building for personal use.
The distinction between "current" and "deleted" never mattered.
Why should the software care?
It doesn't. It just shows what you're looking for.

===============================================================================
                            ACTIVITY AS TEMPORAL AWARENESS
===============================================================================

Activity view shows what changed, when, and where.

IMPLEMENTATION:
    git log --all --grep <uuid_pattern> --pretty=format:"%H|%ai|%s|%b"

Results aggregated across all notebooks or a single notebook tree.
Sorted chronologically. Paginated. Displayed with smart paths.

Each entry shows:
- Action (created, updated, deleted, renamed, restored)
- Type (note, file, sub)
- Title (truncated intelligently)
- Location (smart path: .../parent/child)

WHY IT EXISTS:
Sometimes you don't know what you're looking for.
You just know something changed.
Activity view shows you what you might have missed.

It is not a log.
It is not an audit trail.
It is temporal awareness.
Like glancing at a calendar to see what day it is.

===============================================================================
                            TIMELINE AS MEMORY
===============================================================================

Human memory is not a single snapshot.
It is a continuous record, accessible at any point.

In Thought OS, timeline provides this access.

WHAT IT PROVIDES:
- Every version of every item
- Complete hierarchy at each point
- Read-only access to past states
- Export capability for historical versions
- Recursive reconstruction for subnotebooks

IMPLEMENTATION:
    git log --grep uuid:<UUID> --all --pretty=format:"%H|%ai|%s"

Each commit where the item changed becomes a selectable version.
Selected version is reconstructed in a temporary directory.
Full hierarchy is preserved. Nothing is lost.

WHY THIS MATTERS:

You can see how your thinking evolved.
What you thought then. How it changed.
The path from idea to understanding becomes visible.

TIMELINE IS SEPARATE FROM SEARCH:
- Search finds existence across states
- Timeline shows evolution across time
- Both use the same Git database
- Both are separate because memory has two modes

===============================================================================
                            RESURRECTION AS REGENERATION
===============================================================================

When an item is deleted, it is not destroyed.
It is moved to history. Still there. Still findable.

WHEN YOU FIND A DELETED ITEM:
Press 'r'. The system asks where to put it.
Default: its original location (from parent UUID in commit).
It reappears. Same UUID. Same content. Same history.
The deletion never happened.

FOR SUBNOTEBOOKS:
The entire hierarchy comes back.
All nested notes. All nested files. All nested subnotebooks.
One key press. Everything restored.

IMPLEMENTATION:
    def _collect_all_uuids(notebook):
        # Recursively collects UUIDs of notebook, all notes, all subs
        # Enables filtered content merge from Git history

    def _atomic_filtered_merge(temp_path, live_path, allowed_uuids):
        # Merges only UUIDs that belong to the restored item
        # Atomic write: .tmp → rename

This is not magic.
This is UUIDs + Git + careful merging.
The system knows what belongs together because the data knows.

===============================================================================
                            ERASURE AS CHOICE
===============================================================================

Sometimes forgetting is not enough.
Sometimes you need something truly gone.

TWO KINDS OF DELETE:

SOFT DELETE (forget):
    Removes from current view.
    Remains in Git history.
    Still findable via search.
    Restorable with one key.

HARD DELETE (erase):
    Removes from Git history entirely.
    Uses git-filter-repo to rewrite history.
    Requires confirmation and typing "erase".
    Irreversible. Final.

THE IMPLEMENTATION:
    import git_filter_repo  # Dynamic loading via importlib
    git_filter_repo.main()  # Programmatic execution

    # Filter-repo rewrites history, removing all traces of UUID
    # Then item is removed from current view
    # Git garbage collection cleans up

WHY BOTH EXIST:
Because human memory has two modes too.
Things you've forgotten but could recall.
Things you wish you'd never known.

The system does not decide which is which.
You do.

===============================================================================
                            CRASH RECOVERY AS RESILIENCE
===============================================================================

Systems fail. Editors crash. Power goes out.
Human work should not disappear with them.

THE MECHANISM:
    External editor sessions spawn background autosave thread.
    Every 30 seconds, temp file content saved to:
        .recovery/{note_title}_{uuid[-6:]}.{ext}

    On notebook access, recovery system checks for orphaned files.
    If found and newer than last saved state, content is restored.

    Restoration integrates content, commits to Git, cleans recovery file.

UUID KEYING:
    Recovery files are keyed by UUID, not title.
    Even if you renamed the note, recovery finds it.
    Even if you moved it to another notebook, recovery finds it.

WHY THIS MATTERS:
You never think about saving.
The system assumes your work matters.
It protects without asking.

===============================================================================
                            CONFIGURATION AS PREFERENCE
===============================================================================

First launch creates config.json:

    {
      "edit": "micro",
      "view": "micro",
      "info": "Available: micro, nvim, vim, hx, helix, emacs -nw, nano"
    }

The user can change this file at any time.
No settings menu. No preferences dialog.
Just a text file. Edit it with any editor.

THE SYSTEM DOES NOT CARE:
It reads the file. It uses whatever editor is specified.
If the editor doesn't exist, it falls back to sensible defaults.
The user is in control. The system just follows.

WHY THIS EXISTS:
Because preferences are personal.
The system should not have opinions about your editor.
It should just use what you tell it to use.

===============================================================================
                            CONTAINERIZATION AS PORTABILITY
===============================================================================

Your environment should move with you.
Between machines. Between servers. Between years.

DOCKER PROVIDES:
    - One-command deployment anywhere
    - No dependency installation
    - Isolated, consistent environment
    - Easy backup and migration

MULTI-USER SUPPORT:
    /data/
    ├── user1/notebooks_root/
    ├── user2/notebooks_root/
    └── user3/notebooks_root/

Each user connects via SSH with their own credentials.
Each has their own notebook directory.
The same code serves everyone.
UUIDs ensure no cross-user contamination.

WHY THIS WORKS:
The application never knew about users.
It just reads/writes to ./notebooks_root.
The environment (symlink + directory structure) directs each user to their space.
Multi-user emerged from single-user design.
This is not foresight. This is clean boundaries.

===============================================================================
                    THE TERMINAL AS COGNITIVE SPACE
===============================================================================

The terminal is not a user interface.
It is a cognitive space.

CHARACTERISTICS:

NO VISUAL NOISE
    Only what matters is present.
    No icons. No toolbars. No notifications.
    No flashing. No animations. No movement.

NO COMPETING ELEMENTS
    The cursor and your words.
    Nothing else demands attention.
    The screen is static until you change it.

NO HIDDEN MODES
    Everything you can do is visible when relevant.
    Commands appear in the footer. Numbers on items.
    You never need to remember "how do I...".

NO LEARNING CURVE
    Commands map to intentions.
    Your brain already knows what you want to do.
    'c' is create. 'v' is view. 'd' is delete.

NO INTERRUPTION
    No notifications. No updates. No popups.
    The system waits for you, not the other way around.

NO STATE AWARENESS
    You never need to know "current vs deleted".
    The system handles that. You just search.
    Deleted items appear alongside current items.
    Because in your memory, they are the same.

THIS IS NOT MINIMALISM:

This is cognitive hygiene.
A clean space for thought.
Nothing enters except what you invite.
Nothing distracts except what you allow.

THE TERMINAL DISAPPEARS:

When you're writing, you don't see the terminal.
You see your words. You see your thoughts.
The medium becomes invisible.
Only the message remains.

Users don't think "I am in a terminal."
They think "I am writing."

That is the entire point.

===============================================================================
                    WHAT THE USER ACTUALLY EXPERIENCES
===============================================================================

The user sits down.
They see:

> 

They type:

> s meeting

They see:

[1] updated note: meeting-notes (work)
[2] created file: agenda.md (work/ideas)
[3] deleted note: old-meeting (archive)

They press:

> v1

They see their note.
They read. They maybe edit. They press 'b' to go back.
They press 'q' to leave.

THAT IS THE ENTIRE EXPERIENCE.

The user never sees:
- UUIDs
- Git commits
- JSON structure
- Atomic writes
- Recovery files
- The navigation stack
- Any of the complexity described in this document

THE COMPLEXITY IS HIDDEN:
Not by design. By necessity.
The system cannot show complexity.
The terminal has no room for it.
Only the essentials fit on screen.
Everything else must be invisible.

This is not a feature.
This is a constraint that became a virtue.

===============================================================================
                            WHAT EMERGES
===============================================================================

When all these layers work together,
something emerges that none alone provides:

A SPACE WHERE:
- Thoughts persist forever (Git)
- Nothing is ever truly lost (restore)
- Everything is findable by meaning (search)
- Time is visible and navigable (timeline, activity)
- Identity is permanent (UUIDs)
- Location is flexible (jump, stack)
- Deletion is reversible (soft delete)
- Erasure is possible when needed (hard delete)
- Crashes don't destroy work (recovery)
- Your environment travels with you (SSH, Docker)
- Multi-user works without design (filesystem isolation)
- The interface disappears (terminal)
- Only the writing remains

THE USER EXPERIENCES:
    None of this directly.
    Just a blinking cursor.
    Just their words.
    Just writing.

THE SYSTEM DISAPPEARS:
    Not because it's simple.
    Because it's aligned.
    Because it doesn't compete for attention.
    Because it only exists when called upon.

===============================================================================
                            WHAT THIS ASKS OF YOU
===============================================================================

Nothing.

No configuration.
No learning.
No accounts.
No subscriptions.
No tracking.
No cloud.
No trust.

Just write.

The system does not ask you to understand it.
It does not ask you to configure it.
It does not ask you to maintain it.
It just works. Until you need it to do something else.
Then you press a key. It does that thing. Then it disappears again.

===============================================================================
                            WHAT THIS GIVES YOU
===============================================================================

A space where:

YOUR THOUGHTS PERSIST
    Not because they're saved.
    Because they were never at risk.

NOTHING IS EVER TRULY LOST
    Deleted items are just hidden.
    One key press brings them back.

EVERYTHING IS FINDABLE
    Search by text, type, action, or any combination.
    Results include deleted items. Because why wouldn't they?

TIME IS VISIBLE
    Activity shows what changed.
    Timeline shows how it evolved.
    The past is present when you need it.

THE INTERFACE DISAPPEARS
    You don't think about the system.
    You think about what you're writing.

ONLY THE WRITING REMAINS

===============================================================================
                            A NOTE ON FRAMING
===============================================================================

This document describes Thought OS as a way of understanding.
Not as a claim. Not as a novel invention.

The components are existing tools:
- Python (1991)
- Git (2005)
- JSON (2001)
- Terminal (1960s)
- SSH (1995)
- Docker (2013)

The insight is in the composition.
The way these tools work together.
The way they disappear when used.
The way they serve thought rather than demand it.

This is not a new operating system.
It is a new way of thinking about what an operating system can be.

THE HUMBLE POSITION:

This document does not claim:
- "We designed for cognition"
- "We are innovative"
- "We are the best"

It observes:
- The system exists
- This is how it works
- This is what emerged
- This might be useful to understand

The claims are not claims.
They are descriptions of what exists.

===============================================================================
                            CONCLUSION
===============================================================================

Thought OS is not an application.
It is an environment.

Git provides storage through time.
JSON provides organization.
UUIDs provide permanent identity.
The stack provides working memory.
Commands provide intention mapping.
Search provides remembering.
Activity provides temporal awareness.
Timeline provides memory depth.
Restore provides regeneration.
Soft delete provides forgetting.
Hard delete provides choice.
Recovery provides resilience.
SSH provides presence.
Docker provides portability.
The terminal provides an invisible window.

All connected. All hidden. All serving one purpose:

A space where you can think,
and never think about the space.

The terminal is dark.
The cursor blinks.
You write.

That is the entire point.

===============================================================================
END OF DOCUMENT
===============================================================================
