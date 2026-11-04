# Flex payment · FX-1 / FX-2 / FX-3

One Pay item per code in `county.flex`. The title comes from `flexTypes[code].title`. Opening it sets `?type=<code>`.

## Prompt for Cursor
> **FX-1 Intro:** PageHeader (kicker "Pay", title from `flexTypes[code].title`). Render every string in `flexTypes[code].intro` as its own paragraph. Then branch on `flexTypes[code].mode`.
> **FX-2 Mode T (table):** a charge table. The payer picks one row, then fills the configured fields. Each field has `visible` and `required`. Hidden fields are not rendered. A required field left empty shows a field error and does not add to the cart.
> **FX-2 Mode K (keyed amount):** no charge table. One AmountEntry the payer types. Min $1. Then the same configured fields.
> **FX-2 Mode C (ticket):** LookupForm for the ticket, then a list of matches, then one AmountEntry for the chosen ticket. Then the configured fields.
> **FX-3 Fields:** State is a dropdown of US states. Zip is 5 digits, plus an optional 4-digit box. Add to cart uses the shared cart (delinquent false unless the charge says so) and then the shared checkout. Never render card-number fields.
> Use only tokens, classes and components from /bai-spec/00 and /bai-spec/03. Add as new <section class="screen"> blocks in index.html; register routes in ROUTES. Include loading, empty and error states. Mobile: tables become stacked cards under 720px.

## Acceptance
Marion shows "Residential zoning permit" under Pay and on the service home. Other counties with an empty `flex` list show no flex item. The Help group is separate and stays hidden when `helpPages` is empty.
