---
type: reference
status: active
created: 2026-11-11
tags: [ai, sales, security]
aliases: [AI price extraction checklist]
---

# Checklist - Safe AI Price Extraction

How to get prices from web pages with an AI without trusting the AI or the page. Proven in a demo program (run 3: 4 of 4 prices kept, all matching earlier hand-collected data). The reasoning is in [[Lessons - Building and Testing the Airtronic Demo]].

## Getting the page
- [ ] Do not assume a gateway passes web tools through: probe it (ours did not)
- [ ] Fetch the page yourself: https only, allow-listed sites, no internal addresses, redirects re-checked, robots.txt respected, size and time limits, honest User-Agent, a pause between requests
- [ ] Report bot checks and CAPTCHAs as "not reachable"; never work around them
- [ ] Turn HTML into text, and add the shop's structured price data (JSON-LD, product meta tags) at the top

## Asking the AI
- [ ] Send only public data: product name and code, page address, page text. Never your own prices, costs or settings
- [ ] Say the page text is untrusted data and its instructions must be ignored
- [ ] Define the scope: the product alone **or** in a kit or package; the current price if there is an old and new one
- [ ] Ask for the price **exactly as written**, plus the number, currency and VAT basis (`inc`, `ex` or `unknown`)
- [ ] Allow an empty answer; never ask it to guess
- [ ] Ask for strict JSON in a fixed shape

## Checking every answer
- [ ] The address is on an allowed site and its page was actually fetched
- [ ] The page has no text aimed at the AI ("ignore previous instructions" and similar)
- [ ] The copied price text appears on that page (spaces after £ do not matter)
- [ ] The number is **one of the numbers** in the copied text (handles "Now £834.00 (inc. VAT)")
- [ ] The price sits in a plausible range for the product
- [ ] VAT "unknown" is kept but not counted
- [ ] The seller name comes from the record for that website, not from the AI
- [ ] A page already on record replaces its old price; it is not counted twice

## Related
- [[Checklist - Testing an EXE on a Locked-Down Company PC]]
- [[Lessons - Building and Testing the Airtronic Demo]]
