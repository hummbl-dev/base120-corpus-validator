# ACTIVATION.md
## System B — Corpus Validator (Non-Binding)

**Status:** Dormant  
**Binding Effect:** None  
**Last Updated:** 2026-01-03

---

## Purpose of This Document

This document describes the *theoretical conditions* under which **System B (Base120 Corpus Validator)** could transition from a purely declarative repository to an implemented system containing code, schemas, or CI.

This document:
- Does **not** authorize implementation
- Does **not** establish a roadmap
- Does **not** modify governance
- Does **not** create obligations

It exists solely to prevent ambiguity, premature execution, or accidental scope creep.

---

## Current State (Authoritative)

- System B is a **declared but dormant governed system**
- No code, schemas, CI, or validators exist
- No validation logic is authorized
- Base120 v1.0.0 corpus is **sealed and governed exclusively by System A**
- System B makes **no claims** about Base120 correctness, completeness, or semantics

Default posture: **DO NOTHING**

---

## Preconditions for Activation (All Required)

System B MAY be considered for activation *only if all of the following are true*:

1. **Explicit Governance Authorization**
   - A written governance decision approving activation
   - Decision recorded in `GOVERNANCE.md`
   - Versioned activation declaration (e.g. `v0.1.0-activation`)

2. **Clear Problem Statement**
   - A concrete, externally motivated need that cannot be satisfied by System A
   - Example (non-exhaustive):
     - Independent academic replication
     - Downstream system requiring corpus-level guarantees
     - Regulatory or audit-driven corpus verification

3. **Non-Retroactivity Guarantee**
   - Activation MUST NOT:
     - Modify Base120 v1.0.0
     - Invalidate existing MRCCs
     - Reinterpret canonical semantics
   - System B may only *observe* the corpus, never redefine it

4. **Governance Separation Preserved**
   - Independent versioning continues
   - No inheritance of FM1–FM30 or System A enforcement semantics
   - No shared CI or release coupling

5. **Public Activation Record**
   - An `ACTIVATION_DECISION.md` documenting:
     - Motivation
     - Scope
     - Explicit non-goals
     - Failure conditions
     - Sunset criteria

---

## Permitted Activation Scope (If Authorized)

If activation were approved, System B would be limited to:

- Structural validation of the corpus as data
- Cardinality checks (e.g. 120 entries, domain distribution)
- Schema conformance verification
- Hash and provenance verification

Explicitly **out of scope**:
- Semantic reinterpretation
- Model reclassification
- Canonical corrections
- Back-propagation into System A
- Any “improvement” claims

---

## Prohibited Actions (Always)

Regardless of activation status, System B MUST NEVER:

- Modify the Base120 seed corpus
- Claim authority over Base120 definitions
- Issue MRCCs for System A artifacts
- Act as a gatekeeper for Base120 usage
- Introduce breaking claims about Base120 v1.0.0

---

## Sunset and Deactivation

Any activated System B implementation MUST include:

- Explicit deactivation criteria
- A sunset clause
- A defined process for returning to dormant state
- Assurance that deactivation does not affect downstream consumers

Dormancy is the default and preferred steady state.

---

## Interpretation Rule

If any ambiguity exists regarding whether an action constitutes “activation”:

> **Assume activation is NOT authorized. Stop and escalate.**

---

## Closing Note

System B exists to close an architectural loop, not to create momentum.

The absence of code is a **deliberate success condition**, not a temporary gap.

