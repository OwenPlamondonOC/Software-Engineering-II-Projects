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

## Data Ownership & Isolation
Employee data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Warehouse Managers can see employee information  |
| **Write scope** | Only logged in Warehouse Admins can edit or remove emplyees if they exist `id` and `req.user.id` |
| **Create scope** | Only logged in Warehouse Admins can add new employees |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/employees/read` | Yes | Read a employee's information |
| `POST` | `/employees/edit` | Yes | Change an existing employee's information |
| `POST` | `/employees/add` | Yes | Add a new employee |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "employeeid": 1,
  "employeeName": "Example",
  "employeeAddress": "ExAddress",
  "employeePhone": "111-111-1111:",
  "employeeEmail": "example@example.ex"
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays employee information

### [View: Edit Page] — route name `edit`
*   Fields: fields for all data of the employee.
*   Primary action: **Edit Employee**.
*   Buttons to save or cancel editing of employee
*   Verify pressing of save or cancel button

### [View: Add Page] — route name `add`
*   Fields: fields for all data of the employee.
*   Primary action: **Add Employee**.
*   Buttons to save or cancel addition of employee
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