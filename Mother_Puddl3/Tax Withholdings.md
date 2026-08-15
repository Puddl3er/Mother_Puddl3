# Tax Withholdings

*For how withheld funds physically move — into the Tax Trust pool, through yield, and out to the IRS — see [[Money Flow Operations]].*

## Payout frequency: decided
**2 payouts/day maximum (lunch clock-out + end-of-shift clock-out), each independently final.** Each of the two triggers its own complete, final, fully tax-withheld mini pay-period covering only the hours worked since the previous payout that day — never an estimate, never trued up later.

This was a deliberate trade-off: the alternative (calculate withholding once for the whole day, split across two disbursements) would require the lunch payout to be a provisional estimate reconciled at end-of-day — which risks reading as an advance against a later "real" paycheck rather than final wages, undermining the core EWA-vs-payroll legal position in [[Legal]]. Running two fully independent calculations per worker per day costs more compute/API calls but keeps every disbursement unambiguously final.

## Mechanism
- Withholding is calculated live at each of the (max two) clock-out events via the embedded payroll API (see [[Tech Stack]]), using YTD earnings, W-4/state withholding elections, and work/residence tax jurisdiction — scoped to just the hours since the prior payout, not the full day.
- Both employee-side withholding (federal, FICA, state, local) and employer-side liabilities (employer FICA match, FUTA, SUTA) are calculated per event.
- Each event is its own real, final payroll disbursement, not a running total reconciled later. This is what keeps the product classified as payroll rather than [[Legal|EWA]].

## Open technical/compliance question — flagged, not yet resolved
IRS Publication 15 percentage-method tables do support miscellaneous/daily payroll periods, so per-event withholding is calculable in principle. But running full withholding calculations twice per day, per worker, as independent mini pay-periods is not standard usage for most embedded payroll APIs — needs explicit validation with each vendor candidate in [[Tech Stack]] on:
- Whether their engine supports two independent, final payroll runs per worker per day without under/over-withholding distortion versus a normal periodic assumption.
- How YTD earnings and annualization are tracked accurately across two same-day events.

## W-4 / tax election collection
Collected during the worker's own onboarding/wallet setup — bundled into the same flow as KYC and wallet creation (see [[Frontend-Backend]] worker onboarding flow), completed before the worker's first payout.

## Trust fund handling
- Withheld amounts are trust fund taxes (IRC §7501) from the moment of withholding — routed to a trust/escrow account rather than sent to the worker.
- Held until the statutory federal deposit date (semiweekly or monthly depending on employer size) and equivalent state deposit schedules.
- See [[Legal]] for personal liability exposure (Trust Fund Recovery Penalty) and [[Revenue Models]] for the float income this generates.

## Filings
- Filed by the embedded payroll infra partner acting as Reporting Agent (IRS Form 8655 + state equivalents) — not by Puddl3 directly. See [[Legal]].
- Includes quarterly Form 941, annual Form 940 (FUTA), state UI returns, and year-end W-2s.
