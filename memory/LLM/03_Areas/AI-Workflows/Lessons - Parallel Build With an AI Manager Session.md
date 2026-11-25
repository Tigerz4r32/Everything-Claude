---
type: note
status: active
created: 2026-11-25
tags: [ai, agent, automation]
---

# Lessons - Parallel Build With an AI Manager Session

How a module for an internal web app was built in about a day by many Claude sessions at once, and what went wrong along the way.

## How it was run
- **Plan in Opus, build in Sonnet, hard parts in Opus.** Opus wrote a task list with files and a done-test per task. Sonnet did the mechanical tasks (S0–S15); Opus did the hard ones at the end (O1–O6: AI scan loop, validation and citations, clarification, competitor discovery, estimator, release).
- **One manager session.** An Opus session started each task in its own session, then checked the result itself: read the changes, ran the tests, made sure the task stayed in its own files. Only the manager ticked the task list and edited shared files.
- **Waves.** Tasks that did not depend on each other ran together, 3 to 4 at a time.
- **Git worktrees.** Each parallel task got its own copy of the project (`<project>-wt\<task>`) and its own branch, so builds never clashed. The manager merged each branch after checking it.

## What went wrong, and the rule that came out of it
| Problem | Rule |
|---|---|
| Two tasks each wrote their own catalogue file in different formats | Name one owner for every shared file or format in the briefs |
| Two tasks could have added the same database migration number | Give one task at a time ownership of the next migration |
| The app allows only 10 new sessions per user message | Offer the rest as cards for the user to start |
| Four Opus sessions hit the usage limit before writing code | Commit after every working piece; restart in the same session so its reading is kept |
| Seed data was not published with the app | Test a real publish, not just a build |
| A test broke when a colleague changed a config setting | Tests set every setting they rely on |
| Every site "not reachable" once the app ran behind a corporate proxy | Let the proxy resolve public names, pass the proxy's sign-in, test through a real proxy, and give an admin "test fetch" that says why |
| A leftover worktree folder could not be deleted while File Explorer had it open | Close Explorer windows before cleaning up |
| A shell command used `&&`, which Windows PowerShell rejects | Use `;` in commands for this PC |

## What worked
- Done-tests written before the work made checking each task quick.
- The manager running the tests itself, and trying pages in the browser, caught problems the task reports missed.
- A one-click installer with backups and a tested uninstall made the server install simple.

## Related
- [[Lessons - Building and Testing the Airtronic Demo]]
- [[Checklist - Testing an EXE on a Locked-Down Company PC]]
