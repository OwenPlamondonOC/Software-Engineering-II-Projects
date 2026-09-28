# Feature: Maintain Routes
**Feature ID:** MR
**Branch pattern:** `feature/MSO-maintain-routes`
**Status:** Draft
**Created:** 2026-09-27

---
## User Stories
### US-N.1: Add Route
**As a** Warehouse manager
**I want to** input the information of a route
**So that** the database adds this information to the database
**Priority:** P1
**Independent test:** add a new route and display its information
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Route
**As a** Warehouse manager
**I want to** select an existing route for removal
**So that** the database removes this route's information from the database
**Priority:** P1
**Independent test:** remove a route and see that it no longer exists where it was in the database
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Route
**As a** Warehouse manager
**I want to** input new information for an existing route
**So that** the information for that route is updated in the database
**Priority:** P1
**Independent test:** edit an existing route in the database and have the new information displayed to the user
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit routes
- **FR-002**: System MUST store information of routes in a database

---
## Key Entities
- **User**: warehouse manager; maintains routes
- **Database**: information storage; tracks information including routes and its information

---
## Acceptance Criteria
### US-N.1 - Add Route
#### Scenario: Manager adds a new route to the system
* **Given** I am prompted to enter information for the new route
* **When** I enter the route's information
* **And** The route does not already exist in the system
* **Then** The route's information is added to the system
#### Scenario: Manager attempts to add an existing route to the system
* **Given** I am prompted to enter information for the new route
* **When** I enter the route's information
* **And** The route already exists in the system
* **Then** I am informed that the route already exists and am prompted to either edit the route's information or cancel the operation

### US-N.2 - Remove Route
#### Scenario: Manager removes an existing route from the system
* **Given** I am prompted to enter an route to delete from the system
* **When** I enter the route I wish to delete
* **And** The route exists in the system
* **Then** The route's information is removed from the system
#### Scenario: Manager attempts to remove a nonexistent route from the system
* **Given** I am prompted to enter an route to delete from the system
* **When** I enter the route I wish to delete
* **And** The route does not exist in the system
* **Then** I am informed that the route does not exist and the database remains unchanged

### US-N.3 - Edit Route
#### Scenario: Manager changes an existing route's information
* **Given** I am prompted to enter a route and its information
* **When** I enter a route and new information regarding the route
* **And** The route exists in the system
* **Then** The route's information is updated in the database
#### Scenario:Manager attempts to change the information of a nonexistent route
* **Given** I am prompted to enter a route and its information
* **When** I enter a route and new information regarding the route
* **And** The route does not exist in the system
* **Then** I am informed that the route does not exist and the database remains unchanged