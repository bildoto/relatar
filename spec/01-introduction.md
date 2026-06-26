# 1. Introduction

**Relatar Specification 0.1 – Draft**

---

# 1.1 Purpose

Relatar is a vendor-independent knowledge base for documenting, understanding and tracing technical infrastructure.

Rather than documenting individual devices or producing static diagrams, Relatar models infrastructure as a collection of objects connected through explicit relationships.

These relationships allow Relatar to answer practical questions about an installation while maintaining a single source of truth.

Relatar is designed to describe not only how an installation is built, but also how it is used.

---

# 1.2 Objectives

Relatar has four primary objectives.

1. Document technical infrastructure accurately.
2. Preserve knowledge about complex installations.
3. Enable rapid troubleshooting through relationship tracing.
4. Generate accurate documentation from a single source of truth.

Every feature in Relatar should contribute to one or more of these objectives.

---

# 1.3 Scope

Relatar is intended to document technical infrastructure regardless of technology, manufacturer or application.

Typical applications include:

* Professional audio systems
* Video distribution
* Computer networks
* Structured cabling
* Fibre infrastructure
* Building automation
* Security systems
* Access control
* Industrial control systems

The concepts defined by this specification are intentionally technology-independent.

---

# 1.4 Non-goals

Relatar is not intended to replace specialist engineering tools.

Examples include:

* CAD software
* DSP programming software
* Network monitoring systems
* Device discovery systems
* Configuration backup systems

Instead, Relatar documents how these systems relate to one another.

---

# 1.5 Fundamental Concepts

Relatar is built upon four fundamental concepts.

## Baseline

Every venue has exactly one **Baseline**.

The Baseline represents the canonical description of the permanent installation.

It contains the infrastructure that normally exists at the venue, including:

* locations
* cabinets
* equipment
* ports
* permanent cables
* permanent signal paths
* default operating behaviour

The Baseline serves as the reference against which all temporary changes are measured.

---

## Relationships

Relationships describe how infrastructure is connected.

Examples include:

* contains
* connected to
* located in
* routes through
* controls
* depends on

Relationships are the primary source of knowledge within Relatar.

Without relationships, infrastructure is merely a collection of isolated objects.

---

## Configurations

Technical installations rarely operate in exactly one state.

Equipment may be moved.

Temporary microphones may be installed.

Additional cameras may appear.

Signal routing may change.

Operational modes may differ.

Relatar models these temporary differences using **Configurations**.

A Configuration represents a temporary modification of the Baseline.

Configurations inherit the Baseline and record only the differences required to describe the temporary state of the installation.

---

## Effective Installation

At any moment, the installation visible to the user is the result of combining the Baseline with an optional Configuration.

Conceptually:

```text
Effective Installation
    =
Baseline
    +
Configuration
```

If no Configuration is active, the Effective Installation is simply the Baseline.

---

# 1.6 Configurations

Configurations describe temporary operational changes.

Examples include:

* Sunday Service
* Christmas Concert
* Wedding
* Conference
* Live Stream
* Maintenance
* Testing

A Configuration may:

* add temporary equipment
* relocate existing equipment
* add temporary cables
* disable permanent connections
* modify signal routing
* activate specific operating modes
* add temporary documentation
* define temporary notes

Configurations never modify the Baseline.

Instead, they describe how the installation differs from it.

# Configuration conflicts

A conflict occurs when two or more Configuration layers attempt to modify the same resource in incompatible ways.

Examples:

- Two temporary objects assigned to the same physical port.
- One Configuration disables a connection while another depends on it.
- Two routes require exclusive use of the same device input.
- One Configuration moves an object while another connects to it at its original location.
- Two modes require contradictory state for the same route.

Relatar SHALL detect Configuration conflicts when generating an Effective Installation.

Relatar SHALL NOT resolve conflicts automatically.

A Configuration containing unresolved conflicts SHALL be considered invalid for operational use.

Users MUST resolve conflicts by creating an explicit override or by defining a new Configuration that represents the intended combined state.

---

# 1.7 Inheritance

Every Configuration inherits from exactly one Baseline.

A Configuration stores only the information that differs from the Baseline.

Examples include:

* equipment temporarily relocated
* additional microphones
* temporary patching
* temporary signal routes
* overridden operating modes

This approach minimises duplication while preserving a single authoritative description of the permanent installation.

Future versions of Relatar may support Configuration inheritance, allowing one Configuration to extend another.

For example:

```text
Baseline

└── Sunday Service
        └── Sunday Service + Livestream
                └── Sunday Service + Livestream + Choir
```

---

# 1.8 Single Source of Truth

Relatar maintains one authoritative description of a venue.

The Baseline contains the permanent infrastructure.

Configurations contain only temporary differences.

Reports, diagrams, route sheets and impact analyses are generated from these relationships rather than maintained independently.

This ensures that all documentation remains consistent while avoiding unnecessary duplication.

---

# 1.9 Intended Use

Relatar should enable users to answer questions such as:

* Where is this device normally located?
* Where is this device in the active Configuration?
* What is connected to this port?
* Which connector is required?
* Where does this signal travel?
* Which Configuration changes this route?
* What equipment is required for tomorrow's event?
* What systems are affected if this cable fails?
* What has changed compared to the Baseline?

The value of Relatar is measured by its ability to answer these questions accurately and consistently.

---

# 1.10 Guiding Statement

Relatar exists to preserve technical knowledge and make complex infrastructure understandable.

Its purpose is not merely to document equipment, but to describe how technical systems work together over time.

By combining a permanent Baseline with temporary Configurations, Relatar provides an accurate representation of both the installation and its operational use.

In its simplest form:

> **Know how everything is connected.**
