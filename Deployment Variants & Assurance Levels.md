# Arche Kernel – Deployment Variants & Assurance Levels

**Document Type**: Normative / Strategic  
**Status**: Final  
**Scope**: Trust-building ladder across deployment variants  
**Audience**: Architects, security officers, certification bodies, high-assurance integrators  

---

## 1. Purpose

This document defines the official deployment variants of the Arche ecosystem and establishes a clear **assurance and trust ladder**.

The Arche Kernel is **implementation-complete** and currently in the **final testing phase** prior to certification submission.

The goal is to enable users to select the appropriate assurance level while preserving the kernel as the **absolute zero-trust root**.

---

## 2. Core Principles

- The **Arche Kernel** is the sole absolute source of trust
- The kernel is intentionally non-operational and non-usable standalone
- Higher assurance requires staying closer to the kernel
- Usability and functionality are added only through **explicit trust assumptions** in higher layers
- Variants may never extend, duplicate, or semantically alter the kernel

---

## 3. Official Deployment Variants (Trust Ladder)

| Variant                  | Role                          | TCB Size | Assurance Level     | Key Characteristics                          | Trusted? | Operational Use |
|--------------------------|-------------------------------|----------|---------------------|----------------------------------------------|----------|-----------------|
| **Arche Kernel**         | Zero-trust root               | Minimal  | **Root of Trust**   | Pure verification + WASM execution only      | Yes      | No              |
| **Kratos Core**          | Hardened kernel variant       | Small    | Very High           | Build-time restricted parameters             | Yes      | Limited         |
| **Nomos Layer**          | Trusted policy layer          | Medium   | High                | Explicit policy, resource control, auditing  | Yes      | Yes             |
| **Kosmos Platform**      | Full operational platform     | Large    | Medium              | Enterprise features, ergonomics              | No       | Yes             |

---

## 4. Variant Details

### 4.1 Arche Kernel
Absolute zero-trust execution root.  
**Current status**: Implementation complete, testing phase ongoing.  
**Certification target**: Primary candidate for formal evaluation (EAL4+/EAL5).

### 4.2 Kratos Core
Formally approved, build-time parameterized derivative of Arche.  
No functional extensions – only hardening (e.g., stricter bounds).

### 4.3 Nomos Layer
Thin, certifiable trusted policy layer atop the kernel.  
Suitable for high-assurance operational deployments.

### 4.4 Kosmos Platform
Feature-rich platform for general use.  
Explicitly **untrusted** – prioritizes usability over assurance.

---

## 5. Assurance & Trust Ladder

- **Root of Trust** → Arche Kernel (certification target)
- **Highest Deployable Assurance** → Kratos Core
- **High Assurance Operational** → Kernel + Nomos Layer
- **Enterprise / Commercial** → Kosmos Platform

### Decision Guidance
- Need a formal root-of-trust for certification? → Arche Kernel
- Require limited operational use with minimal added trust? → Kratos
- Accept trusted policy layer? → Nomos
- Prioritize functionality? → Kosmos

---

## 6. Long-Term Commitment

This model guarantees:

- Arche Kernel remains permanently minimal, stable, and non-usable
- Trust is never added implicitly
- Certification feasibility remains focused on the kernel
- Flexibility without kernel compromise

**Summary statement**

> **Arche defines trust.  
> Variants define usability.  
> These concerns are never mixed.**