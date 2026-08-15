# Puddl3 — Legal Briefing (Counsel Meeting Prep)

Prepared ahead of a founder meeting with outside counsel to discuss legal requirements for operating Puddl3. See [[Legal]] for the full operational legal file this was drawn from.

## Lead with this — the core legal premise

**Puddl3 is not Earned Wage Access (EWA); it's real payroll paid on an unusually short cycle.** EWA products advance money against a paycheck that will be finalized later. Puddl3 doesn't do that — it runs the actual payroll calculation live at each clock-out (via a licensed embedded payroll partner), so each payout is a genuine, final, tax-withheld wage payment for a very short pay period. This framing needs to be validated by counsel explicitly before anything else — if counsel disagrees with it, the entire legal posture of the company changes (EWA licensing, fee caps, CFPB exposure).

## Rank-ordered questions for counsel

**1. Yield-bearing balances — highest severity, ask first.**
Puddl3's plan includes generating yield on (a) the employer's pre-funded payroll wallet, shared back with the employer, and (b) withheld payroll tax funds held before IRS/state deposit. Yield-on-pooled-customer-funds products have drawn direct SEC/state enforcement (BlockFi, Gemini Earn) on unregistered-securities theories. Ask: can this be structured to avoid that classification, and does the tax-trust-fund pool (legally the government's money the moment it's withheld, under IRC §7501) even permit this at all, or does it create Trust Fund Recovery Penalty exposure for whoever holds it?

**2. Money transmitter licensing / custody classification.**
Two money flows need review: (a) employer funding — fiat in, converted to USDC under the hood via a banking/stablecoin infra partner; (b) worker wallets — self-custodial in structure via passkey/MPC wallet infrastructure, designed to keep Puddl3 out of "custodian" status. Ask: does routing both through licensed partners actually keep Puddl3 outside Utah's and federal money transmitter definitions, or does Puddl3's *practical control* over the flow still trigger licensing?

**3. Utah-specific launch requirements.**
What does Utah require for (a) a payroll company, (b) a business handling wage payments this frequently, (c) any money-transmission touchpoints? Confirm Utah's wage payment statute (Utah Code Title 34) is satisfied by paying up to twice a day. Also confirm whether Utah has any EWA-specific statute that could apply even to a non-EWA product.

**4. Worker classification.**
Confirm plainly: everything assumes W-2 employees, not 1099 contractors. The whole legal foundation (real payroll, tax withholding, Reporting Agent) depends on that. Contractor payroll would be a different legal analysis entirely (no withholding obligation exists for 1099 pay).

**5. Vendor contract priorities.**
Puddl3 will sign agreements with an embedded payroll provider, a banking/stablecoin infra provider, and a wallet infrastructure provider. Ask what liability-allocation and indemnification language counsel wants in those contracts before signing — especially who's on the hook if trust fund tax money is mishandled, and who bears custody risk on the worker wallet side.

**6. Consumer-facing claims.**
"Zero Employer Cost" and any marketing language will be read by regulators as literally as the technical structure. Ask about a Utah deceptive-practices angle before that language goes out publicly, especially once the yield-share becomes a stated selling point.

## What to bring / have ready

- Puddl3's current entity structure (state of incorporation, entity type) — needed to scope Utah registration/foreign-qualification questions.
- A one-line description of each vendor role planned (embedded payroll API, wallet infrastructure, banking/stablecoin partner, card issuer) — vendor names not needed yet, just what regulated function each absorbs.
- The specific mechanic: 2 payouts/day max, each an independent final calculation — a deliberate legal design choice (not a technical default), made specifically to avoid the advance/estimate problem that would blur into EWA.

## What NOT to expect resolved in one meeting

Full state-by-state licensing analysis, a final answer on the yield structure, or contract drafting. Treat the first meeting as: validate the core legal thesis, get a prioritized punch-list of what needs formal work, and find out what Utah specifically requires to launch. Everything else is follow-up engagement.

## Counsel meeting notes
*(to be filled in after the meeting)*
