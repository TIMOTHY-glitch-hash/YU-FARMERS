# Reasoning & Trade-offs

This doc exists so the team can answer "why this, not that" during judging or code review. Each section: what we picked, why, and what we gave up.

## 1. Next.js (single app) instead of a separate frontend + backend

**Decision:** One Next.js app handles UI and API (Route Handlers / Server Actions), instead of a separate React frontend talking to a standalone backend service (e.g. FastAPI).

**Reasoning:**
- One codebase, one deploy target, one language (TypeScript) for the whole team — less coordination overhead under hackathon time pressure
- Deploys natively to Vercel with zero config — no need to separately host, containerize, or configure CORS for a second service
- Vercel gives free preview deployments per pull request, which is genuinely useful for a multi-person student team reviewing each other's work fast

**Trade-offs:**
- Less separation between frontend and backend — harder to later swap out the API layer independently or reuse it for a mobile app without change
- If the team is more comfortable in Python (e.g. for future matching/ML logic), that logic would need a separate service later — not a blocker for the MVP, but worth knowing upfront
- A dedicated backend framework can give clearer structure at larger scale; for an MVP with ~3 tables and simple CRUD, that structure isn't needed yet

## 2. Supabase instead of a custom backend + database

**Decision:** Supabase for Postgres, authentication, and file storage.

**Reasoning:**
- Auth, database, and storage in one service — no custom auth system to build in a time-boxed hackathon
- Row Level Security (RLS) lets us enforce "a farmer can only edit their own listings" as a database policy rather than backend code, which is fewer places for a bug to hide
- Generous free tier is enough for a hackathon demo
- Pairs naturally with Next.js via `supabase-js`, with first-class examples for both

**Trade-offs:**
- Vendor lock-in — migrating off Supabase later means rebuilding auth and storage elsewhere
- RLS policies can be confusing to debug for anyone new to Postgres row-level security — worth a short team walkthrough before writing policies
- Less low-level control than a hand-rolled backend, which is a non-issue for MVP scope but worth knowing as the project grows

## 3. TypeScript across the whole app

**Decision:** TypeScript, not JavaScript.

**Reasoning:**
- Shared types between the UI and the Server Actions/API layer catch mismatches at compile time instead of at runtime during a demo
- Multiple students editing the same codebase benefit from autocomplete and caught errors more than a solo dev would

**Trade-offs:**
- Small upfront learning curve if any teammate hasn't used TypeScript before — mitigated by keeping types simple (mostly inferred, not heavily hand-annotated) for the hackathon

## 4. Supabase JS client directly, instead of an ORM (Prisma/Drizzle)

**Decision:** Call Supabase's client library directly from Server Actions for the MVP, rather than adding an ORM layer.

**Reasoning:**
- One less dependency and one less thing to configure/migrate under time pressure
- Supabase's generated types (from the DB schema) already give reasonable type safety without an ORM

**Trade-offs:**
- Raw queries can get repetitive as the schema grows past the 3 MVP tables
- If the project continues past the hackathon, adding Prisma or Drizzle later is a reasonable next step for more complex queries and easier migrations — flagged here as a deliberate "not now"

## 5. Tailwind CSS + shadcn/ui

**Decision:** Tailwind for styling, shadcn/ui for pre-built components (forms, buttons, cards, dialogs).

**Reasoning:**
- Fast to get a clean-looking UI without a dedicated designer on the team — important for a judged demo
- shadcn/ui components are copied into the repo (not an npm dependency), so they're easy to tweak without fighting a component library's API

**Trade-offs:**
- Tailwind's utility classes can clutter markup and take getting used to for teammates new to it
- shadcn/ui trades some "out of the box" polish for customizability — fine for a hackathon where a distinct look isn't the priority

## 6. Vercel for hosting

**Decision:** Vercel, as required by the project constraints.

**Reasoning:**
- Zero-config deploys for Next.js, generous free tier, automatic HTTPS, and preview URLs per branch/PR — all useful for a team demoing progress throughout the hackathon

**Trade-offs:**
- Serverless function execution limits (duration/memory) on the free tier — unlikely to matter for MVP CRUD operations, but worth knowing if a stretch feature (e.g. image processing) gets heavy

## 7. Scope cuts — what we deliberately left out of the MVP

| Feature (from Problem Statement) | Why deferred |
|---|---|
| Farmer aggregation for large orders | Needs a matching algorithm — high effort, not needed to demo the core loop |
| Ratings & reviews | Adds a table and UI surface with no bearing on proving the core value prop |
| Transport/delivery coordination | Out of scope for a software-only hackathon demo |
| Admin verification | Trust/verification matters long-term, but slows down demo account creation |
| Payments | Real payment integration is its own project; MVP proves the matching/ordering flow, not the money flow |

Each of these is still in `SRS.md` as a stretch goal, in priority order, in case time allows.