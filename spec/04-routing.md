# 4. Routing Model

**Relatar Specification 0.1 – Draft**

---

# 4.1 Purpose

This chapter defines how Relatar models the movement of signals through technical infrastructure.

The Routing Model describes *what* a signal is intended to do rather than *how* a specific device processes it.

Relatar documents the observable path of a signal through an installation.

It does not attempt to model proprietary internal processing performed by specialist equipment.

---

# 4.2 Route

A Route represents a named signal path through the installation.

Routes are first-class entities within Relatar.

Examples include:

* Main Speech
* Piano
* Livestream Audio
* Recording Feed
* Hearing Loop
* Overflow Room
* Confidence Monitors

A Route describes the intended movement of one or more signals from one or more Sources to one or more Destinations.

A Route represents **engineering intent** rather than merely the physical implementation.

The physical infrastructure, logical assignments and transport technologies together implement the Route.

---

# 4.3 Route Properties

A Route MAY define additional descriptive properties.

Typical properties include:

* Signal Type (Audio, Video, Control, Data, Power)
* Channel Count (Mono, Stereo, Multi-channel)
* Direction
* Priority
* Redundancy
* Required Latency
* Transport Requirements
* Operational Notes

These properties describe the intended behaviour of the Route rather than the implementation details.

Future versions of Relatar MAY extend the set of supported Route properties without changing the underlying Routing Model.

---

# 4.4 Route Components

A Route may consist of:

* Sources
* Physical Connections
* Logical Assignments
* Transport Technologies
* Destinations

Example:

```text
Piano
    ↓
Stage Box M2-3
    ↓
Snake
    ↓
Patch Panel
    ↓
BLU Analog Input 5
    ↓
BLU Analog Input 5 assigned_to Dante TX 17
    ↓
Dante RX 17 assigned_to GLD Channel 20
    ↓
Main PA
```

Every stage of the Route SHALL be traceable.

---

# 4.5 Sources

A Route begins with one or more Sources.

Examples include:

* Microphone
* Piano
* Playback Computer
* Camera
* Media Player

A Route MAY contain multiple Sources.

---

# 4.6 Destinations

A Route ends at one or more Destinations.

Examples include:

* Main Loudspeakers
* Livestream
* Recording
* Hearing Loop
* Overflow Room

Routes MAY branch to multiple Destinations.

---

# 4.7 Branching

Routes are not required to be linear.

A Route MAY split into multiple independent branches.

Example:

```text
Speech
    ↓
Automixer
    ├── Main PA
    ├── Livestream
    ├── Recording
    └── Hearing Loop
```

Each branch SHALL remain traceable.

---

# 4.8 Physical Connectivity

Physical connectivity is described using `connected_to` relationships.

Examples include:

* Cables
* Patch Panels
* Permanent Building Cabling
* Stage Boxes

Physical connectivity describes how signals are capable of travelling.

---

# 4.9 Logical Assignments

Logical Assignments describe software-defined routing required to realise a Route.

Examples include:

* BLU Analog Input → Dante TX
* Dante RX → GLD Channel
* Stage Box Socket → Mixer Channel
* Encoder → Decoder

Logical Assignments are represented using `assigned_to` relationships.

Assignments are considered part of a Route.

---

# 4.10 Transport Technologies

A Route MAY traverse one or more transport technologies.

Examples include:

* Analogue Audio
* AES3
* Dante
* BLU-link
* HDMI
* HDBaseT
* Fibre
* Ethernet

Transport technologies describe how a signal moves between Connection Points.

Relatar SHALL treat transport technologies as implementation details of a Route rather than separate Route types.

---

# 4.11 Internal Processing

Signals frequently pass through equipment performing processing such as:

* Gain
* Equalisation
* Compression
* Delay
* Mixing

Relatar SHALL NOT attempt to model proprietary internal processing unless it is operationally significant.

Instead, Relatar documents the externally observable routing and logical assignments required to reproduce the installation.

---

# 4.12 Route Validation

Implementations MAY validate Routes.

Examples include:

* Missing physical connections
* Missing logical assignments
* Incompatible Connection Point capabilities
* Broken Routes
* Circular Routes
* Orphaned Sources
* Unreachable Destinations

Validation SHALL report detected issues without modifying the documented design.

---

# 4.13 Route Trace

Relatar SHALL be capable of tracing a Route from any point.

Example queries include:

* Where does this microphone connect?
* Which loudspeakers receive this signal?
* Which software assignments are required?
* Which Configurations modify this Route?
* Which devices are involved in this Route?

Route traces MAY include both physical and logical relationships.

---

# 4.14 Route Documentation

Implementations MAY generate Route documentation.

Examples include:

* Signal Flow Report
* Route Sheet
* Commissioning Guide
* Programming Guide
* Fault Finding Guide

Documentation SHALL be generated from stored Relationships.

Implementations SHALL NOT require Route documentation to be maintained manually.

---

# 4.15 Architectural Principles

The Routing Model follows these principles:

* Routes describe engineering intent rather than implementation.
* Physical Connections and Logical Assignments are equally important.
* Internal proprietary processing is outside the scope of Relatar.
* Every Route SHALL be traceable.
* Every Route SHALL be reproducible from documented Relationships.
* Routes MAY differ between Configurations without modifying the Baseline.
* Route properties describe intended behaviour rather than implementation details.
