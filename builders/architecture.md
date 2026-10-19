# How it works

A tour of Youcognito for builders. The source is public: [github.com/GreentimeSolutions/template](https://github.com/GreentimeSolutions/template).

## Stack

| Layer | What's used |
| --- | --- |
| Framework | **TanStack Start** (React 19, file-based routes, server functions) on **Vite** |
| Styling | Tailwind CSS v4 |
| Chain | **Base** mainnet via **viem**; ERC-8021 Builder Code attribution via `ox` |
| Farcaster | `@farcaster/miniapp-sdk` (Mini App), `@farcaster/quick-auth` (server-side JWT checks) |
| Database | Postgres (**Neon**) in production; embedded **PGLite** when no database URL is set |
| AI | xAI Responses API (Grok) for missions and voice; Black Forest Labs FLUX for art |
| Market data | GeckoTerminal (trades, prices), DexScreener (Deep Mission facts) |
| Hosting | **Vercel** |

## Code map

```
src/
  routes/                 pages and API routes (file-based)
    index.tsx             home (the app)
    stats.tsx             public stats page
    privacy.tsx terms.tsx trust pages
    api/…                 JSON endpoints (see API reference)
    [.]well-known/farcaster[.]json.ts   Mini App manifest
  components/youcog/      UI: app shell, faucet, listen boost, ghost stage, Deep Mission, …
  lib/youcog/             logic: faucet, holders, listen, research, sealed reader, RCST, chain
  constants/              tunable values: listen.ts, media.ts, site.ts, builderCode.ts
migrations/               SQL migrations (run on build)
public/                   images, audio, robots.txt, sitemap.xml
```

## The main flows

### Missions and sealed tabs

* `runMission` (server function) sends the mission to the xAI Responses API with web search, then keeps only public source URLs. If AI credits run out, it falls back to a free summary built from on-chain reads, DexScreener and web search (DuckDuckGo HTML and Wikipedia).
* `readSealedPage` (server function) fetches a page **from the server**, with no cookies and no script execution, and returns readable text. It refuses private/local IPs and hostnames, URLs with credentials, and reports bot-protection blocks clearly.
* The session (tabs, brief, trace) lives in a client-side store only. **Burn** resets it.
* Rate limits: about 8 missions per visitor per 10 minutes plus a global cap; the reader has its own cap.

### Faucet

`claimFromFaucet` in `lib/youcog/faucet.server.ts`:

1. Validates the amount (420 / 1,111 / 6,969) and address.
2. Refuses if no shared database is configured in production (anti-drain needs one).
3. Computes the streak from past **sent** claims (by FID in the Mini App, by address on web) and applies 1.25x (day 3+) or 1.5x (day 7+).
4. Checks for a verified listen today, and picks the amount server-side (`pickClaimAmount`).
5. Checks the faucet wallet's ETH (gas) and YOUCOG balances.
6. Enforces one claim per address / hashed IP / FID per UTC day (unique partial indexes).
7. Atomically reserves a slot under the **daily claim cap** and the **daily token budget**. If a boosted claim doesn't fit the budget, it falls back to the normal amount.
8. Sends the ERC-20 transfer with the Builder Code suffix, then marks the claim sent (or failed, which frees the slot).

Web claims go through the `claimFaucet` server function (with a honeypot field); Mini App claims go through `POST /api/fid-claim` with a Quick Auth token.

### Listen boost

* `POST /api/listen/start` creates a server-side session (one active per identity, max 30 starts per day).
* `POST /api/listen/finish` accepts it only if **wall-clock time since start ≥ song length − 3 s** and within 15 minutes after the song ends. The song length lives in `constants/listen.ts` (`LISTEN_SONG_SECONDS`, currently 200) and is the only duration the server trusts.
* Identity is `fid:<fid>` in the Mini App or `web:<address>` on web (not IP, so phone network switches don't break a listen).
* At claim time a completed, unused listen upgrades the claim to `LISTEN_BONUS_AMOUNT` (100,000), unless the faucet would drop below `LISTEN_MIN_FAUCET_BALANCE` (2,000,000) or the daily budget is short.
* The player is the local MP3 by default; set `SOUNDCLOUD_TRACK_URL` to switch to the SoundCloud widget.

### Holder perks (Deep Mission)

* **Mini App:** the Quick Auth FID's verified addresses are looked up and their YOUCOG balances read on Base.
* **Web:** `POST /api/holder-nonce` issues an HMAC-protected challenge; the user signs it; `POST /api/holder-verify` checks the signature and returns a ~24-hour holder session token, which the client sends back in the `x-holder-session` header.
* The threshold defaults to 10,000,000 YOUCOG. The faucet wallet is excluded.

### Buy slides

`GET /api/buys` reads the pool's recent trades from GeckoTerminal, keeps `kind == "buy"` with at least $0.05 volume, drops project wallets (`PROJECT_WALLETS` in `constants/media.ts`), and caches for 60 seconds. On failure it returns an empty list; it never makes data up. The client filters project wallets again.

### Client-only state

* Custom ghost picture: `localStorage["youcog:ghost-pfp"]` (a 256 px data URL or the Farcaster pfp URL). Never sent to the server.
* Soundtrack on/off: `localStorage["youcog:music"]`.

## Security notes

* No user accounts; Farcaster identity comes from verified Quick Auth JWTs, wallet ownership from signatures or Farcaster verifications.
* IPs are stored only as salted SHA-256 hashes.
* Secrets (faucet key, API keys, salts) live in environment variables only. See [Configuration](configuration.md).
* `vercel.json` adds `X-Content-Type-Options: nosniff` and a strict referrer policy. `robots.txt` disallows `/api/`.
