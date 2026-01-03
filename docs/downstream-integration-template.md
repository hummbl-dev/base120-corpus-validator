# 90-Day Downstream Integration Template

**Version**: 1.0  
**Applies to**: Base120 v1.0.0 consumers  
**Authority**: base120-corpus-validator (System B)

---

## Overview

This template defines a 4-phase, 12-week integration pattern for any system consuming Base120 v1.0.0 as immutable infrastructure.

**Constraints**:
- Base120 v1.0.0 is immutable
- Seed JSON + SHA-256 + MRCC are the only trust surface
- Downstream systems are observers/consumers only
- No semantic reinterpretation, no back-propagation

---

## Phase 1: Ingestion (Weeks 1-2)

**Objective**: Establish read-only access to Base120 trust surface.

### Week 1 — Trust Surface Acquisition
- Obtain canonical seed: `hummbl-dev/base120/artifacts/base120.v1.0.0.seed.json`
- Obtain hash file: `hummbl-dev/base120/artifacts/base120.v1.0.0.seed.sha256`
- Obtain MRCC binding: `hummbl-dev/base120/compliance/base120.v1.0.0.seed.mrcc.json`
- Document acquisition method (git clone, API fetch, manual download)
- Store local copy with provenance metadata

### Week 2 — Schema Familiarization
- Parse seed JSON structure: `schema_version`, `model_count`, `models[]`, `governance`
- Map 6 domains × 20 models each
- Domain set is closed and fixed: `{P, IN, CO, DE, RE, SY}` — no additions permitted downstream
- Document model object structure: `id`, `name`, `layer`, `domain`, `definition`, `constraints`, `failure_modes`, `transformations`, `relations`
- Create internal data model (read-only representation)

**Gate 1**: Local seed copy exists, hash documented, schema understood.

---

## Phase 2: Verification (Weeks 3-4)

**Objective**: Establish cryptographic trust before any consumption.

### Week 3 — Hash Verification Implementation
- Implement SHA-256 verification routine
- Verify computed hash against `artifacts/base120.v1.0.0.seed.sha256`
- Implement **fail-closed** behavior: hash mismatch = hard stop
- Log verification result with timestamp

### Week 4 — MRCC Validation
- Parse MRCC binding: `mrcc_version`, `artifact`, `sha256`, `schema_version`, `governance_version`, `claims`, `non_claims`, `sealed_at`
- Verify MRCC hash matches computed hash
- Verify `governance_version` = `base120.v1.0.0`
- Document claims and non-claims in downstream system's own governance docs

**Gate 2**: Automated verification passes; fail-closed behavior confirmed.

---

## Phase 3: Binding (Weeks 5-8)

**Objective**: Integrate Base120 as referenced dependency without modification.

### Week 5 — Reference Architecture
- Define consumption pattern: direct reference vs. cached copy vs. derived index
- Document refresh policy (never for v1.0.0 — immutable)
- Establish namespace isolation (Base120 data separate from downstream data)

### Week 6 — Model Access Layer
- Implement read-only accessors for 120 models
- Support lookup by: `id`, `domain`, `name`
- No mutation methods permitted
- No extension points that could alter semantics

### Week 7 — Integration Contracts
- Define how downstream system references Base120 models
- Establish citation format: `base120:v1.0.0:{model_id}`
- Document any mapping/overlay structures (must be clearly downstream-owned)
- Explicit boundary: Base120 provides definitions, downstream provides interpretations
- Downstream systems MUST NOT introduce alternate IDs, aliases, or renumbering schemes for Base120 models

### Week 8 — Integration Testing
- Verify all 120 models accessible
- Verify no write paths exist
- Verify hash verification runs on startup/deploy
- Document integration test suite

**Gate 3**: Read-only integration complete; no mutation vectors; tests passing.

---

## Phase 4: Observability (Weeks 9-12)

**Objective**: Enable audit trail and consumption monitoring without feedback loops.

### Week 9 — Consumption Logging
- Log which models are accessed
- Log access frequency and patterns
- No telemetry back to Base120 (one-way only)

### Week 10 — Audit Trail
- Record provenance: "This output derived from base120:v1.0.0:{model_id}"
- Include seed hash reference in audit records
- Timestamp all derivations

### Week 11 — Anomaly Detection
- Detect if local seed copy diverges (should never happen)
- Alert on hash verification failures
- Monitor for unauthorized modification attempts

### Week 12 — Documentation & Freeze
- Document complete integration architecture
- Document consumption patterns observed
- Declare integration stable
- Establish change control for downstream system's Base120 binding

**Gate 4**: Observability complete; audit trail functional; integration frozen.

---

## Explicit Non-Goals

| Non-Goal | Rationale |
|----------|----------|
| Modify Base120 seed | Immutable trust anchor |
| Extend model definitions | Semantic purity |
| Add models to corpus | Governance violation |
| Provide feedback to Base120 | One-way consumption only |
| Interpret FM1-FM30 | Belongs to System A (Artifact Validator) |
| Create derived canonical variants | Prohibited by MRCC non-claims |
| Cache with TTL refresh | v1.0.0 is frozen; no refresh needed |
| Introduce alternate model IDs | Shadow vocabulary prohibition |

---

## Failure Modes (Downstream-Specific)

| Code | Name | Trigger | Response |
|------|------|---------|----------|
| DS-FM1 | Hash Mismatch | Computed ≠ declared SHA-256 | **HARD STOP** — Do not proceed |
| DS-FM2 | MRCC Inconsistency | MRCC fields contradict seed | **HARD STOP** — Investigate source |
| DS-FM3 | Write Attempt | Code attempts seed mutation | **REJECT** — Log and alert |
| DS-FM4 | Schema Drift | Downstream expects different structure | **FAIL CLOSED** — Version mismatch |
| DS-FM5 | Provenance Loss | Cannot trace derivation to seed | **DEGRADE** — Mark output as unverified |
| DS-FM6 | Unauthorized Extension | Downstream adds "models" | **REJECT** — Namespace violation |
| DS-FM7 | Governance Drift | Downstream treats template as optional | **HARD STOP** — Compliance breach |

---

## Template Instantiation Checklist

When applying this template to a named system:

1. ☐ Replace "downstream system" with system name
2. ☐ Document system-specific consumption patterns (Week 5)
3. ☐ Define system-specific model mappings (Week 7)
4. ☐ Establish system-specific audit format (Week 10)
5. ☐ Add system-specific failure modes (append to DS-FM list)
6. ☐ Create system-specific integration test suite
7. ☐ Self-attest compliance with this template

---

## Summary Timeline

| Weeks | Phase | Deliverable |
|-------|-------|-------------|
| 1-2 | Ingestion | Local seed copy + schema understanding |
| 3-4 | Verification | Automated hash verification + MRCC validation |
| 5-8 | Binding | Read-only integration + tests |
| 9-12 | Observability | Audit trail + consumption monitoring |
