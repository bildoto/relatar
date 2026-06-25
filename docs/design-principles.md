# Relatar Design Principles

The following principles define the philosophy of Relatar.

Every architectural decision, database change and new feature should be evaluated against these principles.

If a proposed change violates one of these principles, the design should be reconsidered before implementation.

---

# 1. Relationships are the primary data

Relatar is not an inventory system.

Relatar is not a drawing application.

Relatar is a knowledge base built around relationships.

Devices are important.

Cables are important.

Ports are important.

But the relationships between them are what create understanding.

Without relationships there is only a collection of isolated objects.

---

# 2. Reality comes first

Relatar should describe the installation as it actually exists.

The database should represent reality, not assumptions.

If a cable exists, it should exist in Relatar.

If a patch panel has forty-eight ports, Relatar should know about forty-eight ports.

Documentation should never simplify reality merely because it is easier to implement.

---

# 3. Physical before logical

Everything begins with the physical installation.

Physical infrastructure is the foundation upon which all higher-level concepts are built.

```text
Physical
    ↓
Signals
    ↓
Modes
    ↓
Control
```

If the physical layer is incorrect, every layer above it becomes unreliable.

---

# 4. One source of truth

Every fact should exist only once.

Duplicate information eventually becomes inconsistent.

Instead of storing the same information multiple times, Relatar should derive answers from relationships.

The database should contain facts.

Reports should contain interpretations of those facts.

---

# 5. Everything should be traceable

Any object should be traceable through its relationships.

Examples include:

* Follow a microphone to every destination.
* Find every object inside a cabinet.
* Discover every device affected by a failed cable.
* Determine which operating modes affect a signal.

If something cannot be traced, its relationships are probably incomplete.

---

# 6. Reports are generated, never maintained

Users should maintain data.

Relatar should maintain reports.

Cable schedules, route sheets, cabinet documentation and impact analyses should all be generated automatically from the stored relationships.

A report should never become another source of truth.

---

# 7. Documentation should answer questions

Documentation exists to solve real problems.

Relatar should make it easy to answer questions such as:

* Where does this signal go?
* Which cable do I need?
* Which cabinet should I open?
* Which connector is required?
* What will stop working if this cable fails?

Every feature should improve the user's ability to answer practical questions.

---

# 8. Print is a first-class feature

Technical work is not always performed in front of a computer.

Technicians often work:

* behind racks
* above ceilings
* on ladders
* inside cabinets
* on construction sites

Relatar should always be capable of producing clean, printable documentation.

Paper is not legacy.

Paper is a practical tool.

---

# 9. Technology should be generic

Relatar is not an audio documentation system.

It is not a network documentation system.

It is not a building automation system.

It is a documentation platform capable of describing technical infrastructure regardless of technology.

The same architecture should support:

* Audio
* Video
* Networking
* Fibre
* KNX
* Security
* CCTV
* Building automation
* Industrial systems

Technology-specific features should extend the model, not replace it.

---

# 10. Objects are reusable

A mixer is a type of object.

A switch is a type of object.

A patch panel is a type of object.

The system should describe object types once and allow many instances.

Documentation effort should decrease as the library grows.

---

# 11. Relationships are reusable

The same concepts should apply everywhere.

Examples include:

* contains
* connected to
* routes through
* controls
* enables
* disables
* belongs to

A relationship should have one clear meaning throughout the system.

---

# 12. Build layers, not shortcuts

Features should build upon existing concepts instead of introducing exceptions.

For example:

A snake is not a special case.

It is simply an object containing many related connections.

A wall outlet is not a special case.

It is simply another object with ports.

General solutions are preferred over technology-specific solutions.

---

# 13. Model behaviour, not implementation

Relatar should describe *what* happens.

Not *how* a particular manufacturer implements it.

Example:

Instead of documenting a proprietary DSP command, document that:

> "Button A enables Route B."

This allows the knowledge to survive equipment replacement.

---

# 14. Support gradual detail

Every installation is different.

Some users only want to document:

* devices
* cables
* cabinets

Others may wish to document:

* signal processing
* DSP logic
* operating modes
* automation
* control systems

Relatar should provide value at every level of detail.

Users should never be forced to document more than they need.

---

# 15. Documentation should outlive hardware

Equipment changes.

Manufacturers disappear.

Protocols evolve.

The underlying infrastructure and relationships usually remain.

Relatar should document concepts rather than vendor-specific implementations whenever possible.

---

# 16. Simplicity before cleverness

The simplest correct model is usually the best model.

Complexity should only be introduced when it represents real-world complexity.

The database should never become complicated merely because it can.

---

# 17. The architecture is the product

The PHP code, database schema and user interface are implementations.

The architecture is the product.

If the architecture is well designed, multiple user interfaces, importers, reports and integrations can be built on top of it.

---

# Final Principle

Everything in Relatar exists for one purpose:

> **Help people understand how technical systems are connected.**

If a proposed feature does not improve understanding, traceability or documentation, it should be questioned before being implemented.
