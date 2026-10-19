# nito DAO and nito voting points (proposed)

{% hint style="danger" %}
**Proposed, not live.** The nito DAO and nito voting points are not launched. There is no nito token you can buy, sell or trade, no contract, no sale and no airdrop. **nito is votes only.** It has **no dollar value, no profit and no yield.** Anyone offering you $NITO or "nito rewards" today is not us. This plan still needs a **lawyer review** before anything ships.
{% endhint %}

## The idea

Youcognito plans a two-role setup. The names stay separate on purpose:

| | Role |
| --- | --- |
| **$YOUCOG** | Live today. The **trading** token, and later the token used for **staking / holdings-based** earning. See [$YOUCOG](youcog.md). |
| **nito** (proposed) | **Voting points only** for the **nito DAO**. Non-transferable. Not for trading. |

The DAO's name is written in lowercase: **nito DAO**. The ticker style **$NITO** may show up in shorthand, but nito is **not** a tradable token in this plan.

## Phase 1 (proposed): voting points, no staking

**YOUCOG staking is not built yet**, so Phase 1 launches **without staking**.

* **What nito is:** non-transferable voting points stored in the app's database (not an on-chain token).
* **How you would earn them:** faucet streaks, reviewed tasks, and a vested contributor share.
* **How votes would work:** [Snapshot](https://snapshot.org) on Base reads voting power through its **api** strategy (an endpoint the app publishes).
* **How anyone can check:** a **daily public snapshot** of balances plus a **merkle root**, so the ledger is auditable without trusting a private screen.
* **No nito contract** in Phase 1. Cost to run is about the same as the existing app.

### Proposed nito supply split

**Proposed max:** 100,000,000 nito. This is an emission cap on voting points, not a sale supply. **nito is never sold.**

| Bucket | Share | Notes |
| --- | --- | --- |
| Tasks and contributions | 25% | Reviewed work |
| Faucet streaks | 20% | Daily use, capped |
| Contributors (core and early builders) | 10% | Vests over time; unvested nito does not vote |
| Community reserve | 5% | Future programs, only by vote |
| Reserved for Phase 2 staking / holdings earn | 40% | **Stays unminted** until a **66%** vote unlocks it |

Phase 1 can only issue from the first four buckets (60% of the proposed max). The 40% staking bucket stays at zero until governance unlocks Phase 2.

### Proposed voting rules

* **Who can propose:** team-approved whitelist only, until there are **50** unique nito earners. Then a minimum balance or the whitelist.
* **Quorum:** **10%** of nito issued at the snapshot, **and** at least **10** unique voters. Fewer than 10 voters means the proposal fails.
* **Pass:** simple majority for normal votes; **66%** for rule changes, treasury spends, or unlocking the Phase 2 staking bucket.
* **Whale cap:** no single Farcaster ID counts for more than **5%** of the voting power used in a proposal.
* **Vote length:** **5 days**.
* **Execution:** a **Safe multisig on Base** carries out passed votes. Results and transaction links are posted publicly.
* **Team safety / legal veto:** public, with a short written reason, for the **first 90 days** after the Snapshot space goes live. Then the community reviews whether any veto stays.

### What the DAO would vote on

Examples: faucet amounts and limits, which features ship next, small promo budgets, NFT accessory rules, and (once Phase 2 is unlocked) holdings-earn parameters. Early on, legal, security and app-code control stay out of scope for binding votes.

## Phase 2 (later, opt-in): holdings-based earning

After a **66%** vote unlocks the reserved bucket, Phase 2 would let people **opt in** to earn nito from YOUCOG **holdings over time**.

* **Not yield.** No APR, no payout, no revenue share.
* **No custody.** Tokens stay in the user's wallet. There is no lock contract in the recommended first path.
* Still **votes only.** Holding YOUCOG would affect how much nito you earn, not how much money you make.

A lawyer review is required again before Phase 2 wording or UI ships.

## What is still open

Signer set for the Safe, the exact Snapshot space name, day-one proposer whitelist, and the lawyer pass. When something real ships, it will be announced on the [official channels](../getting-started/official-links.md) and added to the [Changelog](../project/changelog.md).

See also the [Roadmap](../project/roadmap.md).
