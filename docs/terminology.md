# Relatar Terminology

This document defines the terminology used throughout Relatar.

The definitions in this document are authoritative.

---

## Object

An object is any identifiable entity that exists within the documented infrastructure.

Examples:

* Device
* Cabinet
* Patch panel
* Wall outlet
* Speaker
* Microphone
* Cable
* Room

Everything in Relatar is an object.

---

## Port

A port is a connection point belonging to an object.

Ports describe where physical or logical connections can be made.

Examples:

* XLR connector
* RJ45 socket
* HDMI connector
* Phoenix terminal
* Dante interface

---

## Connection

A connection links exactly two ports.

Connections describe the physical infrastructure.

Connections may contain metadata such as:

* cable type
* cable ID
* connector type
* length
* notes

---

## Signal

A signal represents information travelling through the infrastructure.

Signals are independent of the physical cables.

Examples:

* Audio
* Video
* Ethernet
* Serial control
* GPIO

---

## Route

A route describes the complete path taken by a signal.

Routes may contain multiple physical connections.

---

## Mode

A mode represents an operating state of the installation.

Different modes may enable or disable routes.

Examples:

* Automatic
* Manual
* Emergency
* Maintenance

---

## Control

A control changes the behaviour of the system.

Examples:

* Push button
* Touch panel
* Companion button
* GPIO input
* DSP preset
