# Agricultural Marketplace — Hackathon MVP

Connects smallholder farmers to buyers (restaurants, retailers, wholesalers) so farmers get better prices and buyers find reliable supply — without relying on middlemen or informal networks.

## Docs

| File | What's in it |
|---|---|
| [`PROBLEM_STATEMENT.md`](./PROBLEM_STATEMENT.md) | The problem this solves and who it's for |
| [`SRS.md`](./SRS.md) | Requirements — what's in the MVP vs. stretch goals |
| [`SYSTEM_DESIGN.md`](./SYSTEM_DESIGN.md) | Architecture, database schema, key workflows |
| [`REASONING_AND_TRADEOFFS.md`](./REASONING_AND_TRADEOFFS.md) | Why this stack, and what we gave up |
| [`CONTRIBUTORS.md`](./CONTRIBUTORS.md) | Who's building what |

## Stack

Next.js (App Router, TypeScript) + Supabase (Postgres, Auth, Storage), deployed on Vercel. See `REASONING_AND_TRADEOFFS.md` for why.

## Getting Started

1. Clone the repo
   ```bash
   git clone <repo-url>
   cd <repo-name>
   ```

2. Install dependencies
   ```bash
   npm install
   ```

3. Set up environment variables
   ```bash
   cp .env.example .env.local
   ```
   Fill in your Supabase project URL and anon key (ask a teammate for these, or find them in the Supabase project settings under API).

4. Run the dev server
   ```bash
   npm run dev
   ```
   App runs at `http://localhost:3000`

## Database Setup

Schema and RLS policies live in Supabase directly (see `SYSTEM_DESIGN.md` for the ER diagram). If you're setting up a fresh Supabase project, run the SQL migrations in `/supabase/migrations` (or recreate the three core tables — `profiles`, `listings`, `orders` — from the schema doc).

## Deployment

Connected to Vercel — pushes to `main` deploy automatically, and pull requests get their own preview URL for review before merging.

## Core Demo Flow

1. Farmer signs up, creates a produce listing
2. Buyer signs up, browses/searches listings
3. Buyer sends an order request
4. Farmer confirms the request
5. Order status updates for both sides

## Status

Hackathon MVP — see `SRS.md` for what's built vs. what's stretch/future work.