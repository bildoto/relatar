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

Configurations describe temporary or alternative operational states of a venue.

A Configuration represents how the installation is intended to operate for a particular purpose without modifying the Baseline.

Typical Configurations include:

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
* include setup and teardown procedures
* include documentation and operational notes
* reference external documentation

Configurations are not limited to describing physical changes.

They may also describe operational knowledge required to reproduce a particular setup.

---

# 1.7 Evolution

Technical infrastructure is not static.

Permanent installations evolve.

Operational procedures improve.

Temporary setups become recurring practices.

Relatar is designed to preserve this evolution rather than overwrite it.

Both the Baseline and Configurations are expected to evolve over time.

Future versions of Relatar may support immutable revision histories for both.

Conceptually:

```text
Temple

Baseline
    Revision 1
    Revision 2
    Revision 3

Christmas Concert
    Revision 1
    Revision 2

Sunday Service
    Revision 1
    Revision 2
```

Revision history allows Relatar to answer questions such as:

* What changed since last year's Christmas concert?
* Which revision introduced this cable?
* When was this routing modified?
* What changed after the renovation?

Revision management is considered an architectural capability of Relatar.

Implementations MAY choose not to expose revision management initially, provided that the architecture does not prevent it from being introduced later.

---

# 1.8 Configuration Inheritance

Every Configuration inherits from exactly one parent.

Normally, this parent is the venue Baseline.

Future versions of Relatar MAY allow Configurations to inherit from other Configurations.

For example:

```text
Baseline

└── Sunday Service
        └── Sunday Service + Livestream
                └── Sunday Service + Livestream + Choir
```

Configuration inheritance exists to reduce duplication by allowing specialised Configurations to extend existing operational setups.

Implementations SHOULD avoid deep inheritance hierarchies.

Long inheritance chains increase complexity and make operational behaviour more difficult to understand.

---

# 1.9 Configuration Conflicts

Configuration inheritance may introduce conflicts.

A conflict occurs when two or more inherited layers attempt to modify the same resource in incompatible ways.

Examples include:

* Two Configurations assigning different signals to the same physical input.
* One Configuration disables a connection required by another.
* Two routes require exclusive use of the same equipment.
* Two Configurations relocate the same object to different locations.
* Two Configurations require contradictory operating modes.

Relatar SHALL detect configuration conflicts before producing an Effective Installation.

Relatar SHALL NOT resolve conflicts automatically.

Instead, implementations SHALL report every detected conflict and require explicit user intervention.

One common resolution is to create a new Configuration representing the intended combined operational state.

Configurations containing unresolved conflicts SHALL be considered invalid for operational use.

---

# 1.10 Effective Installation

The Effective Installation represents the infrastructure visible to the user.

Conceptually:

```text
Effective Installation

=

Baseline Revision

+

Configuration Revision
```

If no Configuration is active, the Effective Installation is identical to the current Baseline.

The Effective Installation is considered valid only if:

* all inherited Configurations can be applied successfully;
* no unresolved conflicts remain;
* all required resources are available.

The Effective Installation is the authoritative source for:

* route tracing
* reports
* impact analysis
* setup documentation
* operational documentation

---

# 1.11 Single Source of Truth

Relatar maintains one authoritative description of every venue.

The Baseline describes the permanent installation.

Configurations describe alternative operational states.

Reports, diagrams, route sheets and impact analyses are derived from these relationships rather than maintained independently.

This ensures consistency while eliminating unnecessary duplication.

---

# 1.12 Physical Connections and Logical Assignments

Relatar distinguishes between **physical connections** and **logical assignments**.

A physical connection represents a tangible relationship between two connection points.

Examples include:

* XLR cable between two devices
* Fibre patch lead
* HDMI cable
* RJ45 network cable
* Permanent building cabling

A logical assignment represents a software-defined relationship required to make the system function.

Examples include:

* BLU Analog Input 1 assigned to Dante Transmit Channel 1
* Dante Receive Channel 12 assigned to GLD Channel 20
* Stage Box Socket 3 assigned to GLD Channel 20
* Button Panel 2 assigned to recall "Full Auto + Dante"
* Kramer Encoder assigned to Decoder 5

Logical assignments are not physical connections.

Instead, they describe how software-configurable systems are intended to use existing infrastructure.

Relatar MAY document logical assignments whenever they are operationally relevant.

Relatar SHOULD NOT attempt to model every internal processing block or proprietary implementation detail of specialist software.

The objective is to document the assignments that must be configured by a technician, not the complete internal operation of a device.

This distinction allows Relatar to remain vendor-independent while still documenting the software configuration necessary to reproduce an installation.

---

# 1.13 Planning and Implementation

Relatar is intended to support both existing and planned installations.

A planned installation may contain infrastructure that has not yet been built or configured.

From the documented relationships, Relatar MAY generate implementation documentation, including:

* Physical connection guides
* Cable schedules
* Patch panel schedules
* Equipment installation lists
* Software configuration guides
* Commissioning checklists
* Setup procedures
* Teardown procedures

Examples of generated software configuration tasks include:

* Assign BLU Analog Input 1 to Dante Transmit Channel 1.
* Assign Dante Receive Channel 12 to GLD Channel 20.
* Configure Kramer Encoder 2 to stream to Decoder 5.
* Recall the "Sunday Service" operating mode.
* Enable the "Full Auto + Dante" microphone configuration.

The purpose of these guides is to assist technicians in implementing the documented design.

Relatar generates implementation instructions from documented relationships.

It does not replace manufacturer-specific configuration software.

---

# 1.14 Intended Use

Relatar should enable users to answer questions such as:

* Where is this device normally located?
* Where is this device in the active Configuration?
* What changed compared to the Baseline?
* Which Configuration introduced this route?
* Which revision changed this setup?
* Which software assignments are required to commission this installation?
* What equipment is required for tomorrow's event?
* Which systems are affected if this cable fails?

The value of Relatar is measured by its ability to answer these questions accurately and consistently.

---
