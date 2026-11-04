# 03 · Component Library

Build each as a JS render function (same pattern as the existing `MENU` renderer). Every service screen is assembled from these. **No screen-specific one-off components.**

| # | Component | Built from (existing) | Props | States |
|---|---|---|---|---|
| 1 | `CountyShell` | `.app .topbar .sidebar` | county config | signed-in / guest |
| 2 | `SideNav` | `#menu-groups`, `MENU` | `config.services`, `labels`, `links` | collapsed, mobile drawer, active item, group hidden when empty |
| 3 | `CartButton` | `.icon-btn` + `.count` | item count, total | 0 (hidden count), n items, pulse on add |
| 4 | `CartDrawer` | `.scrim` + drawer | items, `delinquent`, `year`, `recordKey` | empty, list, remove only when allowed, delinquent lock "Paid oldest first", checkout notices |
| 5 | `PageHeader` | `.main-head .kicker .lead` | module, title, lead, back link | — |
| 6 | `HelpPanel` ("How this works") | `.short-fold` / `.guide-launch` | steps, where-to-find-numbers image | collapsed / open |
| 7 | `SearchMethodSwitch` | `.seg` | methods[] from `config.search[service]` | selected |
| 8 | `LookupForm` | `.field .input .hint` | fields per method, hint text | empty, typing, invalid, submitting |
| 9 | `ProjectedDateField` | `#proj-form .calendar` | date, explainer | default today, past date error |
| 10 | `ResultsTable` | `.tickets .table-scroll .pager` | columns, rows, `onSelect`, address/mapId toggle | loading (`.skel-row`), empty, 1 result (auto-select), n results, paginated |
| 11 | `RecordHeader` | `.detail-head .info-grid` | owner, name 2, account, map/parcel, address, description | — |
| 12 | `BillTable` | `.tickets` + `.badge` | bills[], `payable` | due, overdue, paid, partially paid; desktop table / mobile cards |
| 13 | `AmountEntry` | `.amount-card .input .money` | one amount per record | full, partial, > balance error, 0 error. Bill rows stay read-only. An allocation preview shows oldest-first. Prepay never shows the amount owed. |
| 14 | `AddToCartBar` | `.actions .btn-primary .btn-ghost` | total selected | disabled until amount valid |
| 15 | `TicketDetail` | approved `ticket` screen | ticket | already built — reuse for RE, Mineral |
| 16 | `TransactionTable` | `.timeline .tx-*` | charges/payments/balance | none, list |
| 17 | `InlineNotice` | `.banner .warn .success` | tone (info/warn/danger/success), title, body, action | replaces every legacy "Error on Page" modal |
| 18 | `EmptyState` | `.empty` | title, reasons[], actions[] | — |
| 19 | `HumanCheck` | `.hcaptcha*` | — | unchecked, verifying, ok, failed |
| 20 | `PaymentMethodChooser` | `.choice` cards | amount, `cardFee.percent`, `cardFee.flat` | eCheck selected / card selected. No card-number fields. |
| 21 | `FeeSummary` | `.sum-card .sum-col` | amount, fee, total | — |
| 22 | `ECheckForm` + `CheckPreview` | `.field .switch` + new SVG check | name (when `eCheckNameOnCheck`), routing, account | masked/unmasked, mismatch, routing verified, "Is this your bank?" when `validateRouting`, invalid |
| 23 | `Receipt` | `.print-head .info-grid #print-btn` | payment, lines[] | success; emailed line; Resend email; print layout |
| 24 | `PetCard` / `RecordCard` | `.card .badge` | pet or record summary, action | active, expiring, expired |
| 25 | `PreferenceForm` | `.choice .input` | current preference, email | paper / electronic, email mismatch |
| 26 | `StepIndicator` | `.steps-mini` | steps[], current | used in checkout: Review → Pay → Receipt |
| 27 | `EmailCapture` | `.card.short .field` | email, confirm | hidden once stored; masked "Receipts go to j***@mail.com · Change"; saved-cart banner |
| 28 | `AllocationPreview` | `.point` | bills[], amount | oldest year first; used on RE and PP pay |
| 29 | `FlexForm` | `.field .choice` | mode T, K, or C; fields with visible and required | intro paragraphs, state dropdown, zip 5+4 |

## Copy for replaced legacy errors
| Legacy modal | New `InlineNotice` / `EmptyState` |
|---|---|
| EXISTING CHARGES FOUND – PREPAYMENTS ARE ONLY AVAILABLE WHEN NO BALANCE IS DUE | **This property has a balance due.** Prepayments open once the balance is paid. → [Pay balance] |
| NO OUTSTANDING PAYMENTS FOUND FOR LAST NAME AND ACCOUNT NUMBER ENTERED | **Nothing to pay right now.** We found no outstanding fees for that name and account. Check the spelling or account number, or [contact the Treasurer]. |
| RABIES VACCINATION EXPIRED | Field error: **Vaccination expired on {date}.** Update the vaccination before renewing. |
| Your session may freeze upon submitting filing… | (removed — button shows "Submitting…" and locks; result shown inline) |
| If no names are found, try searching by last name only (red) | `.hint`: "Tip: last name only finds more matches." |
