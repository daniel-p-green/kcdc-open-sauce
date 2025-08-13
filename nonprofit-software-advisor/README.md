# Nonprofit Software Advisor – 2‑Hour MVP

This folder contains a minimal, working set of assets to stand up a Poe bot or Custom GPT that recommends software to small nonprofits.

## Contents
- `catalog.csv` – curated tools and metadata (seed)
- `prompts/poe_bot_prompt.txt` – paste into Poe when creating a bot
- `prompts/custom_gpt_instructions.md` – paste into Custom GPT “Instructions”
- `examples/intake.small_food_pantry.json` – sample intake

## How to try with Poe (fastest)
1. Create a new bot on Poe (poe.com) using GPT‑4.
2. Paste the contents of `prompts/poe_bot_prompt.txt` as the bot prompt.
3. In your first message, paste the contents of `catalog.csv` (or host it and paste key rows). Then paste the intake JSON from `examples`.
4. Ask: “Recommend tools for this intake; include comparison table and links.”

Tip: Keep follow‑ups short: “Budget is $50.” “We need voice.”

## How to try with Custom GPT
1. In ChatGPT, create a Custom GPT.
2. Paste `prompts/custom_gpt_instructions.md` into Instructions.
3. Upload `catalog.csv` as a knowledge file.
4. Start with the intake JSON from `examples`.

## Next steps (post‑hackathon)
- Build a tiny web form → serialize intake JSON → feed GPT
- Store catalog in a Google Sheet; add a review column and last_verified dates
- Add more categories (case management, driver tracking, SMS, CMS)
- Automate a Markdown → PDF export template
