# Product Definition

## Problem

Information about events and communities at the National University of Colombia (UNAL), Bogotá campus is spread across social media, messaging groups, university communications, and other channels. Discovering relevant activities or finding a community can require following many sources, and useful events may go unnoticed.

## Goal

Provide a shared place to discover events and communities, understand whether an activity is relevant and accessible, and participate under clearly stated conditions.

## Primary users

- **Student or visitor:** discovers events and communities, views details, and registers when eligible.
- **Organizer:** represents a community or organization and manages its profile and events.
- **Platform administrator:** reviews organizer applications and handles moderation.

A person may have multiple roles. Permissions are determined by the action and resource, not merely by the account type.

## Initial scope

The product focuses on UNAL Bogotá. Some events may be open to the public or students from other institutions; others may be restricted to the university community or a specific eligible group. Each event must clearly state its access conditions.

## MVP features

- Public event discovery, search, and basic filters.
- Event details with date and time, location or format, organizer, status, and access conditions.
- Public profiles for communities and organizers.
- A process for requesting organizer privileges, with administrative review.
- Authorized event creation, editing, and cancellation.
- Authentication for registration and organizer actions.
- Event registration and cancellation, with capacity enforcement when a limit exists.
- A simple calendar view.
- Basic administration for organizer review and event moderation.

## Out of scope for the MVP

- Native iOS or Android apps.
- Private messaging, comments, or a complex social feed.
- AI-based personalized recommendations.
- Paid tickets, payment processing, or QR-based check-in.
- Automatic importing from WhatsApp, Instagram, or university systems without an authorized integration.
- A multi-university platform with separate administration for each institution.

## Product rules

1. Browsing public events does not require an account.
2. Actions such as registering for an event require authentication.
3. Only authorized organizers can publish or modify events for their organization.
4. Event visibility and attendee eligibility are separate rules and must be represented explicitly.
5. Verifying an organizer does not imply official University endorsement.
6. Canceled events must not appear as upcoming events open for registration.
7. Registration limits and duplicate-registration prevention must be enforced server-side and, where appropriate, in the database.
8. Informal student groups may request an organizer profile; approval grants platform permissions, not institutional recognition.

## MVP completion criteria

The MVP is ready for a pilot when:
- Visitors can discover and view published events.
- Authenticated users can register for and cancel registration for eligible events.
- Authorized organizers can create, edit, and cancel their own events.
- Access rules, permissions, registration uniqueness, and capacity behavior have relevant automated tests.
- A basic process exists to review organizer applications and moderate inappropriate content.
