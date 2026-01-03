# Base120 Corpus Validator (System B)

## Purpose
This repository declares **System B**: a governed project whose sole purpose is to validate the **Base120 corpus itself** (the 120-model mental model dataset), as distinct from validating artifacts *about* Base120.

This system exists to close the architectural loop between:
- Base120 as a **sealed canonical specification** (System A), and
- Downstream systems that **consume, analyze, or extend** the Base120 corpus.

No validation logic is implemented at this stage. This repository is declarative only.

---

## Trust Anchor
System B treats the following as immutable trust anchors:

- **Canonical seed:** Base120 v1.0.0 corpus JSON  
- **Source repository:** [`hummbl-dev/base120`](https://github.com/hummbl-dev/base120)
- **Seed hash (SHA-256):** Verified against `artifacts/base120.v1.0.0.seed.sha256`
- **Compliance artifact:** Canonical MRCC issued by System A

All future validation work, if any, MUST verify against this exact seed and hash.

---

## Scope
**In scope**
- Declaring governance boundaries for corpus-level validation
- Referencing the sealed Base120 v1.0.0 seed as an external dependency
- Serving as an architectural anchor for downstream research systems

**Out of scope**
- Modifying the Base120 seed
- Reinterpreting or extending Base120 semantics
- Implementing validators, schemas, CI, or tooling
- Making compliance claims about Base120 itself

Downstream systems MUST follow the [90-Day Integration Template](docs/downstream-integration-template.md).

---

## Non-Inheritance
This repository **does not inherit** governance rules, freeze mechanics, or failure modes from the Base120 artifact-validation system.

Specifically:
- FM1–FM30 semantics do **not** apply
- Registry-freeze rules do **not** apply
- Canonical authority remains exclusively with `hummbl-dev/base120`

System B is independently governed.

---

## Status
- **Lifecycle:** Pre-canonical
- **Versioning:** Independent (`v0.x`)
- **Authority:** Declarative only
- **Change posture:** Prohibitive by default

No claims are made, implicitly or explicitly, about Base120 v1.0.0 beyond referencing it as a sealed external artifact.
