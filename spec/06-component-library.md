# 6. Component Library

**Relatar Specification 0.2 – Draft**

---

# 6.1 Purpose

The Component Library defines reusable engineering Components.

Components describe the characteristics of equipment and infrastructure independently of any specific installation.

Objects placed within a Venue reference Components rather than redefining their characteristics.

The Component Library promotes consistency, reduces duplication and simplifies documentation.

---

# 6.2 Components

A Component represents a reusable engineering definition.

Components SHALL NOT represent physical equipment installed within a Venue.

Instead, they describe the properties shared by every instance of that Component.

Examples include:

* Allen & Heath GLD-80
* BSS BLU-806
* Kramer KDS-17DEC
* 24-Port XLR Patch Panel
* 42U Equipment Rack
* Duplex LC Fibre Outlet
* RJ45 Wall Outlet

---

# 6.3 Objects

An Object represents a specific instance of a Component.

Example:

```text
Component

Allen & Heath GLD-80

↓

Objects

FOH Mixer
Training Mixer
Backup Mixer
```

Each Object maintains its own identity, location and operational state.

Objects inherit their default characteristics from the referenced Component.

---

# 6.4 Component Definition

A Component MAY define:

* Manufacturer
* Model
* Category
* Description
* Connection Points
* Capabilities
* Default Properties
* Validation Rules
* Documentation
* Images
* Notes

Implementations MAY extend Components with additional metadata.

---

# 6.5 Connection Point Definitions

Components MAY define reusable Connection Points.

Examples:

```text
BSS BLU-806

12 Analog Inputs
8 Analog Outputs
64 Dante Transmit Channels
64 Dante Receive Channels
GPIO
Ethernet
```

```text
Allen & Heath GLD-80

Mic Inputs
Line Outputs
AES
Dante
GPIO
Word Clock
```

Objects inherit these Connection Points from their Component.

Implementations MAY allow individual Objects to add, disable or extend Connection Points where operationally required.

---

# 6.6 Capabilities

Components define the capabilities of the equipment they represent.

Examples include:

* Audio Input
* Audio Output
* Video Input
* Video Output
* Ethernet
* Fibre
* GPIO
* Relay
* DSP
* Mixing
* Encoding
* Decoding

Capabilities describe what a Component is capable of rather than how an Object is currently configured.

---

# 6.7 Properties

Components MAY define default properties.

Examples include:

* Maximum channel count
* Supported transport technologies
* Physical dimensions
* Rack units
* Power requirements
* Cooling requirements
* Weight

Objects MAY define additional instance-specific properties.

---

# 6.8 Validation Rules

Components MAY define validation rules.

Examples include:

* Maximum Dante flows
* Maximum analogue inputs
* Supported connector types
* Maximum power consumption
* Channel limits

Validation rules are advisory.

Implementations MAY use them to identify design issues and configuration errors.

Component validation rules define possible constraints.

Implementations evaluate those constraints against specific Objects and Relationships.

---

# 6.9 Documentation

Components MAY reference supporting documentation.

Examples include:

* Datasheets
* User manuals
* Wiring diagrams
* Programming guides
* Manufacturer documentation

Relatar SHOULD reference external documentation rather than duplicate it.

---

# 6.10 Custom Components

Implementations SHALL allow users to create custom Components.

Custom Components SHALL behave identically to built-in Components.

This enables organisations to model proprietary equipment, custom-built devices and locally defined infrastructure.

## Generic Components

* Generic 24-port patch panel
* Generic 8-channel snake
* Generic HDMI display
* Generic network switch

---

# 6.11 Library Sharing

Component Libraries SHOULD be portable.

Implementations SHOULD support importing and exporting Components independently of any Venue.

Shared Component Libraries encourage reuse and consistent documentation across organisations.

---

# 6.12 Versioning

Components MAY evolve over time.

Implementations SHOULD preserve compatibility between updated Components and existing Objects.

Changes to a Component SHOULD NOT silently invalidate existing installations.

Objects SHOULD retain a reference to the version of the Component from which they were instantiated.

Implementations MAY provide mechanisms for migrating Objects to newer Component versions.

Such migrations SHALL require explicit user action.

---

# 6.13 Architectural Principles

The Component Library follows these principles:

* Components describe engineering definitions.
* Objects represent installed instances.
* Components are reusable.
* Objects inherit from Components.
* Connection Point definitions belong to Components.
* Capabilities describe possibility rather than configuration.
* Component Libraries are intended to be shared between organisations.
