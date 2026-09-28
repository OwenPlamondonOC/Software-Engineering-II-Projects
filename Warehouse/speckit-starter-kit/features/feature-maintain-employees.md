# Feature: Maintain Employees
**Feature ID:** ME
**Branch pattern:** `feature/ME-maintain-employees`
**Status:** Draft
**Created:** 2026-09-24

---
## User Stories
### US-N.1: Add Employee
**As a** Warehouse manager
**I want to** input the information of a new employee
**So that** the database adds this information to the database
**Priority:** P1
**Independent test:** add a new employee and display their information
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Employee
**As a** Warehouse manager
**I want to** select an existing employee for removal
**So that** the database removes this employee's information from the database
**Priority:** P1
**Independent test:** remove a employee and see that it no longer exists where it was in the database
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Employee
**As a** Warehouse manager
**I want to** input new information for an existing employee
**So that** the information for that employee is updated in the database
**Priority:** P1
**Independent test:** edit an existing employee in the database and have the new information displayed to the user
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit employees
- **FR-002**: System MUST store information of employees in a database

---
## Key Entities
- **User**: warehouse manager; maintains employees
- **Database**: information storage; tracks information including employees and their information

---
## Acceptance Criteria
### US-N.1 - Add Employee
#### Scenario: Admin adds a new employee to the system
* **Given** I am prompted to enter information for the new employee
* **When** I enter the employee's information
* **And** The employee does not already exist in the system
* **Then** The employee's information is added to the system
#### Scenario: Admin attempts to add an existing employee to the system
* **Given** I am prompted to enter information for the new employee
* **When** I enter the employee's information
* **And** The employee already exists in the system
* **Then** I am informed that the employee already exists and am prompted to either edit the employee's information or cancel the operation

### US-N.2 - Remove Employee
#### Scenario: Admin removes an existing employee from the system
* **Given** I am prompted to enter an employee to delete from the system
* **When** I enter the employee I wish to delete
* **And** The employee exists in the system
* **Then** The employee's information is removed from the system
#### Scenario: Admin attempts to remove a nonexistent employee from the system
* **Given** I am prompted to enter an employee to delete from the system
* **When** I enter the employee I wish to delete
* **And** The employee does not exist in the system
* **Then** I am informed that the employee does not exist and the database remains unchanged

### US-N.3 - Edit Employee
#### Scenario: Admin changes an existing employee's information
* **Given** I am prompted to enter a employee and their information
* **When** I enter a employee and new information regarding the employee
* **And** The employee exists in the system
* **Then** The employee's information is updated in the database
#### Scenario:Admin attempts to change the information of a nonexistent employee
* **Given** I am prompted to enter a employee and their information
* **When** I enter a employee and new information regarding the employee
* **And** The employee does not exist in the system
* **Then** I am informed that the employee does not exist and the database remains unchanged