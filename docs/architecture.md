# Relatar Architecture

Relatar is built around one central idea:

> Technical infrastructure can be described as objects connected by relationships.

The architecture is divided into layers. Each layer adds meaning without replacing the layer below it.

---

# 1. Architecture overview

Relatar models infrastructure in four main layers:

```text
Physical Layer
  Locations, containers, objects, ports, cables and physical connections

Signal Layer
  Signals, routes, splits, processing and destinations

State Layer
  Modes, presets and operating states

Control Layer
  Buttons, panels, automation and actions that change state or routing
```

The physical layer is the foundation. Everything else depends on it.

---

# 2. Physical layer

The physical layer describes what exists in the real installation.

It answers questions such as:

* Where is this device?
* Which cabinet contains it?
* Which port is connected?
* What connector type is used?
* Which cable links these two points?

## Core structure

```text
Location
  contains
Container
  contains
Object
  contains
Port

Port
  connected to
Port
```

## Example

```text
Tekniikkakoppi
  contains
LK AVK-2
  contains
BLU-806DA
  contains
Analog Output 1

Analog Output 1
  connected to
XLR Patch Panel Port 1
```

## Locations

A location is a physical place.

Examples:

* Tekniikkakoppi
* Stage
* Balcony
* Booth
* AVK-4 location

Locations may be hierarchical.

Example:

```text
Building
  Hall
    Stage
  Technical room
```

## Containers

A container is a physical object that contains other objects.

Examples:

* Cabinet
* Rack
* Wall box
* Patch enclosure
* Equipment case

A container may itself be inside another container.

Example:

```text
Tekniikkakoppi
  LK AVK-2
    Rack shelf
      BLU-806DA
```

## Objects

An object is any identifiable technical item.

Examples:

* Mixer
* DSP
* Patch panel
* Network switch
* Wall outlet
* Microphone
* Speaker
* Kramer encoder
* Cable accessory
* Snake breakout

Objects may have ports.

## Ports

A port is a connection point on an object.

A port should describe the actual point where a cable, adapter or internal connection can attach.

Examples:

* XLR input 1
* RJ45 port 17
* Phoenix output 1
* HDMI output
* Dante primary
* BLU-Link port A
* Multicore channel 3

Ports have metadata such as:

* connector type
* gender
* signal type
* direction
* label
* notes

## Connections

A connection links two ports.

A connection represents a physical or defined logical link between two connection points.

Examples:

```text
Patch Panel Port 1 -> Switch Port 17
BLU Output 1 -> XLR Patch Panel Port 1
Stage Box M2-3 -> Snake M2 Channel 3
```

Connections may have:

* cable ID
* cable type
* length
* installed route
* connector details
* notes

A connection always links two ports, even if the real-world cable is part of a larger multicore.

---

# 3. Cable and multicore architecture

Relatar must support both simple cables and grouped cables.

## Simple cable

A simple cable connects one port to one port.

Example:

```text
GLD Output 1 -> Amplifier Input 1
```

## Multicore / snake

A multicore is a grouped cable containing several channels or pairs.

Example:

```text
Snake M2
  Channel 1
  Channel 2
  Channel 3
  ...
```

Each channel can be traced individually, but the group can also be documented as one physical object.

This allows reports such as:

```text
Piano uses Snake M2 Channel 3
Snake M2 failure affects Piano, Guitar and Cajon
```

## Cable accessories

Cable accessories are objects that convert or expose connections.

Examples:

* Snake break-in
* Snake break-out
* DB25 to XLR loom
* Phoenix to XLR adapter
* Patch bay
* Terminal block

Cable accessories should be modelled as objects with ports.

---

# 4. Signal layer

The signal layer describes what travels through the physical infrastructure.

A signal is not the same as a cable.

A cable describes physical reality.

A signal describes function.

Examples of signals:

* Piano audio
* Pulpit microphone 1
* PC audio
* Main video
* Dante stream
* Control GPIO
* Projector HDMI
* Emergency microphone

## Signal route

A signal route describes how a signal moves through the system.

A route may follow physical connections, logical routing, processing blocks or transport systems.

Example:

```text
Pulpit Mic 1
  -> BLU-806DA Analog Input A1
  -> Automixer
  -> Speech Bus
  -> Main PA
```

Another route for the same source may exist in another mode:

```text
Pulpit Mic 1
  -> Dante
  -> GLD-80
  -> Manual mix
```

## Splits

One source may feed many destinations.

Example:

```text
Speech Bus
  -> Main PA
  -> Stream mix
  -> Hearing loop
  -> Recording
```

Relatar must allow one signal to branch into multiple routes.

## Processing

Some route steps are not cables.

Examples:

* DSP automixer
* Matrix switch
* Mixer channel
* Dante subscription
* Gain stage
* Preset-controlled router

These should be modelled as route steps or logical objects, depending on how detailed the installation needs to be.

---

# 5. State layer

The state layer describes operating modes.

Many systems do not have one fixed signal path. Routes may change depending on mode.

Examples:

* Full auto
* Manual
* Full auto + Dante
* Presentation
* Streaming
* Emergency
* Maintenance

## Mode

A mode represents a named operating state.

A mode may enable, disable or modify routes.

Example:

```text
Mode: Full auto
Enabled:
  Microphones -> BLU automixer -> PA

Disabled:
  Microphones -> GLD manual mix
```

Example:

```text
Mode: Manual
Enabled:
  Microphones -> Dante -> GLD

Disabled:
  BLU automixer as primary route
```

Example:

```text
Mode: Full auto + Dante
Enabled:
  Microphones -> BLU automixer -> PA
  Microphones -> Dante -> GLD

Note:
  This mode is available only through a separate control, not through the default Auto/Manual button.
```

## Route variants

The same source may have several route variants.

Example:

```text
Source: Pulpit Mic 1

Variant: Full auto
Variant: Manual
Variant: Full auto + Dante
```

Reports should be able to show either:

* all possible routes
* routes active in a selected mode
* differences between modes

---

# 6. Control layer

The control layer documents how system behaviour is changed.

Controls do not usually carry the main signal. They affect routing, mode, state or processing.

Examples:

* Button panel
* Touch panel
* Companion button
* GPIO input
* DSP preset
* Kramer control command
* Home Assistant automation
* Manual switch

## Control action

A control action describes what a control does.

Examples:

```text
Button: Auto/Manual
Action:
  Toggles microphone system between Full auto and Manual
```

```text
Button: Auto + Dante
Action:
  Enables Full auto mode while also feeding microphones to Dante
```

```text
Emergency microphone contact
Action:
  Forces emergency route to PA
```

Controls may:

* activate a mode
* enable a route
* disable a route
* recall a preset
* mute or unmute a signal
* change a destination
* override normal behaviour

---

# 7. Reports and derived views

Relatar should store relationships, not finished reports.

Reports are generated from the stored data.

Important report types include:

## Object report

Shows one object and its relationships.

Example:

```text
BLU-806DA
Location: Tekniikkakoppi
Container: LK AVK-2

Ports:
  Input A1 -> Pulpit Mic 1
  Output 1 -> XLR Patch Panel Port 1
```

## Route report

Shows the path of a source or signal.

Example:

```text
Piano

Stage socket M2-3
  XLR-F

Snake M2 Channel 3

AVK-4 RKT-2 Port 3
  RJ45

Backbone C017

AVK-2 RKT-1 Port 3
  RJ45

AR2412 Input 12
  XLR-F

GLD Channel 12
```

## Mode report

Shows what is active in a mode.

Example:

```text
Mode: Full auto

Active routes:
  Pulpit microphones -> BLU automixer -> PA

Inactive routes:
  Pulpit microphones -> GLD manual mix

Controls:
  Auto/Manual button
```

## Impact report

Shows what is affected by an object, cable or port.

Example:

```text
Failure: Snake M2

Affected:
  Piano
  Guitar 1
  Guitar 2
  Cajon

Not affected:
  Wireless microphones
  Pulpit microphones
```

## Print-first output

Reports should be suitable for paper use.

Fault-finding often happens in places where a phone or laptop is inconvenient.

Printable route sheets are a core part of Relatar, not an afterthought.

---

# 8. Diagrams

Relatar may generate diagrams in the future, but diagrams are not the primary data source.

The database stores relationships.

A diagram is only one possible view of those relationships.

This prevents the system from becoming dependent on manually maintained drawings.

---

# 9. Design boundaries

Relatar should document infrastructure and relationships.

Relatar should not try to replace specialist tools.

Examples:

* It should not replace Dante Controller.
* It should not replace DSP programming software.
* It should not replace CAD drawings.
* It should not replace network monitoring.
* It should not replace configuration backups.

Instead, Relatar should document how these systems relate to each other.

---

# 10. Architectural rule

The main rule of Relatar is:

```text
Store facts once.
Generate answers from relationships.
```

If information must be entered in two places to stay correct, the architecture should be reconsidered.
