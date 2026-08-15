# Revenue Models

Core premise: "Zero Employer Cost" — employers are not charged directly to offer instant pay. Revenue is captured on the money-movement side instead. For where each stream sits in the actual end-to-end flow of funds, see [[Money Flow Operations]].

## Confirmed revenue streams

1. **Yield-share on the employer payroll wallet**
   - The employer's pre-funded USDC payroll balance (see [[Frontend-Backend]] funding flow) is itself interest-bearing.
   - Puddl3 takes a flat % cut of the yield generated and passes the remainder back to the employer.
   - This is short-duration float (funds get paid out to workers same-day), but structured as a yield-share rather than pure float capture — and it doubles as an employer incentive: pre-funding isn't just "money sitting idle," the employer earns something on it. Worth surfacing as a sales/marketing point, not just a revenue line — see [[Marketing]].
   - Requires a USDC yield-generation mechanism/partner — see [[Tech Stack]]. Raises a new legal question — see [[Legal]].

2. **Yield-share on withheld tax trust funds**
   - Withheld payroll taxes are held until the statutory federal/state deposit date (semiweekly/monthly, not per-paycheck) — a longer, more predictable float pool than the payroll wallet above.
   - Same yield-bearing mechanism applies. Constrained by trust fund tax liability rules (IRC §7501) — see [[Legal]] for how this limits structuring.
   - Unlike the employer payroll wallet, this money isn't the employer's to share yield with — it's government trust fund money — so this pool is likely pure Puddl3 (or infra partner) revenue rather than a revenue-share. Needs explicit legal confirmation.

3. **Worker instant off-ramp fee**
   - Flat-rate fee (2–3% range, exact number not finalized) when a worker chooses instant withdrawal from their USDC balance to their bank account — confirmed flat, not tiered by amount, and not a flat dollar fee.
   - Standard ACH withdrawal is free (slower) — intentionally the less attractive option to encourage funds staying on the Puddl3 card/balance.
   - **Open modeling question:** what share of workers choose instant (fee) vs. free ACH vs. just holding/spending the card balance. No estimate yet — genuinely unknown until there's live usage data. This is the single biggest unknown for revenue modeling and should be treated as a placeholder/sensitivity range, not a fixed assumption, until real usage data exists.

4. **Interchange fees**
   - From spend on the Puddl3-issued debit card linked to the worker's USDC balance.
   - Actual economics depend on the card program's sponsor bank asset size (Durbin Amendment interchange caps) — see [[Legal]] and [[Tech Stack]].

## Explicitly not a revenue source (for now)
- No direct employer SaaS/subscription fee — "Zero Employer Cost" is a core product claim per the website.

## Open questions
- Relative revenue mix/sizing across the four streams is not yet modeled — instant-withdrawal usage rate is the biggest unknown (see above).
- Exact instant withdrawal fee % within the 2-3% range not finalized.
- Exact yield-share split (Puddl3's cut vs. employer's cut) on the payroll wallet not yet defined.
- Whether the tax trust fund yield is legally shareable with anyone or must stay entirely with Puddl3/infra partner — needs legal confirmation, see [[Legal]].
- Whether a future hybrid funding model (Puddl3 fronting capital, per [[Frontend-Backend]] open questions) introduces a lending-style interest/fee revenue line later.
