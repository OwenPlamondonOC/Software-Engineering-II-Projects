# Feature: Pick Items
**Feature ID:** PI
**Branch pattern:** `feature/PI-pick-items`
**Status:** Draft
**Created:** 2026-09-28

---
## User Stories
### US-N.1: Assign Assignments
**As a** Warehouse worker
**I want to** accept an assignment from the system
**So that** the system tells me what items to get and where to find them
**Priority:** P1
**Independent test:** accept a test assignment and see an item list appear
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria
### US-N.2: Generate Route
**As a** Warehouse worker
**I want to** accept an assignment for picking
**So that** the system generates an efficient route through the warehouse to pick the items
**Priority:** P1
**Independent test:** accept a test assignment and see it generate a route
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria
### US-N.3: Pick Items
**As a** Warehouse worker
**I want to** scan items' UPC labels
**So that** the system acknowledges those items have been picked and removes them from the picking list and inventory
**Priority:** P1
**Independent test:** scan an item and see the assignment and database update
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST know what items each order has
- **FR-002**: System MUST create an efficient route through the warehouse
- **FR-003**: System MUST update inventory based on picked items

---
## Key Entities
- **User**: warehouse worker; moves items around the warehouse
- **System**: automation device; automatically gives and tracks assignments, generates routes, and tracks inventory

---
## Acceptance Criteria
### US-N.1 - Assign Assignments
#### Scenario: Worker accepts the next assignment in the queue
* **Given** An assignment exists in the queue
* **When** A worker accepts an assignment
* **Then** The system generates a list of items that the worker should pick
### US-N.2 - Generate Route
#### Scenario: Worker accepts the next assignment in the queue
* **Given** An assignment exists in the queue
* **When** A worker accepts an assignment
* **Then** The system generates a route that the worker should follow to pick those items efficiently
### US-N.3 - Pick Items
#### Scenario: Worker picks and scans correct items
* **Given** A worker has a picking assignment
* **When** The worker picks and scans all the correct items
* **Then** The system checks off picked items from the assignment and tells the worker when all items have been picked
#### Scenario: Worker picks and scans incorrect items
* **Given** A worker has a picking assignment
* **When** The worker picks and scans an incorrect item
* **Then** The system warns the worker that the item they have scanned is not in the order
#### Scenario: Worker misses an item
* **Given** A worker has a picking assignment
* **When** The worker tries to bring the picked order to shipping
* **And** not all items on the list have been collected
* **Then** The system warns the worker that there are missing items in the order
#### Scenario: Warehouse has run out of item inventory
* **Given** A worker has a picking assignment
* **When** The worker notices or creates an empty bin
* **And** they scan that bin's UPC
* **Then** The system creates a report that the bin is empty and requests a refill

## Data Ownership & Isolation
Each worker can accept a picking assignment. Warehouse managers can see all assignments
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Warehouse Workers and Warehouse Managers can see picking assignments  |
| **Write scope** | Only logged in Warehouse Admins can edit or remove assignments if they exist `id` and `req.user.id` |
| **Create scope** | Only logged in Warehouse Admins can add new assignments, and the system can create them |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/pick-assignment/access` | Yes | Access a picking assignment |
| `POST` | `/pick-assignment/edit` | Yes | Change an existing picking assignment |
| `POST` | `/pick-assignment/add` | Yes | Add a new picking assignment |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "assignmentid": 1,
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `access`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays route and all items to be picked

### [View: Edit Page] — route name `edit`
*   Fields: fields for all data of the picking assignment.
*   Primary action: **Edit Picking Assignment**.
*   Buttons to save or cancel editing of picking assignment
*   Verify pressing of save or cancel button

### [View: Add Page] — route name `add`
*   Fields: fields for all data of the picking assignment.
*   Primary action: **Add Picking Assignment**.
*   Buttons to save or cancel addition of picking assigment
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