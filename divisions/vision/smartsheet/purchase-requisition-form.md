# Vision purchase requisition form — field rules

- Division: Vision (US Vision Marketing). Do not apply these defaults to Aesthetics or Hospital requests.
- System and environment: Smartsheet form titled "New Purchase Requisition Request Form". The live link, cost center codes and tracking-sheet IDs are kept in the internal work system, not here.
- Workflow: raising a purchase requisition (PR) for event costs, physician payments and marketing vendors.
- Subject owner: Kaelyn Gray (Vision event marketing); maintainer review by @the-digital-nicholas-olsen.
- Status: reviewed Vision workflow guidance
- Source and observed date: Kaelyn's working rules, plus the live form's field labels and dropdown values. Both were read on 2026-10-01, but nothing was submitted. The general-purpose form and its required `Date` field were rechecked on 2026-10-05. The live form labels the field `Date`, not event start date, and does not define which date to use. The field defaults below are Vision workflow rules, distinct from form-enforced requirements. The rules were reviewed on 2026-10-06; restricted confirmation evidence remains in the internal work system.

## Use this when

You need to fill out the PR request form for Vision Marketing spend. An AI may fill in the fields but must **stop before Submit** so the requester can review the form.

## Required inputs

What the money is for, the payee, the amount, how it will be paid (ACH or company card), the related event (if any), the applicable date, and any invoice or agreement.

The form supports both event and non-event purchases. Use the internal guide for the live form link and approved US Vision Marketing cost center; those are shared team prerequisites, not personal credentials. If a required value or applicable date is missing, ask the requester or procurement owner before completing that field.

## Field rules

| Field (as labeled on the form) | Rule |
|---|---|
| Business Area | `Vision`. The options seen were Aesthetic, Vision and Hospital. If the request is for an Aesthetics-only or Hospital item, flag it instead of switching on your own. |
| Short/Header Text * | See the formula below. |
| Material * | `LUMINARIES` when paying a physician. `WORKSHOPS` for Accelerate events only. `TRADE SHOW EXPENSES` for trade show spending. For other non-event spending, check the internal PR tracking sheet for similar past requests from the same vendor or for the same kind of spending, and use their category. If there is no clear match, confirm with the requester or procurement owner. All three values were observed in the dropdown on 2026-10-01. |
| Cost Center * | Always use the US Vision Marketing cost center from the internal guide, unless otherwise specified. |
| PGR * | Always match Cost Center, unless otherwise specified. On 2026-10-01 the PGR dropdown had the same 39 options as Cost Center. |
| Vendor # | Always leave blank, unless otherwise specified. |
| Vendor Name | For physician payments by ACH: `Dr. <First> <Last>`; obtain the full name if missing. For other ACH payments: the company named in the header text. For company-card payments: the card provider from the internal guide. Physicians are normally not paid by company card; if one is, use that same company-card provider as Vendor Name. Do not use a personal card or account by default. |
| Amount * | Comes with each request. |
| Date * | Required for every request. For event-related spending, use the **first day of the related event** under the Vision rule. For non-event spending, use the applicable date confirmed by the requester or procurement owner; do not invent an event or automatically substitute the invoice or submission date. |
| Additional Comments | Optional. |
| File Upload | Attach the related invoice or agreement when there is one. |
| Send me a copy of my responses | Check the box and enter the **submitter's own** email. |

## Short/Header Text formula

```
Q<quarter><two-digit year><business-area letter> - <event, person or vendor> <what the money is for>
```

The business-area letter is `V` for Vision. The form's own help text also allows `A` and `H`. When a physician is named, write their full name with the title: `Dr. <First> <Last>`.

Fictional examples showing each pattern:

| Kind of spend | Example |
|---|---|
| Event cost | `Q426V - Example Eye Congress 2026 exhibitor fee` |
| Honorarium at an event | `Q326V - Accelerate Springfield Honorarium + T&E Dr. Gregory House` |
| Consultation / peer-to-peer | `Q126V - Dr. Jane Doe consultation with Dr. John Roe 1hr` |
| Treatments at a show | `Q126V - Example Expo booth treatments 4 hours Dr. Jane Doe` |
| Recurring vendor service | `Q126V - Example Agency marketing services - Jan` |
| Split payment | `Q226V - Example Congress booth build deposit 60%` / `(remainder)` |

## Where to look things up first

- **Event start dates:** the current year's Event Schedule sheet in the Vision Marketing Events Smartsheet workspace. If the event isn't there, check next year's sheet. For dates that matter, confirm against the society's public calendar.
- **Non-event categories:** look for similar past requests in the internal PR tracking sheet, matching the vendor or kind of spending. If the precedent is unclear, ask the requester or procurement owner.
- **Header text from earlier PRs:** the division's PR tracking sheet (internal), in its Header Text column.

## Avoid

- Automatically using the invoice date for event spending. Under the Vision rule, an invoice dated after the show still takes the show's first day.
- Requiring an event for a non-event purchase, guessing its date, or categorizing all non-event spending as trade show expenses.
- Using `WORKSHOPS` for anything that isn't an Accelerate.
- Writing a physician's last name only. Older PR records do this, but new PRs use the full name.
- Submitting the form without the requester's review. This form has been seen to clear itself after sitting open for a while, so check every field again right before submitting.

## Maintenance and review

- Keep the exact cost center value, card provider name and form link in the internal guide. Publishing them is not required to use this procedure.
- Older tracking data sometimes uses `A` for Aesthetics rows that relate to Vision and uses inconsistent dash spacing. These are known inconsistencies, not rules.
- Workflow review date: 2026-10-06. Confirmation evidence and exact internal values stay in the internal work system. Revalidate live form values before use.
