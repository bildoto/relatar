# 2. Domain Model

**Relatar Specification 0.2 – Draft**

---

# 2.1 Purpose

This chapter defines the conceptual entities that make up a Relatar installation.

The Domain Model is implementation-independent.

It defines *what* exists within Relatar rather than *how* it is implemented.

Database schemas, APIs and user interfaces are implementations of this model.

---

# 2.2 Overview

Relatar models infrastructure using a hierarchy of entities.

```text
Organisation
    ↓
Venue
    ↓
Baseline
    ↓
Location
    ↓
Container
    ↓
Object
        ↓
Connection Point

Component
        ▲
        │
Object
```

Relationships connect these entities into a complete representation of the installation.

Configurations extend the Baseline without modifying it.

---

# 2.3 Organisation

An Organisation represents the owner or operator of one or more Venues.

Examples include:

* Church
* Municipality
* Theatre Company
* University
* Broadcast Company

An Organisation owns one or more Venues.

---

# 2.4 Venue

A Venue represents one physical installation.

Examples include:

* Temple
* Parish Hall
* Conference Centre
* Office Building

Every Venue SHALL contain exactly one Baseline.

A Venue MAY contain multiple Configurations.

---

# 2.5 Venue Access

Access to a Venue MAY be restricted to specific users or groups.

Implementations SHALL ensure that users can only access Venues for which they have permission.

Venue access restrictions SHALL apply to:

* Baselines
* Configurations
* Objects
* Connection Points
* Relationships
* Routes
* Reports
* Search results
* Trace results

Search and Trace operations SHALL NOT reveal entities from Venues outside the user's permitted access.

Implementations MAY support role-based permissions within a Venue.

Examples include:

* Viewer
* Editor
* Administrator

Venue access control is implementation-specific, but the visibility rules SHALL be enforced consistently across the system.

---

# 2.6 Baseline

The Baseline is the canonical description of a Venue.

It contains the permanent infrastructure.

Configurations inherit from the Baseline.

The Baseline SHALL always represent the current intended permanent installation.

---

# 2.7 Location

A Location represents a physical area within a Venue.

Examples include:

* Stage
* Balcony
* Technical Room
* FOH
* Basement
* Equipment Room

Locations MAY be hierarchical.

Objects SHALL have exactly one effective Location.

An Object MAY be located directly in a Location or indirectly through a Container.

If an Object is contained by a Container, its effective Location is inherited from that Container unless explicitly overridden by a Configuration.

---

# 2.8 Container

A Container is an Object capable of containing other Objects.

Examples include:

* Equipment Rack
* Wall Cabinet
* Floor Box
* Equipment Case

Containers MAY contain other Containers.

Containers SHALL inherit all properties of an Object.

---

# 2.9 Component

A Component defines the reusable characteristics of a class of equipment.

Examples include:

* Allen & Heath GLD-80
* BSS BLU-806
* Kramer KDS-17DEC
* Shure ULXD4

A Component MAY define:

* manufacturer
* model
* capabilities
* default Connection Points
* default properties
* documentation

Components do not represent physical equipment.

---

# 2.10 Object

An Object represents a specific physical or logical instance.

Examples include:

* FOH Mixer
* DSP-1
* Camera 3
* AVK-2
* Stage Box M2
* Cable

An Object MAY reference a Component.

An Object SHALL exist directly in either one Location or one Container.

An Object SHALL have exactly one effective Location after containment and Configuration overlays are resolved.

An Object MAY contain one or more Connection Points.

An Object MAY participate in Relationships.

---

# 2.11 Connection Point

A Connection Point is an addressable interface through which signals, power, data or control information may enter, leave or be assigned.

Every Connection Point belongs to exactly one Object.

Connection Points may represent physical connectors, logical interfaces or software-defined endpoints.

Examples include:

Physical:

* XLR Connector
* Phoenix Terminal
* RJ45 Connector
* HDMI Connector
* Fibre Connector

Logical:

* Dante Transmit Channel
* Dante Receive Channel
* Mixer Input Channel
* Mixer Output Bus
* DSP Matrix Input
* GPIO Input
* Relay Output

Connection Points are connected, assigned and controlled through Relationships.

Objects SHALL NOT connect directly to one another.

When an Object references a Component, the Connection Point definitions provided by that Component become Object-specific Connection Points for that Object.

Relationships SHALL reference Object-specific Connection Points, not the Component definitions directly.

---

# 2.12 Capabilities

Components MAY define default Capabilities.

Objects and Connection Points MAY inherit, extend or override those Capabilities where operationally required.

Capabilities describe what an entity is capable of rather than how it is currently used.

Examples include:

* Receive Audio
* Transmit Audio
* Receive Video
* Transmit Video
* Ethernet
* GPIO Input
* GPIO Output
* Relay
* Power Distribution

Capabilities may be used to validate Relationships and assist planning.

---

# 2.13 Relationships

Relationships define how entities interact.

Examples include:

* contains
* located_in
* connected_to
* assigned_to
* routes_to
* controls
* depends_on

Relationships are defined in the Relationship Model.

---

# 2.14 Identity

Every entity within Relatar SHALL possess a stable identity.

An entity's identity SHALL remain unchanged throughout its lifetime, regardless of changes to its attributes or relationships.

Examples of attributes that MAY change include:

* Name
* Description
* Location
* Properties
* Relationships

These changes SHALL NOT affect the identity of the entity.

For Objects, the referenced Component is considered part of the Object's technical identity.

Changing an Object's Component SHOULD be treated as replacing the Object with a new Object rather than modifying the existing Object.

The previous Object MAY be retained as historical data.

Stable identities enable Relatar to:

* preserve revision history;
* compare Configurations and Baselines;
* track Objects across relocations;
* identify changes over time;
* maintain reliable references between entities.

Implementations SHALL ensure that an entity's identity remains unique within its scope and is never reused for a different entity.
---

# 2.15 Architectural Principles

The Domain Model follows these principles:

* Every entity has a single responsibility.
* Objects interact only through Connection Points.
* Physical connections and logical assignments are distinct concepts.
* Relationships contain the knowledge of the system.
* Components describe engineering definitions; Objects describe installed instances.
* Configurations extend the Baseline without modifying it.

These principles apply to every Relatar implementation.
