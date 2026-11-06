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

## Data Ownership & Isolation
Route data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Warehouse Managers and Truck Drivers can see route information  |
| **Write scope** | Only logged in Warehouse Admins can edit or remove existing routes `id` and `req.user.id` |
| **Create scope** | Only logged in Warehouse Admins can create new routes |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/route/read` | Yes | Read data of a specific route |
| `POST` | `/route/edit` | Yes | Change an existing route's information |
| `POST` | `/route/create` | Yes | Create a new route |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "routeid": 1,
  "routeName": "name"
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays route information

### [View: Edit Page] — route name `edit`
*   Fields: fields for all data of the route.
*   Primary action: **Edit Route**.
*   Buttons to save or cancel editing of route
*   Verify pressing of save or cancel button

### [View: Create Page] — route name `create`
*   Fields: fields for all data of the route.
*   Primary action: **Create Route**.
*   Buttons to save or cancel creating of route
*   Verify pressing of save or cancel button

---

## Definition of Done

*   [ ] Backend and frontend implemented per this spec (**FR-00N** satisfied)
*   [ ] **Success Criteria (SC-00N)** met
*   [ ] `features/reference/data-model.md` updated (if schema changed)
*   [ ] `features/reference/api.md` updated (if API changed)
*   [ ] `features/reference/behavior.md` updated (if product rules changed)

---

## Out of Scope

*   User Authorization
*   Anything specified in another feature file