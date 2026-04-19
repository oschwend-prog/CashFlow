# CashFlow

**The world's first instant cash delivery marketplace.**
Bringing cash back to you — on-demand, anywhere in the city.

🌐 **Live demo:** [cash-flow-red.vercel.app](https://cash-flow-red.vercel.app)

---

## What it is

CashFlow is a peer-to-peer marketplace that connects people who need physical cash with verified couriers nearby who can deliver it to their door — usually within 10 minutes. Think "Uber for cash."

### For requesters
Open the app, tap an amount (£20–£500), pick delivery or pickup, confirm. A nearby courier brings you cash. Pay with Apple Pay, saved card, or a new card at checkout. £5 delivery fee, plus a small transaction fee set by the courier.

### For couriers
Go online with cash already in your wallet, set your own transaction fee (0–50%), and accept nearby requests. You keep 75% of your fee — we take 25%. Weekly payouts to your bank account.

### For CashPoints (optional)
Run a shop, pub, or newsagent? Become a fixed-location supplier. Customers walk in, collect cash, you earn a fee on every transaction. Zero equipment required — just your phone.

---

## The product

- **Two-sided marketplace** — single app, two modes, bottom-bar switch
- **Weighted courier matching** — reliability score blends rating, on-time rate, cancellation rate, and verification status
- **Live GPS tracking** — requester watches the courier approach in real-time
- **QR-code handover** — 6-digit verification between both parties
- **Bidirectional rating** — requester rates courier, courier rates requester
- **Bank-grade payments** — Airwallex payment processing + payout rails
- **KYC-verified couriers** — Gold/Silver/Bronze tier progression

---

## Tech stack

| Layer | Technology |
|---|---|
| Frontend | Single-file HTML/CSS/JS, Mapbox GL dark maps |
| Backend | Supabase (Postgres + Realtime + Edge Functions) |
| Payments | Airwallex (payment intents + courier payouts + KYC) |
| Auth | Supabase OTP (passwordless email) |
| Hosting | Vercel (auto-deploy from this repo) |

---

## Repo contents

| File | Purpose |
|---|---|
| `index.html` | The live app (currently v6.7) |
| `PROJECT-INDEX.md` | Full project documentation — schema, Edge Functions, brand, deploy runbook |
| `README.md` | This file |

For database migrations, Edge Functions, and deployment instructions, see `PROJECT-INDEX.md`.

---

## Company

**Azure IM Ltd** · London, UK
Olivier Schwend — Founder & CEO

Seeking £15M seed to launch in London and scale across the UK → Europe → APAC.

---

© 2026 CashFlow · Azure IM Ltd
