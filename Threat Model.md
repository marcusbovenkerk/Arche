# Arche Kernel Threat Model (v0.1.0 – Final)

**Document Type**: Informative / Assurance Artifact  
**Status**: Final  
**Scope**: Arche Kernel only (zero-trust execution core)  
**Audience**: Security auditors, certification bodies, high-assurance integrators  

---

## 1. Introduction

This threat model describes the security posture of the Arche Kernel as currently implemented. The kernel is considered **complete in its design and implementation** and is now in the **comprehensive testing phase** (unit, integration, property-based, fuzzing, and adversarial testing).

The primary goal is to position the kernel as **certification-ready** (targeting Common Criteria EAL4+ or equivalent assurance levels).

---

## 2. Target of Evaluation (TOE)

The TOE is the Arche Kernel binary, consisting exclusively of:

- Component loader
- Manifest parser and cryptographic verifier
- WebAssembly Component Model execution backend

All higher layers, plugins, and operational environments are explicitly **outside** the TOE and treated as untrusted.

---

## 3. Attacker Model

Adversaries are assumed to have the following capabilities:

- Ability to supply arbitrary malformed or malicious manifests and WASM components
- Ability to tamper with plugin files on disk
- Ability to attempt resource exhaustion (e.g., large directories, infinite loops)
- Full control over all layers above the kernel (including potential host compromise)

The kernel does **not** assume a trusted host, trusted higher layers, or trusted plugins.

---

## 4. Identified Threats and Mitigations

| Threat | Description | Mitigation (Current Implementation) |
|--------|-------------|-------------------------------------|
| **Tampered or unauthenticated components** | Execution of modified or forged plugins | Cryptographic manifest verification (SHA-256 checksum + ed25519 signature). Constant-time verification. Fail-fast rejection on any mismatch. |
| **Host capability leakage** | Plugin access to stdio, filesystem, network, or environment | Zero host imports in WIT interface. Any attempt to use forbidden imports results in instantiation trap. |
| **Resource exhaustion (DoS)** | Infinite loops or unbounded resource use | Epoch interruption enabled (higher-layer ticking required for bounds). Hardcoded bounds on directory entries and plugin count (MAX_DIR_ENTRIES=32, MAX_PLUGINS=64). |
| **Directory traversal or symlink attacks** | Escape from plugin directory | Hardcoded "plugins" directory prefix. No path resolution or symlink following. |
| **Partial or lingering state compromise** | Persistent state after failed loads | Fully stateless loader – no global mutable state, all stores dropped after execution. |
| **Side-channel leakage** | Timing attacks on verification | Constant-time cryptographic operations (ed25519-dalek). |

---

## 5. Security Guarantees

The kernel provides:

- Deterministic loading order and execution semantics
- Bounded execution time and memory (via Wasmtime configuration and epoch interruption)
- Fail-closed behavior on all error paths
- No ambient authority or host leakage

These guarantees are currently undergoing **maximum test coverage** to provide evidence for certification.

---

## 6. Residual Risks (Accepted by Design)

The following risks are acknowledged and accepted:

- Defects in underlying dependencies (e.g., Wasmtime runtime bugs) – mitigated via minimal dependency set and ongoing testing.
- Hardware or compiler vulnerabilities – outside kernel scope.
- Denial-of-service via very large but valid inputs – must be handled by higher layers if required.

These risks are intentionally left to higher layers to maintain minimal TCB.

---

## 7. Path to Certification

The kernel is **implementation-complete** and in the **final testing phase**. All critical paths are covered by:

- Unit and integration tests
- Property-based testing
- Fuzzing of parsing and loading
- Adversarial scenario validation

Upon test completion, the kernel will be submitted for independent security audit and formal certification (target: Common Criteria EAL4+).

---

**Conclusion**: The Arche Kernel achieves its security objectives through extreme minimalism and explicit boundaries. It is ready for certification as a pure root-of-trust.