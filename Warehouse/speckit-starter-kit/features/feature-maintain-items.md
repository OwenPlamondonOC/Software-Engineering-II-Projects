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