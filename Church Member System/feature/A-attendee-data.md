# Feature: Collect and organize data from attendees

## **Feature ID:** A
**Branch pattern:** `feature/A-attendee-data`
**Status:** Draft
**Created:** 2026-09-10

## User Stories

### US-N.1: Register a new member

**As a** church staff member
**I want to** input data for a new attendee
**So that** the system organizes the data in a database
**Priority:** P1
**Independent test:** register a new attendee into the system and display the information
**Acceptance scenarios:** see US-N.1 under Acceptance Criteria

### US-N.2: Edit a member's data

**As a** church staff member
**I want to** input new data regarding an already registered member
**So that** the system correctly modifies the data in the database
**Priority:** P1
**Independent test:** edit member information and display updated information
**Acceptance scenarios:** see US-N.2 under Acceptance Criteria

### US-N.3: Access member data

**As a** church staff member
**I want to** search for a registered member
**So that** the data for that member is displayed to me
**Priority:** P1
**Independent test:** search for existing member and display their corresponding data
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
- church attendees cannot be trusted to register themselves

---

## Acceptance Criteria
### US-N.1 — Register a new member
#### Scenario: Manager registers a new member
* **Given** a member is not registered in the system
* **When** I input the data of a member
* **Then** the program stores the data in a database

### US-N.2 — Edit a member's data
#### Scenario: Manager changes data of a member
* **Given** a member is already registered in the system
* **When** I input the data of that member
* **Then** the program updates the associated data in a database

### US-N.3 — Access member data
#### Scenario: Manager views a member's information
* **Given** a member is already registered in the system
* **When** I search for the member in the system
* **Then** the member's information is displayed to me.