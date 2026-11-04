# Feature: Report Picking Inventory Issue
**Feature ID:** RPI
**Branch pattern:** `feature/RSI-report-picking-issue`
**Status:** Draft
**Created:** 2026-09-28

---
## User Stories
### US-N.1: Report Empty Bins
**As a** Warehouse Worker
**I want to** scan an empty bin's UPC
**So that** the system sends a priority assignment to refill the bin
**Priority:** P1
**Independent test:** scan an empty test bin and see the assignment be generated
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria
### US-N.2: Report Out Of Stock Item
**As a** Warehouse Manager
**I want to** have workers tell the system if an item is out of stock
**So that** the system makes me a report that an item has run out of stock
**Priority:** P1
**Independent test:** tell the system an item has run out of stock and see the system generate a report
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST know what items each bin has
- **FR-002**: System MUST know item inventory
- **FR-003**: System MUST know how to make a report
- **FR-004**: System MUST deliver reports to a manager

---
## Key Entities
- **User**: warehouse manager; maintains information in the database and communications
- **User**: warehouse worker; moves items around the warehouse
- **Database**: information storage; tracks information inputted by warehouse workers and managers
- **System**: automation device; automatically tracks orders

---
## Acceptance Criteria
### US-N.1 - Report Empty Bins
#### Scenario: System generates a refill order
* **Given** A bin is empty
* **When** A worker scans that bin's UPC
* **Then** A priority assignment is created for another worker to refill the bin
### US-N.2 - Report Out Of Stock Item
#### Scenario: System generates a refill order
* **Given** An item is out of stock
* **When** A worker reports that an item is out of stock
* **Then** The system creates a report documenting the details of the mistake
* **And** Delivers the report to a warehosue manager
* **And** Updates the item in the database to have an inventory of zero

## Data Ownership & Isolation
Warehouse managers can see all reports.
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Warehouse Managers can see reports |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/report-picking/access` | Yes | Access a picking issue report |


**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `access`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays the picking issue report

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