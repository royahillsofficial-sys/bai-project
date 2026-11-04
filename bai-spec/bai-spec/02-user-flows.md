# 02 · User Flows

Legend: `[S-xx]` = screen ID in `04-screens/`. ✅ = already built in `index.html`. Every "Pay" flow ends in the **same shared checkout** (Flow 9).

## Entry (all flows)
`[S-00 Terms ✅ once per session]` → `[S-01 Service home]` → pick service from sidebar or tile.
Private services: if not signed in → `[S-02 Sign in ✅]` (or one-time lookup option on the service's access screen) → return to the service. Signed-in state persists.

## Flow 1 · Pay Real Estate Tax (public)
1. `[RE-1 Find property]` choose method: Name · Account No. · Parcel No. · Dept/Ticket No.
2. `[RE-2 Matching records]` list of owners (Name, Name 2, Map ID; toggle Address ↔ Map ID) → **Select**
   - Dept/Ticket search with a single match skips this step.
3. `[RE-3 Bills for this property]` header (owner, map no., account) + a read-only bill table (Dept, Ticket, Half/Seq, Due date, Description, Amount, Status). **Details** opens `S-TK Ticket detail`. One payment amount for the record, with an oldest-first allocation preview.
4. **Add to cart** → toast "Added $X" + cart count updates. Secondary: **Pay another real estate bill** (back to RE-1, cart kept).
5. **Checkout** → Flow 9.

## Flow 2 · Pay Personal Property Tax (private)
1. `[PP-1 Access your records]` lead: "Paying for someone else? Use the department and ticket number from their bill." Tabs: Signed-in account · Dept + Ticket No. + Last name · Account No. + Last name. Helper: "Department example: PP2026 (PP + tax year)".
2. `[PP-2 Your bills]` read-only vehicle/item rows (Dept, Ticket, Seq, Due, Description e.g. "2019 Honda Civic", Amount). One amount for the record, oldest first → **Add to cart**.
3. Checkout → Flow 9.

## Flow 3 · Prepay (RE public / PP private)
1. RE: `[PR-1 Find property]` (Name · Account · Map ID · Street) → `[RE-2]` select. PP: `[PP-1]` access.
2. `[PR-2 Prepay]` property/account summary (owner, address, description, map ID, acreage, mortgage co., land & improvement value) + **Amount to prepay**. Helper: "This payment is a credit on the account." Never show the amount owed.
3. **Blocked state:** if a balance is due, hard stop. Inline notice "This property has a balance due. Prepayments are only available when nothing is owed." Do not show the dollar amount. Button **Pay the balance instead** (→ RE-3 for that record). No amount field.
4. **Add to cart** → Flow 9.

## Flow 4 · Business License (private)
1. `[BL-1 Access]` tabs: Password (signed in) · Account No. + Last/Business name. No ticket search.
2. `[BL-2 License fees]` fees grouped by business → one amount → Add to cart → Flow 9.
3. **Empty state:** "No outstanding license fees for this account." + links: check spelling · contact treasurer.

## Flow 5 · Utilities (verified)
1. `[UT-1 Find utility account]` Ticket No. or Customer No. + Last/Business name (tooltip: "Ticket No. is on your bill").
2. `[UT-2 Utility bills]` service period, ticket, due, amount → Add to cart → Flow 9.
- One Utilities item. `util-inq` is an alias and is not shown. There is no payment history and no UT-3.

## Flow 6 · Consumer Tax (private)
1. `[CT-1 Choose tax type]` the types on file for that county (Meals, Lodging, Food & beverage, Gas, and others). Access is Business ID/SSN or last name + password.
2. `[CT-2 Access]` Business ID / SSN + Business name, **or** Last name + Password.
3. `[CT-3 Tax periods due]` period, due date, amount → Add to cart → Flow 9.
- Replace legacy "session may freeze" notice with a submit button that shows a spinner + locks until response; show success/failure clearly.

## Flow 7 · Pet Tags (verified)
1. `[PT-1 Pet tags]` two paths: **Renew a tag** (owner last name) · **License a new pet**.
2. `[PT-2 Your pets]` cards: pet name, breed/colour, gender, tag no., expiry, status → **Renew**.
3. `[PT-3 Renew tag]` read-only owner + pet info, editable phone, **Rabies vaccination expiry** date → license type options appear only when date is valid. Expired date → inline field error "Rabies vaccination expired on 06/30/2026. Update your pet's vaccination before renewing." (no modal).
4. Mailing / attention details → Add to cart → Flow 9.
5. `[PT-4 License a new pet]` owner, pet, vaccination, license type from `petLicenseTypes` → Add to cart.

## Flow 8 · Look-ups (no payment unless stated)
- **RE Public Inquiry:** `[IQ-1 Find]` (Name · Account · Map ID · Street + optional projected payment date for penalty/interest) → `[RE-2]` → `[IQ-2 Tickets]` (expandable rows: Name, Description, Map ID, Balance, Details) → `[S-TK Ticket detail]` with transaction history.
- **Mineral Inquiry:** view only. Business name / federal ID. No Pay control. `min-inq` is inquiry-only.
- **Taxes Paid by Year:** RE uses `[YP-1]` Name + Calendar year. PP (`yr-pp`) is sign-in only. Then `[RE-2]` → `[YP-2 Paid in {year}]` principal paid per ticket, total, **Print / Download** (used for tax filing).
- **RE Public Inquiry** Pay on a row that has a balance.
- **PP Inquiry:** ✅ already built.
- **Processing notice** on every look-up result: "Payments made in the last 10 business days may not show returned items yet."

## Flow 9 · Shared checkout (every Pay service)
1. **Cart** `[CO-1 Review your payments]` table: Dept, Ticket, Name, Tax type, Description, Amount. Remove only when `allowRemoveNonDelinquent` is on and the row is not delinquent. A delinquent row shows a shield and "Paid oldest first". Total. **Clear cart** (inline confirm). Mixed tax types allowed. County `checkoutNotices` sit above the table.
2. **EmailCapture** the first time the cart goes from empty to one item and no receipt email is stored.
3. **Human check** inline on CO-1 (existing hCaptcha) — not a separate page.
4. **Choose how to pay** `[CO-2]` two cards: **eCheck — no fee** · **Credit/debit card** with `cardFee.percent` and/or `cardFee.flat`. No card-number fields. Card pay is a redirect.
5a. **Card** `[CO-3 Card summary]` payment amount, processing fee, total, processor note ("Card details are handled by {processor}; the county does not store them") → **Continue to secure payment** → processor hosted page (not designed by us) → back to receipt.
5b. **eCheck** `[CO-4 Bank details]` name on check when `eCheckNameOnCheck` is true, routing no. (+ confirm), account no. (+ confirm), hide/show toggle. When `validateRouting` is true, verify the routing number and ask "Is this your bank?" before authorize. **Live check preview**, warning "Don't use a deposit slip", returned-check fee disclosure, authorization checkbox → **Authorize payment**.
6. **Receipt** `[CO-5]` success header, payment type, date, reference no., transaction no., amount paid, fee, total applied, line items, and a line that the receipt was emailed. **Print**, **Resend email**, **Make another payment**. Print stylesheet = county letterhead.
7. **Failure** `[CO-6]` declined / bank not verified → reason + **Try again** / **Use another method**; cart preserved.

## Flow 10 · e-Bill Options
1. `[EB-1 Go paperless]` tabs: Real Estate · Personal Property · Utilities.
   - RE: Account · Street · Last name. PP: Ticket/Customer No. + Last name (or signed in). Utilities: Ticket/Customer No. + Last name.
2. RE only: `[RE-2]` select record.
3. `[EB-2 Billing preference]` record summary + radio **Paper bill / Electronic bill** + Email + Confirm email. Terms link only when `ebillTermsUrl` is set. → **Save preference**.
4. `[EB-3 Confirmation]` "We'll email bills to j***@mail.com starting with the next bill." Terms link only when `ebillTermsUrl` is set.
5. `[EB-4 Your e-bills]` list with **View PDF**.

## Flow 11 · Flex payment (one Pay item per county.flex code)
1. Sidebar or tile titled from `flexTypes[code].title`. The link sets `?type=<code>`.
2. Intro is one or more paragraphs from `flexTypes[code].intro`.
3. Mode **T**: pick a charge from a table, then the configured fields (each field has visible and required flags).
4. Mode **K**: the payer types the amount.
5. Mode **C**: look up a ticket, then a list, then one amount.
6. State is a dropdown. Zip is 5 digits plus the optional 4. Then Flow 9.
