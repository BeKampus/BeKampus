# Product Definition

## Product vision

BeKampus is a shared digital space for discovering and participating in university life. It brings communities, student groups, events, and announcements together so people do not have to search across social networks, messaging groups, institutional email, and disconnected websites.

The product starts with the National University of Colombia (UNAL), Bogotá campus. Its longer-term direction is to support other universities without making multi-university administration part of the initial release.

## Problem

Information about university life is fragmented across many channels. Students and visitors may miss useful activities because:

- There is no single place to discover the university's communities and activities.
- Announcements are easily buried in email inboxes, social media feeds, or messaging groups.
- Communities and student groups have difficulty reaching people who would be interested in joining them.
- Events can have different audiences and access conditions that are not always easy to understand.

BeKampus addresses this problem by giving communities and organizers a clear place to publish information and giving users one place to discover, follow, and participate.

## Primary users

- **Student or member of the university community:** discovers communities and activities, follows communities, reads announcements, and registers for eligible events.
- **Visitor:** explores public communities and events and registers for activities that are open to them.
- **Organizer:** represents a community or organization and manages its profile, events, and announcements.
- **Platform administrator:** reviews organizer and community applications, moderates content, and manages platform rules.

A person may have more than one role. Permissions are determined by the action and resource, not only by the account type.

## Core concepts

- **Community:** a student group, club, collective, academic group, sports group, cultural group, university unit, or other organization that publishes information on BeKampus.
- **Event:** a dated activity managed by a community or authorized organizer. It may be in person, online, or hybrid.
- **Announcement:** an update from a community that does not need to represent a specific event, such as a call for members, a schedule change, or general information.
- **Follow:** a user's subscription to updates from a community.
- **Registration:** a user's record of intending to attend an event.

## Initial scope

The initial product focuses on UNAL Bogotá. It supports:

- Activities for UNAL students or other defined university groups.
- Activities open to students from other institutions.
- Activities open to the general public.
- Public content that can be viewed without an account.

Each event must state its visibility, audience, and registration conditions clearly. Platform approval of a community or organizer grants permission to publish on BeKampus; it does not imply official University endorsement.

## MVP capabilities

### Discovery

- Public directory of published communities.
- Public event discovery with text search and basic filters.
- Event details including date, time, format, location, organizer, status, audience, and access conditions.
- Community profiles with description, category, links, announcements, and associated events.
- Calendar view for visible events.

### Participation

- Account creation and authentication for protected actions.
- Following and unfollowing communities.
- A simple in-platform view of updates from followed communities.
- Event registration and registration cancellation.
- Capacity enforcement when an event has a limit.
- Clear handling of events that do not require registration.

### Publishing and administration

- A process for requesting organizer or community privileges.
- Administrative review of applications.
- Authorized creation, editing, publishing, and cancellation of events.
- Authorized creation and editing of community announcements.
- Basic moderation, reporting, and unpublishing of inappropriate content.

## Out of scope for the MVP

- Native iOS or Android applications.
- Private messaging, comments, or a complex social feed.
- Personalized recommendations.
- Push notifications or sophisticated email campaigns.
- Paid tickets, payment processing, or QR-based check-in.
- Automatic importing from social networks, messaging services, or university systems.
- Full multi-university administration and institution-specific workspaces.

These items may be considered after the initial product has been validated with UNAL Bogotá users.

## Product rules

1. Browsing published public content does not require an account.
2. Actions such as following a community or registering for an event require authentication.
3. Only authorized organizers can publish or modify content for their community.
4. Event visibility and attendee eligibility are separate rules and must be represented explicitly.
5. Events must state whether they are restricted to UNAL, open to other university students, open to the public, or subject to another defined condition.
6. A community or organizer approved by BeKampus is not automatically endorsed by UNAL.
7. Canceled or unpublished events must not appear as upcoming events available for registration.
8. Registration limits and duplicate-registration prevention must be enforced server-side and, where appropriate, in the database.
9. Informal student groups may request a community profile; approval grants platform permissions, not institutional recognition.
10. Users should receive updates only from communities they follow or from events and actions relevant to them.

## MVP completion criteria

The MVP is ready for a pilot when:

- Visitors can discover published communities and events.
- Users can understand an event's audience, access conditions, and registration requirements.
- Authenticated users can follow communities and view their updates.
- Authenticated users can register for and cancel registration for eligible events.
- Authorized organizers can manage their community profile, events, and announcements.
- Administrators can review applications, moderate content, and respond to reports.
- Visibility, permissions, registration uniqueness, and capacity behavior have relevant automated tests.
- Core screens provide clear loading, empty, error, success, and cancellation states.
