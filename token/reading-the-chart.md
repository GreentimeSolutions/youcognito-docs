# Reading the chart

The [GeckoTerminal chart](https://www.geckoterminal.com/base/pools/0x0c6b7aac93aed41f6a12b99e44b821388bd4df31f9247288feef741edb135614) for YOUCOG can look strange. Here's why.

## Why every buy shows tiny "sells"

Open the trade list and you'll often see one buy followed by **two tiny "sells" in the same transaction**, a fraction of a cent each. For a $1 buy they're roughly 0.7% and 0.15% of the size.

**They're not people selling.** The YOUCOG pool is a Uniswap v4 pool with a Doppler hook, launched through Bankr. When you buy, the pool takes its trading fee and converts part of it inside the same transaction. Chart sites record those fee swaps as separate small "sells".

What this means for you:

* **Count the buy, ignore the fee "sells".** Check that they share the buy's transaction hash.
* Because the fee swaps land at a slightly lower price, a candle that only had a buy in it can **close red**.
* Youcognito's ghost bubble already ignores them and only shows real outside buys.

## Why the dollar price moves when nobody trades

The pool trades **YOUCOG against ETH (WETH)**. The dollar price is YOUCOG's ETH price times ETH's dollar price. So:

* If ETH drops 1.5%, YOUCOG's dollar price drops about 1.5% too, even with zero trades.
* To see YOUCOG's own movement, switch the chart to show the price **in ETH**.

## Why the chart looks "empty"

With only a few trades a day, the chart is mostly flat lines with a few lonely candles. That's low trading activity, not something broken.

## Quick checklist

1. Is the "sell" in the same transaction as a buy? Then it's a fee swap.
2. Did ETH move? Then the dollar price moved with it.
3. Compare in ETH terms to see what YOUCOG itself did.
