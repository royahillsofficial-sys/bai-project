# e-Bill Options · EB-1 / EB-2 / EB-3 / EB-4

## Prompt for Cursor
> **EB-1 Go paperless:** lead "Get your bills by email instead of post." Tabs Real estate · Personal property · Utilities. RE: SearchMethodSwitch Account · Street · Last name → RE-2. PP and Utilities: Ticket No. or Customer No. + Last name (PP skips if signed in). Show the terms link only when `ebillTermsUrl` is set. Continue.
> **EB-2 Billing preference:** RecordHeader (account no., name, map no.), PreferenceForm: radio "Paper bill by post" / "Electronic bill by email"; Email + Confirm email (required for electronic; mismatch error inline). Buttons Previous / Save preference.
> **EB-3 Saved:** success banner "Your bills will be emailed to j***@mail.com starting with your next bill." Links: Set up another account · Back to home.
> **EB-4 Your e-bills:** list of bills already set to email, each with View PDF. Empty state when none are on file.
> Use only tokens, classes and components from /bai-spec/00 and /bai-spec/03. Add as new <section class="screen"> blocks in index.html; register routes in ROUTES. Include loading, empty and error states. Mobile: tables become stacked cards under 720px.
