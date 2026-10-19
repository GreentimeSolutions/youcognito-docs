# Configuration

Youcognito is configured with environment variables (secrets) and a few constants files (public, tunable values). This page lists **names and purposes only**. Never publish real values.

## Environment variables

| Name | Purpose | Secret? |
| --- | --- | --- |
| `DATABASE_URL` | Postgres connection (Neon). Without it, local PGLite is used. | Yes |
| `FAUCET_PRIVATE_KEY` | Key of the faucet wallet that sends YOUCOG and RCST. | **Yes, highly sensitive** |
| `FAUCET_IP_SALT` | Salt for hashing IP addresses. | Yes |
| `HOLDER_SESSION_SECRET` | Signs holder challenges and sessions. | Yes |
| `XAI_API_KEY` | xAI key for missions and Grok Voice. | Yes |
| `BFL_API_KEY` | Black Forest Labs key for the art maker (feature is off without it). | Yes |
| `FARCASTER_ASSOC_HEADER` / `_PAYLOAD` / `_SIGNATURE` (and `_YOUCOGNITO` variants) | Signed Farcaster account association for the Mini App manifest. | No, but keep exact |
| `FARCASTER_DOMAIN` | Override the domain used to verify Quick Auth tokens. | No |
| `BASE_RPC_URL` | Custom Base RPC (defaults to the public Base RPC). | Maybe (paid RPC URLs often contain a key) |
| `FAUCET_DAILY_CAP` | Max faucet claims per UTC day. | No |
| `FAUCET_DAILY_TOKEN_BUDGET` | Max YOUCOG per UTC day, boosts included (default 250,000). | No |
| `HOLDER_MIN_YOUCOG` | Deep Mission threshold (default 10,000,000). | No |
| `RCST_CLAIM_AMOUNT`, `RCST_DAILY_CAP` | $RCST quote-cast amount (default 1,111) and daily cap. | No |
| `IMAGE_PER_USER_DAILY`, `IMAGE_GLOBAL_DAILY` | Art maker limits (defaults 1 and 10). | No |
| `TTS_PER_USER_DAILY`, `TTS_GLOBAL_DAILY` | Grok Voice limits. | No |

Platform-provided variables used by the app builder template (`GROK_*`, `VITE_AUTH_ENABLED`, `VERCEL`, `NODE_ENV`) don't need to be set by hand.

## Constants (in code)

| File | What you can change |
| --- | --- |
| `src/constants/listen.ts` | Boost amount (100,000), song length in seconds (200), tolerance, session grace, max starts per day, faucet balance floor (2,000,000), track title, SoundCloud URL |
| `src/constants/media.ts` | Game URL, soundtrack file and volume, YouTube Short, tile thumbnails, project wallets hidden from buy slides |
| `src/constants/site.ts` | Contact email, X, GitHub and Linktree links, site description |
| `src/constants/builderCode.ts` | Base Builder Codes |

{% hint style="warning" %}
**Swapping the song?** Add the new file under a **new name**, point `SOUNDTRACK_SRC` at it, and update `LISTEN_SONG_SECONDS` to its length in whole seconds, in the same change. The server only trusts that number.
{% endhint %}
