# Architecture

## Status

This document records current architectural principles, not unverified infrastructure choices. Confirm specific implementation decisions against the existing repository before adding dependencies or restructuring the monorepo.

## Approach

- Keep the existing Turborepo monorepo structure unless a concrete requirement justifies changing it.
- Start with a modular application rather than microservices.
- Separate presentation, business rules, and data access.
- Enforce sensitive permissions on the server and use database constraints or transactions where needed.
- Keep a coherent data model for users, communities, events, announcements, follows, and registrations.
- Reuse existing tooling from the starter instead of introducing duplicate linting, formatting, or build systems.
- Design the initial model around UNAL Bogotá without prematurely implementing institution-specific administration.

## Functional domains

1. **Identity and access:** sessions, user identity, authentication, and authorization.
2. **Communities:** profiles, publication status, memberships, applications, and organizer roles.
3. **Events:** content, dates, location or format, visibility, eligibility, registration requirements, and lifecycle.
4. **Announcements:** community updates and their visibility to the public or followers.
5. **Following:** user subscriptions to communities and the updates shown to them.
6. **Registrations:** participation, cancellation, and capacity.
7. **Administration:** organizer review, reports, moderation, and audit records where needed.
8. **Discovery:** public queries, search, filters, and calendar views.

These are logical boundaries; they do not require a separate package or service for each domain.

## Minimum conceptual data model

- **User:** a person's account and basic identity information.
- **Community:** a group, organization, university unit, or collective with a public profile.
- **CommunityMembership:** a user's relationship to a community and their role or authorization.
- **OrganizerApplication:** a request to represent a community on BeKampus.
- **Event:** an activity managed by a community, with lifecycle, visibility, audience, eligibility, and registration rules.
- **Announcement:** an update published by an authorized community organizer.
- **CommunityFollow:** a user's subscription to updates from a community.
- **Registration:** a user's participation record for an event.
- **ModerationAction:** a record of relevant administrative actions when auditability is needed.
- **Report:** a user's report of potentially inappropriate or inaccurate content.

Define actual fields, relationships, and constraints when designing the data layer; do not implement speculative fields without a use case.

## Access and visibility model

Community, announcement, and event visibility must be distinct from the eligibility to participate in an event. For example, an event may be publicly discoverable while registration is limited to UNAL students.

The model should support, at minimum:

- Public content.
- Content restricted to authenticated users.
- Events for UNAL students or a defined university group.
- Events open to students from other institutions.
- Events open to the general public.
- Events that require no registration.

Do not treat a user's claimed institution, role, or eligibility as trusted merely because it was supplied by the client.

## Security and integrity

- Never trust owner IDs, role claims, community IDs, or eligibility values supplied by the client.
- Verify that the current user can perform the requested action on the specific resource.
- Use database constraints and transactions to prevent duplicate follows, duplicate registrations, and capacity overbooking.
- Validate inputs structurally and against business rules.
- Never commit secrets or expose server-only credentials to client code.
- Keep organizer verification separate from institutional endorsement.
- Avoid exposing personal registration data to unauthorized users.

## Future direction

The first release is for UNAL Bogotá. If BeKampus expands to other universities, the architecture may need institution entities, institution-specific administrators, membership or eligibility verification, and separate moderation policies. Those changes should be designed after validating the initial product rather than adding speculative multi-university complexity now.

## Architecture changes

Record significant decisions affecting persistence, authentication, authorization, monorepo boundaries, or deployment in a short Architecture Decision Record (ADR) when the alternatives and consequences are worth preserving. Update this document when the implemented architecture changes.
