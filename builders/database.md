# Database

Youcognito uses Postgres (Neon in production, PGLite locally). Migrations live in `migrations/` and run on every build (`npm run db:migrate`). They are additive: tables and columns are only ever added.

| Migration | What it adds |
| --- | --- |
| `0002_faucet.sql` | `faucet_claims` (one row per claim: day, address, hashed IP, amount, status `pending`/`sent`/`failed`, tx hash) and `faucet_days` (daily claim counter). Unique partial indexes enforce one claim per address and per IP hash per day; failed claims free the slot. |
| `0003_faucet_fid.sql` | `fid` on claims, plus one claim per FID per day. |
| `0004_streaks_tips.sql` | `base_amount` and `streak` on claims, a daily `tokens` budget counter, and the `tips` table (verified ETH/USDC tips). |
| `0005_holders.sql` | `holders`: verified YOUCOG holders (address, FID, balance, method `fid` or `signature`). |
| `0006_rcst_claims.sql` | `rcst_claims` and `rcst_days`: one $RCST claim per FID (lifetime), per address and per cast, plus a daily cap. |
| `0007_listens.sql` | `listen_sessions` (one active per identity; `started` / `completed` / `abandoned`; linked to the claim that used it) and `listen_bonus` on claims. |

`migrations/auth/0001_auth.sql` belongs to the app template's optional sign-in feature, which Youcognito doesn't use.

## What's not stored

* No research missions, briefs or page contents.
* No raw IP addresses (only salted hashes).
* No custom ghost pictures (they stay in the browser).
