# nito DAO and nito voting points (proposed)

{% hint style="danger" %}
**Proposed, not live.** The nito DAO and nito voting points are not launched. There is no nito contract, no sale and no airdrop. **nito is votes only.** nito has no monetary value and cannot be bought, sold or transferred. **nito has no ticker and is not a token. Anyone offering $NITO is not us.** This plan still needs a **lawyer review** before anything ships.
{% endhint %}

## The idea

Youcognito plans a two-role setup. The names stay separate on purpose:

| | Role |
| --- | --- |
| **$YOUCOG** | Live today. The trading token. It is not used for nito votes. See [$YOUCOG](youcog.md). |
| **nito** (proposed) | **Voting points only** for the **nito DAO**. Non-transferable. Not for trading. |

The DAO name is written in lowercase: **nito DAO**. nito is always written in lowercase too.

## nito voting points

nito voting points (proposed, not live). Details will be published after legal review.

* **What nito is:** non-transferable voting points stored in the app database (not an on-chain token).
* **How votes would work:** [Snapshot](https://snapshot.org) on Base reads voting power through its **api** strategy (an endpoint the app publishes).
* **How anyone can check:** a **daily public snapshot** of balances plus a **merkle root**, so the ledger can be audited without trusting a private screen.
* **No nito contract.**
* **Fair play (proposed):** one person, one Farcaster account. Multiple accounts and farming are not allowed and can be reversed.

Any later change to how nito is earned needs a 66% vote and a lawyer review first. nito has no monetary value.

### Proposed voting rules

* **Who can propose:** team-approved whitelist only, until there are **50** unique nito holders. Then at least **1,000 nito** (proposed) or the whitelist.
* **Quorum:** **10%** of nito issued at the snapshot, **and** at least **10** unique voters. Fewer than 10 voters means the proposal fails.
* **Pass:** simple majority for normal votes; **66%** for rule changes and treasury spends.
* **Reserved points:** Reserved, unminted. Locked. Any use needs a 66% vote and a lawyer review.
* **Whale cap:** no single Farcaster ID counts for more than **5%** of the voting power used in a proposal.
* **Vote length:** **5 days**.
* **Execution:** a **Safe multisig on Base** carries out passed votes. Results and transaction links are posted publicly.
* **Team safety and legal veto:** public, with a short written reason, for the **first 90 days** after the Snapshot space goes live. Then the community reviews whether any veto stays.

### What the DAO would vote on

Examples: faucet amounts and limits, which features ship next, small promo budgets and cosmetic rules. Early on, legal and compliance, security fixes, app-code control and paying people are out of scope for votes.

## What is still open

Signer set for the Safe, the exact Snapshot space name, day-one proposer whitelist, and the lawyer pass. When something real ships, it will be announced on the [official channels](../getting-started/official-links.md) and added to the [Changelog](../project/changelog.md).

See also the [Roadmap](../project/roadmap.md).
