# 2. Domain Model

**Relatar Specification 0.1 – Draft**

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

# 2.5 Baseline

The Baseline is the canonical description of a Venue.

It contains the permanent infrastructure.

Configurations inherit from the Baseline.

The Baseline SHALL always represent the current intended permanent installation.

---

# 2.6 Location

A Location represents a physical area within a Venue.

Examples include:

* Stage
* Balcony
* Technical Room
* FOH
* Basement
* Equipment Room

Locations MAY be hierarchical.

Objects SHALL exist within exactly one Location.

---

# 2.7 Container

A Container is an Object capable of containing other Objects.

Examples include:

* Equipment Rack
* Wall Cabinet
* Floor Box
* Equipment Case

Containers MAY contain other Containers.

Containers SHALL inherit all properties of an Object.

---

# 2.8 Object Type

An Object Type defines the reusable characteristics of a class of equipment.

Examples include:

* Allen & Heath GLD-80
* BSS BLU-806
* Kramer KDS-17DEC
* Shure ULXD4

An Object Type MAY define:

* manufacturer
* model
* capabilities
* default Connection Points
* default properties
* documentation

Object Types do not represent physical equipment.

---

# 2.9 Object

An Object represents a specific physical or logical instance.

Examples include:

* FOH Mixer
* DSP-1
* Camera 3
* AVK-2
* Stage Box M2

An Object MAY reference an Object Type.

An Object SHALL exist in exactly one Location or Container.

An Object MAY contain one or more Connection Points.

An Object MAY participate in Relationships.

---

# 2.10 Connection Point

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

---

# 2.11 Capabilities

Objects and Connection Points MAY define Capabilities.

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

# 2.12 Relationships

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

# 2.13 Architectural Principles

The Domain Model follows these principles:

* Every entity has a single responsibility.
* Objects interact only through Connection Points.
* Physical connections and logical assignments are distinct concepts.
* Relationships contain the knowledge of the system.
* Object Types describe equipment; Objects describe installations.
* Configurations extend the Baseline without modifying it.

These principles apply to every Relatar implementation.
