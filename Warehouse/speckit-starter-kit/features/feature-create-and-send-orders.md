# Feature: Create and Send Orders
**Feature ID:** CSO
**Branch pattern:** `feature/CSO-create-and-send-orders`
**Status:** Draft
**Created:** 2026-09-27

---
## User Stories
### US-N.1: Calculate Order Quantities
**As a** Warehouse manager
**I want to** input the minimum and maximum amounts for an item
**So that** the program calculates how many pallets of that item will be needed for ordering based on current stock
**Priority:** P1
**Independent test:** Input working values for min, max, and amount, and return a sufficient value
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Create Orders
**As a** Warehouse manager
**I want to** maintain relevant data for suppliers and items
**So that** the system creates order forms for suppliers based on current item quantities in inventory
**Priority:** P1
**Independent test:** Input working values for several items and output a correctly formatted order form
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Send Orders
**As a** Warehouse manager
**I want to** maintain relevant data for suppliers and items
**So that** order forms automatically created by the system will be sent to the correct suppliers
**Priority:** P1
**Independent test:** lower the inventory of items sold by a fake test supplier and see if the system tries to send them to the correct destination
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST calculate necessary quantities of items
- **FR-002**: System MUST create order forms based on the calculations
- **FR-003**: System MUST send order forms to suppliers

---
## Key Entities
- **User**: warehouse manager; maintains information in the database
- **Database**: information storage; tracks information inputted by warehouse workers
- **Order Form**: documentation; tells suppliers how much of an item to send

---
## Acceptance Criteria
### US-N.1 - Calculate Order Quantities
#### Scenario: System calculates amount for an item that is low on stock
* **Given** An item exists in the system with correct minimum and maximum inventory values
* **When** The inventory of the item drops below the minimum
* **Then** The system calculates how much is needed based on the current amounts and the maximum value

### US-N.2 - Create Orders
#### Scenario: System creates an order for a certain supplier
* **Given** Several items are obtained from a certain supplier
* **When** Those items are low on stock and the system calculates how much is needed
* **Then** The system fills out a digital order form with the information and quantity of the items needed

### US-N.3 - Send Orders
#### Scenario: System sends a filled out order form to a supplier
* **Given** Several items are low on stock and the system creates an order form
* **When** It is time to send the order form to the supplier
* **Then** The order form is digitally transferred to the supplier
#### Scenario: System does not send an empty order form to a supplier
* **Given** no items are low on stock and the system creates an empty order form
* **When** It is time to send the order form to the supplier
* **Then** The order form is not sent to the supplier because it is empty

## Data Ownership & Isolation
Order is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Warehouse Managers can see placed orders  |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/orders/read` | Yes | Read a placed order's information |

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays order information

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