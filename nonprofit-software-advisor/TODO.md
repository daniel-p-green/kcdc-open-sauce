# NonprofitTechFinder — Demo TODO

Use this checklist to track what’s needed for today’s demo. Check items as you complete them.

## Completed
- [ ] Prompts finalized and pushed (Claude + Playground)
- [ ] Design docs and step‑by‑step added
- [ ] Catalog + test prompts added

## Build (Poe bot)
- [ ] Create bot on poe.com (name: NonprofitTechFinder; base: GPT‑4)
- [ ] Paste prompt: `prompts/poe_web_search_prompt.md`
- [ ] Set greeting: `prompts/greeting.md`
- [ ] Settings: Markdown ON; temperature 0.2–0.4; suggest replies ON
- [ ] Optional: upload `catalog.csv` (KB fallback) and enable “Cite sources”

## Smoke tests (copy/paste from repo)
- [ ] Food pantry routing → Bringfood cited with link
- [ ] Volunteer hours → 2–3 tools with reporting/export + links
- [ ] Email donors → free tiers + TechSoup discounts
- [ ] Verify: citations present; pricing pulled live; summary + bullets + table + next steps
- [ ] If over‑questioning or not searching: tighten “Agentic Controls & Efficiency” lines

## Demo assets
- [ ] Capture 3 screenshots (one per scenario) showing sources/links
- [ ] Prepare 60–90s demo script (problem → live search → 2–3 options w/ prices/discounts → next steps)
- [ ] Add “killer line” from design doc
- [ ] Backup one‑pager (export top of `NonprofitTechFinder_Web_Search_Design.md` to PDF)

## Resilience checks
- [ ] Fallback test (pretend search off): outputs
  - [ ] Google Workspace for Nonprofits (free)
  - [ ] Canva for Nonprofits (free)
  - [ ] TechSoup (discounts)
  - [ ] BringFood.care (free routing)
- [ ] HIPAA/BAA guardrail: bot says “not stated by vendor” unless source cites it

## Dry run
- [ ] Pantry prompt + follow‑up “Budget $50, 2 users — adjust recs”
- [ ] Volunteer hours prompt
- [ ] Email donors prompt
- [ ] Keep live demo ≤ 3 minutes total

## Final polish
- [ ] Add quick links section to `Poe_Prompt_Bot_StepByStep.md` (bot URL + 3 prompts)
- [ ] Confirm PR branch link ready for judges

## Contingencies
- [ ] If Poe flaky: replicate in ChatGPT Custom GPT (`prompts/custom_gpt_instructions.md` + upload `catalog.csv`)
- [ ] If voice requested: mention ChatGPT Voice; optionally demo verbally

## Owners
- Owner A:
  - [ ] Build Poe bot
  - [ ] Demo screenshots + script
- Owner B:
  - [ ] Smoke tests + resilience checks
  - [ ] Dry run coordination + final polish

## Quick links
- PRD: `nonprofit-software-advisor/PRD.md`
- Web‑search design: `nonprofit-software-advisor/NonprofitTechFinder_Web_Search_Design.md`
- Poe step‑by‑step: `nonprofit-software-advisor/Poe_Prompt_Bot_StepByStep.md`
- Prompts (Claude/Playground): `nonprofit-software-advisor/prompts/`
- Catalog: `nonprofit-software-advisor/catalog.csv`
- Tests: `nonprofit-software-advisor/examples/test_prompts.md`
