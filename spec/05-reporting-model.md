# 5. Reporting Model

**Relatar Specification 0.2 – Draft**

---

# 5.1 Purpose

The Reporting Model defines how information stored within Relatar is presented to users.

Reports are generated views of the underlying data.

They SHALL NOT introduce information that is not present within the documented Relationships.

Reports SHALL always reflect the currently selected Baseline and Configuration.

---

# 5.2 Philosophy

Relatar maintains a single source of truth.

Reports are generated from that source.

Implementations SHALL NOT require users to maintain reports manually.

If the underlying data changes, regenerated reports SHALL immediately reflect those changes.

---

# 5.3 Reports and Documents

Relatar distinguishes between Reports and Documents.

## Report

A Report is a generated view intended for inspection or analysis.

Examples include:

* Equipment List
* Cable Schedule
* Patch Panel Schedule
* Route List
* Configuration Comparison
* Device Inventory

Reports are typically viewed on screen but MAY also be printed.

---

## Document

A Document is generated to assist technicians during installation, commissioning or maintenance.

Examples include:

* Commissioning Guide
* Programming Guide
* Setup Guide
* Teardown Guide
* Fault Finding Guide
* Route Sheet

Documents are intended to be used while performing work.

They SHOULD be printable.

---

# 5.4 Report Categories

Reports generally fall into one or more categories.

## Inventory

Examples:

* Equipment Inventory
* Rack Contents
* Device List

---

## Connectivity

Examples:

* Cable Schedule
* Patch Panel Schedule
* Connection List
* Cross-reference Report

---

## Routing

Examples:

* Route Sheet
* Signal Flow
* Route Summary

---

## Configuration

Examples:

* Configuration Differences
* Planned Changes
* Temporary Equipment

---

## Validation

Examples:

* Missing Assignments
* Broken Routes
* Unused Connection Points
* Conflicting Assignments
* Orphaned Objects

---

## Planning

Examples:

* Installation Checklist
* Cable Pull List
* Equipment Procurement
* Commissioning Tasks

---

# 5.5 Commissioning Documentation

Relatar MAY generate commissioning documentation.

Examples include:

Physical Tasks

* Install equipment.
* Connect cable PN-017.
* Patch AVK-2 Port 14 to AVK-5 Port 14.

Software Tasks

* Assign BLU Analog Input 1 to Dante TX 1.
* Assign Dante RX 12 to GLD Channel 20.
* Configure Kramer Encoder 2 to Decoder 5.
* Enable the Sunday Service Configuration.

Commissioning documentation SHALL be derived from documented Relationships and Assignments.

---

# 5.6 Fault Finding

Implementations MAY generate fault-finding documentation.

Examples include:

* Route Trace
* Dependency Report
* Impact Analysis
* Equipment Dependencies

Example queries:

* What fails if this cable is disconnected?
* Which Routes use this device?
* Which Configuration introduced this assignment?
* Which loudspeakers depend on this amplifier?

---

# 5.7 Configuration Reporting

Reports SHALL be generated within the context of a Baseline and, optionally, a Configuration.

Examples include:

* Baseline only
* Sunday Service
* Christmas Concert
* Livestream

Implementations SHOULD clearly identify which Configuration was used when generating the report.

---

# 5.8 Report Metadata

Generated reports SHOULD include:

* Venue
* Configuration
* Baseline Revision
* Configuration Revision
* Generation Date
* Generator Version
* Page Numbers

This information assists traceability and version control.

---

# 5.9 Printability

Reports and Documents SHOULD be designed for both screen viewing and printed use.

Printed output SHOULD remain useful during installation and maintenance where mobile devices may be impractical.

Layouts SHOULD prioritise clarity over compactness.

---

# 5.10 Architectural Principles

The Reporting Model follows these principles:

* Reports are generated, never maintained.
* Documents are generated from Reports and Relationships.
* Every report reflects the current Effective Installation.
* Every report SHALL be reproducible.
* Printed documentation remains a first-class use case.
* Reports SHALL never become an independent source of truth.
