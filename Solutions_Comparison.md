# Solutions Comparison – PantrySoft vs Bringfood

## PRD highlights (what we need)
- Volunteer/driver workflows via Telegram; hands-free voice bonus
- Route creation for multiple drivers; quick assignment; Google Maps links
- Delivery confirmation; ability to reassign mid-route
- Back-office data (clients, inventory) is nice-to-have for hackathon, not required today

## PantrySoft snapshot
- Strengths: client CRM, appointments (self-scheduling portal), inventory, reporting; low-cost tiers.
- Gaps vs PRD: no advertised multi-stop delivery routing, driver mobile app, real-time GPS tracking, Telegram/voice, or public API docs (mentions SSO/integrations at higher tiers).
- Indicative pricing: Light $35/mo, Standard $75/mo, Deluxe $125/mo; portal add-on; setup $1k–$1.5k+.
- References: https://www.pantrysoft.com/Features/ , https://www.pantrysoft.com/pricing/

## Bringfood snapshot
- Strengths: purpose-built multi-vehicle, multi-stop route planner for food deliveries; controls by number of vehicles or stops per route; considers vehicle capacity and time-of-day/traffic; outputs maps and downloadable address lists; free for nonprofits/government.
- Gaps vs PRD: appears planner-centric (web app). No mention of driver mobile app usage, real-time driver tracking, volunteer scheduling, Telegram/voice, or API/webhooks.
- Reference: https://bringfood.care/

## Fit matrix
| Capability | PRD priority | PantrySoft | Bringfood |
| --- | --- | --- | --- |
| Client CRM | Medium | Strong | Not in scope |
| Appointments/self-scheduling | Medium | Strong | Not in scope |
| Inventory | Medium | Strong | Not in scope |
| Multi-vehicle routing | High | Not advertised | Strong |
| Vehicle capacity constraint | Medium | Not advertised | Yes |
| Time windows/traffic consideration | Medium | Not advertised | Time-of-day/traffic considered |
| Driver mobile workflow | High | Not advertised | Unclear (planner outputs lists/maps) |
| Real-time driver tracking | High | Not advertised | Not advertised |
| Delivery confirmation | High | Partial (check-in/e-sign for visits) | Unclear |
| Reassignment mid-route | High | No | Unclear |
| Volunteer scheduling | High | Not advertised | Not advertised |
| API/Webhooks | Medium | Unclear (enterprise/integrations) | Not advertised |
| Telegram integration | High | No | No |
| Voice interface | Medium | No | No |
| Nonprofit pricing | Medium | Low-cost | Free for nonprofits/government |

## Takeaways
- PantrySoft solves back-office (CRM, inventory, scheduling) but not routing/driver ops.
- Bringfood solves routing/assignment (planner) but not comms/driver app/tracking.
- For a short-term demo: continue custom Telegram bot + simple routing; optionally pair with Bringfood by uploading address list and sharing generated route lists/maps to drivers.
- For post-hackathon: consider PantrySoft for CRM/inventory + Bringfood for routing, with a thin integration layer; or use a dedicated last‑mile tool for driver ops and tracking.

## Links cited
- PantrySoft: https://www.pantrysoft.com/Features/ , https://www.pantrysoft.com/pricing/
- Bringfood: https://bringfood.care/
