# Vision PO-to-budget reconciliation

- Division: Vision (US Vision Marketing). Do not apply this to Aesthetics or Hospital budgets.
- System and environment: Smartsheet. Uses the division's PR tracking sheet and the per-event `Master Budget` sheets in the Vision events workspace. Sheet names, IDs, links, PO numbers and amounts stay in the internal work system, not here.
- Workflow: checking that ready purchase orders (POs) are recorded on their event's Master Budget, and that the budget lines charged to each PO don't add up to more than the purchase requisition (PR) amount.
- Owner / proposed reviewer: Kaelyn Gray (Vision event marketing); maintainer review by @the-digital-nicholas-olsen.
- Status: draft — revised for Kaelyn review; allocation rules are not yet approved.
- Source and observed date: Kaelyn's working rules, set while running this check on 2026-10-01. Column names, status values and budget layouts were observed in Smartsheet that day. A read-only follow-up on 2026-10-05 confirmed a separate `PO SAP Balance` column and budget rows referencing more than one PO. No real records are reproduced here. The revised allocation safeguards below are proposed for Kaelyn review.

## Use this when

You're asked to audit the PR tracking sheet against event budgets: to find ready POs missing from a Master Budget, flag POs whose budget lines exceed the PR, or flag events whose estimate exceeds their budget.

The audit is **read-only**. Only change a budget when asked, and then follow "Recording missing POs" below.

Its core comparison is planned budget allocations against the PR amount recorded as `Valuation Price`. This does not establish the current approved PO value, remaining SAP balance, or actual invoice allocation. Checking whether an unpaid expense can be covered by an open PO is a separate check, described below.

## Required inputs

- Read access to the PR tracking sheet and to every event folder's `Master Budget`.
- Confirmed allocations for rows referencing multiple POs, or a budget/procurement owner who can resolve them.
- For an open-balance check: a dated, verified SAP balance and the invoice/commitment details needed to identify unpaid amounts and avoid double counting.
- Write access to the budgets, but only if you're asked to record missing POs.

## Rules

1. **"Ready PO" means Status = `PO Created, Pending Invoice`.** Use this status for the missing-PO pass only. A different status is not by itself a finding; read the status rather than assuming the PO was invoiced or paid.
2. **Pull the ready set with a filter.** An unfiltered pull of a large tracking sheet can come back sampled, with rows silently missing. Filter on `Status` and confirm the result isn't sampled.
3. **Match on the PO number, not the description.** Budgets store POs as text (`PO: <number>`, or `PO: <number> & <number>` when a row is shared). Parse each complete PO number and match it exactly; a substring or number prefix is only a search aid.
4. **Only call a PO "missing" if its event has a Master Budget.** Do not assume past events lack budgets. If no budget is found, or the spend is outside this event-budget audit (print, agencies, operations), report that separately.
5. **Calculate confirmed allocations; label assumptions.** Arithmetic can show whether a shared cost could fit, but cannot establish which PO actually pays it. Do not report a possible split as a confirmed allocation.
6. **Don't add rows to a budget.** Fill existing rows only. Adding a column needs the budget owner's approval.

## Procedure

### 1. Pull the ready POs

From the PR tracking sheet, filter `Status` = `PO Created, Pending Invoice` and read `Quarter`, `Vendor`, `Header Text`, `Category`, `PR#`, `Valuation Price` and `PO#`. Read `PO SAP Balance` only when checking open balances, and record its source/date and any error. Use `Header Text` to identify the likely event; confirm ambiguous matches.

### 2. Collect every Master Budget

Browse the events workspace folder by folder each run, because new events add new folders. Budget layouts differ:

- **Trade show budgets:** `Line Item / Projected Cost / Actual Cost / Notes / PR/PO`. The last column is sometimes titled `PR / PO #`.
- **Accelerate budgets:** `Line Item / Rate / PR/PO Number / Notes`.

A sheet summary may return fewer rows than the sheet holds. Confirm with a search for the PO-number prefix on each larger budget.

### 3. Find missing POs

For each ready PO, work out its event from `Header Text`. If that event has a Master Budget, check whether the PO number appears on it. Sort each PO into one of these buckets:

- **Missing:** the event has a budget, but the PO isn't on it.
- **Possibly misfiled:** the PO is on a budget, but its description points to a different event or line.
- **No budget to compare / outside scope:** no event budget was found, or the purchase is non-event spending. State which applies; an event being in the past is not enough to put it here.
- **Data issue:** the PO number looks wrong, for example it matches the PR number or isn't 10 digits.

### 4. Compare planned allocations with PR amounts

Check **every PO that appears on a Master Budget**, not only the ready ones.

1. Collect all detailed expense rows referencing the PO across all event budgets. Use `Projected Cost` for trade shows. For Accelerates, verify that `Rate` represents the full line cost; if it is a unit rate, use the quantity/formula-backed line total. Do not invent missing quantities or totals.
2. Look up the associated `Valuation Price` on the tracking sheet, regardless of status. If the PO has multiple tracking records, determine whether they are distinct approved requests, revisions or duplicates before choosing its comparison amount. Do not blindly sum records or pick the first match. Missing or ambiguous values are data issues.
3. Assign each single-PO expense once. For shared rows, use the allocation procedure below; do not charge the full row to every listed PO.
4. Flag a confirmed allocation total above the associated PR amount as **planned allocations exceed PR amount**. Keep unresolved allocations separate. A result within the PR amount is not proof of an adequate SAP balance or procurement approval.

Skip summary rows (`Estimated Total`, `GRAND TOTAL`, `Subtotal`, `US Budget`, `BUDGET`) when adding detailed expenses, even if a PO is written on them. Never count both a subtotal and its underlying lines.

**Rows shared by two or more POs.** A reference such as `PO: A & B` does not specify the split.

1. Check the request, invoice, agreement, row notes or owner-confirmed allocation. Confirm that each PO covers the relevant vendor and purpose; unused capacity does not make unrelated POs interchangeable.
2. Maintain one allocation ledger per PO across every budget. Start from its verified PR comparison amount, then deduct every confirmed allocation, including shares of earlier shared rows. These are remaining planned capacities, not SAP balances.
3. Use the documented split when available and ensure the shares total the row cost. Carry each deduction forward before checking the next shared row.
4. If the split is unknown, report **allocation needs confirmation**. For an isolated shared row with compatible POs and fully known other allocations, compare its cost with their combined remaining planned capacity. If it fits, report **combined capacity sufficient; split unconfirmed**, not a confirmed per-PO result. If it does not fit, report a combined planned funding gap for owner review.
5. Evaluate multiple unresolved rows using the same PO pool together, counting each expense once. For overlapping pools (for example A/B and B/C), do not reuse B's capacity in both or invent a greedy allocation. Leave the affected per-PO result unresolved until the owner confirms the allocations. Any hypothetical split must be labeled and must account for all affected rows.

**Accelerate hotel spend.** Confirm which marketing-spend and hotel-contingency POs cover the hotel expenses. Compare their confirmed allocations with the hotel lines (F&B, service charge, taxes, parking, rooms to master and miscellaneous hotel charges), counting each cost once. Do not compare the hotel POs with the event grand total, which also includes AV, production and speakers. For an event shared with another division, obtain Vision's approved share before calling a gap a confirmed Vision overage.

**Accelerate AV.** Compare the AV vendor's line cost and confirmed allocation with that vendor's AV PO/PR reference.

### Optional: check whether an unpaid expense fits an open PO

Do this when the request includes checking remaining purchasing capacity. Keep it separate from the planned-budget comparison above.

- Use a current verified SAP open balance. A blank value, formula error (including `#NO MATCH`) or balance without a reliable source/date means **open balance unavailable or unverified**; do not replace it with `Valuation Price` or zero.
- Confirm the PO's vendor, purpose and current approved value with procurement/SAP where needed. A PR amount is not evidence of a current approved PO value.
- Compare only the unpaid amount intended for that PO with its verified remaining balance. Account for other unpaid commitments and whether SAP already includes them, so they are not counted twice.
- Do not compare an entire event budget, including already-paid expenses, with an open balance. Report missing invoice/allocation information separately.

### 5. Check each event's total

Flag any budget whose `Estimated Total` (or `GRAND TOTAL`) is more than its `US Budget` (or `BUDGET`). List budgets with a blank budget cell as "couldn't check."

## Recording missing POs (only when asked)

Enter the PO as text in the budget's PR/PO column, matching the format already there: `PO: <number>`, or `PO: <number> & <number>` when two POs share a row.

- **Trade show budgets:** put the PO on the line item it pays for (exhibitor fees, show services, booth build, the named speaker's row, and so on).
- **Accelerate budgets:** where the existing template uses `GRAND TOTAL` to hold hotel-related PO references, preserve that convention only after the budget owner confirms the POs and their purpose. That reference is not a cost allocation to the entire event total. Keep the confirmed hotel allocation breakdown in the internal work system. Put the AV PO on the AV vendor's row.

If a budget has no PR/PO column, ask before adding one, and match the name and position used on the other budgets of that type.

## Examples (fictional)

**One shared row with a confirmed split.** The owner confirms $200 on PO A and $150 on PO B for a $350 row.

| PO | PR amount | Other confirmed allocations | Capacity before shared row | Confirmed share | Capacity after shared row |
|---|---|---|---|---|---|
| PO A | $500 | $300 | $200 | $200 | $0 |
| PO B | $1,000 | $700 | $300 | $150 | $150 |

Both fit their PR amounts. If the owner had not confirmed the split, the conclusion would be only that $500 of combined planned capacity could cover the $350 row; the per-PO split would remain unresolved.

**Two shared rows using the same PO pool.** With the same initial $500 combined capacity, two $350 rows require $700. The combined planned funding gap is $200. Do not check each row against the original $500 and pass both. This example says nothing about either PO's SAP open balance.

## Avoid

- Treating an assumed A-first split as confirmed, or reusing the same capacity for multiple shared rows.
- Counting a shared expense in full against every referenced PO.
- Treating PR headroom as a SAP open balance or ignoring a balance error.
- Comparing a PO to a total row, or comparing an Accelerate's hotel PO to the whole event's grand total.
- Treating a PO as missing when its event has no Master Budget.
- Copying real PO numbers, amounts, payee names or sheet links into public issues or pull requests.

## Missing information / decisions

- Kaelyn review: confirm the source of shared-row allocations, treatment of multiple PR records per PO, and the line-cost field/formula for each Accelerate template.
- Whether the marketing-spend POs for an Accelerate shared with another division should cover the full hotel bill or only Vision's share. This needs the budget owner.
- Placing the Accelerate spend PO on `GRAND TOTAL` mixes a PO reference with a total row. This was the owner's choice on 2026-10-01 because the template has no single hotel line, and it may be worth a dedicated row in the template.
- Approval evidence and review date: blank until approved.
