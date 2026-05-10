# HONEST Software

**The canonical home of the HONEST Software Manifesto and its companion documents.**

This is **the movement, not a product.**

> *Honest, Owned, Network-free, Ephemeral, Sealed, Transparent — software that owes its filial duty to the human at the keyboard, not to the institutions that would prefer to harvest them.*

---

## What is HONEST?

HONEST is a movement to build software that treats the user as its principal — not as a product, not as a data source, not as a captive audience. It rejects the architectural choices of the era we call **yester-day-ta-centers**: cloud-mandatory consumer AI, telemetry-by-default operating systems, surveillance-shaped social platforms, and the recasting of "free" software as a vehicle for extractive cloud appropriation.

The movement is rooted in two principles, named from two languages:

> ***Loka-hita-niṣṭhā*** *(Sanskrit: steadfast devotion to the welfare of the world)* — the moral foundation of HONEST software.
>
> ***Pietas erga utentem*** *(Latin: duty toward the one who uses)* — the legal-philosophical companion phrase, used in the License.

The acronym **HONEST** stands for the Six Pillars:

| Letter | Pillar | Means |
|---|---|---|
| **H** | Honest | Says what it knows; says what it doesn't; cites evidence; refuses to fabricate. |
| **O** | Owned | The user owns their data, their derived state, their fine-tuned adaptations. Export, deletion, portability are first-class. |
| **N** | Network-free | No telemetry. No phone-home. No silent updates. Federation is on user consent only. |
| **E** | Ephemeral | Peripheral access is requested, scoped, and released. No ambient capture. |
| **S** | Sealed | Trust boundaries are kernel-enforced where possible. The user's vault is the user's, full stop. |
| **T** | Transparent | Source published. File formats documented. The user can leave with everything intact. |

Above the pillars stands a constitutional commitment we call **[Inviolata](./INVIOLATA.md)** — *domus inviolata*, the inviolate home — which declares that the user's vault is protected with the same architectural rigor that constitutional democracies extend to the physical home.

---

## The documents that govern this movement

In reading order:

1. **[`MANIFESTO.md`](./MANIFESTO.md)** — *The HONEST Software Manifesto v0.1.* The values. The primary artifact. **Released under CC BY 4.0; adoption is free.**

2. **[`INVIOLATA.md`](./INVIOLATA.md)** — *The Inviolata Principle v0.1.* The constitutional layer. *Domus inviolata.* The user's vault is the inviolate home of the digital era; extrajudicial access is foreclosed in code; lawful access requires due process between user and state. Pre-committed Lavabit stance: if a jurisdiction mandates a backdoor, operations cease in that jurisdiction. **Released under CC BY 4.0.**

3. **[`SUCCESSION.md`](./SUCCESSION.md)** — *Designed-In Succession v0.1.* The hardest case for Inviolata is *the user dies; heirs need access; we hold no keys.* Without a designed-in answer, every "no backdoor" promise becomes a wedge for a backdoor later. This document is the answer: user-designed succession via Shamir's Secret Sharing, configurable triggers, compartment-aware key splitting, mandatory dry-run testing. **Released under CC BY 4.0.**

4. **[`FEDERATION.md`](./FEDERATION.md)** — *The Federation Concept v0.1: Owner-Sovereign Federation.* The architectural-layer commitment for federation between vaults. Each vault is a first-class peer; no central identity provider; no operator-mediated directory; trust expressed as a typed, scoped, time-bounded, revocable graph owned by the granting user. Includes the *doctor scenario* worked example (unconscious in the ER, no operator to call). Concept-level; the wire protocol is deferred. **Released under CC BY 4.0.**

5. **[`LICENSE-CONCEPT.md`](./LICENSE-CONCEPT.md)** — *The HONEST License v0.1 (Concept).* The legal mechanism in concept form. Source-available, with broad rights for individual / household / educational / charitable / research use, and conditional rights for commercial and institutional operators who themselves honor the six HONEST pillars toward their end users. **Deliberately not OSI-approved**, because OSI's Open Source Definition forbids the field-of-endeavor discrimination this license depends on. To be drafted into enforceable text by qualified counsel before any production use.

6. **[`TRADEMARK.md`](./TRADEMARK.md)** — *The HONEST Trademark Policy v0.1 (Placeholder).* No marks are filed yet. The intended policy is documented so good-faith adopters know what they are agreeing to.

7. **[`ADOPTERS.md`](./ADOPTERS.md)** — *The HONEST Adopters' Registry.* Public list of projects that have declared adherence to the Manifesto. Open, on the honor system, no certification. Currently lists only the first reference implementation; that is the honest current state.

---


## Adoption

Adoption of the HONEST Manifesto is **public, voluntary, and free**:

1. Read the [Manifesto](./MANIFESTO.md), the [Inviolata Principle](./INVIOLATA.md), and the [License Concept](./LICENSE-CONCEPT.md). Make sure you genuinely agree.
2. Publish a **Filial Duty Statement** (see the [Manifesto §Adoption](./MANIFESTO.md) and [License Concept §5](./LICENSE-CONCEPT.md)) describing how your project honors each of the six pillars.
3. License your project's code under the HONEST License (when v1.0 exists) or under terms at least as protective of the user.
4. Open a pull request to [`ADOPTERS.md`](./ADOPTERS.md) to be added to the public registry.

There is no certification body. There is no audit. There is no fee. You are publicly held to the principles you declared, and that accountability — between you and your users — is the entire mechanism.

---

## What this repository is NOT

- **It is not a product.** No code is built here. No binaries are released here. The Manifesto and its companions are documents; this repository's purpose is to host them canonically.
- **It is not a foundation yet.** A maintainer-collective entity (foundation, LLC, or similar) is on the roadmap. Until one is formed, all marks and domains are held in good-faith trust by the original maintainer ([@sgireddy](https://github.com/sgireddy)) on terms documented in [`TRADEMARK.md`](./TRADEMARK.md).
- **It is not the website.** [honestsoftware.org](https://honestsoftware.org) will eventually serve a public-facing website rendering these documents. That website will be built at an appropriate time. The canonical *content* lives in this repository regardless.
- **It is not a forum.** Discussion of the Manifesto happens in issues and PRs *on this repository*, but adoption of the Manifesto in any other project's repository is welcome and expected to remain self-organizing.

---

## Contributing

The Manifesto, Inviolata Principle, License Concept, Succession design, and Adopters' Registry evolve through normal pull-request review on this repository. Major version bumps require all current adopters to re-declare; minor edits may proceed without re-declaration.

Suggestions, criticism (including adversarial criticism — we mean it), translations, ports to other legal jurisdictions, and proposed adoptions are all welcome. Open an issue or a PR.

---

## License of these documents

The Manifesto, Inviolata Principle, Succession design, and License Concept are each released under **[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)**. You may copy, modify, and republish — including under different names — with attribution to the source. The point is for the principles to spread, not for any party (us included) to control them.

The names "HONEST," "HONEST Software," "HONEST Manifesto," "HONEST License," and "HONEST-compliant" are governed by [`TRADEMARK.md`](./TRADEMARK.md). Names are gated where claims of identity are made; descriptive, editorial, journalistic, academic, and adversarial-critical use is explicitly permitted.

---

## Contact

For now: open an issue on this repository. As the maintainer-collective entity forms, dedicated channels will be established. Patience is asked of early correspondents; we are explicitly not building the operations of a large foundation on Day 1.

---

*HONEST is a movement. The Manifesto is its primary artifact. Inviolata is its constitutional layer. Designed-In Succession is its load-bearing commitment. The License operationalizes the values legally. The Trademark Policy protects the name. The Adopters' Registry makes adherence visible.*

*This is the work. Read, sign, build, criticize, and improve.*
