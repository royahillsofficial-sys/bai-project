# Pet Tags · PT-1 … PT-4  (verified)

## Prompt for Cursor
> **PT-1 Pet tags:** two large choice cards: "Renew a pet tag" (field: owner last name → Search) and "License a new pet" (→ PT-4).
> **PT-2 Your pets:** PetCard grid: pet name, colour, gender, tag no., license expiry, status badge (active / expiring / expired) → "Renew".
> **PT-3 Renew tag:** read-only owner (name, address, city/state/zip) and pet (name, gender, colour). Editable: Phone. Rabies vaccination expiry (date picker). License type select appears only after a valid, future rabies date; the options come from `petLicenseTypes`. Expired → field error "Vaccination expired on {date}. Update your pet's vaccination before renewing." Mailing / Attention details. Fee shown live. Add to cart.
> **PT-4 License a new pet:** steps Owner → Pet → Vaccination → License type; same fields as PT-3, editable. Add to cart.
> Use only tokens, classes and components from /bai-spec/00 and /bai-spec/03. Add as new <section class="screen"> blocks in index.html; register routes in ROUTES. Include loading, empty and error states. Mobile: tables become stacked cards under 720px.
