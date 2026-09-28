# Feature: Pick Items
**Feature ID:** PI
**Branch pattern:** `feature/PI-pick-items`
**Status:** Draft
**Created:** 2026-09-28

---
## User Stories
### US-N.1: Assign Assignments
**As a** Warehouse worker
**I want to** accept an assignment from the system
**So that** the system tells me what items to get and where to find them
**Priority:** P1
**Independent test:** accept a test assignment and see an item list appear
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria
### US-N.2: Generate Route
**As a** Warehouse worker
**I want to** accept an assignment for picking
**So that** the system generates an efficient route through the warehouse to pick the items
**Priority:** P1
**Independent test:** accept a test assignment and see it generate a route
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria
### US-N.3: Pick Items
**As a** Warehouse worker
**I want to** scan items' UPC labels
**So that** the system acknowledges those items have been picked and removes them from the picking list and inventory
**Priority:** P1
**Independent test:** scan an item and see the assignment and database update
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST know what items each order has
- **FR-002**: System MUST create an efficient route through the warehouse
- **FR-003**: System MUST update inventory based on picked items

---
## Key Entities
- **User**: warehouse worker; moves items around the warehouse
- **System**: automation device; automatically gives and tracks assignments, generates routes, and tracks inventory

---
## Acceptance Criteria
### US-N.1 - Assign Assignments
#### Scenario: Worker accepts the next assignment in the queue
* **Given** An assignment exists in the queue
* **When** A worker accepts an assignment
* **Then** The system generates a list of items that the worker should pick
### US-N.2 - Generate Route
#### Scenario: Worker accepts the next assignment in the queue
* **Given** An assignment exists in the queue
* **When** A worker accepts an assignment
* **Then** The system generates a route that the worker should follow to pick those items efficiently
### US-N.3 - Pick Items
#### Scenario: Worker picks and scans correct items
* **Given** A worker has a picking assignment
* **When** The worker picks and scans all the correct items
* **Then** The system checks off picked items from the assignment and tells the worker when all items have been picked
#### Scenario: Worker picks and scans incorrect items
* **Given** A worker has a picking assignment
* **When** The worker picks and scans an incorrect item
* **Then** The system warns the worker that the item they have scanned is not in the order
#### Scenario: Worker misses an item
* **Given** A worker has a picking assignment
* **When** The worker tries to bring the picked order to shipping
* **And** not all items on the list have been collected
* **Then** The system warns the worker that there are missing items in the order
#### Scenario: Warehouse has run out of item inventory
* **Given** A worker has a picking assignment
* **When** The worker notices or creates an empty bin
* **And** they scan that bin's UPC
* **Then** The system creates a report that the bin is empty and requests a refill