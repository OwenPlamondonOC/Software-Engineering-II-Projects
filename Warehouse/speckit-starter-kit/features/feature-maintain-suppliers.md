# Feature: Maintain Suppliers
**Feature ID:** MS
**Branch pattern:** `feature/MS-maintain-suppliers`
**Status:** Draft
**Created:** 2026-09-22

---
## User Stories
### US-N.1: Add Supplier
**As a** Warehouse manager
**I want to** input the information of a new supplier
**So that** the database adds this information to the database
**Priority:** P1
**Independent test:** add a new supplier and display their information
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Supplier
**As a** Warehouse manager
**I want to** select an existing supplier for removal
**So that** the database removes this supplier's information from the database
**Priority:** P1
**Independent test:** remove a supplier and see that it no longer exists where it was in the database
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Supplier
**As a** Warehouse manager
**I want to** input new information for an existing supplier
**So that** the information for that supplier is updated in the database
**Priority:** P1
**Independent test:** edit an existing supplier in the database and have the new information displayed to the user
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit suppliers
- **FR-002**: System MUST store information of suppliers in a database

---
## Key Entities
- **User**: warehouse manager; maintains suppliers
- **Database**: information storage; tracks information including suppliers and their information

---
## Acceptance Criteria
### US-N.1 - Add Supplier
#### Scenario: Manager adds a new supplier to the system
* **Given** I am prompted to enter information for the new supplier
* **When** I enter the supplier's information
* **And** The supplier does not already exist in the system
* **Then** The supplier's information is added to the system
#### Scenario: Manager attempts to add an existing supplier to the system
* **Given** I am prompted to enter information for the new supplier
* **When** I enter the supplier's information
* **And** The supplier already exists in the system
* **Then** I am informed that the supplier already exists and am prompted to either edit the supplier's information or cancel the operation

### US-N.2 - Remove Supplier
#### Scenario: Manager removes an existing supplier from the system
* **Given** I am prompted to enter an supplier to delete from the system
* **When** I enter the supplier I wish to delete
* **And** The supplier exists in the system
* **Then** The supplier's information is removed from the system
#### Scenario: Manager attempts to remove a nonexistent supplier from the system
* **Given** I am prompted to enter an supplier to delete from the system
* **When** I enter the supplier I wish to delete
* **And** The supplier does not exist in the system
* **Then** I am informed that the supplier does not exist and the database remains unchanged

### US-N.3 - Edit Supplier
#### Scenario: Manager changes an existing supplier's information
* **Given** I am prompted to enter a supplier and their information
* **When** I enter a supplier and new information regarding the supplier
* **And** The supplier exists in the system
* **Then** The supplier's information is updated in the database
#### Scenario:Manager attempts to change the information of a nonexistent supplier
* **Given** I am prompted to enter a supplier and their information
* **When** I enter a supplier and new information regarding the supplier
* **And** The supplier does not exist in the system
* **Then** I am informed that the supplier does not exist and the database remains unchanged

## Data Ownership & Isolation
Supplier data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Warehouse Managers can see suppliers  |
| **Write scope** | Only logged in Warehouse Admins can edit or remove suppliers if they exist `id` and `req.user.id` |
| **Create scope** | Only logged in Warehouse Admins can add new suppliers |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/suppliers/read` | Yes | Read a supplier's information |
| `POST` | `/suppliers/edit` | Yes | Change an existing supplier's information |
| `POST` | `/suppliers/add` | Yes | Add a new supplier |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "supplierid": 1,
  "supplierName": "Example",
  "supplierAddress": "ExAddress",
  "supplierPhone": "111-111-1111:",
  "supplierEmail": "example@example.ex"
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays supplier information

### [View: Edit Page] — route name `edit`
*   Fields: fields for all data of the supplier.
*   Primary action: **Edit Supplier**.
*   Buttons to save or cancel editing of supplier
*   Verify pressing of save or cancel button

### [View: Add Page] — route name `add`
*   Fields: fields for all data of the supplier.
*   Primary action: **Add Supplier**.
*   Buttons to save or cancel addition of supplier
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