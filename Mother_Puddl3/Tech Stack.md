# Tech Stack

Running list of infrastructure categories Puddl3 needs to license/partner for, plus candidate vendors surfaced so far. None of these vendor names are confirmed decisions yet — they're starting points to evaluate during vendor selection.

## Vendor selection criteria (applies across every category below)
Ranked priorities for choosing between candidates in each category:
1. **Latency/real-time performance** — must support the hard "seconds, not minutes" payout requirement from [[Frontend-Backend]]; disqualifies anything batch-oriented or slow.
2. **Utah + planned-expansion-state compliance coverage** — prioritize vendors whose licensing footprint already covers Utah and the other low-regulation states identified in the [[Legal]] expansion roadmap.
3. **Cost/pricing at startup scale** — startup-friendly pricing/minimums over enterprise-grade vendors built for large payroll platforms.

Explicitly not a top priority: integration speed/developer experience — acceptable to take on more integration work for a vendor that wins on the three criteria above.

**Team**: Puddl3 has existing engineering capacity (technical co-founder/engineers already in place), not pre-technical. **Some vendor conversations from the candidate lists below are already in motion** — vendor selection is further along in practice than the candidate lists alone suggest.

## Embedded Payroll API (tax calc, withholding, filings)
- Purpose: real-time gross-to-net calculation per clock-out, W-4/jurisdiction handling, and acts as IRS Reporting Agent (Form 8655) + state filings on behalf of employer clients.
- Candidates to evaluate: Check, Gusto Embedded, Zeal, Rippling Embedded Payroll

## Wallet-as-a-Service (WaaS) — worker wallets
- Purpose: self-custody wallets with MPC/passkey-based key management so workers never see seed phrases and can't get permanently locked out, while Puddl3 avoids "custodian" classification.
- Candidates to evaluate: Turnkey, Privy, Dynamic, Particle Network
- Note: Stellar has native passkey/smart-wallet support worth investigating directly.

## Banking-as-a-Service (BaaS) / Stablecoin Infra — employer funding + fiat rails
- Purpose: accepts employer ACH/debit-card funding, holds funds in an FBO/pooled trust account, converts fiat to USDC under the hood. This is the partner that likely holds money transmitter licensing so Puddl3 doesn't have to build that stack itself.
- Candidates to evaluate: Bridge, Brale, or a bank partner with an existing trust charter

## Stablecoin / Settlement Rail
- Circle (USDC issuer)
- Stellar network (on-chain settlement rail — ~5 sec finality, low fees)

## Card Issuing (worker debit card / interchange)
- Purpose: physical/virtual card tied directly to worker's USDC balance; requires a card processor plus a sponsor bank.
- Candidates to evaluate: Marqeta, Galileo

## Off-Ramp (instant USDC → bank withdrawal, 2-3% fee option)
- Purpose: powers the "instant withdrawal" fee product and the free standard ACH option.
- May be bundled within the BaaS/stablecoin infra partner above rather than a separate vendor — needs confirming during vendor selection.

## KYC/AML
- Purpose: identity verification for employers (KYB) and workers (KYC), likely required by multiple partners above (BaaS, card issuer, WaaS).
- Candidates to evaluate: Persona, Alloy
- Note: may come bundled with the BaaS partner rather than needing a standalone vendor.

## Time & Attendance
- Native Puddl3 clock-in/out app (built in-house)
- Integrations with existing employer T&A systems: Homebase, When I Work, Deputy, etc.

## Yield Generation (USDC balance interest)
- Purpose: generates the yield behind the two yield-share revenue lines in [[Revenue Models]] — the employer's pre-funded payroll wallet and (pending legal confirmation) the withheld-tax trust pool. See [[Legal]] for why this needs careful structuring, especially for the tax trust pool.
- Candidates to evaluate: Circle's yield-bearing product lines, tokenized treasury/cash-management partners (e.g. Ondo Finance-style structures), or a yield feature bundled directly within the BaaS/stablecoin infra partner above.
- Note: this partner needs to be selected jointly with legal input, not on API/pricing merits alone — the compliance structure of *how* yield is generated (e.g. short-duration T-bill-backed vs. other strategies) directly affects the securities-law exposure flagged in [[Legal]].
