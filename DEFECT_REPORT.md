# Learning Practice 8: Defect Management

## 1. Classification of Findings

The findings below are based on the supplied requirements and inspected source code. Runtime testing is still needed to confirm user-visible behavior.

| ID | Finding | Classification | Explanation |
|---|---|---|---|
| F-01 | Guest count has no maximum of 12 | Product defect | The guest input specifies a minimum of 1 but no maximum. |
| F-02 | Checkout date is missing | Product defect | The form provides one date field rather than separate check-in and checkout fields. |
| F-03 | Stay duration and date order are not validated | Product defect | The inspected form does not calculate nights or compare check-in and checkout. |
| F-04 | Availability is not checked in the inspected booking flow | Product defect; investigate other services | The booking context adds a booking to state without checking requested-night availability. |
| F-05 | Required $50 cleaning fee is missing | Product defect in the inspected flow | No cleaning-fee calculation is present in the inspected booking logic. |
| F-06 | Complete validation and error feedback are missing | Product defect | The submit handler calls addBooking without checking all stated requirements or displaying application-level errors. |

No separate test-environment problem or requested change has been established by the inspected code.

## 2. Detailed Defect Report

| Field | Details |
|---|---|
| Defect ID | DEF-002 |
| Title | Booking form does not provide a checkout date |
| Date reported | October 8, 2026 |
| Reporter | Student tester |
| Application or feature | North Vacation Booking — Add Booking |
| Test environment | macOS, React, TypeScript, Vite, local browser |
| Preconditions | Application is running and Add Booking is accessible. |
| Steps to reproduce | 1. Open the application. 2. Navigate to Add Booking. 3. Inspect the form. 4. Attempt to enter check-in and checkout dates. 5. Observe the available date inputs. |
| Expected result | Separate check-in and checkout fields allow a reservation lasting 1–31 nights. |
| Actual result | The inspected AddBooking.tsx contains one date input named date and no checkout field. |
| Severity | High |
| Priority | High |
| Initial status | New — awaiting runtime confirmation and developer review |
| Related requirement | A reservation lasts 1–31 nights, and check-in must occur before checkout. |
| Supporting evidence | Screenshot of the booking form and relevant source code excerpt. |

## 3. Severity and Priority

Severity describes impact. Priority describes how soon a defect should be fixed. Ratings are preliminary pending confirmation by the team.

| Defect | Severity | Priority | Explanation |
|---|---|---|---|
| DEF-001: Guest maximum missing | Medium | High | More than 12 guests may be entered. |
| DEF-002: Checkout date missing | High | High | The required stay period cannot be entered. |
| DEF-003: Date validation missing | High | High | Invalid date order and stay lengths are not checked in the inspected flow. |
| DEF-004: Availability check missing | High | High | Requested nights are not checked in the inspected booking logic. |
| DEF-005: Cleaning fee missing | Medium | High | The required one-time $50 fee is absent from the inspected flow. |
| DEF-006: Complete validation and error feedback missing | Medium | High | Invalid information may not receive the required application-level validation. |

## 4. Defect Status Tracking

All defects start as New. No fix or successful retest is claimed.

| ID | Status | Next action | Closure condition |
|---|---|---|---|
| DEF-001 | New | Test 13 guests. | Values above 12 are rejected with an error. |
| DEF-002 | New | Confirm the missing checkout field in the running app. | Separate check-in and checkout fields are available. |
| DEF-003 | New | Test checkout before check-in and stays of 0 and 32 nights. | Invalid date ranges are rejected. |
| DEF-004 | New | Investigate availability data and test overlapping dates. | Unavailable nights cannot be booked. |
| DEF-005 | New | Inspect the reservation price and fee display. | Exactly one $50 fee is included per valid reservation. |
| DEF-006 | New | Submit invalid inputs and observe error feedback. | Invalid bookings are rejected with clear messages. |

### Defect lifecycle
1. New — finding recorded.
2. Triaged — impact, severity, and priority reviewed.
3. Assigned — developer takes responsibility.
4. Fixed — code change is available.
5. Retest — tester repeats the reproduction steps.
6. Closed — the requirement is satisfied.
7. Reopened — the defect persists or returns.

These are lifecycle definitions, not claims that the defects have advanced through these stages.

## 5. Root-Cause Analysis

The causes below are hypotheses based on source inspection and require developer confirmation.

| Finding | Possible root cause | Process improvement |
|---|---|---|
| Guest maximum missing | The input has a minimum but no maximum. | Validate both boundaries. |
| Checkout date missing | The form stores only one date. | Add separate check-in and checkout fields. |
| Date validation missing | Submission does not compare dates or calculate nights. | Validate date order and 1–31 nights. |
| Availability check missing | The inspected context appends bookings directly to state. | Check every requested night before confirmation. |
| Cleaning fee missing | No fee calculation exists in the inspected flow. | Include the $50 fee exactly once per reservation. |
| Validation feedback missing | The submit handler does not validate all requirements. | Validate before saving and display actionable errors. |

### Recommended tests
- Guests: 1, 12, 0, and 13.
- Stay duration: 1, 31, 0, and 32 nights.
- Dates: valid order, equal dates, and checkout before check-in.
- Availability: available dates and overlapping reservations.
- Cleaning fee: verify the $50 fee is charged once, not per night.
- Invalid submissions: confirm the booking is rejected with an error.

## Conclusion

The inspected source does not implement several booking requirements, including the guest maximum, checkout date, date validation, availability checking, and cleaning-fee calculation. Findings should be reproduced in the running application and reviewed by the development team before being treated as confirmed.

## AI Transparency

AI assistance was used to organize and draft this report. Findings are based on the supplied requirements and inspected source code; runtime behavior and proposed root causes should be verified.
