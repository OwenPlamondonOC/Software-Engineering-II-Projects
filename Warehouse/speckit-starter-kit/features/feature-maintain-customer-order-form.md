# Feature: Maintain Customer Order Forms
**Feature ID:** MCO
**Branch pattern:** `feature/MCO-maintain-customer-order-forms`
**Status:** Draft
**Created:** 2026-09-24

---
## User Stories
### US-N.1: Add Customer Order Form
**As a** Warehouse manager
**I want to** input the information of a new customer order form
**So that** the database adds this information to the database
**Priority:** P1
**Independent test:** add a new customer order form and display its information
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Customer Order Form
**As a** Warehouse manager
**I want to** select an existing customer order form for removal
**So that** the database removes this customer order form's information from the database
**Priority:** P1
**Independent test:** remove a customer order form and see that it no longer exists where it was in the database
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Customer Order Form
**As a** Warehouse manager
**I want to** input new information for an existing customer order form
**So that** the information for that customer order form is updated in the database
**Priority:** P1
**Independent test:** edit an existing customer order form in the database and have the new information displayed to the user
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit customer order forms
- **FR-002**: System MUST store information of customer order forms in a database

---
## Key Entities
- **User**: warehouse manager; maintains customer order forms
- **Database**: information storage; tracks information including customer order forms and its information

---
## Acceptance Criteria
### US-N.1 - Add Customer Order Form
#### Scenario: Manager adds a new customer order form to the system
* **Given** I am prompted to enter information for the new customer order form
* **When** I enter the customer order form's information
* **And** The customer order form does not already exist in the system
* **Then** The customer order form's information is added to the system
#### Scenario: Manager attempts to add an existing customer order form to the system
* **Given** I am prompted to enter information for the new customer order form
* **When** I enter the customer order form's information
* **And** The customer order form already exists in the system
* **Then** I am informed that the customer order form already exists and am prompted to either edit the customer order form's information or cancel the operation

### US-N.2 - Remove Customer Order Form
#### Scenario: Manager removes an existing customer order form from the system
* **Given** I am prompted to enter an customer order form to delete from the system
* **When** I enter the customer order form I wish to delete
* **And** The customer order form exists in the system
* **Then** The customer order form's information is removed from the system
#### Scenario: Manager attempts to remove a nonexistent customer order form from the system
* **Given** I am prompted to enter an customer order form to delete from the system
* **When** I enter the customer order form I wish to delete
* **And** The customer order form does not exist in the system
* **Then** I am informed that the customer order form does not exist and the database remains unchanged

### US-N.3 - Edit Customer Order Form
#### Scenario: Manager changes an existing customer order form's information
* **Given** I am prompted to enter a customer order form and its information
* **When** I enter a customer order form and new information regarding the customer order form
* **And** The customer order form exists in the system
* **Then** The customer order form's information is updated in the database
#### Scenario:Manager attempts to change the information of a nonexistent customer order form
* **Given** I am prompted to enter a customer order form and its information
* **When** I enter a customer order form and new information regarding the customer order form
* **And** The customer order form does not exist in the system
* **Then** I am informed that the customer order form does not exist and the database remains unchanged