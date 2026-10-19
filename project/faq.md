# FAQ

## About the app

### What is Youcognito?

A private AI research app and a daily $YOUCOG faucet on Base. You ask Youcog a question, it reads the web for you in sealed tabs, and you burn the session when you're done. It works in any browser and as a Farcaster Mini App.

### Do I need an account or a wallet?

No account. You only need a Base wallet address to claim from the faucet, and a wallet holding 10M YOUCOG for Deep Mission.

### Is my research saved anywhere?

No. Your mission and the pages Youcog reads live in memory. **Burn** or a refresh wipes them. Your question is sent to the AI provider (xAI) to get an answer, but Youcognito doesn't keep a history. See [Privacy and terms](../features/privacy-and-terms.md).

### Can sites see me when Youcog reads them?

No. Youcog's server fetches the page, without your cookies, and page scripts never run. Your network can see you used Youcognito, but not which sites were read.

### Why can't Youcog open some sites?

Private or local addresses are blocked for safety, and some sites block automated readers. Youcog tells you when that happens, so you can open the page in your own browser.

## The link and X

### Why does X warn about the link?

X sometimes shows **"Warning: this link may be unsafe"** for youcognito.vercel.app. That warning comes from **X's own link filter**, not from the app:

* Free **vercel.app** addresses are shared by many sites, and scammers have abused some of them, so X's filter is wary of the whole address space.
* Crypto faucet wording and the same link being posted many times make filters more suspicious.

The app itself is clean: **Google Safe Browsing and Sucuri SiteCheck report no issues.**

**What to do:** use **[linktr.ee/youcognito](https://linktr.ee/youcognito)**. It passes X without a warning and links to the app. A custom domain is on the [Roadmap](roadmap.md) as the long-term fix.

### Is the link safe?

Yes, as long as it's exactly **youcognito.vercel.app** (or comes from our Linktree). Youcognito never asks for your seed phrase or private key. Check the [Official links](../getting-started/official-links.md).

## Faucet

### How much can I claim?

840, 2,222 or 13,938 YOUCOG a day, up to 1.5x with a streak, or 100,000 with the listen boost. See [Daily faucet](../features/faucet.md).

### When does the day reset?

At midnight UTC. That's 7 PM Central while daylight saving time is on (6 PM in winter).

### Why does it say someone on my connection already claimed?

On the web, there's one claim per internet connection per day, so two people on the same Wi-Fi can't both claim. In the Farcaster Mini App the limit is per Farcaster account instead.

### I lost my streak. Why?

A streak needs a claim every UTC day. Missing one resets it to day 1.

### Does the listen boost stack with my streak?

No. The boost pays a flat 100,000 YOUCOG instead of your normal amount. See [The 100k listen boost](../features/listen-boost.md).

## Token

### What's the YOUCOG contract?

`0x92Bff5D88157114DfC4a0A00F3496AA7e2E7EbA3` on Base. See [$YOUCOG](../token/youcog.md).

### Why does the chart show sells when nobody is selling?

Each buy also logs two tiny fee swaps in the same transaction, which charts show as "sells". And because YOUCOG trades against ETH, its dollar price moves when ETH moves. See [Reading the chart](../token/reading-the-chart.md).

### What is nito / $NITO?

**Proposed voting points** for the nito DAO, not a tradable token. The plan is not live: there is nothing to buy or claim, and **nito has no dollar value, profit or yield**. A lawyer review is still pending. See [nito DAO](../token/nito-dao.md).

### Is YOUCOG an investment?

No. It has no promised value. See the [Disclaimer](disclaimer.md).

## Help

### How do I contact the team?

Email [ghost.youcog@gmail.com](mailto:ghost.youcog@gmail.com), or reach out on [X @Youcognito](https://x.com/Youcognito) or [t.me/YoucogChat](https://t.me/YoucogChat). The team will never DM you first asking for funds or keys.
