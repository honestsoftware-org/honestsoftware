# The Inviolata Principle

**Version 0.1 (Draft) · Released under CC BY 4.0 · Adoption is free**

> ***Domus inviolata*** — *the inviolate home.*
>
> *The user's data, kept under the user's keys, on the user's hardware, is the
> digital extension of their physical home. Extrajudicial access is foreclosed
> in code. Lawful access requires due process between the user and the state.*

---

## What this principle declares

A system honoring **Inviolata** is architected such that:

1. The system's operator **cannot read** end-user content under any
   circumstance, including circumstances where the operator would prefer
   to and circumstances where the operator is legally compelled to.
2. The system's operator **holds no keys, no escrow, no master key, no
   recovery key** for end-user content. Keys live only on user-controlled
   hardware.
3. The system **publicly pre-commits** that no backdoor, lawful-intercept
   capability, exceptional-access mechanism, key-escrow system, or any
   equivalent will be introduced under any name, for any reason, ever.
4. If a jurisdiction mandates such a capability, the system's operator
   **ceases distributing or operating in that jurisdiction** in lieu of
   compliance. (The *Lavabit stance.*)
5. The system is **tamper-evident**: a modified binary is detectable on
   next boot; a silent backdoor push to a single user is mechanically
   prevented.
6. The system supports **user-designed succession**: when the user dies
   or becomes incapacitated, the user — not the operator — has
   pre-designated who can recover the keys and under what protocol.

## Why it is named *Inviolata*

The Latin phrase ***domus inviolata*** — *the inviolate home* — is the
oldest articulation of a principle that runs through every constitutional
democracy: **a person's dwelling cannot be entered without due process.**
The Fourth Amendment of the United States Constitution, Article 8 of the
European Convention on Human Rights, Article 12 of the Universal
Declaration of Human Rights, and the German doctrine of *Unverletzlichkeit
der Wohnung* are all variations on this theme.

The digital home of the AI era — the personal data vault that holds a
human's writing, conversations, health, finances, relationships, and the
AI that has learned them — must be protected by an equivalent
architectural commitment. *Inviolata* is the name we give to that
commitment.

It is not a synonym for "private." Privacy is what we *want*. Inviolata
is what we *enforce in code*, with mechanisms that survive bad-faith
demands by anyone — including the operator, the maintainer, the
investor, the host, and the state.

## What this principle does NOT claim

We owe honesty about the limits, because the alternative — overpromising
— is exactly the failure mode of the surveillance-capitalism era we are
replacing.

| Inviolata *cannot* | And so |
|---|---|
| Prevent the user from being legally compelled to grant access | A court can hold the user in contempt; this is between user and state, not between user and architecture. The right against self-incrimination, the privilege against compelled decryption, and similar protections are matters of jurisprudence, not code. |
| Prevent rubber-hose cryptanalysis | If someone can physically threaten the user, no architecture stops that. |
| Prevent traffic analysis at the network layer absent mixnet routing | Federation protocols can minimize, but not eliminate, metadata leakage on Day 1. |
| Prevent supply-chain compromise of dependencies | Mitigated via reproducible builds, vendored dependencies, and independent audit. Not made impossible. |
| Prevent the user from being socially-engineered into granting access | The UX must make the gravity of grants obvious. The architecture cannot replace user judgment. |

The principle is: **extrajudicial access is foreclosed in code; lawful
access becomes a question between the user and the state, where it
constitutionally belongs.** That is the limit, and it is the right limit.

## Real-world precedent we stand on

We are joining a tradition, not inventing one. Each of these is cited in
this document so that adopters and critics know where the principle
comes from.

| Precedent | What it established |
|---|---|
| **Apple v. FBI** *(San Bernardino, 2016)* | A company can refuse to write a backdoor, even on a single device, even with a court order, even for terrorism investigation. The case was withdrawn before final ruling, but the precedent of refusal stuck. |
| **Signal** | A service can architect itself such that the only data it has to surrender under subpoena is "registration date and last seen" — because that's all it ever held. |
| **Lavabit** *(2013)* | A service can shut itself down rather than comply with a demand for SSL keys. The owner faced contempt charges; the service ended; the principle survived. The "Lavabit stance" is named after this precedent. |
| **WhatsApp v. India** *(2021–ongoing)* | A service can refuse to comply with traceability demands, accepting potential market exit as the cost. |
| **Tutanota / Threema / ProtonMail / Tresorit** | E2E-encrypted services routinely refuse to provide content because they architecturally cannot. They face periodic legal pressure and operate. |

## The seven architectural commitments

A system claiming to honor Inviolata MUST implement all of the following:

### 1. Zero-knowledge architecture

The maintainer, operator, host, and supply-chain participants
**cannot read** end-user content under any circumstance. All user data
is encrypted with keys that live only on user-controlled hardware.
Account recovery via the maintainer is structurally impossible — the
user's own key custody (with their own backup mechanism) is the only
path. There is no master key, no escrow, no "support" override.

### 2. User-controlled keys, hardware-rooted where available

Keys are generated on the user's hardware and never leave it. Where
hardware roots of trust are available (Apple Secure Enclave, Windows
TPM, Linux TPM2, Snapdragon SPU, YubiKey/HSM), they are used to bind
keys to the device. Software-only key custody is the **floor** for
early releases on platforms where hardware roots are unavailable;
hardware roots of trust are the **target** as platforms support them.

Cold-storage backup uses the user's chosen mechanism: BIP-39 seed
written on paper, hardware token, trusted-friend split, or any
equivalent the user trusts. *We provide the cryptographic primitive;
the user designs their own custody.*

### 3. Reproducible builds and transparency log

Every release binary is verifiable against published source code by
any party. Release hashes are published in an append-only public
transparency log (Sigstore-shaped, or equivalent). A modified binary
distributed to a single targeted user is **mechanically detectable**
because that binary's hash will not appear in the transparency log,
and other instances will not corroborate it.

### 4. No backdoor, no lawful intercept, no exceptional access, no key escrow — ever

Under any name, for any reason, at any layer. Including but not
limited to features described as:
- "Lawful intercept"
- "Exceptional access"
- "Responsible encryption"
- "Key escrow" or "trusted third-party recovery"
- "Master key" or "operator key"
- "Child-safety scanning"
- "National-security access"
- "Decryption-on-demand"
- "Account recovery via the maintainer"

This commitment is **non-negotiable** and **pre-stated**. It cannot be
reversed by a future version of this principle without the principle
being renamed; *Inviolata* refers exclusively to the version that
includes this commitment.

### 5. Metadata minimization

Federation protocols are designed to minimize metadata leakage —
who-talks-to-whom, when, how often, from where. Padded constant-time
messaging, sealed-sender protocols, mixnet-style relay with onion
routing, and user-controlled relay choice are the techniques. Day-1
implementations may not deploy all of these; **the design must
accommodate them as they mature**, never foreclose them by
architectural lock-in.

### 6. Tamper-evident architecture

Modifications to the user's binary, trust enclave, or cryptographic
state are **detectable on next boot**. Reproducible builds plus signed
releases plus transparency log plus optional remote attestation
together make this real. If tampering is detected, the system refuses
to unlock without explicit user re-authorization.

### 7. Designed-In Succession (the load-bearing commitment)

This is the *most important* of the seven, and the hardest. The
zero-knowledge commitment (#1) creates an obvious problem: **the user
dies. Heirs need access. The maintainer has no keys.** Without a
designed-in answer to this, every "no backdoor" promise becomes an
excuse for a backdoor later — *"we have to add recovery for the dead-
user case."*

We refuse that excuse. The full design of Designed-In Succession is in
[`SUCCESSION.md`](./SUCCESSION.md). The headline: **the user — not the
maintainer — designs their own succession**, and we provide the
cryptographic primitives.

## Political commitments

A system honoring Inviolata pre-commits, *publicly*, to the following:

### The Lavabit stance

If a jurisdiction mandates a backdoor, lawful-intercept capability,
key-escrow system, or any equivalent — including under the names
"exceptional access," "responsible encryption," "child-safety
exception," "national-security exception," or any other
characterization — the operator **ceases distributing or operating in
that jurisdiction** rather than comply. Notification of the
withdrawal is published openly. The withdrawal is not a panicked
retreat; it is a pre-committed posture, declared in this document
before it is needed.

### Honest about the costs

A system honoring Inviolata accepts:

- **Hostile jurisdictions.** The UK's Investigatory Powers Act, Australia's
  TOLA Act, China's Cybersecurity Law, India's IT Rules 2021 traceability
  mandate, and periodic EU "Chat Control" proposals are hostile to this
  stance. We will face real legal pressure where they apply.
- **Market exit.** We may lose access to entire jurisdictions. We
  accept this as the cost of meaning what we say.
- **Personal legal exposure for maintainers** during the period before
  a maintainer-collective entity is formed.
- **The "going dark" framing** by some law-enforcement and political
  actors. We answer with the lock analogy: *locks on physical homes
  protect every honest occupant; the unavoidable cost is that bad
  actors also benefit from locks; the alternative — a master key for
  authorities — protects no one because the master key inevitably
  leaks.*

### Jurisdictional posture

The maintainer-collective entity for any project claiming Inviolata
should be chartered in a jurisdiction friendly to the principle, with
an explicit secondary jurisdiction prepared in case the primary
becomes hostile. The Inviolata-honoring projects originating from this
movement adopt **United States as primary** (for First Amendment
protection of code-as-speech and the legal precedent of *Apple v. FBI*)
and **Switzerland or Iceland as secondary** (for strong privacy
constitutional traditions and operational independence from US
dependencies).

## Who can claim Inviolata

A project may claim to honor the Inviolata Principle when it
implements all seven architectural commitments and pre-commits
publicly to all the political commitments above. Adherence is
self-declared, on the same model as the [HONEST Manifesto's Adopters'
Registry](./ADOPTERS.md) — no certification body, no audit, no fee.

A project that introduces a feature violating any of the architectural
commitments **must immediately drop the Inviolata claim** until the
feature is removed. Public misrepresentation is a trademark violation
under [`TRADEMARK.md`](./TRADEMARK.md).

This is a *high bar*. We expect few projects to meet it on Day 1. That
is correct. The principle is meaningful precisely because it is
demanding.

## Relationship to the HONEST Manifesto

Inviolata is the **constitutional layer** of the HONEST movement. The
[HONEST Manifesto](./MANIFESTO.md) declares the six pillars that HONEST
software *does* (Honest, Owned, Network-free, Ephemeral, Sealed,
Transparent). Inviolata declares what HONEST software *will not betray
under any pressure*.

A project may honor Inviolata without claiming HONEST adherence (the
seven commitments are themselves a complete principle). A project
claiming HONEST adherence must honor Inviolata as the constitutional
layer of HONEST itself — there is no HONEST adherence that is not also
Inviolata adherence.

## Versioning

This document is **v0.1**. The principle is intended to remain stable;
the architectural specifics may evolve as cryptographic primitives,
hardware capabilities, and jurisdictional realities change. Major
version bumps require all adherents to re-declare; we will not silently
shift the bar.

---

*The Inviolata Principle v0.1 — companion to the [HONEST Software Manifesto](./MANIFESTO.md). Released under [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/). Adoption is free. Citation by other projects is encouraged. The principle becomes stronger every time it is honored.*
