# Men's Growth & Resilience Group — CRM & Automation Contract

## Scope
This contract covers the Mental Capital × Living Evolution Men's Growth & Resilience Group registration-to-consultation campaign only. It must not alter Archetype Intensive or unrelated Mental Capital workflows.

## Public program facts
- Program: `Men's Growth & Resilience Group`
- Internal program value: `mens_growth_resilience_group`
- Collaboration: `Mental Capital × Living Evolution`
- Partner: `Living Evolution`
- Facilitator: `River Krimmer`
- Group area: Aptos, Santa Cruz County
- Group schedule: Wednesdays, 7:30 PM–9:00 PM
- Exact meeting location: provided directly after registration / during enrollment process
- Funnel: Flyer/QR → registration → Mental Capital free consultation calendar → booking → confirmation/reminders

## Routes
- Public registration: `https://mentalcapital.world/santa-cruz-mens-group`
- Registration confirmation: `https://mentalcapital.world/santa-cruz-mens-group/thanks`
- Consultation bridge: `https://mentalcapital.world/santa-cruz-mens-group/consultation`
- Route key: `mc_sc_mens_group_interest_v1`

## Core attribution
- Lead Source: `Santa Cruz Men's Groups`
- Campaign: `Men's Groups QR Launch`
- Partner: `Living Evolution`
- Facilitator: `River Krimmer`
- Program: `mens_growth_resilience_group`
- Default cohort: `launch_interest`
- Default flyer variant: `general_flyer`

## Contact / custom fields
| Payload key | CRM destination | Type |
| --- | --- | --- |
| `first_name` | Contact First Name | text |
| `last_name` | Contact Last Name | text |
| `email` | Contact Email | email |
| `phone` | Contact Phone | phone |
| `county_area` | `mc_sc_county_area` | single-select |
| `life_satisfaction` | `mc_sc_life_satisfaction` | number 1-10 |
| `current_priority` | `mc_sc_current_priority` | long text |
| `preferred_contact_method` | `mc_preferred_contact_method` | single-select: Text, Email, Phone |
| `sms_consent_transactional` | operational SMS consent record | boolean |
| `sms_consent_marketing` | marketing SMS consent record | boolean |
| `partner` | `mc_partner` | text |
| `facilitator` | `mc_facilitator` | text |
| `program` | `mc_program` | text |
| `cohort` | `mc_cohort` | text |
| `flyer_variant` | `mc_flyer_variant` | text |
| `distribution_source` | `mc_distribution_source` | text |
| `submitted_at` | `mc_registration_submitted_at` | datetime |
| `consultation_status` | `mc_consultation_status` | single-select |
| `consultation_booked` | `mc_consultation_booked` | boolean |
| `consultation_date_time` | `mc_consultation_date_time` | datetime |
| `utm_source` | `mc_utm_source` | text |
| `utm_medium` | `mc_utm_medium` | text |
| `utm_campaign` | `mc_utm_campaign` | text |
| `utm_content` | `mc_utm_content` | text |
| `page_url` | `mc_registration_page_url` | text |

### County area values
- Aptos
- Capitola
- Santa Cruz
- Scotts Valley
- Soquel
- Watsonville
- San Lorenzo Valley
- Other Santa Cruz County area

### Consultation status values
- `not_yet_booked`
- `booked`

## Tags
Apply at registration:
- `mc_sc_mens_group_interest`
- `program_mens_growth_resilience_group`
- `source_santa_cruz_mens_groups`
- `campaign_mens_groups_qr_launch`
- `partner_living_evolution`
- `facilitator_river_krimmer`
- `consultation_not_yet_booked`
- `cohort_<cohort>`

Remove / do not apply:
- `partner_river_crimmer`
- `program_mens_groups`

On successful consultation booking:
- remove `consultation_not_yet_booked`
- add `consultation_booked`
- set `mc_consultation_status = booked`
- set `mc_consultation_booked = true`
- set `mc_consultation_date_time` from the calendar appointment

## Minimal registration workflow
Trigger only when `route_key = mc_sc_mens_group_interest_v1`.

1. Create/update contact before any calendar redirect.
2. Map all registration + attribution fields.
3. Apply registration/program/partner/facilitator tags.
4. Set consultation status to `not_yet_booked`.
5. Send internal new-registration notification.
6. Send one immediate acknowledgement email.
7. Send operational SMS acknowledgement only when `sms_consent_transactional = true`.
8. Create one follow-up task owned by the designated Mental Capital follow-up owner, due after a short booking window, with instruction to contact only if consultation remains unbooked.
9. End. Do not start a long nurture sequence.

## Consultation booking workflow
Use the existing approved Mental Capital free-consultation calendar. Do not create a competing calendar.

When an appointment is booked through that calendar for this campaign:
1. Match/create-update the contact.
2. Set consultation status = `booked`.
3. Store appointment date/time.
4. Replace the not-yet-booked tag with `consultation_booked`.
5. Complete/cancel the abandoned-booking follow-up task.
6. Send normal calendar confirmation/reminders using existing Mental Capital scheduling architecture and consent rules.

## Abandoned scheduling
A submitted registration must remain a lead even if no calendar booking occurs.

Use one short operational follow-up only:
- condition: `mc_consultation_status = not_yet_booked`
- action: one follow-up task to the designated Mental Capital owner or one operational contact attempt
- stop when consultation status becomes `booked`

No long nurture campaign.

## Internal registration notification
Recommended title: `New Men's Growth & Resilience Registration — {{contact.name}}`

Include name, email, phone, county area, life-satisfaction response, preferred contact method, optional written response, SMS consent values, partner, facilitator, program, cohort, flyer/distribution source, UTM values, registration timestamp, and consultation status.

## Immediate acknowledgement
Email direction:
`Thanks for your interest in the Men's Growth & Resilience Group. Your registration has been received. Continue to the Mental Capital free-consultation calendar to choose an available consultation time.`

Operational SMS when consent permits:
`Mental Capital: We received your Men's Growth & Resilience Group registration. Please continue to the free-consultation calendar to choose an available time. Reply STOP to opt out.`

Do not promise acceptance, placement, enrollment, outcomes or a specific consultation slot.

## Measurement events
Front-end events:
- `mens_group_interest_view`
- `mens_group_interest_submit`
- `mens_group_interest_confirmation`
- `mens_group_consultation_continue`
- `mens_group_consultation_page_view`

CRM/calendar reporting states:
- registration submitted
- consultation not yet booked
- consultation booked
- consultation date/time
- contact rate
- enrollment later after payment infrastructure exists

## QR parameter contract
Stable base URL: `https://mentalcapital.world/santa-cruz-mens-group`

General flyer parameters remain reusable:
- `utm_source=flyer`
- `utm_medium=qr`
- `utm_campaign=mens_groups_qr_launch`
- `flyer_variant=general_flyer`
- `distribution_source=<distribution identifier>`
- `cohort=launch_interest`

Future cohorts change attribution parameters without rebuilding the form or QR route architecture.

## Remaining scheduling input
The consultation bridge is built but intentionally does not hard-code the only calendar URL found in records because it belongs to a prior event labeled `TEST`.

Single required scheduling input before launch:
- the approved current Mental Capital **Free Consultation** calendar booking URL / calendar ID for this program, with consultation availability configured by Zeus.

Once supplied, set it as `CALENDAR_URL` in `santa-cruz-mens-group-consultation.html` and verify the booking webhook/workflow updates consultation status and date/time.

## Guardrails
- No payment collection or Stripe products.
- No clinical intake or unnecessary health data.
- Do not characterize the program as psychotherapy unless separately approved.
- Credentials are not a blocker for this funnel and are not published here.
- Do not modify Archetype Intensive flows or unrelated Mental Capital workflows.
