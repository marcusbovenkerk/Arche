# Arche Kernel — Security Target (Audit-Grade)

**Document Type**: Security Target / Audit Master Document
**Standard Alignment**: ISO/IEC 15408 (Common Criteria)
**Evaluation Context**: EAL4+ / EAL5-oriented design
**Audience**: Certification bodies, Common Criteria evaluation labs, independent security auditors
**Status**: Final – Canonical

---

## 1. Introduction and Purpose

This document constitutes the definitive, self-contained Security Target–style description of the **Arche Kernel**. It is intended to be handed over directly to an evaluation laboratory or certification authority without additional explanatory material.

The purpose of this document is to:

* Define the Target of Evaluation (TOE)
* Describe the security objectives and design intent
* Specify security-relevant functionality and guarantees
* Explicitly state non-goals, assumptions, and residual risks

This document contains no roadmap items, future intentions, or speculative features. It describes the Arche Kernel **as designed and implemented**.

---

## 2. Target of Evaluation (TOE) Definition

### 2.1 TOE Overview

The Target of Evaluation (TOE) is the **Arche Kernel binary**.

The TOE consists exclusively of:

* The component loader
* The manifest parser and verifier
* The WebAssembly Component Model execution backend

### 2.2 TOE Boundaries

The following elements are **explicitly excluded** from the TOE:

* Host operating system and hardware
* Compiler toolchain
* Any platform layer, orchestration, or governance logic
* All plugins, extensions, and policy layers
* Tooling, SDKs, and developer interfaces

All excluded components are treated as **untrusted** unless otherwise stated.

---

## 3. Security Objectives and Design Intent

### 3.1 Primary Security Objective

The primary security objective of the Arche Kernel is to act as a **minimal, deterministic, zero-trust execution root** for the verification and loading of WebAssembly Component Model components.

### 3.2 Intentional Non-Usability

The Arche Kernel is **intentionally not usable as a standalone system**.

This non-usability is a binding design constraint and a security feature. The kernel provides no facilities for configuration, policy definition, resource management, or input/output. All meaningful functionality must be implemented in higher layers with explicitly declared trust assumptions.

### 3.3 Design Principles

The design of the Arche Kernel is governed by the following principles:

* Extreme minimization of the Trusted Computing Base (TCB)
* Deterministic and bounded execution for all kernel operations
* Fail-closed behavior on all error paths
* Permanence of kernel responsibilities once introduced

---

## 4. Security Functional Description

### 4.1 Component Verification

The kernel verifies all components prior to loading using cryptographic signatures. Verification is implemented in constant time to prevent side-channel leakage.

Components that fail verification are rejected without partial execution or persistent state changes.

### 4.2 Deterministic Loading

Verified components are loaded in a deterministic order with bounded execution time and bounded memory usage. The kernel maintains no mutable global state across load operations.

### 4.3 Isolation Model

All component execution occurs within the WebAssembly Component Model. The kernel provides no host I/O, no system calls, and no ambient authority.

### 4.4 Extensibility Model

The kernel exposes declarative extension points in the form of interfaces only. No extension logic is implemented within the kernel.

All extensions are treated as untrusted and may not alter kernel control flow, state, or security guarantees.

---

## 5. Threat Model and Risk Treatment

### 5.1 Attacker Model

The kernel assumes adversaries capable of:

* Supplying arbitrary malformed manifests or components
* Attempting to bypass verification logic
* Attempting resource exhaustion through pathological inputs
* Compromising all layers above the kernel

### 5.2 Security Goals

The kernel aims to:

* Prevent execution of unauthenticated components
* Prevent escape from WebAssembly isolation
* Ensure bounded and deterministic behavior under adversarial input

### 5.3 Mitigations

Identified threats are mitigated through:

* Strict input validation
* Cryptographic signature verification
* Hard execution bounds
* Fail-fast, stateless error handling

---

## 6. Security Guarantees and Explicit Non-Guarantees

### 6.1 Guaranteed Properties

* Deterministic execution semantics
* Bounded execution time and memory usage
* Constant-time cryptographic verification
* Fail-closed behavior on all errors

### 6.2 Explicit Non-Guarantees

The kernel does not guarantee:

* Availability, fairness, or liveness
* Runtime resource quotas or scheduling
* Authorization, governance, or policy enforcement
* Any form of input/output or device access

---

## 7. Assumptions and Operational Environment

The security claims of the kernel rely on the following assumptions:

* The host operating system enforces basic process isolation
* The hardware operates according to specification
* The compiler toolchain is trusted and validated through reproducible builds

Violations of these assumptions are outside the scope of the kernel.

---

## 8. Assurance Measures

### 8.1 Testing and Verification

Testing activities provide evidence that the kernel satisfies its declared security properties. Testing is treated as **evidence**, not as a security mechanism.

Verification methods include:

* Unit testing of all critical paths
* Integration testing of the full load-and-verify flow
* Property-based testing for boundary conditions
* Adversarial and malformed input testing

### 8.2 Reproducible Builds

The kernel is built using deterministic build processes. Binary artifacts are reproducible, and deviations between expected and observed outputs are treated as verification failures.

### 8.3 Software Bill of Materials (SBOM)

All build-time and runtime dependencies are explicitly enumerated, version-pinned, and auditable.

---

## 9. Residual Risks and Acceptance Statement

The following residual risks are acknowledged:

* Defects in the underlying WebAssembly runtime
* Compiler or hardware-level vulnerabilities
* Denial-of-service through legitimate but resource-intensive inputs

These risks are accepted by design and must be addressed by higher layers if mitigation is required.

---

## 10. Change Control and Lifecycle Commitments

Any change affecting:

* Kernel responsibilities
* Trust boundaries
* Security guarantees

requires formal review and unanimous approval by the Kernel governance authority.

The Arche Kernel commits to long-term stability and resistance to functional scope expansion.

---

**End of Security Target**

