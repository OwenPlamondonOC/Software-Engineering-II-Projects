# Feature: Report Supply Delivery Issue
**Feature ID:** RSI
**Branch pattern:** `feature/RSI-report-supply-issue`
**Status:** Draft
**Created:** 2026-09-28

---
## User Stories
### US-N.1: Report Recieving Less Than Ordered
**As a** Warehouse Manager
**I want to** have recieved items' UPCs be scanned
**So that** the system makes me a report if the items delivered do not match the order
**Priority:** P1
**Independent test:** scan the wrong amount of items for a test order and see the system generate a report
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST know what items each order has
- **FR-002**: System MUST know how to make a report
- **FR-003**: System MUST deliver reports to a manager

---
## Key Entities
- **User**: warehouse manager; maintains information in the database and communications
- **Database**: information storage; tracks information inputted by warehouse workers and managers
- **System**: automation device; automatically tracks orders

---
## Acceptance Criteria
### US-N.1 - Report Recieving Less Than Ordered
#### Scenario: System generates a supply issue report
* **Given** An incorrect order is recieved
* **When** The UPCs of the order are scanned
* **Then** The system creates a report documenting the details of the mistake
* **And** Delivers the report to a warehosue manager