# KCDC Open Sauce – PRD + 4-Hour Build Planning Doc

## Goal
Build a working Telegram bot demo for Jewish Family Services food delivery routing within 4 hours. Bonus: voice input for availability using Whisper.

## Constraints
- 2 team members; one is more comfortable with Postgres
- Local dev is fine; no production deploy required
- Use existing CSVs where possible; create a small seed CSV if needed

## Definition of Done (Demo-Ready)
- Volunteer can register and set availability via Telegram
- Load address CSV into DB
- Generate a route and reply with:
  - Ordered stop list
  - Google Maps deep link with waypoints
- Mark stops delivered via inline buttons and persist status
- Bonus: voice sets availability via Whisper transcription

## Tech Choices (fastest path)
- Bot: Python + `python-telegram-bot`
- DB: Postgres (Neon or local Docker)
- CSV ingest: `pandas`
- Routing: simple CSV order or nearest neighbor (optional) to produce Google Maps deeplink
- Voice (bonus): Telegram voice → OpenAI Whisper API

## Repo Assets We Can Leverage
- `JFS - Food/converted/Delivery Addresses for Hackathon (Fake)__Report_1.csv` (currently shows 0 rows; use other CSVs or seed file)
- Other CSVs under `JFS - Food/converted/Current Documents for Reference/*` (route info, shopping sheet). If schema doesn’t match, we’ll use a tiny `seed.csv` for demo (8–10 addresses)

## Team Split and Timeline (by blocks)

0:00–0:30
- Person A (Bot): Python venv, install deps, basic `/start` skeleton
- Person B (DB): Provision Postgres (Neon or Docker), create schema, confirm app connection

0:30–1:10
- A: Implement `/register` and `/availability` (parse free text; store)
- B: CSV loader script to `stops` table; flexible mapping of columns

1:10–2:00
- A: Implement `/route N` to assign N unassigned stops to volunteer and reply with step list + Google Maps link
- B: SQL for assignment and completion operations

2:00–2:40
- A: Inline keyboards: “Start route”, per-stop “Delivered” buttons; update DB
- B: Admin commands: `/loadcsv`, `/resetday`, `/liststops N`

2:40–3:20
- A: Error handling, polish replies; end-to-end test
- B: Simple metrics (assigned/completed counts)

3:20–4:00 (Bonus)
- Voice: handle `voice` → Whisper → parse availability text
- Final demo dry runs

## Telegram Commands and Flows
- `/start`: welcome + help
- `/register` "Full Name, 555-1212": create volunteer profile
- `/availability` "fri 9-12, sat afternoon": store as free text
- `/loadcsv` (admin): load CSV into `stops`
- `/route 10`: create a route of 10 stops (CSV order or nearest-neighbor); reply with:
  - Numbered list of stops
  - Google Maps link
  - Inline buttons: “Start route” and per-stop “Delivered”

## Google Maps Deeplink
Build URL:
https://www.google.com/maps/dir/?api=1&origin=<encoded>&destination=<encoded>&waypoints=<p1|p2|...>&travelmode=driving
- If no lat/lon, encode full addresses
- Waypoint limit: keep to ~20 for demo

## Database Schema (SQL)
-- volunteers
CREATE TABLE IF NOT EXISTS volunteers (
  tg_user_id BIGINT PRIMARY KEY,
  display_name TEXT,
  phone TEXT,
  created_at TIMESTAMPTZ DEFAULT now()
);

-- availability (store text for speed)
CREATE TABLE IF NOT EXISTS volunteer_availability (
  tg_user_id BIGINT REFERENCES volunteers(tg_user_id) ON DELETE CASCADE,
  availability_text TEXT,
  updated_at TIMESTAMPTZ DEFAULT now()
);

-- stops (ingested from CSV)
CREATE TABLE IF NOT EXISTS stops (
  id BIGSERIAL PRIMARY KEY,
  name TEXT,
  address_line TEXT,
  city TEXT,
  state TEXT,
  zip TEXT,
  lat DOUBLE PRECISION,
  lon DOUBLE PRECISION,
  notes TEXT,
  dietary_code TEXT,
  assigned BOOLEAN DEFAULT FALSE
);

-- routes (one per volunteer per request)
CREATE TABLE IF NOT EXISTS routes (
  id BIGSERIAL PRIMARY KEY,
  tg_user_id BIGINT REFERENCES volunteers(tg_user_id),
  route_date DATE DEFAULT CURRENT_DATE,
  status TEXT DEFAULT 'planned'
);

-- stops in a route
CREATE TABLE IF NOT EXISTS route_stops (
  id BIGSERIAL PRIMARY KEY,
  route_id BIGINT REFERENCES routes(id) ON DELETE CASCADE,
  stop_id BIGINT REFERENCES stops(id) ON DELETE CASCADE,
  seq INT,
  status TEXT DEFAULT 'pending',
  delivered_at TIMESTAMPTZ
);

CREATE INDEX IF NOT EXISTS route_stops_route_seq_idx ON route_stops(route_id, seq);
