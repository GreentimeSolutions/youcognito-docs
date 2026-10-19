# Farcaster and Base integration

## Farcaster Mini App

* **Manifest:** `GET /.well-known/farcaster.json` serves the Mini App manifest (name, icons, splash, required chain `eip155:8453`, category `utility`). It's host-aware: the canonical domain `youcognito.vercel.app` and the legacy preview domain each get their own signed account association.
* **Embed:** pages include an `fc:miniapp` embed with the button **Open Youcognito**.
* **SDK:** the app calls `ready`, reads the context (FID, username, pfp), and uses:
  * `quickAuth.fetch` for authenticated calls (faucet, streak, holder, listen, RCST, tips)
  * `wallet.getEthereumProvider` to fill in the connected wallet and switch to Base
  * `actions.swapToken` for the one-tap **Get 10M YOUCOG** swap (ETH → YOUCOG)
  * `actions.composeCast` for the $RCST quote-cast and streak shares
  * `actions.openUrl` for external links (game, Short, Bankr, Coinbase Wallet)
* **Server checks:** Quick Auth JWTs are verified server-side against the app's domain. FIDs are trusted only from verified tokens, never from the request body.

## Base

* **Token:** YOUCOG ERC-20 at `0x92Bff5D88157114DfC4a0A00F3496AA7e2E7EbA3`, 18 decimals.
* **Pool:** YOUCOG / WETH, Uniswap v4 with a Doppler hook, launched through Bankr. Pool id `0x0c6b7aac93aed41f6a12b99e44b821388bd4df31f9247288feef741edb135614`.
* **Faucet wallet:** `0x3067ab541253746ab353b842fdc0970ffbde13c7` sends faucet and RCST payouts. Its balance is public on the [stats page](https://youcognito.vercel.app/stats).
* **Donations:** `0xa959d8eeded6fb440ca584d1e87e581168bbf628` (ETH or USDC at `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`).

## Base Builder Codes (ERC-8021)

Every transaction the app sends or asks a wallet to send (faucet payouts and tips) carries an **ERC-8021 attribution suffix** with Youcognito's Builder Code `bc_q72p8qc9`, so activity is credited to the app on Base. The stats page counts these transactions.
