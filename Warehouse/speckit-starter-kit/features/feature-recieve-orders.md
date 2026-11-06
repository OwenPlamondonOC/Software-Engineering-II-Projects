# Feature: Create and Send Orders
**Feature ID:** RO
**Branch pattern:** `feature/RO-recieve-orders`
**Status:** Draft
**Created:** 2026-09-27

---
## User Stories
### US-N.1: Confirm Delivery of Order
**As a** Warehouse manager
**I want to** recieve an order from a supplier and input the BOL's PO number
**So that** the system verifies the order as recieved
**Priority:** P1
**Independent test:** Tell scan the UPC of a test order and see it confirm that order is meant to be delivered
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Confirm Correct Quantitiy Recieved
**As a** Warehouse worker
**I want to** scan the UPC of items recieved from the supplier
**So that** the system confirms it is the right amount of items and automatically adds that amount of the items to the inventory
**Priority:** P1
**Independent test:** scan the correct amount of item UPCs for a test order and see it confirm
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST know what orders should arrive
- **FR-002**: System MUST know what each order contains
- **FR-003**: System MUST confirm that the data reported matches expected values

---
## Key Entities
- **User**: warehouse manager; maintains information in the database
- **User**: warehouse worker; accepts orders from suppliers
- **Database**: information storage; tracks information inputted by warehouse workers

---
## Acceptance Criteria
### US-N.1 - Confirm Delivery of Order
#### Scenario: Worker recieves an anticipated order from a supplier
* **Given** An order has been placed by the system
* **When** The supplier delivers that order and a worker inputs the PO number of the BOL
* **Then** The system acknowledges it and continues to check order quantity
#### Scenario: Worker does not recieve an anticipated order from a supplier
* **Given** An order has been placed by the system
* **When** The supplier does not deliver the order and the order's BOL's PO number is not inputted
* **Then** The system reports the absence of a delivery

### US-N.2 - Confirm Correct Quantitiy Recieved
#### Scenario: Worker recieves an order with the correct contents
* **Given** An order has been placed by the system and arrives
* **And** The contents of the recieved order are correct
* **When** A worker scanns each of the items' UPCs
* **Then** The system confirms that the amount is correct and adds to items' inventories in the database
#### Scenario: Worker recieves an order with the incorrect contents
* **Given** An order has been placed by the system and arrives
* **And** The contents of the recieved order are incorrect
* **When** AA worker scanns each of the items' UPCs
* **Then** The system reports that an incorrect amount of items has been recieved and adds what was actually recieved to items' inventories in the database

## Data Ownership & Isolation
Each worker can accept a received order. Warehouse managers can see all orders.
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Warehouse Workers and Warehouse Managers can see orders to accept  |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/recieve/access` | Yes | Access a recieved order |
| `POST` | `/recieve/confirm` | Yes | Confirm a recieved order |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "assignmentid": 1,
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `confirm`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays items to be checked

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