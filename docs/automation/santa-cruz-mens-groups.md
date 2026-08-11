# Men’s Growth & Resilience Group — CRM & Automation Contract

## Scope
Mental Capital × Living Evolution — Men’s Growth & Resilience Group. Preserve Archetype Intensive isolation. No payment or clinical intake.

## Routes
- Registration: `https://mentalcapital.world/santa-cruz-mens-group`
- Confirmation: `https://mentalcapital.world/santa-cruz-mens-group/thanks`
- Consultation: `https://mentalcapital.world/santa-cruz-mens-group/consultation`
- Route key: `mc_sc_mens_group_interest_v1`

## Program facts
- Public program: `Men's Growth & Resilience Group`
- Internal program value: `mens_growth_resilience_group`
- Collaboration: `Mental Capital × Living Evolution`
- Partner: `Living Evolution`
- Facilitator: `River Krimmer`
- Aptos, Santa Cruz County
- Wednesdays, 7:30 PM–9:00 PM
- Exact meeting location provided directly to participants.

## Existing Mental Capital consultation calendar
Connected booking URL:
`https://app.mentalcapital.world/widget/booking/Wf3KAULlFOr3wSG8VsnS`

This calendar was recovered from an existing Mental Capital booking record and is embedded in the consultation bridge. HighLevel availability should be reviewed/adjusted for Zeus before flyer launch; changing availability does not require a website or QR change.

## Attribution
- Lead Source: `Santa Cruz Men's Groups`
- Campaign: `Men's Groups QR Launch`
- Partner: `Living Evolution`
- Facilitator: `River Krimmer`
- Program: `mens_growth_resilience_group`
- Default cohort: `launch_interest`
- Default flyer variant: `general_flyer`

## Core CRM fields
- `mc_sc_county_area` — single select
- `mc_sc_life_satisfaction` — number 1–10
- `mc_sc_current_priority` — long text
- `mc_preferred_contact_method` — Text / Email / Phone
- `mc_partner` — text
- `mc_facilitator` — text
- `mc_program` — text
- `mc_cohort` — text
- `mc_flyer_variant` — text
- `mc_distribution_source` — text
- `mc_registration_submitted_at` — datetime
- `mc_utm_source` — text
- `mc_utm_medium` — text
- `mc_utm_campaign` — text
- `mc_utm_content` — text
- `mc_registration_page_url` — text
- `mc_consultation_status` — `not_yet_booked` / `booked`
- `mc_consultation_booked` — boolean
- `mc_consultation_date_time` — datetime

## County area options
- Aptos
- Capitola
- Santa Cruz
- Scotts Valley
- Soquel
- Watsonville
- San Lorenzo Valley
- Other Santa Cruz County area

## Tags
Apply on registration:
- `mc_sc_mens_group_interest`
- `program_mens_growth_resilience_group`
- `source_santa_cruz_mens_groups`
- `campaign_mens_groups_qr_launch`
- `partner_living_evolution`
- `facilitator_river_krimmer`
- `consultation_not_yet_booked`
- `cohort_<cohort>`

On booking remove `consultation_not_yet_booked` and add `consultation_booked`.

Do not use legacy `partner_river_crimmer`.

## Minimal HighLevel workflow
Registration trigger: `route_key = mc_sc_mens_group_interest_v1`.

1. Create/update contact using email/phone.
2. Map fields and attribution.
3. Set `mc_consultation_status = not_yet_booked` and `mc_consultation_booked = false`.
4. Apply registration tags.
5. Internal new-registration notification.
6. Immediate acknowledgement email with consultation link.
7. Operational SMS acknowledgement only if `sms_consent_transactional = true`.
8. Create one follow-up task for unbooked consultation.
9. End; no long nurture.

Appointment trigger from the existing Mental Capital consultation calendar:
1. Match contact.
2. Set `mc_consultation_status = booked`.
3. Set `mc_consultation_booked = true`.
4. Set `mc_consultation_date_time = appointment start`.
5. Swap consultation tags.
6. Complete/cancel abandoned-booking follow-up task.
7. Run consultation confirmation/reminder sequence.

## Acknowledgement copy
`Thanks for your interest in the Men’s Growth & Resilience Group. Your registration has been received. Choose an available time for your free consultation: https://mentalcapital.world/santa-cruz-mens-group/consultation`

## Measurement events
- `mens_group_interest_view`
- `mens_group_interest_submit`
- `mens_group_interest_confirmation`
- `mens_group_consultation_continue`
- `mens_group_consultation_page_view`

Booking state/date-time comes from HighLevel appointment automation.

## Guardrails
- No payment collection or Stripe.
- No clinical intake.
- No psychotherapy characterization unless separately approved.
- No credential claims added here.
- No unrelated workflow or Archetype Intensive changes.
