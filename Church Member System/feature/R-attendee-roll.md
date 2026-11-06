# Feature: Keep track of attendees at events

## **Feature ID:** R
**Branch pattern:** `feature/R-attendee-roll`
**Status:** Draft
**Created:** 2026-09-10

## User Stories

### US-N.1: Change data of number of attendees at an event

**As a** church staff member
**I want to** input data for number of attendees at an event
**So that** the system organizes the data in a database
**Priority:** P1
**Independent test:** input a number in the system and display that number to the user
**Acceptance scenarios:** see US-N.1 under Acceptance Criteria

### US-N.2: Add registered members

**As a** church staff member
**I want to** select registered church members and an event
**So that** the system keeps track of which members were present at that event
**Priority:** P1
**Independent test:** choose a church event and input the members who attended, then display them
**Acceptance scenarios:** see US-N.2 under Acceptance Criteria

### US-N.3: Access roll data

**As a** church staff member
**I want to** choose a past church event
**So that** the data for the people who attended that event is displayed
**Priority:** P1
**Independent test:** choose a church event and display the members who attended
**Acceptance scenarios:** see US-N.3 under Acceptance Criteria

---
### Functional Requirements

- **FR-001**: System MUST accept input from church staff members
- **FR-002**: System MUST update databases based on the received input
- **FR-003**: System MUST allow a church staff member to access the existing database
- **FR-004**: System MUST display correct data to a church staff member

---

## Initial Data

- 120 to 150 people already attend the church
- current system of filling out cards is unreliable
- many church members would not be able to check themselves in

---

## Acceptance Criteria
### US-N.1 — Change data of number of attendees at an event
#### Scenario: Staff member counts number of people in a service
* **Given** I have counted the number of people in a service
* **When** I input the number into the system
* **Then** the program stores the data in a database

### US-N.2 — Add registered members
#### Scenario: Staff member keeps attendance of members in a class
* **Given** some members attended a particular class
* **When** I select those members in the system
* **Then** the program adds those members to a list associated with the class

### US-N.3 — Access roll data
#### Scenario: Manager views a class's information
* **Given** a class already happened and data was entered for it
* **When** I search for the class in the system
* **Then** the number of attendees and registered members in that class are displayed to me