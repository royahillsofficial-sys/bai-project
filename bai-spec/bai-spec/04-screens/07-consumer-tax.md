# Pay Consumer Tax · CT-1 / CT-2 / CT-3  (private)

## Prompt for Cursor
> **CT-1 Choose tax type:** the tax type comes from the county's data (Meals, Lodging, Food & beverage, Gas, and whatever else that county files). Each card has a one-line explainer. Continue.
> **CT-2 Access:** SearchMethodSwitch "Business ID / SSN" (Business name + Business ID or SSN, masked) · "Last name + password". Link "Create password / access options".
> **CT-3 Tax periods due:** RecordHeader (business, tax type), BillTable (period, due date, amount, penalty/interest, status) + AmountEntry + Add to cart. Submit button shows "Submitting…" and locks until response (replaces legacy "session may freeze" notice).
> Use only tokens, classes and components from /bai-spec/00 and /bai-spec/03. Add as new <section class="screen"> blocks in index.html; register routes in ROUTES. Include loading, empty and error states. Mobile: tables become stacked cards under 720px.
