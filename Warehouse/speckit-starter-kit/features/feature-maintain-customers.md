# Feature: Maintain Customers
**Feature ID:** MC
**Branch pattern:** `feature/MC-maintain-customers`
**Status:** Draft
**Created:** 2026-09-22

---
## User Stories
### US-N.1: Add Customer
**As a** Warehouse manager
**I want to** input the information of a new customer
**So that** the database adds this information to the database
**Priority:** P1
**Independent test:** add a new customer and display their information
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Customer
**As a** Warehouse manager
**I want to** select an existing customer for removal
**So that** the database removes this customer's information from the database
**Priority:** P1
**Independent test:** remove a customer and see that it no longer exists where it was in the database
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Customer
**As a** Warehouse manager
**I want to** input new information for an existing customer
**So that** the information for that customer is updated in the database
**Priority:** P1
**Independent test:** edit an existing customer in the database and have the new information displayed to the user
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit customers
- **FR-002**: System MUST store information of customers in a database

---
## Key Entities
- **User**: warehouse manager; maintains customers
- **Database**: information storage; tracks information including customers and their information

---
## Acceptance Criteria
### US-N.1 - Add Customer
#### Scenario: Manager adds a new customer to the system
* **Given** I am prompted to enter information for the new customer
* **When** I enter the customer's information
* **And** The customer does not already exist in the system
* **Then** The customer's information is added to the system
#### Scenario: Manager attempts to add an existing customer to the system
* **Given** I am prompted to enter information for the new customer
* **When** I enter the customer's information
* **And** The customer already exists in the system
* **Then** I am informed that the customer already exists and am prompted to either edit the customer's information or cancel the operation

### US-N.2 - Remove Customer
#### Scenario: Manager removes an existing customer from the system
* **Given** I am prompted to enter an customer to delete from the system
* **When** I enter the customer I wish to delete
* **And** The customer exists in the system
* **Then** The customer's information is removed from the system
#### Scenario: Manager attempts to remove a nonexistent customer from the system
* **Given** I am prompted to enter an customer to delete from the system
* **When** I enter the customer I wish to delete
* **And** The customer does not exist in the system
* **Then** I am informed that the customer does not exist and the database remains unchanged

### US-N.3 - Edit Customer
#### Scenario: Manager changes an existing customer's information
* **Given** I am prompted to enter a customer and their information
* **When** I enter a customer and new information regarding the customer
* **And** The customer exists in the system
* **Then** The customer's information is updated in the database
#### Scenario:Manager attempts to change the information of a nonexistent customer
* **Given** I am prompted to enter a customer and their information
* **When** I enter a customer and new information regarding the customer
* **And** The customer does not exist in the system
* **Then** I am informed that the customer does not exist and the database remains unchanged

## Data Ownership & Isolation
Customer data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Warehouse Managers can see customers  |
| **Write scope** | Only logged in Warehouse Admins can edit or remove customers if they exist `id` and `req.user.id` |
| **Create scope** | Only logged in Warehouse Admins can add new customers |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/customers/read` | Yes | Read a customer's information |
| `POST` | `/customers/edit` | Yes | Change an existing customer's information |
| `POST` | `/customers/add` | Yes | Add a new customer |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "customerid": 1,
  "customerName": "Example",
  "customerAddress": "ExAddress",
  "customerPhone": "111-111-1111:",
  "customerEmail": "example@example.ex"
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays customer information

### [View: Edit Page] — route name `edit`
*   Fields: fields for all data of the customer.
*   Primary action: **Edit Customer**.
*   Buttons to save or cancel editing of customer
*   Verify pressing of save or cancel button

### [View: Add Page] — route name `add`
*   Fields: fields for all data of the customer.
*   Primary action: **Add Customer**.
*   Buttons to save or cancel addition of customer
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