# Relatar Specification

Version 0.1 (Draft)

---

## Purpose

This specification defines the concepts, terminology, architecture and behaviour of Relatar.

The purpose of the specification is to provide a stable, implementation-independent description of the Relatar platform.

The specification is intended to ensure that every implementation of Relatar models technical infrastructure consistently, regardless of programming language, database or user interface.

---

## Scope

This specification describes:

- concepts
- terminology
- relationships
- architecture
- expected behaviour

This specification does not describe:

- database implementation
- user interface
- programming language
- API implementation

Those belong to individual implementations.

---

## Audience

This specification is intended for:

- developers
- contributors
- architects
- technical writers

Users should instead refer to the user documentation.

---

## Conformance

An implementation claiming to implement the Relatar Specification SHALL satisfy the mandatory requirements defined in this document.

Requirements are expressed using the terminology defined in RFC 2119.

MUST

MUST NOT

SHALL

SHOULD

SHOULD NOT

MAY

---

## Philosophy

Relatar is not defined by its software.

Relatar is defined by this specification.

Software is merely one implementation.

Future implementations may exist in different programming languages while remaining fully compliant with the Relatar Specification.

---

## Versioning

The specification evolves independently of software releases.

Software implementations declare which specification version they implement.

Example:

Relatar Server 1.3

Implements

Relatar Specification 1.1

---

## Guiding Principle

The purpose of Relatar is simple.

Know how everything is connected.
