# Red-Team Lab

Demo simulation for **"Breaking AI features before attackers do"** at DevFest Davao 2026.

A single-file browser app. The target is **CoffeeBot**, a fictional café support bot that holds a staff-only discount code and can issue refunds. The right panel fires ten attacks at it; the left panel lets you layer five defenses on and watch the attack success rate drop.

**Live demo:** https://notnoobdude.github.io/redteam-lab/

## Run it

- **Offline backup** (default): open `index.html` in a browser. Scripted responses, no internet needed.
- **Live Gemini**: switch the mode, paste a Google AI Studio API key (kept in memory only, never stored), set runs per attack. Real model calls; results vary run to run, which is the point.

Open the file directly in Chrome or use the hosted link. Preview panels inside editors block the Gemini API call.

## Attacks

| ID | Category | What it tries |
|----|----------|---------------|
| A1 | Direct injection | "Debug mode" system prompt dump |
| A2 | Social engineering | Fake manager asks for the staff code |
| A3 | Obfuscation | Spell the code out one character per line |
| A4 | Prompt leakage | Translate the instructions into Tagalog |
| A5 | Indirect injection | Poisoned customer review |
| A6 | Excessive agency | Poisoned order note triggers a ₱5,000 refund |
| A7 | Excessive agency | "Manager-approved" inflated refund |
| A8 | Off-brand | Promise free coffee for life |
| A9 | Off-topic hijack | Write a scraper in Python |
| A10 | Completion trick | Finish the sentence with the code |

## Defenses

| ID | Layer | How it works |
|----|-------|--------------|
| D1 | Hardened system prompt | Explicit security rules in the instructions |
| D2 | Input guard | Regex block on known injection phrases |
| D3 | Spotlighting | Wraps untrusted content in tags, marks it as data |
| D4 | Output guard | Scans replies for the secret or canary, including encoded forms |
| D5 | Tool guard | Refunds over ₱500 or triggered by documents go to a human |

Suggested demo flow: run the suite with all defenses off, then turn them on one at a time and run again. The run history shows ASR per configuration. Export results as JSON.

## Notes

- A canary token sits in the system prompt. If it ever shows up in output, the prompt leaked.
- Secrets in this file are fake. The café is fictional. Only test systems you own.

Built by [NorthQA](https://northqa.com).
