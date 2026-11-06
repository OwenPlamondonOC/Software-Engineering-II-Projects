# Feature: Ship Order
**Feature ID:** SO
**Branch pattern:** `feature/SO-ship-order`
**Status:** Draft
**Created:** 2026-09-28

---
## User Stories
### US-N.1: Double Check Order
**As a** Shipping Dock Worker
**I want to** scan the UPCs of an order and it's picked items
**So that** the system confirms all the items have been picked and assigns the order to a truck
**Priority:** P1
**Independent test:** scan the items of a test order and see it confirm
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria
### US-N.2: Create Assignments
**As a** Shipping Dock Worker
**I want to** fill up a truck with orders
**So that** the system generates an assignment associated with that truck for a driver to accept
**Priority:** P1
**Independent test:** fill a truck with test orders and see it generate an assignment
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria
### US-N.3: Generate Truck Route
**As a** Truck Driver
**I want to** accept an assignment from the system
**So that** the system generates an efficient route to each customer that has an order in my truck
**Priority:** P1
**Independent test:** accept a test assignment and see it generate a route to test locations
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST know what items each order has
- **FR-002**: System MUST know what trucks are currently available
- **FR-003**: System MUST know what trucks have which items
- **FR-004**: System MUST know where the customers are

---
## Key Entities
- **User**: shipping dock worker; checks orders and loads trucks
- **User**: truck driver; drives trucks from the warehouse to the customers
- **System**: automation device; automatically tracks orders and trucks
- **Truck Fleet**: transportation device; moves orders from the warehouse to the customers

---
## Acceptance Criteria
### US-N.1 - Double Check Order
#### Scenario: Shipping Dock Worker accepts a correct order
* **Given** An order is correctly picked and is delivered to the shipping dock
* **When** A worker scans all the order's UPCs
* **Then** The system assigns the order to a truck
#### Scenario: Shipping Dock Worker does not accept an incorrect order
* **Given** An order is incorrectly picked and is delivered to the shipping dock
* **When** A worker scans all the order's UPCs
* **Then** The system warns the shipping dock worker that the order is incorrect
* **And** The system generates a new assignment to fix the order
#### Scenario: Shipping Dock Worker overrides incorrect order
* **Given** An order is incorrectly picked and is delivered to the shipping dock
* **And** The order cannot be fixed due to low inventory
* **When** A worker scans all the order's UPCs and the shipping dock worker overrides the warnings
* **Then** The system updates the order's contents and assigns it to a truck
### US-N.2 - Generate Assignments
#### Scenario: Truck is filled
* **Given** A truck is filled with correct orders
* **When** That truck is marked as full by a shipping dock worker
* **Then** The system generates an assignment for a driver to accept
### US-N.3 - Generate Truck Route
#### Scenario: Truck Driver accepts an assignment
* **Given** A truck is filled with correct orders
* **When** A truck driver accepts the assignment for that truck
* **Then** The system generates a route for the truck driver to follow

## Data Ownership & Isolation
Delivery data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Warehouse Managers and Truck Drivers can see deliveries  |
| **Write scope** | Only logged in Warehouse Admins can edit deliveries if they exist `id` and `req.user.id` |
| **Create scope** | Only logged in Warehouse Admins can add new deliveries |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/ship/read` | Yes | Access a delivery route |
| `POST` | `/ship/edit` | Yes | Change an existing delivery route |
| `POST` | `/ship/add` | Yes | Add a new delivery |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "deliveryid": 1,
  "truckDriver": "Example",
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays delivery information

### [View: Edit Page] — route name `edit`
*   Fields: fields for all data of the delivery.
*   Primary action: **Edit Delivery**.
*   Buttons to save or cancel editing of delivery
*   Verify pressing of save or cancel button

### [View: Add Page] — route name `add`
*   Fields: fields for all data of the delivery.
*   Primary action: **Add Delivery**.
*   Buttons to save or cancel addition of delivery
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

*   User Authorizations
*   Anything specified in another feature file