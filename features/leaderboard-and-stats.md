# Leaderboard and stats

## Leaderboard

The **Leaderboard** card has two tabs:

* **Claimers:** ranked by total YOUCOG claimed. Each row shows the Farcaster name and picture (or a short address), current and longest streak, and a **Holder** badge for verified [Deep Mission](deep-mission.md) holders.
* **Tippers:** people who [supported Youcog](support-tips.md), with their total tips in ETH and USDC. Only tips verified on-chain are listed.

## Public stats page

[youcognito.vercel.app/stats](https://youcognito.vercel.app/stats) shows live numbers from the faucet:

* Total claims (all time, last 24 hours, last 7 days)
* Unique claimers (wallets and Farcaster accounts)
* YOUCOG given out
* Active streaks and the longest streak
* Tips in ETH and USDC
* Verified holders (Deep Mission unlocked)
* $RCST quote-cast claims
* Transactions tagged with Youcognito's Base Builder Code
* A chart of daily claims over the last 30 days
* The faucet wallet's YOUCOG and ETH balance, with Basescan links

Anyone can check the faucet wallet on Basescan, so the numbers are verifiable.

Apps and agents are welcome to read the same numbers from [/api/stats](https://youcognito.vercel.app/api/stats). That is not botting. The response is cached for 60 seconds, so checking more than once a minute gives nothing new.

## BuildBoard

Youcognito is also ranked on BuildBoard by Builder Circle by transactions tagged with our builder code. See [Live stats on BuildBoard](../project/live-stats.md).
