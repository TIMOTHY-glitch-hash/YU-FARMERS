# Software Requirements Specification (SRS)

## 1. Purpose & Scope

This SRS defines the requirements for the hackathon MVP build of the agricultural marketplace platform described in `PROBLEM_STATEMENT.md`. Scope is deliberately narrowed to a core loop that can be built, tested and demoed within the hackathon timeframe. Anything not in the MVP list is a stretch goal or future-work item — see `REASONING_AND_TRADEOFFS.md` for why the cuts were made.

## 2. User Roles

| Role | Description |
|---|---|
| Farmer | Lists produce for sale, manages own listings, responds to order requests |
| Buyer | Browses/searches listings, sends order requests to farmers |
| (Admin) | Stretch — would verify users and moderate listings |

## 3. Functional Requirements — MVP (must-have)

| ID | Requirement |
|---|---|
| FR1 | A user can sign up / log in as either a Farmer or a Buyer (Supabase Auth) |
| FR2 | A Farmer can create a produce listing: crop type, quantity, unit, price, location, optional photo |
| FR3 | A Farmer can view, edit and delete their own listings |
| FR4 | A Buyer can browse all active listings |
| FR5 | A Buyer can filter/search listings by crop type and/or location |
| FR6 | A Buyer can send an order request on a listing, specifying quantity wanted |
| FR7 | A Farmer can view incoming order requests on their listings |
| FR8 | A Farmer can confirm or reject an order request |
| FR9 | Both parties can see the current status of an order (requested → confirmed/rejected → completed) |

## 4. Functional Requirements — Stretch (build if time remains)

- Farmer aggregation: combine multiple farmers' listings to fulfil one large buyer order
- Ratings & reviews after a completed order
- In-app messaging/negotiation on price or quantity
- Delivery/transport coordination
- Admin verification step for new Farmer/Buyer accounts

## 5. Non-Functional Requirements

- **Low bandwidth tolerance** — lightweight pages, compressed images, minimal client-side JS where possible
- **Mobile-first** — majority of target users will access via phone
- **Simple UI** — icon + short-label patterns usable by users with limited digital literacy
- **Data isolation** — a Farmer can only edit their own listings; a Buyer can only see/edit their own order requests (enforced via Supabase Row Level Security)
- **Demoable** — deployed and reachable via a public URL before judging

## 6. Core Use Cases

**UC1 — Farmer lists produce**
- Actor: Farmer
- Precondition: logged in
- Steps: open "New Listing" → enter crop type, quantity, unit, price, location, (optional photo) → submit
- Postcondition: listing appears in Buyer browse/search results

**UC2 — Buyer requests an order**
- Actor: Buyer
- Precondition: logged in, viewing a listing
- Steps: open listing → enter quantity wanted → send request
- Postcondition: request appears in the Farmer's incoming requests with status "requested"

**UC3 — Farmer confirms an order**
- Actor: Farmer
- Precondition: has an incoming request with status "requested"
- Steps: open request → confirm or reject
- Postcondition: status updates to "confirmed" or "rejected"; Buyer sees updated status

## 7. Constraints & Assumptions

- Demo scoped to one geographic area and a small set of crop types
- No real payment processing in the MVP (marked future work)
- No SMS/USSD fallback in this build, despite it being flagged as a real-world need in the problem statement — noted as a known limitation, not a solved requirement
- Single currency, no multi-language UI for the hackathon build