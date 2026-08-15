# Front-end / Back-end

## Architecture model: Path C (embedded infrastructure, Puddl3 owns UX + settlement layer)
Puddl3 does not build payroll tax compliance, money transmission, or custody from scratch. It licenses/partners for each regulated function (see [[Tech Stack]]) and owns the product experience and the USDC settlement orchestration on top.

## Core event flow (fires every clock-out — can happen multiple times/day, e.g. lunch break + end of shift)
1. **Time & attendance capture** — native Puddl3 clock app, or integration with employer's existing T&A system (Homebase, When I Work, Deputy, etc.). Both supported.
2. **Hours → gross pay** — hourly rate × hours for that punch, applying accrued OT/premium rules.
3. **Tax & withholding calculation** — call embedded payroll API (see [[Tech Stack]]) with YTD earnings, W-4/jurisdiction data → returns federal/state/local withholding + employer-side liabilities (FICA match, FUTA/SUTA).
4. **Net pay determination** — gross minus withholding = USDC amount owed now.
5. **Funding check** — employer must have pre-funded their Puddl3 balance (see funding flow below). No fronting of capital by Puddl3 at this stage (see [[Revenue Models]] / [[Legal]] for future hybrid credit model).
6. **USD → USDC conversion** — happens automatically under the hood via the BaaS/stablecoin infra partner; invisible to both employer and employee.
7. **Stellar settlement** — USDC sent over Stellar to the worker's wallet.
8. **Withheld tax routing** — withheld amounts (employee + employer portions) routed to a trust/escrow account, held until statutory deposit date, not sent to worker.

## Employer dashboard
- "Add Funds" flow: employer connects bank account or debit card, enters an amount, funds arrive as a Puddl3 balance. Fiat→USDC conversion happens invisibly via the BaaS/stablecoin rail underneath — employer never sees or touches crypto.
- Employee management, real-time labor cost visibility, funding balance/history.

## Worker-side experience
- **Wallet**: WaaS-provisioned embedded wallet (MPC/passkey-based). Self-custody in structure (no single party unilaterally controls keys, keeping Puddl3 out of money-transmitter/custodian classification) but zero-seed-phrase UX — worker never sees or manages private keys directly, and cannot get permanently locked out.
- **Spend**: Puddl3-issued debit card linked directly to the USDC balance (drives interchange revenue, see [[Revenue Models]]). Default behavior keeps funds on the card/in USDC rather than pushing to a bank.
- **Off-ramp options**:
  - Free standard ACH withdrawal to worker's bank account (slower).
  - Instant withdrawal to bank account for a 2–3% fee.

## MVP / launch scope
No phased de-scoping — the full stack is required at launch, not built up in phases:
- Native T&A clock app (in addition to integrations)
- Puddl3-issued card
- Instant off-ramp (fee-based)
- Yield-share on employer wallet (see [[Revenue Models]])

This is an aggressive v1 scope — every regulated/partner-dependent piece in [[Tech Stack]] needs to be live simultaneously for launch, which has real sequencing implications (e.g. card program and yield-generation partner selection, per [[Legal]], are on the critical path, not add-ons).

## Worker onboarding flow
Hybrid: employer pre-invites workers (adds name/contact info during roster setup, reserving their spot), but each worker must individually complete their own identity verification (KYC) and wallet setup before their first payout can be sent. Wallets are not fully bulk-provisioned without worker action.

## Payout latency requirement
Must feel instant — worker clocks out and sees USDC land within seconds. This is a hard product/marketing requirement (see [[Marketing]] — "get paid the moment you clock out"), not a soft target. This constrains vendor selection across the whole pipeline in [[Tech Stack]] (embedded payroll API response time, BaaS conversion speed, Stellar settlement) — every step between clock-out and wallet balance needs to run in real time, not batched.

## Open build questions (not yet decided)
- Employer funding: pre-funding is the model for now; hybrid risk-based credit buffer is a possible future addition, not in v1 scope.
- Vendor selection across every category in [[Tech Stack]] is still open — now higher-stakes given the aggressive full-stack MVP scope and hard latency requirement above.
