# Feature: Recieve Customer Orders
**Feature ID:** RCO
**Branch pattern:** `feature/RCO-recieve-customer-orders`
**Status:** Draft
**Created:** 2026-09-28

---
## User Stories
### US-N.1: Accept Orders
**As a** Warehouse manager
**I want to** accept orders from customers
**So that** the system automatically creates picking assignments for floor workers
**Priority:** P1
**Independent test:** accept a test order and see it generate an assignment
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST know what customers have sent which orders
- **FR-002**: System MUST know when orders must be delivered

---
## Key Entities
- **User**: warehouse manager; maintains information in the system and database
- **System**: automation device; automatically recieves orders and generates assignments

---
## Acceptance Criteria
### US-N.1 - Accept Orders
#### Scenario: Manager accepts an order from a customer
* **Given** An order has been placed by a customer
* **And** The system recieves the order and reports it to a warehosue manager
* **When** The manager accepts the order
* **Then** The system generates a new picking assignment and adds it to the assignment queue
#### Scenario: Manager rejects an order from a customer
* **Given** An order has been placed by a customer
* **And** The system recieves the order and reports it to a warehosue manager
* **When** The manager rejects the order
* **Then** The system discards the order