# DBR77 USA event journey audit — 2026-08-28

## Release decision

**PARTIAL / DO NOT START THE EXTERNAL NEWSLETTER SEND YET.**

The corrected AI Tour and IEX journeys work locally, but the public AI Tour and IEX domains still serve older prototypes that do not submit to HubSpot. The IMTS form on `automate.dbr77.com` is already connected to its separate HubSpot form.

## Journey matrix

| Journey | Entry point | Destination | HubSpot form | Result |
|---|---|---|---|---|
| AI Tour newsletter main CTA | `Save the Date Near You` | `https://aitour.dbr77.com/#apply` | AI Tour | Ready in newsletter builder; public LP stale |
| AI Tour newsletter city CTA | Six city tiles | `?workshop=<city>#apply` | AI Tour | Ready; location is preselected locally |
| AI Tour LP primary registration | Hero, location cards, final CTA | Registration form | `10fb95a0-021f-4d5e-b835-96c0033ecebb` | Ready locally |
| AI Tour partner enquiry | Partner tab | Partner form | AI Tour form, marked `Journey: Partner enquiry` | Ready locally |
| IEX registration | All registration CTAs | IEX registration form | `4930d8c8-3c01-48ca-ac73-41aa7ca53659` | Ready locally |
| IMTS meeting request | `automate.dbr77.com` | IMTS form | `eece5c36-22c1-41a5-b4e7-223a14e7f328` | Live |

## Verified

- Desktop layout: no horizontal overflow.
- Mobile layout at 390 × 844: no horizontal overflow; AI Tour form fits the viewport.
- Six AI Tour locations and dates are consistent between newsletter and LP.
- Newsletter city links use distinct slugs and open the correct preselected workshop.
- AI Tour host photos load successfully (Torian Richardson and Piotr Wiśniewski).
- Host LinkedIn and meeting links are present.
- AI Tour and IEX use separate HubSpot form GUIDs.
- Successful registration UI appears only after a successful HubSpot response.
- Event administration consent is separate from the optional solutions follow-up choice.
- AI Tour calendar links are generated only after a successful registration.
- Local browser console showed no warnings or errors after the partner-form correction.

## Blocking findings

1. `aitour.dbr77.com` still contains the old local-only prototype and does not contain the AI Tour HubSpot GUID.
2. `iex2026.dbr77.com` still contains the old local-only prototype and does not contain the IEX HubSpot GUID.
3. The locally linked Railway project is `Pitchdeck`, not the service serving the event domains. Deploying from this context would risk changing the wrong site.
4. The AI Tour and IEX HubSpot forms currently encode workshop/interest details in submission context rather than dedicated structured contact properties. This is sufficient for attribution and separate lists, but weaker for reporting and automation.
5. The separate active IMTS registered list is not yet verified. AI Tour list ID is `1931`; IEX list ID is `1932`.
6. HubSpot marketing-contact status and subscription handling must be checked before the external send. Event administration consent alone must not be treated as general marketing consent.

## Content review

- The main narrative is practical and anti-hype: profitability, production flow, recurring losses and evidence before technology.
- The first CTA asks only for the intended action: select a local date and register.
- Scarcity is not fabricated; the copy says the application does not yet confirm a seat.
- The audience is clear: C-level, operations and plant leaders.
- The host pairing is credible and differentiated: technology leadership plus manufacturing/automotive operating experience.
- Product references remain secondary to the event value proposition.

## Graphics review

- AI Tour: route visualization, location cards and two host portraits provide adequate visual hierarchy. The route graphic is illustrative and venue status is explicit.
- IEX: strong visual system, report mockup and studio treatment, but no real speaker/event imagery yet. Add verified speaker portraits or a real studio/industrial visual once rights and final speakers are confirmed.
- Newsletter: intentionally lightweight and email-safe. It currently has no remote hero image, which improves deliverability and avoids broken assets. A tested 600 px-wide event banner can be added later only after it is hosted on a stable HTTPS asset URL and has useful alt text.

## Go-live sequence

1. Identify the Railway project/service actually owning `aitour.dbr77.com` and `iex2026.dbr77.com`.
2. Deploy the corrected local files to that exact service and verify both custom domains.
3. Run one synthetic registration per event and verify contact creation plus list membership in HubSpot.
4. Verify IMTS list separation and marketing-contact/subscription settings for all three event forms.
5. Send the newsletter only to the four internal testers, inspect Outlook desktop/mobile rendering, links and footer.
6. Remove/exclude synthetic test contacts and approve the external recipient segment.

