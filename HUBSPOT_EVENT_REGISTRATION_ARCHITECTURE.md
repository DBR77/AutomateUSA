# DBR77 event registration architecture — HubSpot

Status: implementation specification. Do not publish AI Tour or IEX forms until their dedicated HubSpot form GUIDs are assigned and verified.

## Three independent registration streams

| Event code | Public page | HubSpot form | Operational list |
|---|---|---|---|
| `IEX_2026` | `https://iex2026.dbr77.com/` | `DBR77 | EVENT | IEX USA 2026 | Registration` (`4930d8c8-3c01-48ca-ac73-41aa7ca53659`) | `DBR77 | EVENT | IEX USA 2026 | Registered` (ID `1932`) |
| `AI_TOUR_2026` | `https://aitour.dbr77.com/` | `DBR77 | EVENT | AI Tour USA 2026 | Registration` (`10fb95a0-021f-4d5e-b835-96c0033ecebb`) | `DBR77 | EVENT | AI Tour USA 2026 | Registered` (ID `1931`) |
| `IMTS_2026` | `https://imts.dbr77.com/` (currently `https://automate.dbr77.com/`) | existing form GUID `eece5c36-22c1-41a5-b4e7-223a14e7f328`; rename to `DBR77 | EVENT | IMTS 2026 | Lead / Meeting` | `DBR77 | EVENT | IMTS 2026 | Leads` |

The three lists are HubSpot active lists, not separate external databases. A person can belong to more than one event list without creating duplicate contacts because email remains the contact identity.

## Shared contact properties

- `dbr77_event_code` — multi-checkbox: `IEX_2026`, `AI_TOUR_2026`, `IMTS_2026`.
- `dbr77_event_status` — `registered`, `pending_confirmation`, `confirmed`, `attended`, `no_show`, `cancelled`.
- `dbr77_event_location` — workshop/city or `online`.
- `dbr77_event_interest` — primary subject selected by the visitor.
- `dbr77_event_source_url` — page URL that produced the submission.
- `dbr77_event_registered_at` — submission timestamp.
- `dbr77_event_marketing_consent` — separate explicit consent; never inferred from event-administration consent.

## Event-specific fields

### IEX 2026

- first name, last name, business email, company, position;
- primary conversation/interest;
- access type: online / studio invitation request;
- report and recording entitlement after registration.

### AI Tour 2026

- first name, last name, business email, company, role;
- selected workshop location and date;
- manufacturing priority and optional challenge;
- event-administration consent and separate optional solutions-contact consent.

### IMTS 2026

- first name, last name, business email, phone;
- manufacturing challenge / requested conversation;
- source domain must become `imts.dbr77.com` after DNS cutover.

## Required HubSpot workflows

1. Form submission sets the event code and event-specific status.
2. The active list filters on event code plus the corresponding form submission.
3. The confirmation email and internal notification are event-specific.
4. Existing contacts are updated, not duplicated.
5. Marketing subscription is changed only when the separate marketing consent is checked.
6. Test records use `integration.test` in the email/local marker and are excluded from production lists and reporting.

## Acceptance test for each event

1. Submit a unique internal test address from the public domain.
2. Receive HTTP `2xx` from HubSpot.
3. Read the contact back from the CRM and verify all mapped properties.
4. Verify membership in exactly the intended event list.
5. Verify no membership in the other two event lists.
6. Verify the correct confirmation workflow and sender.
7. Verify mobile and desktop success/error states.

## Current verified state — 2026-08-28

- IMTS form submission endpoint is live and accepted a technical test.
- AI Tour local code submits to its dedicated HubSpot form GUID.
- IEX local code submits to its dedicated HubSpot form GUID.
- AI Tour active list `1931` and IEX active list `1932` filter on their respective form submissions.
- IMTS active-list creation is pending because the renamed existing form has not yet appeared in the segment-builder form index.
- The local newsletter-builder process is not running with `HUBSPOT_ACCESS_TOKEN`, so dedicated form/list/property creation and authenticated CRM read-back remain unavailable from the local API process.
