# Legal

## Core distinction: this is payroll, not Earned Wage Access (EWA)
EWA is a regulated category (Nevada, Missouri, Wisconsin, and others; CFPB scrutiny at federal level) that applies specifically to products **advancing money against wages already calculated/owed on a future scheduled payday** — i.e. the "real" payroll run happens later, and a third party fronts cash early against it.

Puddl3 avoids this classification only if every clock-out payout is a **genuine, final, tax-withheld payroll disbursement** — not an advance against a later "real" paycheck. This is why Path A (payment rail on top of ADP/Gusto's normal cycle) is structurally EWA and can't be engineered around, while Path C (Puddl3 runs the actual payroll calculation live) is not EWA — it's just a very short, real pay period, governed by wage-and-hour law instead of lending/EWA law.
**This distinction is foundational — the whole legal posture of the company depends on every payout being real, final payroll, not an advance.**

## State pay-frequency laws
Every state has statutory pay-frequency rules (weekly/biweekly/semimonthly buckets are common); a few states cap how frequently or set specific rules. Paying every clock-out is far more frequent than any standard cycle — needs a state-by-state legal review to confirm compliance (or identify where more frequent pay needs specific structuring/disclosure).

## Reporting Agent (federal/state payroll filings)
- IRS Form 8655 designates a "Reporting Agent" authorized to file employment tax returns (941 quarterly, 940 annual FUTA, W-2s) and make federal deposits via EFTPS on behalf of a client-employer. States have parallel POA/TPA registrations for state withholding and UI filings.
- In the Path C model, **the embedded payroll infrastructure partner is the Reporting Agent**, not Puddl3 and not the employer. Employer signs an 8655-equivalent authorization during Puddl3 onboarding that flows through to the infra partner. Puddl3 does not need to register as a Reporting Agent itself.
- Employer remains the legal employer of record throughout.

## Trust fund taxes — liability exposure
- Withheld income/FICA taxes are trust fund taxes under IRC §7501 from the moment they're withheld — legally not the employer's or platform's money.
- Whoever holds that cash before statutory deposit (deposits are semiweekly/monthly depending on employer size, not per-paycheck) carries real personal liability exposure via the **Trust Fund Recovery Penalty** if mishandled.
- Earning float/interest on held trust fund tax money before deposit is an established industry practice (ADP has long earned float income this way), but requires a compliant trust/custodial account structure. Needs explicit terms with the payroll infra partner on custody and liability allocation. See [[Revenue Models]].

## Money transmitter licensing (MTL) exposure
- **Employer funding side**: employer sends fiat via ACH/debit card into a Puddl3 balance, converted to USDC under the hood. Puddl3 avoids building an MTL stack itself by routing this through a BaaS/stablecoin infra partner holding an FBO/pooled trust account — that partner carries the licensing burden. See [[Tech Stack]].
- **Worker wallet side**: using a WaaS provider (MPC/passkey key management, no single party holding full key control) is intended to keep Puddl3 out of "custodian" classification. Important caveat: regulators evaluate **practical control**, not just labeling — needs explicit legal review of the specific WaaS provider's key-management structure before relying on "non-custodial" as a compliance position.

## Card program compliance
- Card issuance requires a card processor (e.g. Marqeta/Galileo) sponsored by a bank — separate regulatory track from wallet custody.
- Durbin Amendment caps interchange rates differently depending on the sponsor bank's asset size — materially affects interchange revenue economics. See [[Revenue Models]].

## KYC/AML/KYB
- Required for both employers (KYB) and workers (KYC), likely satisfied partly through partner stacks (BaaS, card issuer, WaaS) rather than needing a fully standalone Puddl3-built compliance program — needs confirming per vendor during selection.

## Yield-bearing balances — new question, high sensitivity
Per [[Revenue Models]], both the employer's pre-funded payroll wallet and the withheld-tax trust pool are intended to be interest/yield-bearing, with Puddl3 taking a cut and (for the employer wallet) passing the remainder back to the employer.
- **Regulatory precedent to weigh heavily**: yield-bearing crypto/stablecoin balance products have drawn direct SEC and state enforcement action (e.g. BlockFi's 2022 SEC settlement, Gemini Earn) on the theory that offering yield on pooled customer funds can constitute an unregistered securities offering (investment contract) or unregistered money-services activity, depending on structure.
- The employer-wallet yield-share is likely lower risk than the worker-facing case (no consumer yield product is being marketed to individuals), but "employer earns yield on their payroll float, split with Puddl3" still needs a structure that doesn't read as Puddl3 operating an investment/lending product — e.g. sourcing yield via a compliant tokenized treasury/cash-management partner rather than Puddl3 itself deploying pooled funds into yield strategies.
- **The tax trust fund pool is the more constrained case**: this money is legally trust fund tax money (IRC §7501) the moment it's withheld — deploying it into any yield-generating strategy needs explicit confirmation it doesn't violate trust fund custodial obligations or create additional Trust Fund Recovery Penalty exposure. This likely needs sign-off from the payroll infra/Reporting Agent partner, not just a Puddl3 legal opinion.
- **Recommendation to validate**: get specific legal counsel on this before it's treated as a settled revenue line — it's the highest-risk item in the current model, not just a compliance detail.

## Launch geography and sequencing
- **First launch state: Utah.**
- Rollout strategy is deliberately regulation-driven, not market-driven: as a resource-constrained startup, Puddl3 expands next into whichever states have the *lightest* pay-frequency/licensing burden, rather than following market size or vertical demand. State prioritization for [[Marketing]] and business development should follow the legal review's output, not the other way around.
- Direct consequence: the state-by-state pay-frequency review (above) is not just a compliance checkbox — it is the actual expansion roadmap and needs to be treated as a live, ranked list of states (easiest → hardest) rather than a one-time legal memo.

## Legal engagement approach
- Decision made: engage specialized fintech/payroll legal counsel now, across all open fronts in parallel (Reporting Agent/payroll infra structure, BaaS/MTL custody, yield-bearing balance structure, state pay-frequency review) — not sequenced one at a time.
- **Risk posture**: build product/architecture in parallel with legal review. Development is not gated on legal sign-off. Only actual public launch and live movement of employer/worker money is gated on legal clearance for the relevant piece.

## Open legal questions (not yet resolved)
- State-by-state pay-frequency ranking (easiest-to-hardest) — doubles as the expansion roadmap, starting from Utah.
- Specific liability/float allocation terms with payroll infra and BaaS partners.
- Legal opinion on WaaS custody structure vs. money transmitter classification.
- Employer-of-record risk is NOT part of the model — Puddl3 is not the employer (confirmed: Path C, not EOR).
- Legal structure for yield-bearing employer and tax-trust balances (see above) — highest-priority open item given securities/trust-fund exposure.
- Specialized fintech/payroll counsel engagement — decided to pursue now, across all fronts; actual engagement/firm selection still open.
