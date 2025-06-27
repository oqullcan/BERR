
---

<div align="center">
  <h1 style="font-weight: bold;">BERR (Berrmili)</h1>
</div>

<p align="center">
  <strong>A composable, misuse-resistant, and post-quantum cryptography framework.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-design%20%26%20specification-blue" alt="Project Status"/>
  <img src="https://img.shields.io/badge/source%20code-pending-lightgrey" alt="Source Code Status"/>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT%20%2F%20Apache--2.0-blue" alt="License"/></a>
</p>

---

## 📌 Project Status: Architectural Design & Public Specification

Welcome to **BERR**, the public home for the design, specification, and eventual implementation of the Berrmili cryptographic framework.

**Note:** Source code has not yet been published. We believe that robust cryptographic systems are born from transparent, auditable, and formally reasoned design. This repository serves as a public forum for specification drafts, architectural models, and community feedback before any code is committed.

---

## 🚀 The Vision: A New Foundation for Secure Software

The demand for secure, private-by-default applications has never been greater. Yet developers often face a trade-off: either use brittle, low-level cryptographic primitives prone to misuse, or rely on monolithic, application-specific protocols with limited flexibility. **BERR eliminates this compromise.**

BERR is a **general-purpose cryptographic framework** designed to empower developers in building diverse, end-to-end secure systems — ranging from secure messaging to IoT, decentralized applications, and collaborative real-time systems — all with post-quantum security guarantees.

---

## 🔍 What Makes BERR Different?

| Feature                   | Conventional Approach (e.g., Signal Protocol)                               | BERR Framework Approach                                                                                                                                  |
| :------------------------ | :-------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Scope & Purpose**        | Specialized protocol for **secure messaging**.                              | General-purpose, composable **framework** for secure applications: messaging, IoT, collaborative apps, decentralized systems, etc.                      |
| **Architecture**           | Tightly integrated and monolithic.                                           | **Explicitly composable**: Developers select formal handshake patterns (e.g., `IK`, `XX`) matching their application's trust model.                     |
| **Post-Quantum Security**  | Post-quantum upgrades as extensions or forks.                                | **Post-Quantum Native**: Hybrid cryptography (classical + PQC) is default and baked into Layer 0.                                                       |
| **Core Vision**            | Focused primarily on secure message transport.                              | Extends to **state synchronization (CRDTs)** and **privacy-preserving proofs** (e.g., Private Set Intersection).                                        |

---

## 📖 Threat Model

**BERR is designed under the assumption of a Dolev-Yao network adversary model**:
- Adversary has full control over the network: can intercept, drop, replay, reorder, or inject messages.
- Passive and active attacks are both in scope.
- Post-compromise security (PCS) and forward secrecy (FS) are supported where applicable.
- Side-channel attacks (timing, power analysis) are explicitly out of scope for the initial framework design but should be addressed at implementation and deployment level.

---

## 🛡️ Core Security Principles

### 🔒 Misuse-Resistance by Design
- Nonce management is fully automated.
- No API paths for unauthenticated encryption.
- Strongly typed key abstractions prevent accidental misuse (e.g., encryption keys cannot be used for signing).

### 🧾 Transcript-Based Protocol Integrity & Replay Protection
- Every handshake and protocol message is hashed into a running **transcript state**.
- Each new key derivation depends on the **entire protocol history**.
- Replay attacks are prevented by transcript hash chaining and optional sequence numbers in transport messages.

### 🛡️ Aggressive Domain Separation
- All derived keys and secrets are **context-bound** by unique, human-readable labels (e.g., `berr-v1-handshake`).
- Enforced at the API and cryptographic primitive level.

### 🎲 Cryptographically Secure Randomness
- All cryptographic operations requiring randomness (e.g., ephemeral key generation, nonce seeds) rely on a secure entropy source (e.g., OS-provided CSPRNG via libsodium, Rust `rand_core` + hardware entropy where available).
- Entropy quality is validated at runtime.

---

## 🏗️ Architectural Blueprint

```mermaid
graph TD
    subgraph Applications
        App1[Secure Messaging]
        App2[Collaborative Apps]
        App3[IoT / Embedded Systems]
    end

    subgraph BERR Framework
        L2["<b>Layer 2: Advanced Protocols</b><br/><i>e.g., Private Set Intersection, CRDTs</i>"]
        L1["<b>Layer 1: Protocol Primitives</b><br/><i>e.g., Identity, Handshake</i>"]
        L0["<b>Layer 0: Core Cryptography</b><br/><i>e.g., Hybrid PQC, KDF</i>"]
    end

    App1 --> L2
    App2 --> L2
    App3 --> L2

    L2 --> L1
    L1 --> L0
````

---

## 📅 Development Roadmap

**Phase 1: Specification & RFC (In Progress)**

* [x] Define system architecture and core doctrines.
* [ ] Publish detailed cryptographic specifications for all layers.
* [ ] Community discussion & feedback period via Issues.
* [ ] Invite peer-review from security researchers.

**Phase 2: Core Implementation (`berr::core`)**

* [ ] Publish initial source code.
* [ ] Implement foundational cryptographic primitives with hybrid PQC support.

**Phase 3: Protocol Layer & Examples**

* [ ] Implement handshake and identity modules.
* [ ] Provide reference application examples.

**Phase 4: Advanced Features & Formal Audits**

* [ ] Implement advanced Layer 2 protocols (CRDT sync, PSI, etc.).
* [ ] Engage third-party auditors for specification and code review.
* [ ] Optionally explore formal verification (e.g., Tamarin/ProVerif).

---

## 💬 How to Get Involved

This project is in its most critical design phase. Contributions of any kind are welcome.

* 📌 **Watch this repository** for updates.
* 📌 **Open an Issue** to discuss assumptions, suggest improvements, or request clarifications.
* 📌 **Review and critique the upcoming specifications when published.**

---

## 📄 License

The BERR framework is **dual-licensed** under the terms of:

* [MIT License](LICENSE-MIT)
* [Apache License 2.0](LICENSE-APACHE)

You may freely choose either license for your use.

---

## 🔐 Disclaimer

**BERR is experimental software under active specification and design.**
No production deployments should be based on this framework until a formal security audit is completed and v1.0 is released.

---
