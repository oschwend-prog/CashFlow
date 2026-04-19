# CashFlow — Project File Index

## Entity: Azure IM Ltd
## Supabase Project: intjyovslhvxsvxcbhgk
## Airwallex Sandbox Client ID: JPrFRPnCTYG4NeNpgKBHKw
## Live URL: cash-flow-red.vercel.app
## Current version: **v6.7**

---

## Files

### index.html (v6.7 — currently deployed)
Full interactive prototype. Single-file HTML, ~256KB, 3900+ lines. Contains:

**Core flows**
- Supabase OTP auth (8-digit codes)
- Airwallex payment UI (Apple Pay, saved card, add new card) — scaffolded, not live-wired
- Mapbox geocoding + dark-v11 themed maps
- Two-mode architecture: Get Cash (requester) / Supply Cash (courier) / CashPoint sub-role
- Courier cash-on-hand float system with inline editor
- **Fee model (locked):** fixed £5 delivery fee + courier-set transaction fee (0–50%) + 2.9% + £0.20 Airwallex processing; 25%/75% platform/courier split on the courier fee
- Mapbox-powered demand heatmap (amber) on courier screen

**Matching & trust**
- Weighted `autoMatch()` algorithm: fees×0.4 + eta×2 − reliability×0.35 − cashReadyBonus
- Reliability score 0–100 composite (rating + on-time % + non-cancellation + verified bonus)
- Rich courier data: deliveries count, on-time %, cancellation rate, cumulative £ moved, tenure months, verified flag
- Match sheet with reliability meter, verified badge, veteran tenure badge, three trust stats, alternatives drawer
- **Bidirectional rating**: requester rates courier (existing), courier rates requester (v6.7)

**Navigation**
- Two-button bottom mode bar: Get Cash / Supply Cash with 240ms theme swap
- State preservation across mode swaps via `_MODE_CACHE`
- Inactive-side hints (LIVE red pulse, £ balance badge, draft dot)
- Swipe-left-from-Cash / swipe-right-from-Flow gesture
- Left-edge Profile drawer (Airbnb pattern) with unread notification dot on avatar
- Peek bottom-sheets for Activity, Wallet, Notifications, Disputes (60vh, map visible above)

**Safety & trust (v6.7)**

- Share trip with trusted contact via Web Share API (clipboard fallback)
- Report issue flow (courier side) — creates dispute record, support notified

- Disputes list with status, raise-a-dispute CTA
- Notifications feed with unread tracking, mark all read

**Transaction flow (matches pitch deck)**
1. User creates request (amount + location) via number pad modal
2. Algorithm matches to courier — `autoMatch()` with reliability weighting
3. **Courier accepts/declines** request card (v6.7) — 15s countdown, full trust data, haptic + sound
4. Live GPS tracking + safety features (v6.7 panic/share cluster)
5. Cash handover via 6-digit QR code
6. Transaction closes → auto-payout → bidirectional rating

**Interaction polish**
- Haptics on every consequential tap (6 patterns: tick, light, medium, success, warn, heavy)
- Web Audio sound effects (off by default, toggle in Profile): tick / success / match arpeggios
- Pull-to-refresh on Activity
- First-time welcome card (one-shot)
- Live courier approach animation on tracking (pin interpolates toward requester every 500ms)
- Screen-enter fade (320ms), scale-on-press throughout
- Skeleton loaders, empty states, number pad modal with £20–£500 validation
- 30-second match auto-cancel countdown
- Back buttons on every screen

**Brand (locked)**
- Dark background: #050A12
- Instrument Serif wordmark: "Cash" upright white + "Flow" italic emerald #00E8B8
- Icon mark: italic F alone (favicon, app icon)
- Mode-scoped theme: white accents for Cash side, emerald for Flow side
- Amber #FFB800 reserved for demand heatmap and financial indicators only
- Outfit body font

### migrations/001_schema.sql
Run FIRST in Supabase SQL Editor. Creates:
- 5 enums (user_role, kyc_status, order_status, payout_status, denomination_type)
- 6 tables (profiles, orders, payouts, messages, disputes, notifications)
- 4 triggers (auto-profile on signup, fee calculation, QR generation, courier stats on completion)
- 10 indexes + realtime on orders & notifications

### migrations/002_rls.sql
Run SECOND. Row Level Security policies for all 6 tables.

### edge-functions/create-payment-intent/index.ts
Creates an Airwallex PaymentIntent when a requester orders cash. Stores client_secret on the order.

### edge-functions/airwallex-webhook/index.ts
Handles Airwallex webhook events (payment_intent.succeeded / failed). Updates order status and sends notifications.

### edge-functions/payout-courier/index.ts
Releases funds to courier on delivery completion. Calculates: cash amount + 75% fee share + tip.

---

## Deploy Edge Functions

```bash
npm install -g supabase
supabase login
supabase link --project-ref intjyovslhvxsvxcbhgk
supabase functions deploy create-payment-intent --no-verify-jwt
supabase functions deploy airwallex-webhook --no-verify-jwt
supabase functions deploy payout-courier --no-verify-jwt
```

## Set Secrets

```bash
supabase secrets set AIRWALLEX_API_URL=https://api-demo.airwallex.com
supabase secrets set AIRWALLEX_CLIENT_ID=JPrFRPnCTYG4NeNpgKBHKw
supabase secrets set AIRWALLEX_API_KEY=<your-api-key>
```

## Airwallex Webhook URL
https://intjyovslhvxsvxcbhgk.supabase.co/functions/v1/airwallex-webhook

Subscribe to: payment_intent.succeeded, payment_intent.failed, refund.succeeded

---

## Deploy the frontend

1. Drop `index.html` into the root of the GitHub repo connected to `cash-flow-red.vercel.app`
2. Commit — Vercel auto-deploys within ~30 seconds
3. Verify: splash screen should read **v6.7**; console shows `CashFlow v6.7 loaded — [timestamp]` in green

---

## Brand (locked Apr 2026)

- Dark background: `#050A12`
- Emerald (courier side): `#00E8B8`
- Amber (data-viz / demand heatmap only): `#FFB800`
- Red (SOS, alerts): `#DC2626`
- Body font: Outfit
- Wordmark: Instrument Serif — "Cash" upright white, "Flow" italic emerald (letter-spacing -0.035em)
- Icon mark: italic F alone (favicon, app icon)
- Rule: never recolor "Cash", never add space between "Cash" and "Flow"

---

## Known limitations (flagged for post-fundraise work)

- Edge Functions exist but are not live-wired in v6.7 — prototype runs in demo mode
- No admin app yet
- FCA regulatory opinion still outstanding (critical path)
- Business verification for CashPoint suppliers not enforced (anyone can type any shop name)
- Bottom-up financial model doesn't yet reconcile to the £15M top-down pitch model
- Trust & safety: share trip is UI-wired in v6.7 but needs backend integration for the location-share receiver
