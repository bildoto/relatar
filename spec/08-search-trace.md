# 8. Search & Trace

**Relatar Specification 0.2 – Draft**

---

# 8.1 Purpose

The Search & Trace Model defines how users retrieve and explore information stored within Relatar.

Search identifies entities.

Trace follows relationships between entities.

Together they enable users to understand complex technical infrastructure without requiring prior knowledge of its implementation.

Search and Trace SHALL operate on the Effective Installation unless another scope is explicitly requested.

---

# 8.2 Search

Search locates entities matching specified criteria.

Implementations SHOULD support searching by any indexed property.

Examples include:

* Name
* Identifier
* Description
* Manufacturer
* Component
* Location
* Category
* Route
* Configuration

Search results MAY include:

* Organisations
* Venues
* Locations
* Containers
* Components
* Objects
* Connection Points
* Routes
* Relationships
* Configurations

Implementations SHOULD rank exact matches above partial matches.

---

# 8.3 Trace

Trace follows Relationships between entities.

Tracing SHALL preserve relationship meaning and direction.

Examples include:

* Trace upstream
* Trace downstream
* Trace dependencies
* Trace containment
* Trace assignments
* Trace routes

Tracing MAY traverse both physical and logical Relationships.

---

# 8.4 Traversal

Traversal defines how Relatar explores the relationship graph.

Common traversal modes include:

## Upstream

Trace towards Sources.

Example:

```text
Main Loudspeaker
    ↑
Amplifier
    ↑
DSP
    ↑
Microphone
```

---

## Downstream

Trace towards Destinations.

Example:

```text
Microphone
    ↓
DSP
    ↓
Amplifier
    ↓
Main Loudspeaker
```

---

## Neighbour

Return directly related entities.

Example:

```text
DSP

↓

Analogue Inputs
Dante
GPIO
Amplifiers
```

---

## Containment

Traverse physical hierarchy.

Example:

```text
Venue

↓

Technical Room

↓

Rack

↓

DSP
```

---

## Dependency

Traverse operational dependencies.

Example:

```text
Livestream

↓

Encoder

↓

Network

↓

Switch

↓

UPS
```

---

# 8.5 Compare

Implementations MAY compare two documented states.

Typical comparisons include:

* Baseline vs Configuration
* Configuration vs Configuration
* Revision vs Revision

Comparison results SHOULD identify:

* Added entities
* Removed entities
* Modified entities
* Added Relationships
* Removed Relationships
* Changed Routes

---

# 8.6 Impact Analysis

Implementations MAY determine the impact of a proposed change.

Example queries include:

* What Routes use this Object?
* What fails if this cable is disconnected?
* Which Configurations depend on this Component?
* Which systems depend on this UPS?
* What is affected if this Route is disabled?

Impact analysis SHOULD use documented Relationships and derived dependencies.

---

# 8.7 Exploration

Exploration supports interactive navigation through documented infrastructure.

Users SHOULD be able to move naturally between related entities.

Example workflow:

```text
Microphone

↓

Route

↓

DSP

↓

Amplifier

↓

Main Loudspeaker
```

Implementations SHOULD minimise the number of interactions required to move between related entities.

---

# 8.8 Search Scope

Search and Trace MAY operate within different scopes.

Supported scopes include:

* Entire Organisation
* Venue
* Baseline
* Configuration
* Route
* Location
* Container

Implementations SHOULD clearly indicate the active search scope.

Search and Trace results SHALL respect Venue access restrictions.

---

# 8.9 Search Results

Search results SHOULD provide sufficient context for users to identify the correct entity.

Typical contextual information includes:

* Entity type
* Name
* Location
* Component
* Configuration
* Parent entity

Implementations MAY group results by entity type.

---

# 8.10 Trace Results

Trace results SHALL preserve the documented Relationships used to reach each entity.

Trace output SHOULD distinguish between:

* Physical Connections
* Logical Assignments
* Control Relationships
* Dependencies
* Derived Relationships

Implementations MAY provide graphical or textual trace representations.

---

# 8.11 Architectural Principles

The Search & Trace Model follows these principles:

* Search locates entities.
* Trace follows Relationships.
* Traversal preserves relationship meaning.
* Search operates across the entire documented model.
* Trace SHALL remain deterministic and reproducible.
* Exploration SHOULD minimise user effort.
* Impact analysis is derived from documented Relationships.
