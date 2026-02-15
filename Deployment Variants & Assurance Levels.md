### Arche Kernel – Deployment Variants & Assurance Levels (Reduced Detail)

**Document Type**: Normative / Strategic  
**Status**: Final  
**Scope**: Trust-building ladder  

---

## 1. Purpose

Defines official deployment variants and the assurance ladder, preserving the kernel as the absolute zero-trust root.

---

## 2. Core Principles

- Arche Kernel is the sole absolute source of trust
- Kernel remains intentionally non-operational
- Higher assurance = closer to kernel
- Usability added only via explicit trust in higher layers

---

## 3. Official Deployment Variants

| Variant            | Role                        | TCB Size | Assurance Level | Key Characteristics                     | Trusted? | Operational |
|--------------------|-----------------------------|----------|-----------------|-----------------------------------------|----------|-------------|
| **Arche Kernel**   | Zero-trust root             | Minimal  | Root of Trust   | Pure verification + execution only      | Yes      | No          |
| **Kratos Core**    | Hardened variant            | Small    | Very High       | Restricted build-time parameters        | Yes      | Limited     |
| **Nomos Layer**    | Trusted policy layer        | Medium   | High            | Explicit policy and resource control    | Yes      | Yes         |
| **Kosmos Platform**| Full platform               | Large    | Medium          | Enterprise features and ergonomics      | No       | Yes         |

---

## 4. Long-Term Commitment

Arche Kernel remains permanently minimal and stable. Trust and usability are strictly separated.

> **Arche defines trust.  
> Variants define usability.  
> These concerns are never mixed.**

### Arche Kernel Readme (Reduced Detail)

# Arche Kernel

**Ultra-minimalist zero-trust root-of-trust for WebAssembly Component Model components**

### Intended Audience
- Security auditors and evaluators
- High-assurance system architects
- Researchers in trusted execution

### Not Intended For
- General developers
- Rapid prototyping
- Standalone production use

The Arche Kernel is an extremely minimalist execution core that serves exclusively as an **absolute root of trust** for verifying and loading isolated WASM components.

> **Arche is designed to be trusted — and nothing more.**

Code is not yet public to avoid premature trust assumptions prior to full verification.

## Status
- Design, assurance, and documentation complete
- In final testing phase
- Goal: certification-ready root-of-trust

## Core Principles
- Extreme TCB minimization
- Absolute zero-trust
- Bounded and deterministic execution
- Intentional non-usability

## Documentation
- Security Target (Audit-Grade)
- Kernel Charter
- Threat Model
- Deployment Variants & Assurance Levels

## License
Apache-2.0 or MIT