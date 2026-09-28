# Feature: Maintain Warehouse Inventory
**Feature ID:** MIN
**Branch pattern:** `feature/MIN-maintain-inventory`
**Status:** Draft
**Created:** 2026-09-21

---
## User Stories
### US-N.1: Add Item Inventory
**As a** Warehouse worker
**I want to** input the type of item added and amount added
**So that** the database adds this number to its existing stock number in the database
**Priority:** P1
**Independent test:** add a non-zero amount of an item and see the database change the stock
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Item Inventory
**As a** Warehouse worker
**I want to** input the type of item removed and amount removed
**So that** the database subtracts this number from its existing stock number in the database
**Priority:** P1
**Independent test:** remove a non-zero amount of an item and see the database change the stock
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Item Inventory
**As a** Warehouse worker
**I want to** input the type of item and the new amount that is in stock
**So that** the database changes the stock number in the database to this number
**Priority:** P1
**Independent test:** enter a new quantity for an item and see the database change the stock
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit item inventory
- **FR-002**: System MUST store quantity of individual items in the warehouse in a database

---
## Key Entities
- **User**: floor worker; maintains item inventory
- **Database**: information storage; tracks information including item inventory

---
## Acceptance Criteria
### US-N.1 - Add Item Inventory
#### Scenario: Worker adds to an existing item's stock
* **Given** I am prompted to enter a value to increase the stock by
* **When** I enter an item ID and quantity to increase the stock by
* **And** The item exists in the system
* **Then** The quantity of that item is updated in the database
#### Scenario: Worker attempts to add to the stock of a nonexistent item
* **Given** I am prompted to enter a value to increase the stock by
* **When** I enter an item ID and quantity to increase the stock by
* **And** The item does not exist in the system
* **Then** I am informed that the item does not exist and the database remains unchanged

### US-N.2 - Remove Item Inventory
#### Scenario: Worker removes items from an existing item's stock
* **Given** I am prompted to enter a value to decrease the stock by
* **When** I enter an item ID and quantity to decrease the stock by
* **And** The item exists in the system
* **Then** The quantity of that item is updated in the database
#### Scenario: Worker attempts to remove items from the stock of a nonexistent item
* **Given** I am prompted to enter a value to decrease the stock by
* **When** I enter an item ID and quantity to decrease the stock by
* **And** The item does not exist in the system
* **Then** I am informed that the item does not exist and the database remains unchanged

### US-N.3 - Edit Item Inventory
#### Scenario: Worker changes an existing item's stock
* **Given** I am prompted to enter a value to change the stock to
* **When** I enter an item ID and quantity to change the stock to
* **And** The item exists in the system
* **Then** The quantity of that item is updated in the database
#### Scenario: Worker attempts to change the stock of a nonexistent item
* **Given** I am prompted to enter a value to change the stock to
* **When** I enter an item ID and quantity to change the stock to
* **And** The item does not exist in the system
* **Then** I am informed that the item does not exist and the database remains unchanged