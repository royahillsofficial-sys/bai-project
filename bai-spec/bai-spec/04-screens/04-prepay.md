# Prepay RE / PP · PR-1 / PR-2

## Prompt for Cursor
> **PR-1:** RE uses RE-1 with methods Name · Account · Map ID · Street → RE-2. PP uses PP-1 (password only).
> **PR-2 Prepay:** HelpPanel "This payment is a credit on the account. It is applied when the next bill is issued." RecordHeader + info grid (Owner, Address, Description, Map ID, Acreage, Mortgage company Y/N, Land value, Improvement value, Zip). AmountEntry "Amount to prepay" (free amount, min $1). Never display the amount owed. Buttons Previous / Add to cart.
> **Blocked state:** when a balance is due, hard-stop. InlineNotice warn "This property has a balance due. Prepayments are only available when nothing is owed." Do not show the dollar amount. Primary "Pay the balance" (→ RE-3 for this record). No amount field.
> Use only tokens, classes and components from /bai-spec/00 and /bai-spec/03. Add as new <section class="screen"> blocks in index.html; register routes in ROUTES. Include loading, empty and error states. Mobile: tables become stacked cards under 720px.
