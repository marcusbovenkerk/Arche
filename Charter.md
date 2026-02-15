### Arche Kernel Charter (Public Version – Reduced Detail)

**Document type**: Normative / Governing  
**Status**: Final  
**Scope**: Kernel-only (Absolute Zero Trust Computing Base)  
**Audience**: Maintainers, security auditors, high-assurance integrators, reviewers  

---

## 1. Mission

The **Arche Kernel** is an extremely minimalist, high-assurance **zero-trust execution core** for securely loading and executing isolated WebAssembly Component Model components.

The kernel is **not designed as an operational or standalone usable system**.  
It exists solely as an **absolute root of trust** on which higher layers can **explicitly, controllably, and auditably** build trust.

Core objectives:
- Execute untrusted code safely and deterministically
- Keep the Trusted Computing Base as small and sharply bounded as possible
- Guarantee maximum auditability, predictability, and long-term stability

---

## 2. Core Principles (binding)

- **Absolute Zero-Trust by Design** – no implicit assumptions about host, environment, or higher layers
- **Extreme Minimal TCB** – only absolutely necessary responsibilities
- **Security > Assurance > Features > Convenience**
- **Intentional Non-Usability** – kernel is explicitly not configurable, ergonomic, or complete
- All usability, policy, and operational value arises exclusively outside the kernel
- Critical paths must be deterministic, bounded, and constant-time where required

---

## 3. Role and Responsibilities (current state)

Permitted kernel responsibilities (exclusively):

- Execution & isolation via WebAssembly Component Model (sole runtime)
- Manifest parsing + cryptographic signature verification
- Loading of components from a designated directory with bounded iteration
- Bounded execution via interruption mechanism (higher layer ticking)
- Stateless, fail-fast loader (no lingering state)

Current implementation characteristics:
- No host imports in WIT (fully sealed – instantiation trap on leaks)
- Hardcoded bounds on directory entries and component count
- No resource management or fuel in kernel

---

## 4. Kernel Prohibitions (strict)

The kernel must **NEVER** contain:

- Configuration options or parameters
- Additional runtimes or backends
- Resource management, scheduling, or quotas
- Policy, governance, or licensing logic
- Observability or metrics export
- Hooks or dynamic extensions with own semantics

These belong exclusively in higher, non-kernel layers.

---

## 5. Long-Term Guarantee

The Arche Kernel promises:

- Stability and consistency over decades
- No functional or semantic scope creep
- Full reproducibility and verifiability
- Suitability as cryptographic and execution root-of-trust
- Deployability as foundation for critical infrastructure (via explicit higher layers)

---

**Summary statement**

> *Arche is not designed to be used.  
> Arche is designed to be trusted — and nothing more.*