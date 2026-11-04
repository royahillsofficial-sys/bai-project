# 00 · Design System (source: approved `index.html`)

**Rule zero:** every new screen is a `<section class="screen" data-screen="...">` inside the existing `#app` shell (topbar + `#sidebar` + `#content`). No new layout shells.

## Tokens (already defined on `:root`, with dark-mode overrides — reuse, never hardcode)
| Group | Tokens | Use |
|---|---|---|
| Ink | `--ink-900 #141B34` `--ink-800 #1E2750` `--ink-700` `--ink-100` `--ink-50` | Headings, hero, sidebar |
| Surface | `--canvas #F7F6F2` `--card #FFF` `--line #E6E3DC` | Page bg, cards, dividers |
| Text | `--text #1B1F2E` `--text-muted #6A6F80` | Body / secondary |
| Action | `--action #0E7A68` `--action-hover #0C6B5C` `--action-soft` `--action-text` | Primary buttons, links, focus |
| Calm | `--calm #14A38B` `--calm-soft` `--calm-text` | Info, reassurance, "how this works" |
| Status | `--paid*` green · `--due*` amber · `--danger*` red | Badges, notices, validation |
| Shape | `--radius 16px` `--shadow` `--shadow-sm` `--top 64px` | Cards, topbar height |

Fonts: **Plus Jakarta Sans** (headings), **Inter** (body/UI), **Nunito** (numbers/amounts). Money always right-aligned, tabular figures (`.money`, `.mono`).

## Existing components to reuse (class names in `index.html`)
- Layout: `.app .topbar .sidebar .main .main-head .wrap .split .grid-2 .card .card-h .panel`
- Nav: `#menu-groups` (rendered from `MENU`), `.group .group-btn .item .rail-search .nav-search .side-foot`
- Buttons: `.btn .btn-primary .btn-ghost .btn-ink .btn-block .btn-print .text-btn .icon-btn .chip .chip-btn`
- Forms: `.field .input .hint .seg` (segmented control) `.switch .choice .code-box .meter` `.hcaptcha*` (human check), `.calendar` (date picker), `#proj-form` (projected payment date)
- Data: `.tickets .table-scroll .pager .pages .badge .pill .status .paid .due .overdue .due-flag .money`
- Summary: `.hero .hero-amt .sum-card .sum-col .sum-due .amount-card .stat .info-grid .detail-*`
- Feedback: `.banner .warn .success .empty .skel .skel-row .toast .err-code`
- History: `.timeline .tx-head .tx-type .tx-count`
- Steps: `.stepper .step .step-num .steps-mini`
- Print: `.print-head #print-btn`
- Accessibility: `#text-size` controls, `.skip` link, `#a11y-btn` — keep on every screen.

## Rules for every new screen
1. Page header = `.main-head` with kicker (module name), H1 (task), one-line `.lead`.
2. One primary action per screen (`.btn-primary`), bottom-right on desktop, full-width on mobile.
3. Legacy "Error on Page" modals → **inline** `.banner.warn` / `.banner` with a next-step link. Never `alert()`.
4. Legacy red italic hint text → `.hint` under the field; legacy red notices → `.banner.warn`.
5. Legacy "Show 25 entries / First Previous 1 Next Last" → existing `.pager` + `#page-size`.
6. Remove legacy version strings (`Version: 251210-1412`) from UI — move to footer `.side-foot` in small muted text if BAI wants it.
7. Tables collapse to stacked cards below 720px (same as the approved PP ticket list).
8. Every amount shows `$` + 2 decimals. Dates `MM/DD/YYYY` (US).
9. Empty, loading (`.skel`), error and success states are required for every list.
10. All copy in sentence case. No ALL CAPS messages.
