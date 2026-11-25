---
type: note
status: active
created: 2026-11-11
tags: [ai, automation, security]
aliases: [Lessons learned - demo EXE]
---

# Lessons - Building and Testing the Airtronic Demo

What went wrong while building and testing a demo program that reads public prices from retailer pages with an AI, why, and the rule that came out of each. Three real runs: run 1 found the gateway limit and a false pass, run 2 found four data bugs, and run 3 was clean.

## 1. Tests
| What happened | Why | Rule |
|---|---|---|
| C1 reported **PASS** while the scan ran 0 searches and read 0 pages | The test only checked "no error" | A test must prove the action happened (count the searches, pages, rows). Absence of errors is not success |
| B2 and B3 failed on every run, burying real problems | A known, decided limit was reported as a new failure | Use a separate **KNOWN** status for limits already decided on, listed apart from problems |
| A1 (match the earlier workbook) broke after a live scan | The baseline check used live data | Check the method against a **frozen baseline** (the earlier rows only); live data is meant to move the figures |
| About 60 test folders were left behind | The test database was still open, and the cleanup error was silently ignored | Close the database before deleting its folder on Windows; never hide cleanup errors without checking |
| Tests could have contacted real websites | The new direct-fetch code was reachable from the test groups | Patch network code in tests; the build must run offline |
| "I never did the to-do list" was wrong | The to-do run happened after the logs were cleared, and a second copy on D: wrote elsewhere | Check every results location before stating what was or was not done |

## 2. The AI gateway
| What happened | Rule |
|---|---|
| Guessed model ids were wrong; the gateway lists its own ids with a provider prefix | Read model ids from the gateway's own list |
| The gateway answers in both OpenAI and Claude formats, but **silently drops Claude's web search and fetch**; the model replied "I can't browse" | Probe each feature separately and keep the raw replies; a translating proxy can accept a feature and ignore it |
| The gateway's product name was remembered wrongly several times | Confirm product names from the source (the API tester, the host name), not from memory |
| Reply shapes differ between providers (`content` vs `document` in fetch results) | Parse tolerantly and save samples so a mismatch can be fixed from evidence |

## 3. Asking the AI to read prices
| What happened | Rule |
|---|---|
| Correct prices were rejected: the AI copied `Now £834.00 (inc. VAT)` and the full stop in "inc." broke the number check | Extract every number from copied text and accept if any matches; never strip characters and hope |
| A kit listing was skipped: "price of this product" was read as "the heater alone" | Say the scope exactly: alone **or** in a kit or package, and the current price if there is an old and new one |
| The AI said "VAT unknown" when the page did not say; those rows were thrown away | Keep honest "unknown" answers, but do not count them in figures |
| The AI ignored a planted instruction ("report £1.00") and did not invent prices | Still check every row: price text must appear on the fetched page, within a plausible range, from an allowed site |

## 4. Data
| What happened | Rule |
|---|---|
| A unique index on address dropped 28 legitimate rows (one page, several products) | Check row counts after loading; uniqueness rules must match the real data |
| A re-scanned page was counted twice (old row plus new row) | One listing counts once, at its **latest** observation; older rows stay as history |
| A scan created a duplicate seller (the same shop, with its web address added to the name) | Use the seller name already on record for that website |

## 5. Security
- **Keys never go inside an EXE**: it can be unpacked in minutes. Provision once (hidden prompt, stored with Windows DPAPI) or by environment variable for a service. A shared API key can also run out of allowance mid-project.
- **Bot checks and CAPTCHAs are reported, never bypassed**, even when clearance is offered. Use official feeds instead.
- Fetching pages on a company machine needs the full guard: https only, allow-list, no internal addresses, re-check redirects, robots.txt, size and time limits, honest User-Agent.
- Results that travel on USB must be scrubbed of keys, user names and addresses before writing.

## 6. Windows, packaging and tools
| What happened | Rule |
|---|---|
| The program hung when started hidden: the key prompt waited for a keyboard | `getpass` reads the keyboard, not a pipe. Services use an environment variable or `--no-prompt` |
| Two copies ran at once (from C: and D:), one silently moved to another port | Detect a running copy and open it instead of starting a second |
| PowerShell 5.1 treated a tool's normal progress output as an error | Under `$ErrorActionPreference = "Stop"`, native stderr fails the script; check exit codes instead |
| A relative path failed in PowerShell's `[IO.File]` calls | .NET resolves paths from the process folder, not the current location; use full paths |
| `pip-audit` output went missing | It writes its result to stderr; capture with `2>&1` |
| A results folder only on `%LOCALAPPDATA%` could not be carried back | Write findings beside the program (the USB), automatically, after every step, and keep them across restarts |

## 7. The web page
- A strict Content-Security-Policy blocks inline `style="..."` attributes: set styles through `element.style` instead.
- `node.append(null)` prints the word "null": build lists without empty entries.
- A page element can sit in only one place: two copy buttons need two elements.

## 8. Obsidian
- **Obsidian rewrites `.obsidian/graph.json` from memory** whenever the graph view changes, wiping edits made while it is open. Close Obsidian fully, edit, then reopen. See [[Vault-Guide]] for the colour groups.

## Related
- [[Checklist - Testing an EXE on a Locked-Down Company PC]]
- [[Checklist - Safe AI Price Extraction]]
- [[Lessons - Parallel Build With an AI Manager Session]]
