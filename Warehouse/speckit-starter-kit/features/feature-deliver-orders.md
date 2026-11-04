# Feature: Deliver Order
**Feature ID:** DO
**Branch pattern:** `feature/DO-deliver-order`
**Status:** Draft
**Created:** 2026-09-28

---
## User Stories
### US-N.1: Double Check Order
**As a** Truck Driver
**I want to** scan the UPCs of items accepted by a customer
**So that** the system confirms those items have been delivered successfully
**Priority:** P1
**Independent test:** scan the items of a test order and see it confirm
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST know what items each order has
- **FR-002**: System MUST know what trucks have which items
- **FR-003**: System MUST know where the customers are

---
## Key Entities
- **User**: truck driver; drives trucks from the warehouse to the customers
- **System**: automation device; automatically tracks orders and trucks
- **Truck Fleet**: transportation device; moves orders from the warehouse to the customers

---
## Acceptance Criteria
### US-N.1 - Double Check Order
#### Scenario: Customer accepts a correct order
* **Given** An order is correctly shipped to a customer
* **When** A truck driver scans the UPCs of the items accepted by the customer
* **Then** The system marks the order as completed
#### Scenario: Customer does not accept all items in an order
* **Given** An order is incorrectly shipped to a customer
* **When** A truck driver scans the UPCs of the items accepted by the customer
* **And** The truck driver does not scan the UPCs of items the customer does not accept
* **Then** The system generates a report that some items were incorrect
#### Scenario: Customer does not recieve the full order
* **Given** An order is incorrectly shipped to a customer
* **When** A truck driver scans the UPCs of the items accepted by the customer
* **And** Not all items in the order have been delivered
* **Then** The system generates a report that some items were missing

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
| `POST` | `/deliveries/read` | Yes | Access a delivery |
| `POST` | `/deliveries/confirm` | Yes | Confirm that an order has been delivered |

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

### [View: Confirm Page] — route name `confirm`
*   Fields: fields for all items in the delivery.
*   Primary action: **Confirm Delivery**.
*   Buttons to save or cancel confirmation of delivery
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