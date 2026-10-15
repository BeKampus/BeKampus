# Architecture

## Status

This document records current architectural principles, not unverified infrastructure choices. Confirm specific implementation decisions against the existing repository before adding dependencies or restructuring the monorepo.

## Approach

- Keep the existing Turborepo monorepo structure unless a concrete requirement justifies changing it.
- Start with a modular application rather than microservices.
- Separate presentation, business rules, and data access.
- Enforce sensitive permissions on the server and use database constraints or transactions where needed.
- Keep a coherent data model for users, organizations, events, and registrations.
- Reuse existing tooling from the starter instead of introducing duplicate linting, formatting, or build systems.

## Functional domains

1. **Identity and access:** sessions, user identity, and authorization.
2. **Organizations:** profiles, memberships, approval status, and roles.
3. **Events:** content, dates, location or format, visibility, eligibility, and lifecycle.
4. **Registrations:** participation, cancellation, and capacity.
5. **Administration:** organizer review and moderation.
6. **Discovery:** public queries, search, filters, and calendar.

These are logical boundaries; they do not require a separate package or service for each domain.

## Minimum conceptual data model

- **User:** a person's account.
- **Organization:** a community, club, collective, department, or other organizer.
- **OrganizationMembership:** a user's relationship to an organization and their role.
- **Event:** an activity managed by an organization, with lifecycle, visibility, and access rules.
- **Registration:** a user's participation record for an event.
- **OrganizerApplication:** a request for organizer privileges.
- **ModerationAction:** a record of relevant administrative actions when auditability is needed.

Define actual fields, relationships, and constraints when designing the data layer; do not implement speculative fields without a use case.

## Security and integrity

- Never trust owner IDs, role claims, or eligibility values supplied by the client.
- Verify that the current user can perform the requested action on the specific resource.
- Use database constraints and transactions to prevent duplicate registrations and capacity overbooking.
- Validate inputs structurally and against business rules.
- Never commit secrets or expose server-only credentials to client code.
- Keep organizer verification separate from institutional endorsement.

## Architecture changes

Record significant decisions affecting persistence, authentication, authorization, monorepo boundaries, or deployment in a short Architecture Decision Record (ADR) when the alternatives and consequences are worth preserving. Update this document when the implemented architecture changes.
