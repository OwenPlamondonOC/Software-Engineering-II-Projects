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