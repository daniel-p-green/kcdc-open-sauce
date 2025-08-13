# Nonprofit Software Advisor – 2‑Hour MVP

<!-- markdownlint-disable-next-line MD033 -->
<p align="center"><img src="nonprofit-software-advisor/avatar/Tech%20Support%20Sloth_avatar-kcdc.png" alt="Tech Support Sloth avatar" width="300" height="300" /></p>

This folder contains a minimal, working set of assets to stand up a Poe bot or Custom GPT that recommends software to small nonprofits.

## Try it online

- [NonprofitTechGuide on Poe](https://poe.com/NonprofitTechGuide)
- [Nonprofit Tech Guide on ChatGPT (Custom GPT)](https://chatgpt.com/g/g-689cea4f047c819183003748bce08db7-nonprofit-tech-guide)

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
