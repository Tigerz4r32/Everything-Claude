---
type: reference
status: active
created: 2026-11-11
tags: [automation, security]
aliases: [EXE test checklist]
---

# Checklist - Testing an EXE on a Locked-Down Company PC

Reusable steps for building a test program on one PC and running it on a managed company PC, learned from a demo program. Why each step exists is in [[Lessons - Building and Testing the Airtronic Demo]].

## Build
- [ ] Clean virtual environment; every package pinned **with hashes** (`pip install --require-hashes`)
- [ ] Few third-party packages (the demo used the Python standard-library web server plus `openpyxl`)
- [ ] Vulnerability check (`pip-audit`, capture with `2>&1`) and a component list (SBOM)
- [ ] PyInstaller **onedir**, no UPX, version information set
- [ ] All tests run offline as part of the build; no leftover temporary folders afterwards
- [ ] SHA-256 list of every shipped file; full source in the pack so IT can review and rebuild

## Secrets and settings
- [ ] No key inside the program or the pack
- [ ] Key provided once: stored encrypted with Windows DPAPI (for example a `--set-key` option), or supplied by environment variable for a service; never a plain-text file that travels with the pack
- [ ] Connection settings built in and locked; users only change output preferences
- [ ] Administrator overrides by environment variable or start-up flag, never through the web page

## Behaviour on the PC
- [ ] No administrator rights needed; listens on `127.0.0.1` only
- [ ] Detects a copy already running and opens it instead of starting another
- [ ] Never waits for a keyboard when started without a console (`--no-prompt` or environment variable)
- [ ] Reads and writes only its own folders; states exactly what it reads and contacts

## Capturing results
- [ ] Findings written automatically **beside the program** (on the USB), after every test, note and scan
- [ ] Results survive closing and reopening; one summary file with problems at the top
- [ ] Raw replies from outside services kept, so format surprises can be fixed from evidence
- [ ] Startup failures written to a file, and the window stays open
- [ ] Keys, user names and IP addresses scrubbed from everything written
- [ ] A "still to do" list for the manual steps (security-software reaction, long job, restart check)

## Tests worth having
- [ ] Each test proves the action happened, not just "no error"
- [ ] A separate status for limits already known and decided on
- [ ] Baseline checks run on frozen data, not live data
- [ ] Security checks: no inline script, formula-safe exports, address guard, no secret in files or pages, loopback only
- [ ] Environment checks: data folder, port, proxy, long-running request through the network

## Before handing it over
- [ ] Clear logs and past runs, after archiving them as evidence (keep the stored key)
- [ ] Refresh every copy of the pack (C: and the USB) and verify hashes on each
- [ ] IT signs the EXE and its DLLs; signing changes their hashes, which is expected

## Related
- [[Lessons - Building and Testing the Airtronic Demo]]
- [[Checklist - Safe AI Price Extraction]]
- [[Lessons - Parallel Build With an AI Manager Session]]
