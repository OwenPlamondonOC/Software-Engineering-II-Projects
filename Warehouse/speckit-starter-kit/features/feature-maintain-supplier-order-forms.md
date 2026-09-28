# Feature: Maintain Supplier Order Forms
**Feature ID:** MSO
**Branch pattern:** `feature/MSO-maintain-supplier-order-forms`
**Status:** Draft
**Created:** 2026-09-24

---
## User Stories
### US-N.1: Add Supplier Order Form
**As a** Warehouse manager
**I want to** input the information of a new supplier order form
**So that** the database adds this information to the database
**Priority:** P1
**Independent test:** add a new supplier order form and display its information
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Supplier Order Form
**As a** Warehouse manager
**I want to** select an existing supplier order form for removal
**So that** the database removes this supplier order form's information from the database
**Priority:** P1
**Independent test:** remove a supplier order form and see that it no longer exists where it was in the database
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Supplier Order Form
**As a** Warehouse manager
**I want to** input new information for an existing supplier order form
**So that** the information for that supplier order form is updated in the database
**Priority:** P1
**Independent test:** edit an existing supplier order form in the database and have the new information displayed to the user
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit supplier order forms
- **FR-002**: System MUST store information of supplier order forms in a database

---
## Key Entities
- **User**: warehouse manager; maintains supplier order forms
- **Database**: information storage; tracks information including supplier order forms and its information

---
## Acceptance Criteria
### US-N.1 - Add Supplier Order Form
#### Scenario: Manager adds a new supplier order form to the system
* **Given** I am prompted to enter information for the new supplier order form
* **When** I enter the supplier order form's information
* **And** The supplier order form does not already exist in the system
* **Then** The supplier order form's information is added to the system
#### Scenario: Manager attempts to add an existing supplier order form to the system
* **Given** I am prompted to enter information for the new supplier order form
* **When** I enter the supplier order form's information
* **And** The supplier order form already exists in the system
* **Then** I am informed that the supplier order form already exists and am prompted to either edit the supplier order form's information or cancel the operation

### US-N.2 - Remove Supplier Order Form
#### Scenario: Manager removes an existing supplier order form from the system
* **Given** I am prompted to enter an supplier order form to delete from the system
* **When** I enter the supplier order form I wish to delete
* **And** The supplier order form exists in the system
* **Then** The supplier order form's information is removed from the system
#### Scenario: Manager attempts to remove a nonexistent supplier order form from the system
* **Given** I am prompted to enter an supplier order form to delete from the system
* **When** I enter the supplier order form I wish to delete
* **And** The supplier order form does not exist in the system
* **Then** I am informed that the supplier order form does not exist and the database remains unchanged

### US-N.3 - Edit Supplier Order Form
#### Scenario: Manager changes an existing supplier order form's information
* **Given** I am prompted to enter a supplier order form and its information
* **When** I enter a supplier order form and new information regarding the supplier order form
* **And** The supplier order form exists in the system
* **Then** The supplier order form's information is updated in the database
#### Scenario:Manager attempts to change the information of a nonexistent supplier order form
* **Given** I am prompted to enter a supplier order form and its information
* **When** I enter a supplier order form and new information regarding the supplier order form
* **And** The supplier order form does not exist in the system
* **Then** I am informed that the supplier order form does not exist and the database remains unchanged