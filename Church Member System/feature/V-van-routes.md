# Feature: Create and Manage Van Routes

## **Feature ID:** V
**Branch pattern:** `feature/V-van-routes`
**Status:** Draft
**Created:** 2026-09-10

## User Stories

### US-N.1: Create van routes

**As a** church staff member
**I want to** input data for a van route
**So that** the system organizes and shows the data to the correct van driver
**Priority:** P1
**Independent test:** create new van route and display it to corresponding driver
**Acceptance scenarios:** see US-N.1 under Acceptance Criteria

### US-N.2: Access van routes

**As a** van driver
**I want to** access the system
**So that** the system displays the route I must take
**Priority:** P1
**Independent test:** login to app and see the correct van route
**Acceptance scenarios:** see US-N.2 under Acceptance Criteria

### US-N.3: Change van routes

**As a** church staff member
**I want to** modify data for a van route
**So that** the data updates and notifies the van driver
**Priority:** P1
**Independent test:** edit van route and display changes to corresponding driver
**Acceptance scenarios:** see US-N.3 under Acceptance Criteria

---
### Functional Requirements

- **FR-001**: System MUST accept input from church staff members
- **FR-002**: System MUST update databases based on the received input
- **FR-003**: System MUST display correct data to the van drivers

---

## Initial Data

- Van routes already exist
- Each route has a unique driver

---

## Acceptance Criteria
### US-N.1 — Create van routes
#### Scenario: Manager creates the first van route
* **Given** there are currently no registered van routes
* **When** I input the data corresponding to a new van route
* **Then** the program stores the data in a database

### US-N.2 — Access van routes
#### Scenario: Van driver accesses their route
* **Given** I am the van driver
* **When** I access the van route database
* **And** I verify which driver I am
* **Then** the program displays the route I will take

### US-N.3 — Manage van routes
#### Scenario: Manager edits a van route
* **Given** there is an existing van route
* **When** I input new data for the existing van route
* **Then** the program updates the data in the database