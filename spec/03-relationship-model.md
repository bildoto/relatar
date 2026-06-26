# 3. Relationship Model

**Relatar Specification 0.2 – Draft**

---

# 3.1 Purpose

This chapter defines how entities in Relatar relate to one another.

The Domain Model defines the entities that exist.

The Relationship Model defines how those entities interact.

Relationships are first-class data in Relatar.

A Relatar implementation SHALL preserve relationship meaning, direction and scope.

---

# 3.2 Relationship Overview

A Relationship describes a meaningful association between two entities.

Examples include:

* a Location contains a Container
* an Object contains a Connection Point
* a Connection Point is physically connected to another Connection Point
* a Connection Point is assigned to another Connection Point
* a Control activates a Configuration
* a Signal depends on a route

Relationships may describe physical structure, logical routing, control behaviour or dependency.

---

# 3.3 Relationship Direction

Every Relationship has a direction.

The direction defines how the relationship should be interpreted.

Example:

```text
Rack A
    contains
Mixer 1
```

This is not the same as:

```text
Mixer 1
    contains
Rack A
```

Implementations MAY provide inverse views for convenience, but the stored relationship SHALL retain its defined direction.

Example inverse views:

```text
Rack A contains Mixer 1
Mixer 1 is contained by Rack A
```

Both describe the same Relationship.

---

# 3.4 Relationship Scope

Relationships may exist in different scopes.

The required scopes are:

* Baseline
* Configuration
* Revision

A Baseline Relationship describes the permanent installation.

A Configuration Relationship describes a temporary or alternative relationship.

A Revision Relationship describes the relationship as it existed in a specific revision.

Implementations SHALL be able to determine which Relationships are active in an Effective Installation.

---

# 3.5 Relationship Types

Relatar defines several core relationship types.

Implementations MAY define additional relationship types, provided that the core semantics are preserved.

---

## contains

Describes containment.

Examples:

```text
Venue contains Location
Rack contains Mixer
Object contains Connection Point
```

Rules:

* `contains` is hierarchical.
* An entity MAY contain multiple entities.
* An entity SHOULD NOT contain itself directly or indirectly.
* Implementations SHALL prevent containment loops.

---

## located_in

Describes physical location.

Examples:

```text
Mixer located_in Technical Room
Camera located_in Balcony
```

Rules:

* Physical Objects SHALL have a location either directly or through a Container.
* Logical Objects MAY omit physical location.
* Location inheritance through Containers MAY be used.

---

## connected_to

Describes a physical connection between two Connection Points.

Examples:

```text
XLR Output 1 connected_to XLR Input 1
Patch Panel Port 12 connected_to Switch Port 17
Phoenix Output 1 connected_to XLR Patch Panel Port 1
```

Rules:

* `connected_to` SHALL link Connection Points.
* `connected_to` represents a physical or defined infrastructure connection.
* Connector types MAY differ if the cable or adapter supports the connection.
* Implementations MAY validate compatibility using Capabilities.
* `connected_to` SHOULD NOT be used for software-defined routing.

---

## assigned_to

Describes a logical or software-defined assignment.

Examples:

```text
Dante RX 12 assigned_to GLD Channel 20
AR2412 Socket 3 assigned_to GLD Channel 20
BLU Analog Input 1 assigned_to Dante TX 1
Button 3 assigned_to Preset Full Auto + Dante
```

Rules:

* `assigned_to` SHALL be used for software-defined mappings.
* `assigned_to` MAY represent one-to-one, one-to-many or many-to-one relationships.
* `assigned_to` SHALL NOT imply a physical cable.
* Implementation guides MAY be generated from `assigned_to` relationships.

---

## routes_to

Describes signal flow.

Examples:

```text
Pulpit Microphone routes_to BLU Automixer
Speech Bus routes_to Main PA
Camera routes_to Streaming Encoder
```

Rules:

* `routes_to` MAY describe physical, logical or combined signal movement.
* `routes_to` MAY pass through multiple Relationships.
* `routes_to` MAY branch to multiple destinations.
* `routes_to` SHOULD be used when the purpose is to describe signal behaviour rather than physical wiring.

---

## controls

Describes control influence.

Examples:

```text
Button Panel controls Microphone Mode
Companion Button controls Livestream Configuration
GPIO Input controls Mute State
```

Rules:

* `controls` describes influence, not signal flow.
* `controls` MAY affect Configurations, Modes, Routes or Objects.
* `controls` SHOULD describe operationally relevant behaviour.

---

## depends_on

Describes dependency.

Examples:

```text
Piano Signal depends_on Snake M2
Livestream depends_on Streaming Laptop
Main PA depends_on DSP-1
```

Rules:

* `depends_on` MAY be derived from other Relationships.
* `depends_on` MAY also be entered explicitly where dependency is not obvious.
* Impact reports MAY use `depends_on`.

---

# 3.6 Physical Connections vs Logical Assignments

Relatar SHALL distinguish between physical connections and logical assignments.

A physical connection is represented by `connected_to`.

A logical assignment is represented by `assigned_to`.

Example:

```text
Microphone
    connected_to
Stage Box Socket 3

Stage Box Socket 3
    assigned_to
GLD Channel 20
```

These Relationships describe different kinds of reality.

Implementations SHALL NOT treat them as interchangeable.

---

# 3.7 Relationship Metadata

Relationships MAY contain metadata.

Examples include:

* cable ID
* cable type
* length
* installation date
* installer
* confidence level
* notes
* source document
* configuration scope
* revision

Relationship metadata SHALL describe the Relationship, not the entities themselves.

Example:

The cable ID belongs to the `connected_to` Relationship.

The connector type belongs to the Connection Point.

---

# 3.8 Conflicting Relationships

Relationships may conflict when applied together.

Examples:

* two physical connections claim exclusive use of the same Connection Point
* two assignments map the same exclusive input differently
* one Relationship disables another required Relationship
* a Configuration moves an Object while another Relationship depends on its original location

Relatar SHALL detect unresolved conflicts before producing an Effective Installation.

Relatar SHALL NOT silently choose one conflicting Relationship over another.

Conflicts SHALL be reported to the user.

---

# 3.9 Derived Relationships

Some Relationships may be derived from other Relationships.

Example:

If:

```text
Piano connected_to Stage Box
Stage Box connected_to Snake
Snake connected_to Patch Panel
Patch Panel connected_to Mixer
```

then Relatar may derive:

```text
Piano depends_on Mixer path
```

Derived Relationships SHALL NOT replace source Relationships.

Implementations SHOULD distinguish between stored and derived Relationships.

---

# 3.10 Relationship Validity

A Relationship may be valid, invalid, planned or historical.

Suggested states include:

* planned
* active
* disabled
* historical
* unknown

Implementations SHALL be able to exclude inactive Relationships from the Effective Installation unless explicitly requested.

---

# 3.11 Relationship Principle

The central principle of Relatar is:

```text
Entities describe what exists.

Relationships describe what matters.
```

A Relatar implementation that stores entities without meaningful Relationships does not fulfil the purpose of the specification.
