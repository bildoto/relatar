# 7. Validation Model

**Relatar Specification 0.2 – Draft**

---

# 7.1 Purpose

The Validation Model defines how Relatar evaluates the consistency and integrity of documented infrastructure.

Validation analyses the documented model without modifying it.

The purpose of validation is to identify inconsistencies, conflicts and potential issues before they become operational problems.

---

# 7.2 Principles

Validation SHALL analyse the documented infrastructure.

Validation SHALL NOT modify the documented infrastructure.

Validation results are advisory unless explicitly defined as Errors by this specification.

Validation SHALL be repeatable.

The same documented installation SHALL always produce the same validation results.

---

# 7.3 Validation Scope

Validation MAY be performed against:

* a Component
* an Object
* a Route
* a Configuration
* a Baseline
* a complete Venue

Implementations SHOULD allow validation at multiple levels.

---

# 7.4 Validation Severity

Validation findings SHALL be assigned a severity.

## Information

Provides useful observations.

Examples:

* Route uses three Dante flows.
* Component has unused Connection Points.
* Route traverses four transport technologies.

---

## Warning

Indicates a potential issue that may require attention.

Examples:

* Inefficient Dante channel allocation.
* Object has many unused Connection Points.
* Route contains unnecessary conversions.
* Configuration overrides a large number of Baseline relationships.

Warnings do not necessarily indicate incorrect documentation.

---

## Error

Indicates an inconsistency or impossible condition.

Examples:

* Duplicate exclusive assignments.
* Broken Route.
* Missing Connection Point.
* Circular dependency.
* Conflicting Configuration.
* Connection Point connected to multiple exclusive destinations.

Errors SHALL prevent an Effective Installation from being considered valid.

---

# 7.5 Validation Categories

Validation MAY include:

## Structural

Examples:

* Orphaned Objects
* Missing Locations
* Invalid containment
* Containment loops

---

## Connectivity

Examples:

* Broken physical connections
* Duplicate physical connections
* Incompatible Connection Point capabilities

---

## Routing

Examples:

* Broken Routes
* Circular Routes
* Missing logical assignments
* Unreachable Destinations

---

## Configuration

Examples:

* Configuration conflicts
* Missing inherited Objects
* Invalid overrides
* Resource conflicts

---

## Component

Examples:

* Constraint violations
* Unsupported Connection Point usage
* Exceeded channel limits
* Exceeded flow limits

---

## Documentation

Examples:

* Missing descriptions
* Missing documentation
* Missing manufacturer
* Missing Component reference

---

# 7.6 Constraints

Components MAY define Constraints.

Examples include:

* Maximum analogue inputs
* Maximum Dante transmit flows
* Maximum power consumption
* Maximum channel count
* Supported transport technologies

Validation evaluates documented infrastructure against these Constraints.

Constraints describe the capabilities of Components.

They are not validation rules themselves.

---

# 7.7 Technology-specific Validation

Implementations MAY provide technology-specific validation.

Examples include:

* Dante flow utilisation
* HDBaseT distance limits
* Fibre compatibility
* PoE power budgets

Technology-specific validation SHALL be advisory unless a documented Constraint is violated.

---

# 7.8 Effective Installation Validation

Before an Effective Installation is generated, Relatar SHALL validate:

* inherited Relationships
* inherited Objects
* inherited Routes
* Configuration overrides
* resource conflicts

An Effective Installation SHALL be considered valid only if no unresolved Errors remain.

---

# 7.9 Validation Reports

Validation results MAY be presented as reports.

Typical reports include:

* Validation Summary
* Error Report
* Warning Report
* Commissioning Readiness
* Technology Diagnostics

Reports SHOULD reference the affected entities directly.

---

# 7.10 Architectural Principles

The Validation Model follows these principles:

* Validation analyses; it never modifies.
* Constraints define capability.
* Validation evaluates Constraints.
* Technology-specific validation complements the generic model.
* Validation assists engineering judgement rather than replacing it.
* Validation SHALL be deterministic and repeatable.
