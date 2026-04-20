# CashFlow Web Deploy Bundle — v7.6

Drop the contents of `public/` into your `cash-flow-red` GitHub repo's `public/` folder.
Vercel auto-deploys within ~30 seconds of the commit.

## What's in this version

All yesterday's v7.5 fixes + today's changes baked in:

### v7.6 (today)
- `.wheel-cta` "Request £X →" button on Get Cash (the missing confirm button)
- Address line reverted from "tap-to-book" to plain "Change" pattern
- Fee slider + ruler capped at 20% (was 50%)
- Cash preset amounts: £20, £40, £60, £80, £100, £150, £200, £300, £500
- CashPoint float presets: same 9 values
- `color-scheme: dark` meta tag (prevents browser auto-dark inversions)

### v7.3 foundation (untouched)
- Map-first home, bottom sheet UI, peek sheets
- Mode-scoped theme: Cash side = white, Supply side = emerald
- autoMatch weighted algorithm, bidirectional rating
- Haptics, Web Audio, pull-to-refresh
- Panic/SOS, share trip, disputes, notifications
- 6-digit QR handover, banknote verification
- CashPoint sub-role, chat system
- Skip demo button

## Verify after deploy

Open https://cash-flow-red.vercel.app/ and confirm:
- Splash shows **v7.6**
- Console logs `CashFlow v7.6 loaded`
- Get Cash screen shows "Request £100 →" button below the wheel ruler
