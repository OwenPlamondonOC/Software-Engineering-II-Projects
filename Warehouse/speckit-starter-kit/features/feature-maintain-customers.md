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