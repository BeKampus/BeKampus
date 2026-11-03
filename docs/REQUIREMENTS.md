# Requirements

Implementation tasks and user stories belong in GitHub Issues. This document defines stable, testable product requirements for the initial UNAL Bogotá release.

## Functional requirements

| ID | Requirement | Acceptance condition |
|---|---|---|
| FR-001 | Public community discovery | Visitors can browse published communities without signing in. |
| FR-002 | Public event discovery | Visitors can browse published events visible to them without signing in. |
| FR-003 | Search and filtering | Users can search communities and events and filter events by available attributes, at minimum date and category. |
| FR-004 | Community profiles | Published communities have a public profile with a description, category, associated events, and relevant links. |
| FR-005 | Community updates | Authorized organizers can publish announcements associated with their community. |
| FR-006 | Following communities | An authenticated user can follow or unfollow a published community and view updates from communities they follow. |
| FR-007 | Event details | Event details show title, description, date/time, location or format, organizer, status, audience, and access conditions. |
| FR-008 | Authentication | Protected actions require a valid authenticated session. |
| FR-009 | Community or organizer application | An authenticated person can request permission to represent a community or organization. |
| FR-010 | Organizer authorization | Only approved organizers and explicitly authorized community members can publish or manage content for that community. |
| FR-011 | Event management | Authorized organizers can create, edit, publish, and cancel events they are permitted to manage. |
| FR-012 | Event registration | An authenticated user can register only if the event requires registration, is open, and the user meets its access rules. |
| FR-013 | Registration cancellation | A user can cancel their own registration according to the event's rules. |
| FR-014 | Capacity enforcement | When a capacity limit exists, concurrent requests cannot exceed it. |
| FR-015 | Access control | Community listings, event details, announcements, and registration actions respect their visibility and eligibility rules. |
| FR-016 | Calendar | Users can browse visible events organized by date. |
| FR-017 | Moderation and reporting | Administrators can review applications, receive content reports, and remove or unpublish content under platform rules. |
| FR-018 | UI states | Relevant screens provide clear loading, empty, error, success, and cancellation states. |

## Non-functional requirements

| ID | Requirement | Acceptance condition |
|---|---|---|
| NFR-001 | Server-side authorization | Every protected operation validates identity and permission for the specific resource on the server or data layer. Hiding a UI control is not sufficient. |
| NFR-002 | Data integrity | Database constraints or transactions prevent duplicate follows, duplicate registrations, and capacity overbooking. |
| NFR-003 | Data protection | Only necessary personal data is exposed; secrets and credentials are not committed to the repository. |
| NFR-004 | Responsive usability | Core discovery, following, and registration flows work on mobile and desktop layouts. |
| NFR-005 | Basic accessibility | Forms have labels, controls support keyboard use, important states are communicated, and text has readable contrast. |
| NFR-006 | Maintainability | Code follows the existing monorepo's TypeScript, linting, and formatting conventions; business rules are not implemented only in UI components. |
| NFR-007 | Testability | Permissions, visibility, following, registration, and capacity rules have automated tests. |
| NFR-008 | Safe error handling | Validation and server errors are understandable without exposing sensitive implementation details. |
| NFR-009 | Performance | Measurable performance targets are defined before the pilot and checked against representative routes and data. |

## Domain rules

- Communities and events have explicit publication states; at minimum, content can be pending, published, unpublished, or canceled where applicable.
- Only an authorized organizer may publish content for a community.
- Event visibility and registration eligibility are distinct concepts.
- A user may not have duplicate active follows for the same community or duplicate active registrations for the same event.
- Organizer verification is distinct from official University endorsement.
- A user cannot manage a community's content without explicit permission.
- Changes to capacity, event status, or eligibility must have defined behavior for existing registrations.
- An event may be informational and require no registration.

## Decisions needed during implementation

- Authentication provider and how eligibility is checked for restricted events.
- Required community, announcement, and event fields and validation rules.
- Community membership and delegated organizer permissions.
- Notification delivery for followed-community updates.
- Cancellation, waitlist, and capacity-change policies.
- Personal-data retention and deletion.
- Reporting and moderation policy.
- Performance targets for the pilot.
