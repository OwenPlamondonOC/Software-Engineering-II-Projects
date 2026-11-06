# Feature: Closed system with admin control

## **Feature ID:** C
**Branch pattern:** `feature/C-closed-system`
**Status:** Draft
**Created:** 2026-09-10

## User Stories

### US-N.1: Login as admin

**As a** church staff member
**I want to** input my username and password into the system
**So that** the system allows me to view and modify the databases
**Priority:** P1
**Independent test:** sign in as a staff member and display a home screen
**Acceptance scenarios:** see US-N.1 under Acceptance Criteria

### US-N.2: Add new admin

**As a** church admin
**I want to** input a new username and password
**So that** the system allows those credentials to be used to access the system
**Priority:** P1
**Independent test:** create a new admin account and use it to sign in
**Acceptance scenarios:** see US-N.2 under Acceptance Criteria

### US-N.3: Remove an admin

**As a** church admin
**I want to** select an existing admin account
**So that** those credentials no longer work for accessing the database
**Priority:** P1
**Independent test:** remove a user and unsuccessfully attempt to log in using those credentials
**Acceptance scenarios:** see US-N.3 under Acceptance Criteria

---
### Functional Requirements

- **FR-001**: System MUST allow access to the system ONLY if entered credentials match registered ones
- **FR-002**: System MUST allow credentials to be added and removed
- **FR-003**: System MUST keep track of active credentials
- **FR-004**: System MUST have a default admin to allow creation of other credentials

---

## Initial Data

- One trustworthy church member needs to initially have access to the system

---

## Acceptance Criteria
### US-N.1 — Login as admin
#### Scenario: Admin logs into the system
* **Given** I am on the login page
* **And** my credentials are registered
* **When** I input my credentials
* **Then** the program redirects me to the home page

### US-N.2 — Add new admin
#### Scenario: Church administrator adds new credentials
* **Given** I am currently logged to the system as an admin
* **When** I enter new admin credentials into the system
* **Then** the program will add those credentials to the database
* **And** those credentials will be able to be used to log in

### US-N.3 — Remove an admin
#### Scenario: Church administrator removes credentials
* **Given** I am currently logged to the system as an admin
* **And** there are currently existing admin credentials
* **When** I select those credentials for deletion
* **Then** the program will remove those credentials from the database
* **And** those credentials will no longer be able to be used to log in