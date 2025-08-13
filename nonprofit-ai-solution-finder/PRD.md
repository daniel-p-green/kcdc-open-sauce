# AI Solutions for Non‑Profits to Discover the Right Software — PRD

## 1. Executive Summary
Small nonprofits lack dedicated IT capacity and face an overwhelming software market. This PRD proposes a conversational AI advisor (Custom GPT/RAG) that interviews staff in plain language, maps needs to software categories, recommends vetted tools (with nonprofit pricing where available), and explains why — optionally with voice. The goal is fast, accurate, cited guidance, so staff can pick and adopt the right tools without hiring consultants.

## 2. Problem Statement
- Limited/no IT staff; small nonprofits may have ~3 IT personnel across all operations vs. >10 at very large orgs.
- Market overload: hundreds of tools across fundraising, volunteers, operations; staff are unsure what they “need or think they need.”
- Outcomes today: improvised spreadsheets or overspending on ill‑fitting software; research is time‑consuming and favors vendors with louder marketing.

## 3. Existing Resources (Gaps)
- Directories/lists (e.g., TechSoup catalogs; curated lists by sector groups) help but require tech savvy and significant time.
- Advisory services (SoftwareAdvice/TechnologyAdvice) route to human reps; recommendations may be vendor‑biased.
- Peer forums (TechSoup, Reddit) are helpful but slow and inconsistent.
- Missing: an interactive “solution finder” that a staffer can ask, “We need X,” and get tailored, unbiased, on‑the‑spot answers.

References (examples):
- TechSoup discounts/catalogs: https://www.techsoup.org/
- Bringfood (niche routing for food delivery; free for nonprofits): https://bringfood.care/

## 4. Vision and Value
- A nonprofit staffer describes their challenge; the AI returns 2–5 specific tools with costs, pros/cons, and links, plus brief guidance (“what to look for,” “how to implement”).
- Voice support lowers barriers for non‑technical users; they can “talk to an advisor.”
- Outcome: better fits, lower costs, faster adoption, less staff burnout.

## 5. Users and Use Cases
- Program/Operations Manager: “We deliver food weekly; need routes and driver coordination.” → Suggests Bringfood for planning; complementary options for driver ops; messaging tools; simple SOPs.
- Development Lead: “We need donation tracking + receipts.” → Suggests donor CRMs (e.g., SMB‑friendly), forms, email automation.
- Volunteer Coordinator: “We schedule volunteers for recurring events.” → Suggests volunteer management platforms; SMS reminders; calendaring.

## 6. Scope (MVP)
In scope (first release):
- Conversational intake (web; optional voice via device/app)
- Needs→category mapping, budget/lang/hosting filters
- Top 3–6 tool recommendations with citations and nonprofit pricing notes
- Comparison matrix, cost band, risks, and next 3 steps
- Export: Markdown/PDF, shareable link

Out of scope (MVP):
- Live procurement, vendor integrations, SSO
- Full implementation services

## 7. Functional Requirements
7.1 Intake
- Plain‑language prompts; structured capture (org type/size, budget, needs, constraints: privacy/BAA, hosting, language, region)
- Optional voice input

7.2 Catalog + Retrieval
- Curated catalog (CSV/Sheet → DB) of 50–100 tools across ~12 categories to start
- Fields: vendor, product, categories, tags/features, pricing_band, nonprofit_discount, hosting, BAA/PHI stance, locale, url, notes, last_verified_at
- Embedding search + rule filters (budget ceiling, BAA required, region/language)

7.3 Reasoning + Output
- LLM composes: recommendations, “why fit,” comparison table, cost bands, risks/gaps, quick‑start steps
- Always cite vendor URLs; avoid fabricating features/pricing
- Export to Markdown/PDF; include link list

7.4 Feedback
- Per‑tool thumbs up/down + free‑text comment stored for tuning

## 8. Non‑Functional Requirements
- Accuracy: ≥80% users say “top‑3 look right” in pilots
- Latency: ≤5s with ≤200 tools, ≤10s with ~1k tools
- Explainability: every claim cited; pricing shown as bands with “last verified”
- Privacy: no PHI; minimal PII (optional email for report)
- Accessibility: voice optional; readable outputs

## 9. Information Architecture
- Taxonomy: needs → categories (donor CRM, online fundraising, volunteer mgmt, program delivery, routing, grant mgmt, events/auctions, accounting, productivity, marketing, web/CMS).
- Evidence: links to vendor pages, nonprofit pricing, case studies where available (e.g., Bringfood for home delivery routing).
- Versioning: entries carry last_verified_at; admin review reminders at 6 months.

## 10. System Architecture (MVP)
- UI: lightweight web app (Next.js or Flask/Jinja form)
- Backend: FastAPI (Python)
- DB: Postgres + pgvector (familiar stack)
- Embeddings: sentence‑transformers (all‑MiniLM‑L6‑v2)
- LLM: GPT‑4o‑mini (structured output)
- RAG flow: retrieve k=12 → rule filter → score → LLM compose answers + citations
- Exports: WeasyPrint/wkhtmltopdf for PDF

## 11. Data Model (sketch)
- tools(id, vendor_id, name, categories[], tags[], pricing_band, nonprofit_discount, hosting, baa, locale, url, notes, last_verified_at)
- vendors(id, name, website, contact)
- sessions(id, org_profile_json, needs_json, constraints_json, created_at)
- recommendations(id, session_id, output_md, output_json, created_at)
- feedback(id, recommendation_id, tool_id, rating, comments)

## 12. Voice Enablement (optional day‑2)
- Web voice input (browser speech‑to‑text) or use ChatGPT/Poe voice clients
- Summarized, spoken responses for accessibility

## 13. Success Metrics
- Time‑to‑recommendation ≤5 minutes end‑to‑end
- Top‑3 relevance ≥80%
- Catalog freshness ≥90% reviewed/6 months
- Click‑throughs to vendor links; initiated trials from report

## 14. Risks & Mitigations
- Catalog gaps → show “no strong match,” collect category feedback; expand catalog
- Pricing drift → show bands + timestamps; verify top tools quarterly
- Hallucination → strong rule filtering; strict citation requirement; limited generative claims
- Bias toward cataloged vendors → clear “not exhaustive” note; accept user‑suggested additions

## 15. Rollout Plan
- Week 1: curate 80 tools; intake + retrieval + rule filters; skeleton report
- Week 2: comparison table, cost bands, PDF export; feedback loop; pilot with 3–5 nonprofits
- Week 3: expand categories (routing/driver ops, case management), content hardening, publish public beta

## 16. Example Categories and Exemplars (for seeding)
- Home‑delivery routing/logistics: Bringfood (planner; free for nonprofits) — https://bringfood.care/
- Donor CRM (SMB‑friendly): (examples to seed with nonprofit pricing)
- Volunteer management: (e.g., VolunteerHub/Rosterfy — add nonprofit pricing details)
- Grant management: (e.g., GrantHub/Instrumentl)
- Events/Auctions: (e.g., OneCause/Handbid)
- Accounting: (e.g., QuickBooks Nonprofit/Aplos)
- Productivity: Google Workspace (Google for Nonprofits), Microsoft 365 nonprofit
- Marketing/Design: Mailchimp nonprofit, Canva for Nonprofits, social schedulers

## 17. Compliance & Privacy
- No PHI; avoid sensitive PII
- Optional contact email for report delivery; clear retention policy
- Vendor BAAs flagged where applicable

## 18. References
- TechSoup catalogs/discounts: https://www.techsoup.org/
- Bringfood (routing): https://bringfood.care/
