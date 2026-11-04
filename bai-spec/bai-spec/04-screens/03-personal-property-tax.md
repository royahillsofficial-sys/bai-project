# Pay Personal Property Tax · PP-1 / PP-2  (private)

## Prompt for Cursor
> **PP-1 Access your records:** lead "Paying for someone else? Use the department and ticket number from their bill." If signed in, skip straight to PP-2 with a chip "Signed in as {name} · Not you?". Else SearchMethodSwitch: "Sign in" (existing sign-in card inline) · "Dept + Ticket No." (Last name, Department with hint "e.g. PP2026 = PP + tax year", Ticket No.) · "Account No." (Last name, Account No.). Secondary link "Create account / password options" → existing register.
> **PP-2 Your personal property bills:** reuse RE-3 layout: RecordHeader (name), read-only BillTable rows per vehicle/item (Dept, Ticket No., Seq, Due date, Description e.g. "2019 Honda Civic", Amount, status). One AmountEntry for the record, oldest-first allocation preview, Total due, Add to cart / Checkout.
> Reuse the approved PP Inquiry vehicle visuals where possible.
> Use only tokens, classes and components from /bai-spec/00 and /bai-spec/03. Add as new <section class="screen"> blocks in index.html; register routes in ROUTES. Include loading, empty and error states. Mobile: tables become stacked cards under 720px.
