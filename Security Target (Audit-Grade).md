### Arche Kernel — Security Target (Reduced Detail)

**Document Type**: Security Target / Audit Master Document  
**Standard Alignment**: ISO/IEC 15408 (Common Criteria)  
**Evaluation Context**: High assurance design  
**Audience**: Certification bodies, evaluation labs, auditors  
**Status**: Final – Canonical

---

## 1. Introduction and Purpose

This document is the definitive Security Target-style description of the **Arche Kernel**, suitable for direct submission to evaluation laboratories.

It describes the kernel **as designed and implemented**, with no roadmap or speculative content.

---

## 2. Target of Evaluation (TOE) Definition

### 2.1 TOE Overview

The TOE is the **Arche Kernel binary**, consisting exclusively of:

* Component loader
* Manifest parser and verifier
* WebAssembly Component Model execution backend

### 2.2 TOE Boundaries

Explicitly excluded (treated as untrusted):

* Host OS and hardware
* Compiler toolchain
* Any platform, orchestration, or policy layers
* All components and extensions

---

## 3. Security Objectives and Design Intent

Primary objective: act as a **minimal, deterministic, zero-trust execution root** for verified WebAssembly Component Model components.

Intentional non-usability is a binding security feature.

Design principles:
* Extreme TCB minimization
* Deterministic and bounded execution
* Fail-closed on all error paths
* Permanence of responsibilities

---

## 4. Security Functional Description

- Cryptographic verification of components prior to loading
- Deterministic loading order with bounded execution
- No host I/O or ambient authority
- Declarative extension points only (no kernel-side logic)

---

## 5. Threat Model and Risk Treatment

Adversaries can supply malformed data, tamper with files, attempt exhaustion, and control higher layers.

Mitigations: strict validation, cryptographic checks, hard bounds, stateless error handling.

---

## 6. Security Guarantees and Non-Guarantees

**Guaranteed**:
* Deterministic semantics
* Bounded execution
* Constant-time verification
* Fail-closed errors

**Not guaranteed** (by design):
* Availability or liveness
* Resource quotas
* Policy enforcement
* I/O access

---

## 7. Assumptions

- Basic process isolation by host OS
- Correct hardware operation
- Trusted, reproducible compiler toolchain

---

## 8. Assurance Measures

- Comprehensive testing (unit, integration, property-based, fuzzing)
- Reproducible builds
- Auditable dependency list

---

## 9. Residual Risks

Accepted risks include underlying runtime bugs, compiler/hardware issues, and DoS via large valid inputs — to be mitigated by higher layers if needed.

---

## 10. Change Control

Any change affecting responsibilities, boundaries, or guarantees requires formal review.

