# Santa Cruz County Men's Groups — CRM & Automation Contract

## Scope
This contract covers the Mental Capital × River Crimmer Santa Cruz County Men's Groups interest-registration campaign only. It must not alter Archetype Intensive or unrelated Mental Capital workflows.

## Route
- Public route: `https://mentalcapital.world/santa-cruz-mens-group`
- Confirmation route: `https://mentalcapital.world/santa-cruz-mens-group/thanks`
- Route key: `mc_sc_mens_group_interest_v1`

## Core attribution
- Lead Source: `Santa Cruz Men's Groups`
- Campaign: `Men's Groups QR Launch`
- Partner: `River Crimmer`
- Program: `Men's Groups`
- Default cohort: `launch_interest`
- Default flyer variant: `general_flyer`

## Contact fields
| Payload key | CRM destination | Type |
| --- | --- | --- |
| `first_name` | Contact First Name | text |
| `last_name` | Contact Last Name | text |
| `email` | Contact Email | email |
| `phone` | Contact Phone | phone |
| `county_area` | `mc_sc_county_area` | text |
| `life_satisfaction` | `mc_sc_life_satisfaction` | number 1-10 |
| `current_priority` | `mc_sc_current_priority` | long text |
| `preferred_contact_method` | `mc_preferred_contact_method` | single-select: Text, Email, Phone |
| `sms_consent_transactional` | operational SMS consent record | boolean |
| `sms_consent_marketing` | marketing SMS consent record | boolean |
| `source` | lead source | text |
| `campaign` | campaign | text |
| `partner` | `mc_partner` | text |
| `program` | `mc_program` | text |
| `cohort` | `mc_cohort` | text |
| `flyer_variant` | `mc_flyer_variant` | text |
| `distribution_source` | `mc_distribution_source` | text |
| `submitted_at` | `mc_registration_submitted_at` | datetime |
| `utm_source` | `mc_utm_source` | text |
| `utm_medium` | `mc_utm_medium` | text |
| `utm_campaign` | `mc_utm_campaign` | text |
| `utm_content` | `mc_utm_content` | text |
| `page_url` | `mc_registration_page_url` | text |

## Tags
Apply:
- `mc_sc_mens_group_interest`
- `program_mens_groups`
- `source_santa_cruz_mens_groups`
- `campaign_mens_groups_qr_launch`
- `partner_river_crimmer`
- `cohort_<cohort>`

Do not create cohort-specific pipelines unless operational need develops later.

## Minimal workflow
Trigger only when `route_key = mc_sc_mens_group_interest_v1`.

1. Create or update contact using email and phone.
2. Map the campaign fields above.
3. Apply the tags above.
4. Record the submission timestamp.
5. Send an internal new-registration notification.
6. Send one immediate acknowledgement.
   - Email acknowledgement is allowed for the registration.
   - Send SMS acknowledgement only when `sms_consent_transactional = true`.
   - Marketing messages require the separate marketing consent.
7. Create one follow-up task for the designated Mental Capital owner or place the contact into one existing/simple Men's Groups interest stage if such a stage already exists.
8. End. Do not start a long nurture sequence until schedule, pricing and enrollment are approved.

## Internal notification
Recommended subject/title: `New Santa Cruz Men's Groups Registration — {{contact.name}}`

Include:
- Name
- Email
- Mobile phone
- Santa Cruz County area
- Life-satisfaction response
- Preferred contact method
- Optional written response when provided
- Operational SMS consent: yes/no
- Marketing SMS consent: yes/no
- Partner
- Program
- Cohort
- Flyer variant
- Distribution source
- UTM values
- Submission timestamp

## Immediate acknowledgement
`Thanks for your interest in the Santa Cruz County Men's Groups. We've received your registration. We'll contact you with upcoming group locations, schedules, format and enrollment details as they are confirmed.`

Do not promise placement, acceptance, outcomes or a start date.

## Measurement events
Front-end dataLayer events:
- `mens_group_interest_view`
- `mens_group_interest_submit`
- `mens_group_interest_confirmation`

CRM/reporting measures when data exists:
- QR/form visits
- Form submissions
- Completed registrations
- Contact rate
- Enrollment later after payment/enrollment infrastructure is activated

## QR parameter contract
Base URL:
`https://mentalcapital.world/santa-cruz-mens-group`

Recommended reusable parameters:
- `utm_source=flyer`
- `utm_medium=qr`
- `utm_campaign=mens_groups_qr_launch`
- `flyer_variant=general_flyer`
- `distribution_source=<distribution identifier>`
- `cohort=launch_interest`

Future cohorts should change `cohort`, `flyer_variant`, and distribution parameters without rebuilding the form.

## Guardrails
- No payment collection.
- No Stripe products.
- No clinical intake or therapy intake language.
- No unnecessary medical or clinical data.
- No River Crimmer professional credentials until exact licensed name, license number, participating legal entity and approved program description are verified.
- No modification of Archetype Intensive flows.
