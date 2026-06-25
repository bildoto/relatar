# Relatar Concept

## Vision

Relatar is an open-source technical infrastructure knowledge base.

Its purpose is to document technical systems in a way that allows people to understand how everything is physically and logically connected.

Rather than focusing on diagrams or inventory, Relatar focuses on relationships between objects. From these relationships it becomes possible to answer practical questions that arise during installation, maintenance and troubleshooting.

The goal is simple:

> **Know how everything is connected.**

---

# Why Relatar exists

Modern technical installations are increasingly complex.

A single signal may travel through multiple cabinets, patch panels, multicore cables, network switches, DSPs, digital transports and control systems before reaching its destination.

Traditional documentation is usually split across several independent sources:

* Rack elevations
* Cable schedules
* Patch panel schedules
* Signal flow diagrams
* DSP programming
* Network documentation
* Equipment inventories
* Printed drawings

Each document describes only part of the installation.

When troubleshooting, technicians often need to combine information from several different sources before they can answer a simple question such as:

* Where does this microphone end up?
* Which cable do I need?
* Which cabinet should I open?
* Which patch panel contains this connection?
* What happens if this cable fails?
* Which operating modes affect this signal?

Relatar exists to answer these questions from a single source of truth.

---

# Philosophy

Relatar is not primarily a drawing application.

Relatar is not an inventory application.

Relatar is not a network management system.

Relatar is a knowledge base built around relationships.

Everything inside Relatar is connected to something else.

Examples include:

* Devices contain ports.
* Ports are connected by cables.
* Cabinets contain equipment.
* Signals travel through routes.
* Modes enable or disable routes.
* Controls modify system behaviour.

The relationships themselves are the most valuable information.

---

# Scope

Relatar is designed to document technical infrastructure of any size.

Possible applications include:

* Professional audio systems
* Video distribution
* Computer networks
* Fibre infrastructure
* Building automation
* Security systems
* Access control
* KNX installations
* CCTV
* Industrial control systems
* Hybrid installations combining several technologies

The underlying concepts remain identical regardless of technology.

---

# Core principles

## One source of truth

Information should exist only once.

Reports, diagrams and documentation should be generated from the stored relationships instead of requiring duplicate data entry.

## Physical first

The physical installation forms the foundation.

Devices, ports, connectors and cables describe reality.

Logical signal routing is built on top of the physical infrastructure.

## Relationships over diagrams

Diagrams are useful.

Relationships are essential.

A diagram represents one view of the system.

Relationships describe the system itself.

## Printable documentation

Relatar should always be capable of generating technician-friendly documentation suitable for printing.

Paper documentation remains valuable during installation, maintenance and troubleshooting.

---

# Questions Relatar should answer

Relatar should be able to answer questions such as:

* Where is this device located?
* Which cabinet contains it?
* Which connectors does it have?
* Which cables are connected?
* What is connected to this port?
* Where does this signal travel?
* Which devices depend on this cable?
* Which operating modes affect this signal?
* Which control panel changes this routing?
* Which connector or adapter is required?

If Relatar can answer these questions reliably, it has achieved its purpose.

---

# Future vision

Relatar should grow without becoming tied to any specific technology.

Audio, networking, automation and control systems should all be represented using the same underlying relationship model.

The objective is not to model every possible protocol.

The objective is to describe how real technical systems are interconnected so that they can be understood, maintained and expanded over time.
