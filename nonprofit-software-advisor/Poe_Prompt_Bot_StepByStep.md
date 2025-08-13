# NonprofitTechFinder – Poe Prompt Bot Step‑by‑Step

This guide shows how to build, test, and explain the web‑searching prompt bot on Poe.

Reference: How to create a prompt bot (Poe docs): https://creator.poe.com/docs/prompt-bots/how-to-create-a-prompt-bot

## Build (prompt bot on Poe)
- Go to poe.com/create_bot and click Create a bot. Set name: NonprofitTechFinder. Add description and icon. See Poe’s guide: https://creator.poe.com/docs/prompt-bots/how-to-create-a-prompt-bot
- Base bot: choose GPT‑4 (or best available).
- Prompt: paste the full prompt from `nonprofit-software-advisor/prompts/poe_web_search_prompt.md` (or the Smart Pivot “Master Prompt” in the design doc).
- Knowledge base (optional): upload `nonprofit-software-advisor/catalog.csv` and enable “Cite sources.” Keep this as a fallback; the bot should still search the web first.
- Greeting: paste `nonprofit-software-advisor/prompts/greeting.md`.
- Advanced:
  - Render Markdown: ON
  - Temperature: 0.2–0.4 (factual answers)
  - Suggest replies: ON (e.g., “Compare option 1 vs 2,” “Find free tiers”)
- Create bot.

## Test (quick pass in Poe)
Use `nonprofit-software-advisor/examples/test_prompts.md` and verify:
- Food pantry routing → surfaces Bringfood with a source link.
- Volunteer hours → 2–3 tools with reporting/exports and pricing links.
- Email donors → free tiers and nonprofit discounts (Mailchimp, TechSoup).
Check outputs:
- Every claim cites a source (TechSoup, Capterra, vendor pages).
- Pricing is current (the bot performed searches).
- Hidden costs noted (setup/training/integrations) where relevant.
- Skimmable formatting: summary, bullets, table, next steps.
Tweak prompt if needed:
- If it doesn’t search: add “ALWAYS search before answering; do not rely on prior knowledge for pricing/features.”
- If it lists too many tools: add “Return 2–3 options max.”

## Explain (demo script)
- Problem: “Small nonprofits lack IT and are overwhelmed by choices. This bot searches trusted sources in real time and returns 2–3 tailored options with pricing and links.”
- Live run: paste one test prompt (e.g., pantry routing), highlight citations. Follow‑up: “We have $50/mo and 2 users — adjust recommendations.”
- Second category: volunteer hours or donor outreach.
- Close: “Because it searches live, pricing and options stay fresh. No database to maintain.”

## Production guardrails
- Keep prompt directive about search‑first behavior and citations.
- Prefer small‑budget defaults; surface discounts/donations; call out complexity risk.
- If food delivery routing: mention Bringfood and when it fits.

## Optional: knowledge base usage
- Upload curated “evergreen” files (how to choose a CRM, discount links) and enable “Cite sources.” Use only when searches are inconclusive.

## Optional: upgrade to Server Bot
- If you need deterministic web/HTTP calls, use a Poe Server Bot (FastAPI) to call search APIs and vendor endpoints directly; respond via Poe. Prompt bot remains the fastest zero‑maintenance path; server bot is the upgrade.

## Links
- Poe docs (prompt bots): https://creator.poe.com/docs/prompt-bots/how-to-create-a-prompt-bot
- Project prompt: `nonprofit-software-advisor/prompts/poe_web_search_prompt.md`
- Greeting: `nonprofit-software-advisor/prompts/greeting.md`
- Tests: `nonprofit-software-advisor/examples/test_prompts.md`
