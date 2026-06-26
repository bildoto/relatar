# 6. Object Library

**Relatar Specification 0.1 – Draft**

---

# 6.1 Purpose

The Object Library defines reusable Object Types.

Object Types describe the characteristics of equipment and infrastructure independently of any specific installation.

Objects placed within a Venue reference Object Types rather than redefining their properties.

The Object Library promotes consistency, reduces duplication and simplifies documentation.

---

# 6.2 Object Types

An Object Type represents a reusable engineering template.

Object Types SHALL NOT represent physical equipment.

Instead, they describe the characteristics shared by all instances of that type.

Examples include:

* Allen & Heath GLD-80
* BSS BLU-806
* Kramer KDS-17DEC
* 24-Port XLR Patch Panel
* 42U Equipment Rack
* Duplex LC Fibre Outlet
* RJ45 Wall Outlet

---

# 6.3 Object Instances

An Object represents one instance of an Object Type.

Example:

```text
Object Type

Allen & Heath GLD-80

↓

Objects

FOH Mixer

Training Mixer

Backup Mixer
```

Each Object maintains its own identity, location and operational state.

---

# 6.4 Library Contents

An Object Type MAY define:

* Manufacturer
* Model
* Category
* Description
* Default Connection Points
* Capabilities
* Default Properties
* Validation Rules
* Documentation
* Images
* Notes

Implementations MAY extend Object Types with additional metadata.

---

# 6.5 Connection Point Templates

Object Types MAY define reusable Connection Point templates.

Examples:

```text
BLU-806

12 Analog Inputs
8 Analog Outputs
64 Dante Transmit Channels
64 Dante Receive Channels
GPIO
Ethernet
```

```text
GLD-80

Mic Inputs
Line Outputs
AES
Dante
GPIO
Word Clock
```

Object instances inherit these Connection Points from their Object Type.

Implementations MAY allow individual instances to add or disable Connection Points where operationally required.

---

# 6.6 Capabilities

Object Types define the capabilities of the equipment they represent.

Examples include:

* Audio Input
* Audio Output
* Video Input
* Video Output
* Ethernet
* Fibre
* GPIO
* Relay
* Power Distribution
* DSP
* Mixing
* Encoding
* Decoding

Capabilities describe what an Object is capable of rather than how it is currently configured.

---

# 6.7 Properties

Object Types MAY define default properties.

Examples include:

* Maximum channel count
* Supported transport technologies
* Physical dimensions
* Rack units
* Power requirements
* Cooling requirements
* Weight

Object instances MAY override instance-specific properties where appropriate.

---

# 6.8 Validation Rules

Object Types MAY define validation rules.

Examples include:

* Maximum Dante flows
* Maximum analogue inputs
* Supported connector types
* Maximum power consumption
* Channel limits

Validation rules are advisory.

Implementations MAY use them to identify design issues and configuration errors.

---

# 6.9 Documentation

Object Types MAY reference supporting documentation.

Examples include:

* Datasheets
* User manuals
* Wiring diagrams
* Programming guides
* Manufacturer documentation

Relatar SHOULD reference external documentation rather than duplicate it.

---

# 6.10 Custom Object Types

Implementations SHALL allow users to create custom Object Types.

Custom Object Types SHALL behave identically to built-in Object Types.

This enables organisations to model proprietary equipment, custom-built devices and locally defined infrastructure.

---

# 6.11 Library Sharing

Object Libraries SHOULD be portable.

Implementations SHOULD support exporting and importing Object Types independently of a Venue.

Shared libraries encourage reuse and consistent documentation across organisations.

---

# 6.12 Versioning

Object Types MAY evolve over time.

Implementations SHOULD preserve compatibility between Object Types and existing Object instances.

Changes to an Object Type SHOULD NOT silently invalidate existing installations.

---

# 6.13 Architectural Principles

The Object Library follows these principles:

* Object Types describe equipment; Objects describe installations.
* Object Types are reusable.
* Object instances remain independent after creation.
* Connection Point definitions belong to the Object Type.
* Capabilities describe possibility, not configuration.
* Object Libraries are intended to be shared between organisations.

```
```
