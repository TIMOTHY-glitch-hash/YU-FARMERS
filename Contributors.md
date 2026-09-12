# Contributors

Task references (FR#) point back to `SRS.md`.

## Rogers and Hannah — Frontend / UI
- Set up Next.js project structure, Tailwind + shadcn/ui
- Build listing browse/search page (FR4, FR5)
- Build listing detail page + "request order" form (FR6)
- Build farmer dashboard: my listings, my incoming requests (FR3, FR7)
- Responsive/mobile-first pass on all pages

## Joel , Noela and Agatha— Auth & Data Layer
- Configure Supabase project (Auth, Postgres, Storage buckets)
- Build `profiles` table + sign-up/login flow, farmer vs buyer role selection (FR1)
- Write Row Level Security policies (farmers edit own listings; buyers edit own orders)
- Build `listings` and `orders` tables + migrations

## Baker + others  — Core Feature Logic
- New listing form + Server Action (FR2)
- Edit/delete listing Server Actions (FR3)
- Order request Server Action (FR6)
- Confirm/reject order Server Action + status updates (FR7, FR8, FR9)

## Timothy and Marvin — Deployment, Docs & Demo
- Connect repo to Vercel, set up environment variables, verify preview deployments
- Keep `PROBLEM_STATEMENT.md`, `SRS.md`, `SYSTEM_DESIGN.md`, `REASONING_AND_TRADEOFFS.md` current as scope shifts
- Prepare demo script / walkthrough for judging
- QA pass on the full core loop before submission (create listing → search → request → confirm)

## Shared / Whoever has time
- Stretch features from `SRS.md`, in priority order: ratings & reviews → in-app messaging → farmer aggregation → transport coordination
- README with setup instructions for anyone cloning the repo

---
**Notes for the team:**

- If someone finishes early, pull from "Shared" rather than idling
- Flag blockers early in your team channel — with a hard hackathon deadline, a half-day stuck on one task usually means dropping a stretch feature, not pushing the deadline