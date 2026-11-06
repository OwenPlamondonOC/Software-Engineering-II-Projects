# Feature: Maintain Item Types
**Feature ID:** MIT
**Branch pattern:** `feature/MIT-maintain-items`
**Status:** Draft
**Created:** 2026-09-21

---
## User Stories
### US-N.1: Add Item Type
**As a** Warehouse manager
**I want to** input the information of a new item
**So that** the database adds the information of the new item and begins tracking its stock
**Priority:** P1
**Independent test:** add a new item to the database and have the information displayed to the user
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Item Type
**As a** Warehouse manager
**I want to** select an existing item for deletion
**So that** the information for that item is removed from the database
**Priority:** P1
**Independent test:** remove an item and see that it no longer exists where it was in the database
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Item Type
**As a** Warehouse manager
**I want to** input new information for an existing item
**So that** the information for that item is updated in the database
**Priority:** P1
**Independent test:** edit an existing item in the database and have the new information displayed to the user
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit item types
- **FR-002**: System MUST store information of items in a database

---
## Key Entities
- **User**: warehouse manager; maintains item types
- **Database**: information storage; tracks information including item types and information

---
## Acceptance Criteria
### US-N.1 - Add Item Type
#### Scenario: Manager adds a new item to the system
* **Given** I am prompted to enter information for the new item
* **When** I enter a name, price, SKU number, UPC, supplier, and description
* **And** The item does not already exist in the system
* **Then** The item and its information are added to the system and its stock is set to zero
#### Scenario: Manager attempts to add an existing item to the system
* **Given** I am prompted to enter information for the new item
* **When** I enter an item ID and quantity to increase the stock by
* **And** The item already exists in the system
* **Then** I am informed that the item already exists and am prompted to either edit the item or cancel the operation

### US-N.2 - Remove Item Type
#### Scenario: Manager removes an existing item from the system
* **Given** I am prompted to enter an item ID to delete from the system
* **When** I enter the ID of the item I wish to delete
* **And** The item exists in the system
* **Then** The item and its information are removed from the system
#### Scenario: Manager attempts to remove a nonexistent item from the system
* **Given** I am prompted to enter an item ID to delete from the system
* **When** I enter the ID of the item I wish to delete
* **And** The item does not exist in the system
* **Then** I am informed that the item does not exist and the database remains unchanged

### US-N.3 - Edit Item Type
#### Scenario: Manager changes an existing item's price
* **Given** I am prompted to enter a value to change the price to
* **When** I enter an item ID and value to change the price to
* **And** The item exists in the system
* **Then** The price of that item is updated in the database
#### Scenario:Manager attempts to change the price of a nonexistent item
* **Given** I am prompted to enter a value to change the price to
* **When** I enter an item ID and value to change the price to
* **And** The item does not exist in the system
* **Then** I am informed that the item does not exist and the database remains unchanged
#### Scenario: Manager changes an existing item's SKU number
* **Given** I am prompted to enter a value to change the SKU number to
* **When** I enter an item ID and value to change the SKU number to
* **And** The item exists in the system
* **Then** The SKU number of that item is updated in the database
#### Scenario:Manager attempts to change the SKU number of a nonexistent item
* **Given** I am prompted to enter a value to change the SKU number to
* **When** I enter an item ID and value to change the SKU number to
* **And** The item does not exist in the system
* **Then** I am informed that the item does not exist and the database remains unchanged
#### Scenario: Manager changes an existing item's UPC
* **Given** I am prompted to enter a value to change the UPC to
* **When** I enter an item ID and value to change the UPC to
* **And** The item exists in the system
* **Then** The UPC of that item is updated in the database
#### Scenario:Manager attempts to change the UPC of a nonexistent item
* **Given** I am prompted to enter a value to change the UPC to
* **When** I enter an item ID and value to change the UPC to
* **And** The item does not exist in the system
* **Then** I am informed that the item does not exist and the database remains unchanged
#### Scenario: Manager changes an existing item's supplier
* **Given** I am prompted to enter a value to change the supplier to
* **When** I enter an item ID and value to change the supplier to
* **And** The item exists in the system
* **Then** The supplier of that item is updated in the database
#### Scenario:Manager attempts to change the supplier of a nonexistent item
* **Given** I am prompted to enter a value to change the supplier to
* **When** I enter an item ID and value to change the supplier to
* **And** The item does not exist in the system
* **Then** I am informed that the item does not exist and the database remains unchanged
#### Scenario: Manager changes an existing item's description
* **Given** I am prompted to enter a value to change the description to
* **When** I enter an item ID and value to change the description to
* **And** The item exists in the system
* **Then** The description of that item is updated in the database
#### Scenario:Manager attempts to change the description of a nonexistent item
* **Given** I am prompted to enter a value to change the description to
* **When** I enter an item ID and value to change the description to
* **And** The item does not exist in the system
* **Then** I am informed that the item does not exist and the database remains unchanged

## Data Ownership & Isolation
Item data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Warehouse Managers can see item types and information  |
| **Write scope** | Only logged in Warehouse Admins can edit or remove items if the item exists `id` and `req.user.id` |
| **Create scope** | Only logged in Warehouse Admins can create new items |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/items/read` | Yes | Read data of a specific item |
| `POST` | `/items/edit` | Yes | Change an existing item's information |
| `POST` | `/items/create` | Yes | Create a new item type |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "itemid": 1,
  "itemName": "name",
  "price": "$0.00",
  "SKU": "sku",
  "UPC": "11111111111",
  "Supplier": "supplier",
  "description": "desc"
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays item id, name, price, SKU, UPC, Supplier, and description

### [View: Edit Page] — route name `edit`
*   Fields: id, name, price, SKU, UPC, Supplier, description.
*   Primary action: **Edit Item**.
*   Buttons to save or cancel editing of item
*   Verify pressing of save or cancel button

### [View: Create Page] — route name `create`
*   Fields: id, name, price, SKU, UPC, Supplier, description.
*   Primary action: **Create Item**.
*   Buttons to save or cancel creating of item
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