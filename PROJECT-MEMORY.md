# BAI e-Treasurer — project memory

Handoff for the citizen e-Treasurer demo. This file describes the project as it stands. Extend `index.html`. Do not redesign it.

## What this is

A single-file citizen treasurer prototype. People look up a bill and pay it. There is no build step and no server. Open `index.html` in a browser, including from `file://`.

Repo: https://github.com/royahillsofficial-sys/bai-project

GitHub `main` is commit `35c8604`. One local change is not pushed yet: a 16px gap between the password field and the Sign in button in `index.html`.

## How the code is organized

- `index.html` is the app: CSS, HTML, and one script. This file is the source of truth.
- Specs are in `bai-spec/bai-spec/` (the folder is nested). Start with `00-design-system.md` and `03-component-library.md`.
- `COUNTY_CONFIG` is embedded in `index.html`. The same data is in `bai-spec/bai-spec/county.config.json`. On load the page tries to fetch the JSON. If that fetch succeeds, it replaces the embedded defaults and counties. A stale JSON file wipes newer keys. Keep both copies identical.
- The sidebar is built from `MASTER_MENU` in `index.html`, filtered by the county `services` list. Demo County is the county that is turned on.

## Rules that are already decided

- Reuse the existing CSS tokens, classes, and components. Do not add new colors, fonts, radii, or button styles.
- Exception already approved: action buttons are `#0E7A68`, hover `#0C6B5C`.
- No `alert`, `confirm`, or `prompt`. No external libraries. Icons are inline SVGs in the Lucide stroke style so `file://` still works.
- Do not remove existing IDs or functions.
- Sentence case. US dates. Money as `$0.00`.
- Do not show a description under main page titles. `pageHead` ignores a lead argument.
- Do not invent legal or disclaimer copy. A short Real Estate disclaimer was added and then removed. The original Legal Statement and Personal Property inquiry terms were already in the file and stay.
- Empty search fields fill demo data and the search still continues. That is intentional. The decline-routing value `000000000` stays.
- Never show an amount owed on prepay. Never render a card-number field. Card payment is a redirect.
- Do not change git config. Commits for this repo use author `royahillsofficial` and email `royahillsofficiual@gmail.com` (spelled that way on purpose). Do not commit as any other GitHub account. The remote URL must not contain an access token.

## What the app does now

Landing opens on **Select a service**, not the terms page. Terms stay available from County links / legal.

Sidebar groups are **Payment Options** and **Inquiry Options**.

The service list is a card grid. Each card has an inline icon and a line generated from that service’s configured search methods.

Search screens with more than one method (Real Estate, Personal Property, and the same pattern elsewhere) use one centered card, class `.signin-stack`, width `min(520px, 100%)`. Tabs are an underline: Sign in, Name, Account no., Parcel no., Dept. / ticket no. Only the fields inside the card change. The page title stays at the top of the content, for example:

Payment Options  
Personal Property Tax

Sign-in inside that card is Email / Social Security Number, email, password, Sign in, Forgot password, Create New Account. There is a 16px gap between the password field and the Sign in button. That gap is only on the local file right now.

Signing in is a demo. Any submit sets Jane Keaton, account `180624`, `jane.keaton@example.com`, and `state.signedIn = true`.

## Real Estate Tax

Search methods, in both the embedded config and `county.config.json`: password, name, account, parcel, dept/ticket.

- Name search shows a list with Name, Name 2, and Map ID. “Coleman” returns three people.
- Account, parcel, and dept/ticket skip the name list and open the ticket list.
- Ticket list: checkboxes choose what can go in the cart. One amount field for the whole selection, not one per row. Totals are shown. Sort and pagination are on (page size 2).
- Add to cart only if the user is signed in. Otherwise the button says Sign in.
- Owner / profile details show only after sign-in.
- “Where to find these numbers” is not on the Real Estate search page.
- Ticket detail shows balance, dept, ticket, half, due, description, status, and payments. After sign-in it also shows name, name 2, account, map, parcel, address, acreage, mortgage, and values.
- Checkout review has Clear cart, Back, and Continue.

Demo person: Coleman Amanda L, map `45-12`, account `43110001`. Extra overdue 2024 halves exist so the list has two pages.

## Personal Property

Jane Keaton’s bills are the demo. Do not change the `JANE_TICKETS` math. Her hero total stays `150012` cents. `DEMO_TODAY` is 24 Sep 2026.

## Parking Fines

Demo County only. Vehicle tag `ABC-1842`, Jane Keaton, `jane.keaton@example.com`. Citations `P-44102` ($25.00, Main Street at Court, expired meter) and `P-44188` ($40.00, 200 Church Street, overtime). Total $65.00. Empty fields fill those values. Match on tag or citation number.

## Checkout and cart

Cart item shape: `{id, service, dept, ticket, name, taxType, description, amount, delinquent, year, recordKey}`. Receipt email uses `sessionStorage` and a cookie. The cart is seeded only when the URL has `?demo-cart=1` and no cart key exists.

## Known quirks

- `audit()` expects the original `MASTER_MENU` item label order. Group labels were renamed. Item labels inside the menu were not.
- A 2025 payment can show on the 2024 Real Estate bill because those rows share a ticket number.
- `file://` cannot fetch the JSON, so it uses the embedded `COUNTY_CONFIG`. If you change county data, change both copies.
- GitHub `main` and this folder match at `35c8604`, except the uncommitted password-button gap.

end