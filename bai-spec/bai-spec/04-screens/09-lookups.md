# Look-ups · IQ (RE Public Inquiry) / MN (Mineral) / YP (Taxes Paid by Year)

## Prompt for Cursor
> **IQ-1 Real estate public inquiry:** SearchMethodSwitch Name · Account No. · Map ID · Street name + ProjectedDateField ("To estimate penalty and interest, choose your planned payment date"). Search → RE-2.
> **IQ-2 Tickets for this property:** RecordHeader + list of tickets by year (Dept e.g. RE2006, Ticket, Seq, Account, Due date) with expandable row (Name, Description, Map ID, Balance, Details). Balance > 0 → "Pay" (adds that balance to the cart). Details → existing TicketDetail with TransactionTable (Date, Type, Transaction no., Amount, Balance). Processing InlineNotice: "Payments made in the last 10 business days may not show returned items yet." Buttons New search / Back.
> **MN Mineral inquiry:** view only. Same find and ticket list as IQ-1/IQ-2; Name label "Business or owner name", Account label "Account / Federal ID". No Pay and no Add to cart. `min-inq` is in `inquiryOnly`.
> **YP-1 Taxes paid by year (RE and PP share one screen, title from service):** RE: Name (hint "Last name first; businesses enter business name") + Calendar year select (last 10 years). PP (`yr-pp`) is sign-in only. → RE-2.
> **YP-2 Paid in {year}:** RecordHeader, table (Dept, Ticket, Description, Date paid, Principal paid), total, buttons Print / Download (for tax filing). Empty: "No payments recorded for {year}."
> Use only tokens, classes and components from /bai-spec/00 and /bai-spec/03. Add as new <section class="screen"> blocks in index.html; register routes in ROUTES. Include loading, empty and error states. Mobile: tables become stacked cards under 720px.
