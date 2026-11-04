# 01 · Information Architecture

## The three actors (from the PM call)
| Phase | Actor | App | In this build? |
|---|---|---|---|
| 1 | **Citizen** — views tickets, pays taxes | e-Treasurer (citizen app) | **Yes** |
| 2 | Commissioner — creates tickets (RE, PP, etc.) | e-Commissioner | No |
| 3 | County employee — settings, which menus each county sees | Employee package | No (but our nav config is what it will control) |

Data path: Commissioner creates ticket → AS/400 backend → shown to citizen. Field values come from the backend; we design the fields, not the data.

## Modules (citizen app)
```
e-Treasurer (county-branded)
├── Home ............................ service home (welcome, refund policy, service tiles)
├── Pay
│   ├── Real Estate Tax              [public]
│   ├── Personal Property Tax        [private]
│   ├── Prepay Real Estate Tax       [public]
│   ├── Prepay Personal Property Tax [private]
│   ├── Business License             [private]
│   ├── Utilities                    [verified]  (one item; util-inq is an alias)
│   ├── Consumer Tax                 [private]  (tax type comes from county data)
│   ├── Pet Tags                     [verified] (license types from config)
│   └── Flex payment                 [per county.flex] one Pay item, title from flexTypes
├── Look up
│   ├── Real Estate Public Inquiry   [public]   (Pay on a balance)
│   ├── Personal Property Inquiry    [private]  ✅ already approved
│   ├── Real Estate Taxes Paid (yearly)       [public]
│   ├── Personal Property Taxes Paid (yearly) [private, sign-in only]
│   └── Mineral Inquiry              [public]   (view only)
├── Help (optional, from helpPages; hidden when empty)
├── Account & preferences
│   ├── e-Bill Options (RE / PP / Utilities)
│   ├── Sign in · Register · Forgot password  ✅ already approved
│   └── Terms & conditions (generic, once per session) ✅ already approved
├── Cart → Checkout → Receipt (shared by every Pay service)
└── County links (external): e-Treasurer home, e-Commissioner home, e-Assessor home, County main page, Contact treasurer
```

## Access model (decides whether sign-in is required)
| Level | Meaning | How user gets in | Services |
|---|---|---|---|
| **public** | Public record | Search by name / account / map-parcel ID / street / dept-ticket. No login. | RE Tax, Prepay RE, RE Inquiry, RE Taxes Paid, Mineral |
| **verified** | Record key + last name | Ticket/customer no. + last name. No account needed. | Utilities, Pet Tags |
| **private** | Personal data | Signed in (existing sign-in), **or** one-time lookup by Dept + Ticket No. + last name / Account No. + last name | PP Tax, Prepay PP, PP Inquiry, PP Paid, Business License, Consumer Tax |

- Sign in **once per session**; it carries across every private service (confirmed by PM).
- Terms shown **once**, generic, not per service (confirmed by PM). The legacy "Legal Statement" first screen is out of scope.

## Master side navigation
Every item exists in code. `county.config.json` decides what each county sees. Groups with no visible items hide automatically.

| Group | Item ID | Default label | Phase-1 scope |
|---|---|---|---|
| Pay | `re-tax` | Real Estate Tax | ✅ |
| Pay | `pp-tax` | Personal Property Tax | ✅ |
| Pay | `pre-re` | Prepay Real Estate Tax | ✅ |
| Pay | `pre-pp` | Prepay Personal Property Tax | ✅ |
| Pay | `biz` | Business License | ✅ |
| Pay | `util` | Utilities | ✅ |
| Pay | `cons` | Consumer Tax | ✅ |
| Pay | `pets` | Pet Tags | ✅ |
| Pay | `decals` | Decals | ⛔ out of scope (keep in config, off) |
| Pay | `park` | Parking Fines | ✅ demo county |
| Pay | `permit` | Building Permit | ⛔ |
| Pay | `landfill` | Landfill Fees | ⛔ |
| Pay | `airport` | Airport Fee | ⛔ |
| Pay | `public-svc` | Public Service | ⛔ |
| Pay | `flex:<code>` | title from `flexTypes` | ✅ one item per `county.flex` (Marion: Residential zoning permit) |
| Pay | `zoning` | Zoning / Sign / Special Use Permits | ⛔ kept in the master list, off unless a county lists it |
| Look up | `re-inq` | Real Estate Public Inquiry | ✅ |
| Look up | `pp-inquiry` | Personal Property Inquiry | ✅ done |
| Look up | `yr-re` | Real Estate Taxes Paid | ✅ |
| Look up | `yr-pp` | Personal Property Taxes Paid | ✅ sign-in only |
| Look up | `util-inq` | Utility Inquiry | alias of `util`; not shown |
| Look up | `min-inq` | Mineral Inquiry | ✅ view only |
| Help | `help:<id>` | title from `helpPages` | optional; hidden when the county has none |
| Account | `ebill` | e-Bill Options | ✅ |
| Account | `register` | Create account | ✅ done |
| Account | `forgot` | Forgot password | ✅ done |
| e-Commissioner | `file-biz` `file-cons` `cards` `vehicle` `req-pp` `addr` | (links to Phase 2) | ⛔ links only |
| County links | `home-t` `home-c` `home-a` `county` `contact` `legal` | external links | ✅ links |

**Label overrides per county** (same screen, different words): Mecklenburg "Unpaid Real Estate Tax" = `re-inq`; "Paid Real Estate Tax" = `yr-re`; Culpeper "RE Taxes Paid" = `yr-re`, "CO-Address Change Request" = `addr`.

## Removed from the legacy nav (propose to client)
1. Legacy "Payment Help" / "Inquiry Options Help" groups → a county may still publish an optional **Help** group from `helpPages`. Each service also keeps a **How this works** panel (`HelpPanel`).
2. "– OLD" / "– NEW" duplicate groups → one list.
3. "Multiple Payments" → replaced by the **global cart** (topbar cart button with count).

## Global chrome (every screen)
Topbar: county seal + name + treasurer name · search menu · **Cart (n)** · text size · profile/sign in. Sidebar: config-driven groups. Footer: county contact, refund policy link, terms link, version (muted).
