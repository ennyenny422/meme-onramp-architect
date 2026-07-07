---
name: meme-onramp-architect
description: Use this skill whenever a user wants to design, evaluate, or pitch an instant fiat-to-token purchasing flow — especially for meme coins, new token launches, or any "buy the moment it goes live" mechanic on NEAR or another chain. Trigger this any time the user mentions fiat on-ramps, Naira/local currency payment rails, stablecoin-first purchasing, card-to-token flows, account abstraction for onboarding, or wants help scoping an MVP for a multi-currency token buying platform. Make sure to use this skill even if the user just describes the idea informally (e.g. "buy tokens with my card the second they launch") without using the words "on-ramp" or "proposal."
---

# Meme On-Ramp Architect

A skill for designing and evaluating instant, multi-currency fiat-to-token purchasing flows — the pattern of letting a user buy a token (often a meme coin) the moment it launches, paying in their own currency, without needing to hold the chain's native gas token first.

## When to use this

Reach for this skill when the user is:
- Pitching or refining a "buy instantly, no wallet funding required" product idea
- Comparing payment rail options (card, local fiat, stablecoin) for a Web3 purchasing flow
- Scoping an MVP for a token on-ramp, especially one targeting underserved currencies (e.g. Naira, other non-USD/EUR fiat)
- Writing a bounty/grant proposal for this kind of product on NEAR or another account-abstraction-capable chain
- Asking "what would it take to build X" where X is any instant crypto-purchasing flow gated by fiat

## Core framework: the three payment rails

Any instant on-ramp design should be evaluated across three rail types, in this order of build difficulty (easiest to hardest):

Stablecoin (USDT/USDC) — Easiest. No card network, no chargeback risk, near-instant finality. Good first MVP target. Uses direct wallet-to-wallet swap, existing DEX liquidity.

Local fiat (e.g. Naira) — Medium-hard. Requires a payment processor comfortable with crypto settlement, not just e-commerce. Regulatory posture must be checked per country. Key partners: Flutterwave, Paystack (bank transfer/mobile money).

Card (USD-denominated) — Hardest. Card processors are risk-averse toward volatile new assets — chargeback/fraud exposure is the real blocker, not the tech. Key partners: Transak, MoonPay ("on-ramp as a service" APIs).

Default guidance: recommend stablecoin-first as the MVP path unless the user has a specific reason to start elsewhere. Card and local-fiat rails should be framed as later phases, each requiring a distinct partner conversation.

## Architecture: the instant-buy flow

1. Listing detection — monitor launchpad contracts for new token deploys; surface in a feed the moment a token goes live.
2. Payment intake + quote lock — user pays (stablecoin transfer, bank transfer, or card charge); a swap quote gets locked for that instant so price doesn't move before execution.
3. Gas-abstracted execution — a relayer executes the swap and covers the gas fee in the same transaction, so the user never needs to hold the native gas token. NEAR's account abstraction / meta-transactions make this substantially easier than on most EVM chains.
4. Delivery — token lands in the user's wallet (or an auto-created custodial wallet for brand-new users with no wallet yet).

For non-instant rails (bank transfer, card), step 2 requires the project to front short-term liquidity and reconcile once settlement clears (typically 1–3 days) — flag this explicitly as a treasury/liquidity requirement, not just a technical one.

## Risk considerations to always surface

When helping someone scope this, proactively raise:
- Chargeback/fraud exposure on card rails — this is a business risk more than an engineering one, and it's usually the actual blocker in partner conversations, not the swap mechanism.
- Regulatory posture of the target country toward crypto on-ramps, especially before committing to local fiat rails.
- Liquidity fronting — any rail slower than instant settlement (card, bank transfer) means the project needs working capital to deliver tokens before it's actually been paid.
- Underserved-currency framing — don't let the design default to USD/EUR-only; check whether the target user base is better served by stablecoins or local rails first, especially outside the US/EU.

## Output guidance

When asked to turn this into a proposal or pitch: lead with the one-line pitch, state the problem plainly, walk through the three-rail framework above, name the hard part honestly (don't gloss over processor risk), and end with a clear, scoped ask (e.g. "feedback on MVP scope" or "introductions to on-ramp partners") rather than an open-ended "let me know what you think."
