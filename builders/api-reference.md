# API reference

Youcognito's HTTP endpoints. They exist to power the app; they're documented here for transparency and for builders. They may change without notice, are rate-limited, and are not a stable public API.

All responses are JSON unless noted. "Quick Auth" means a Farcaster Quick Auth token in `Authorization: Bearer <token>` (sent automatically by the Mini App SDK's `sdk.quickAuth.fetch`).

## Read-only

| Method and path | What it returns |
| --- | --- |
| `GET /api/buys` | Up to 10 recent outside buys from the YOUCOG / WETH pool: `{ buys: [{ tokens, usd, from, at, tx }] }`. Cached ~60 s. Empty list on failure. |
| `GET /api/stats` | Public faucet stats (claims, unique claimers, YOUCOG given, streaks, tips, holders, RCST, Builder Code txs, 30-day chart, faucet wallet balances). Cached 60 s. Fine for apps and agents to read. |
| `GET /api/leaderboard` | `{ claimers, tippers }` for the leaderboard. |
| `GET /api/streak?address=0x…` | Streak for a web address: `{ streak, claimedToday, nextStreak, nextMultiplier }`. With Quick Auth, returns the FID's streak instead. |
| `GET /api/holder` | Holder status for a Quick Auth FID or an `x-holder-session` header: `{ holder, verified, balance, min, address }`. |
| `GET /api/image` | Art maker status: `{ enabled, perUser, total, left }`. |
| `GET /api/rcst-claim?link=…` | Checks a quote-cast link without claiming (the promotion has ended). |
| `GET /api/feedback?address=0x…` | Whether this Farcaster account (Quick Auth) or address already sent the survey: `{ done, reward }` (`reward` is the current gift size). |
| `GET /.well-known/farcaster.json` | Farcaster Mini App manifest (host-aware). |
| `GET /stats`, `/privacy`, `/terms`, `/feedback` | HTML pages. |

## Actions

| Method and path | Body | Notes |
| --- | --- | --- |
| `POST /api/fid-claim` | `{ address, amount }` | Mini App faucet claim. **Quick Auth required.** `amount` is 840, 2222 or 13938 (legacy 420, 1111 and 6969 are accepted and paid at 2x). |
| `POST /api/listen/start` | `{ address?, source? }` | Starts a listen session. Quick Auth in the Mini App, or `address` on web. Returns a session id. |
| `POST /api/listen/finish` | `{ address?, sessionId, playedSeconds? }` | Finishes a listen. Accepted only after the song length has really passed on the server clock. |
| `POST /api/listen/status` | `{ address? }` | `{ unlocked, used }` for today. |
| `POST /api/holder-nonce` | `{ address }` | Issues a message to sign for web holder verification. |
| `POST /api/holder-verify` | `{ message, mac, signature }` | Verifies the signature and returns holder status plus a session token. |
| `POST /api/deep-mission` | `{ mission }` | Holders only (Quick Auth or `x-holder-session`). 2–600 characters. About 20 per holder per 10 minutes. |
| `POST /api/rcst-claim` | `{ link, address? }` | **Quick Auth required.** Sends $RCST to a Farcaster-verified address (launch promotion, ended). |
| `POST /api/feedback` | `{ answers, address? }` | Saves survey answers. Quick Auth in the Mini App, or `address` on web. If a gift is available, the faucet wallet sends a one-time thank-you gift. Once per FID, wallet and (on web) connection; small daily cap; counted separately from the faucet daily budget. |
| `POST /api/tip` | `{ hash }` | Records a tip after verifying the transaction on-chain. Quick Auth optional (links the FID). |
| `POST /api/tts` | `{ text }` | Returns `audio/mpeg` of the text read by Grok Voice. Daily limits apply. |
| `POST /api/image` | `{ prompt }` | Makes a FLUX image (3–300 characters). Returns `{ ok, url }`; the URL expires in about 10 minutes. |

## Server functions

These are called by the web app through TanStack Start server functions, not as plain REST routes:

| Function | Input | What it does |
| --- | --- | --- |
| `runMission` | `{ mission }` (2–400 chars) | Research brief with sources. |
| `readSealedPage` | `{ url }` | Reads a public page server-side and returns `{ title, text, url }`. |
| `claimFaucet` | `{ address, amount }` | Web faucet claim (one per address and per connection per UTC day). |

## Errors

Errors come back as `{ ok: false, reason: "…" }` with a plain-English reason meant to be shown to the user, often with HTTP 400, 401, 429 or 503.
