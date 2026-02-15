# Arche Kernel

**Ultra-minimalist zero-trust root-of-trust for WebAssembly Component Model plugins**

### Intended Audience
- Security auditors and evaluators
- High-assurance system architects
- Researchers in trusted execution and isolation

### Not Intended For
- General application developers
- Rapid prototyping or feature-driven platforms
- Production deployment without explicit higher layers



The Arche Kernel is an extremely minimalist, high-assurance execution core that serves exclusively as an **absolute root of trust** for verifying and loading isolated WASM components.

The project is explicitly designed **not as a usable platform or framework**, but as a permanent, auditable foundation on which higher layers can explicitly build trust.

> **Arche is designed to be trusted — and nothing more.**

The Arche Kernel code is intentionally not published at this stage to avoid premature trust assumptions prior to full verification and hardening.



## Status

- **Current phase**: Design, assurance, and documentation completed.
- **Security Target** (Common Criteria-aligned, audit-grade) publicly available.
- **Code and tests**: In private development (verification and hardening). Public release follows completion of maximum test coverage (unit → integration → fuzz → property-based).
- **Goal**: Certification-ready root-of-trust (EAL4+/EAL5-oriented).

## Core Principles

- Extreme minimization of the Trusted Computing Base (TCB)
- Absolute zero-trust by design
- Bounded and deterministic execution
- Fail-fast and stateless behavior
- Intentional non-usability: all usability, policy, and resource control belong explicitly outside the kernel

## Documentation

- [Security Target (Audit-Grade)](docs/Security_Target.md) – Formal CC-aligned document, directly usable for certification processes.
- [Kernel Charter](docs/Charter.md) – Binding governance, scope, and principles.
- [Threat Model](docs/Threat_Model.md) – Attacker model, mitigations, and residual risks.
- [Deployment Variants & Assurance Levels](docs/Deployment_Variants.md) – Trust-building ladder (Arche → Kratos → Nomos → Kosmos).

## License

Licensed under either of:

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE))


## Contact & Feedback

- Issues and discussions welcome for feedback on design, charter, or assurance artifacts.
- No feature requests for the kernel itself – scope is frozen per charter.

Thank you for your interest in high-assurance systems.
