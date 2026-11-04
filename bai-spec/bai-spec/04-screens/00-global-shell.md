# Global shell · S-00 / S-01 / NAV / CART

## Prompt for Cursor
> Refactor the existing `MENU` array in index.html so the sidebar is rendered from `/bai-spec/county.config.json` (default county = "demo"; allow `?county=culpeper`). Groups: Pay, Look up, Account, e-Commissioner (external links), County links. Apply `labels` overrides. Hide empty groups. Replace topbar county text with `config.name` and `config.treasurer`.
> Add a **CartButton** to the topbar (count badge, opens CartDrawer). Cart state lives in a single `cart` store (array of {dept, ticket, name, taxType, description, amount, service, delinquent, year, recordKey}) shared by all services; persist in sessionStorage inside try/catch. Remove a line only when `allowRemoveNonDelinquent` is true and the line is not delinquent. A delinquent line shows a shield and the text "Paid oldest first". `?demo-cart=1` seeds one delinquent RE2024 line and one current RE2026 line. Clear cart stays available, with the confirm inline.
> **EmailCapture** sits in the cart drawer the first time an item is added and no receipt email is stored: Email, Confirm email, and "Used to save your cart and send your receipt." Save it in sessionStorage and a cookie, both inside try/catch. After that, the cart shows "Receipts go to j***@mail.com · Change". If a stored cart loads, show "We saved your cart from your last visit."
> Upgrade the **Service home** (S-01) into: welcome line, refund policy (from config), sanitized `homeHtml` (only p, a, strong, em, ul, li), and service tiles grouped Pay / Look up / Account. Utilities is one tile. `util-inq` is an alias of `util` and is not shown. One Pay item per `county.flex` entry, titled from `flexTypes`, linking `?type=<code>`. An optional Help group comes from `helpPages` and hides when empty. County `checkoutNotices` render in the cart.
> Keep Terms (S-00) as is but show it once per session (sessionStorage flag).
> Use only tokens, classes and components from /bai-spec/00 and /bai-spec/03. Add as new <section class="screen"> blocks in index.html; register routes in ROUTES. Include loading, empty and error states. Mobile: tables become stacked cards under 720px.

## Acceptance
- Switching county changes menu, labels, header, refund text — no code edits.
- Out-of-scope services never render even if listed.
