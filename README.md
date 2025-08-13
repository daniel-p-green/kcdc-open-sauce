# kcdc-open-sauce

![Tech Support Sloth avatar](nonprofit-software-advisor/avatar/Tech%20Support%20Sloth_avatar-kcdc.png)

## Nonprofit Tech Guide (aka Nonprofit Software Advisor)

A lightweight guide and prompt pack to help small nonprofits pick the right tools fast. It includes a minimal, working setup for either a Poe bot or a Custom GPT that recommends software based on a short intake.

- Folder: [`nonprofit-software-advisor`](nonprofit-software-advisor/)
- Quickstart docs: [`nonprofit-software-advisor/README.md`](nonprofit-software-advisor/README.md)

### What’s inside

- `catalog.csv` – curated list of tools and metadata (seed set)
- `prompts/poe_bot_prompt.txt` – copy/paste into Poe when creating a bot
- `prompts/custom_gpt_instructions.md` – paste into Custom GPT “Instructions”
- `examples/intake.small_food_pantry.json` – sample intake JSON

### Try it in 2 minutes (Poe)

1. Create a new bot on Poe using GPT‑4.
2. Paste the contents of `prompts/poe_bot_prompt.txt` as the bot prompt.
3. In your first message, paste `catalog.csv` (or host it and paste key rows), then the intake JSON from `examples`.
4. Ask: “Recommend tools for this intake; include a comparison table and links.”

### Try it with Custom GPT (ChatGPT)

1. Create a Custom GPT in ChatGPT.
2. Paste `prompts/custom_gpt_instructions.md` into Instructions.
3. Upload `catalog.csv` as a knowledge file.
4. Start with the intake JSON from `examples` and ask for recommendations.

### Next steps (nice-to-have)

- Small web form → serialize intake JSON → send to model
- Store catalog in a Google Sheet; add review column and `last_verified` dates
- Add more categories (case management, driver tracking, SMS, CMS)
- Automate Markdown → PDF export for handouts
