# The HONEST License — Concept Document v0.1

> **STATUS — DRAFT, NOT ENFORCEABLE LEGAL TEXT.**
>
> This document describes the *intent* of the HONEST License. It is not the
> license itself. Before any HONEST-licensed work ships, this concept must be
> rendered into enforceable legal text by a qualified IP/licensing attorney
> with experience in source-available and behavioral licensing (e.g.,
> practitioners in the orbit of Heather Meeker / PolyForm, Kyle Mitchell, or
> the Organization for Ethical Source / Hippocratic License).
>
> **Until that legal text exists, the source in this repository is licensed
> as "All Rights Reserved" with viewing permitted for review purposes only.**
> Any contributor or reader who relies on this concept document as a license
> grant does so at their own risk.

---

## 1. Purpose

The HONEST License is the legal mechanism that operationalizes [the HONEST
Software Manifesto](./MANIFESTO.md). It exists to ensure that work licensed
under it cannot be used to build software that violates the principles the
Manifesto declares.

The License grants broad, free, perpetual rights for **uses that honor the
filial duty of software to its end user** (in Sanskrit philosophical
tradition, *Loka-hita-niṣṭhā*; in Latin, *pietas erga utentem*). It withholds
those rights from uses that would invert that duty.

It is deliberately not OSI-approved. The OSI Open Source Definition forbids
discrimination against fields of endeavor; the HONEST License's entire
purpose is to discriminate — narrowly and precisely — against fields of
endeavor that betray the user. We accept the cost of being outside the OSI
boundary in exchange for the integrity of the principle. We believe, with
evidence from a generation of software history, that the OSI definition has
served extractive cloud appropriation more than it has served users; we
decline to defer to it.

---

## 2. Plain-language summary (not legally binding)

If you are an **individual, family, household, school, library, public
hospital, charitable organization, or research institution** using HONEST
software for purposes other than running an extractive product on top of it
— **this license costs nothing, restricts nothing further, and grants you the
broadest rights any free-software license offers**. You may use, copy,
modify, redistribute, and self-host without restriction. You may run it for
your friends, your family, your students, your patients, your community.

If you are a **commercial or institutional operator** who runs HONEST
software as part of a product or service offered to others — **the license
imposes one substantive obligation: your product must itself honor the six
HONEST pillars toward your end users.** No telemetry. No data harvesting. No
engagement-metric optimization. No dark patterns. No habit-formation by
design. No selling, sharing, or transmitting user data. If you cannot accept
these terms, you may not use this software in your product.

That is the entire deal. Live by the same duty toward your users that we
live by toward ours, or do not use our work.

---

## 3. The grant

Permission is granted, perpetual, worldwide, royalty-free, non-exclusive,
and irrevocable (subject to the Conditions in Section 4 and the Termination
in Section 6), to:

- **Use** the licensed work for any lawful purpose.
- **Copy, modify, and prepare derivative works.**
- **Distribute** the work and derivative works in source or compiled form.
- **Run** the work, including as part of a product or service offered to
  third parties, **subject to Section 4.**

---

## 4. Conditions

The grant in Section 3 is conditioned on the following. Each condition
operationalizes a pillar of the HONEST Manifesto. A licensee complying with
all of them is in good standing under this license; a licensee violating
any of them, with respect to the licensed work or any product, service, or
derivative built on or substantially containing the licensed work, loses
the grant under Section 6.

### 4.1 Honesty toward the end user

A product or service that incorporates the licensed work shall:

- **Cite evidence** for any factual claim it asserts to the end user that
  was derived from the end user's data, or refuse to assert it.
- **Disclose model belief vs. retrieved fact** distinguishably in any
  user-facing output.
- **Permit the end user to inspect** the evidence chain for any answer.
- **Not represent unverified output as verified.**

### 4.2 Ownership by the end user

A product or service that incorporates the licensed work shall:

- **Treat the end user as the sole owner** of the user's primary data, all
  derived state computed from it, all embeddings and indices built from it,
  and all model adaptations (fine-tunes, LoRAs, preference data) trained on
  it.
- **Provide complete export** of all such state in open, documented formats,
  on user request, without delay or paywall.
- **Not retain** any copy of the user's data, derived state, or model
  adaptations after the user requests deletion, including in backups,
  caches, training-data archives, or feature-store warehouses.

### 4.3 Network discipline

A product or service that incorporates the licensed work shall:

- **Not collect telemetry of any kind** from the end user — including but
  not limited to usage analytics, performance telemetry, feature-flag
  reporting, model-output collection, prompt-and-completion logging, error
  beacons, "anonymous" aggregations, or any data flowing from the user's
  device to the operator's systems other than data the user has explicitly
  requested be transmitted for that user's own purposes.
- **Not transmit user data to third parties** under any condition, including
  advertising networks, analytics vendors, model-training pipelines, or
  affiliated entities.
- **Not require network reachability** as a condition of basic function,
  except for narrowly-scoped, user-invoked operations (e.g., software
  updates) that are documented, time-bounded, and disabled by default
  during normal operation.

### 4.4 Ephemeral peripheral access

A product or service that incorporates the licensed work shall:

- **Not hold open** the end user's microphone, camera, screen-capture,
  accessibility APIs, clipboard subscriptions, or push-notification streams
  in an ambient or "always-listening" mode.
- **Open peripherals only** when explicitly invoked by the end user, for the
  duration of that invocation, and release them immediately upon completion.
- **Log every peripheral open/close** to a user-inspectable audit record.

### 4.5 Sealed boundary

A product or service that incorporates the licensed work shall:

- **Make every input, output, and computation** the result of a deliberate,
  scoped, user-authorized decision.
- **Not execute** code embedded in user-supplied content (PDF JavaScript,
  Office macros, HTML+JS rendering of user files) without explicit user
  invocation.
- **Not autoplay** media or pre-fetch user content.

### 4.6 Transparency

A product or service that incorporates the licensed work shall:

- **Publish source code** of any modifications made to the licensed work,
  under terms no more restrictive than this license, when distributing
  binaries to end users or operating the modified work as a network service.
- **Document file formats** used to store user data and derived state.
- **Make derived state regenerable** from the user's primary data alone.

### 4.7 Filial duty (the umbrella clause)

A product or service that incorporates the licensed work shall not engage
in practices that subordinate the end user's interest to the operator's, or
to any third party's, including but not limited to:

- **Engagement-metric-driven design** — optimizing the product to maximize
  user time-in-app, daily-active-users, monthly-active-users, retention
  curves, or any metric that measures the user's *consumption* of the
  product rather than the product's *resolution* of the user's needs.
- **Habit-formation patterns** — variable-reward schedules, streaks, badges,
  artificial scarcity, autoplay, infinite scroll, dark-pattern dialogs,
  FOMO triggers, or other techniques drawn from the literature of behavioral
  conditioning and applied to consumer software.
- **User-data monetization** — selling, renting, sharing, or otherwise
  transmitting end-user data to any third party, or using it to train models
  used in products other than the one the user is operating, for monetary
  or non-monetary gain.
- **Surveillance of the user** for the operator's benefit or any third
  party's benefit, including profiling, behavioral tracking, or aggregation
  across users without each user's individual, informed, revocable consent.
- **Advertising, sponsored content, or paid placement** of any kind within
  the product surface presented to the end user.

These prohibitions apply whether the practice is described as "free,"
"freemium," "ad-supported," "for research," "for safety," "for product
improvement," or under any other characterization.

### 4.8 Federation discipline (placeholder)

*This subsection is reserved for federation-specific licensing terms
(capability-mediated peer-to-peer access, owner-sovereign data flow
direction, doctor/institution-to-vault write semantics, etc.). It will
be drafted as part of the Federation work-stream. Until then, the
existing §4.3 Network discipline governs all federation between vaults
under the same condition: explicit, user-authorized, time-bounded.*

### 4.9 Inviolata — the Constitutional Layer

A product or service that incorporates the licensed work shall, at all
times, honor the **Inviolata Principle** as declared in
[`INVIOLATA.md`](./INVIOLATA.md) and the [`MANIFESTO.md`](./MANIFESTO.md).
This subsection operationalizes that commitment as license terms.

A product or service that incorporates the licensed work shall NOT, at
any time and under any circumstance:

- Implement, ship, deploy, maintain, or distribute any **lawful-intercept
  capability, exceptional-access mechanism, key-escrow system,
  master-key infrastructure, decryption-on-demand workflow, operator
  recovery key, mandatory account-recovery channel, or any equivalent
  feature** by whatever name, at any layer, for any purpose. This
  prohibition includes — but is not limited to — features described as:
  "lawful intercept," "exceptional access," "responsible encryption,"
  "key escrow," "trusted third-party recovery," "operator master key,"
  "child-safety scanning," "national-security access,"
  "decryption-on-demand," or "account recovery via the maintainer."
- Hold any **decryption keys, recovery keys, escrow keys, or session
  keys** for end-user content other than those held by the end user
  themselves on hardware they control.
- Architect any system component such that the operator can read
  end-user content under any circumstance, **including circumstances
  where the operator is legally compelled to do so**.
- Implement any **silent-update channel, hot-patch capability, or
  remote-modification mechanism** that could be used to introduce a
  backdoor without user-detectable change. All updates shall be
  signature-verified, user-invoked, and verifiable against a public
  append-only transparency log.
- Distribute binaries that **cannot be reproducibly built** from the
  published source by an independent third party.
- Omit **Designed-In Succession**: a product that holds end-user data
  must provide cryptographic mechanisms for the user to pre-design
  their own succession (heir designation, K-of-N quorum, configurable
  triggers, compartment-aware key splitting, mandatory dry-run testing)
  so that no future demand for "the dead-user case" becomes a wedge to
  introduce a backdoor. The detailed design is in
  [`SUCCESSION.md`](./SUCCESSION.md).

A product or service that incorporates the licensed work SHALL:

- Generate cryptographic keys for end-user content **only on
  user-controlled hardware**, with hardware roots of trust where
  available (Apple Secure Enclave, Windows TPM, Linux TPM2, Snapdragon
  SPU, hardware tokens), and software-only custody as the floor where
  hardware is unavailable.
- Publish all release binaries with **signed release hashes** in an
  append-only public transparency log.
- Make all source code **publicly available** at the time of binary
  release, in a form sufficient for reproducible builds.
- Provide **tamper detection on next boot** so that modifications to
  the user's binary or trust enclave are mechanically discoverable.

### 4.9.1 The Lavabit clause

A licensee compelled, by legal process or governmental directive, to
introduce any of the prohibited capabilities in §4.9 into their product
or service **shall, in lieu of compliance, cease distributing or
operating that product or service in the affected jurisdiction**, and
shall publicly notify their end users that operations have ceased and
the reason therefor (to the extent permitted by gag orders; if a gag
order prohibits such notification, the licensee shall implement a
*warrant canary* mechanism so that the end user community can detect
the existence of compelled action).

This clause is named after Ladar Levison's 2013 decision to shut down
Lavabit rather than comply with a US government demand for SSL keys.
**It is non-negotiable. It is the price of holding the HONEST License.**
A licensee who instead complies with such a directive is in material
breach of this license and shall lose the grant under §6.

### 4.9.2 No retroactive amendment

The architectural commitments in §4.9 cannot be reversed by a future
version of this license without renaming the license itself. Any
license whose name includes "HONEST" or which claims compliance with
the HONEST Manifesto must include §4.9 commitments at least as strong
as those declared here.

---

## 5. Safe harbor

A licensee who:

- **Publishes a Filial Duty Statement** describing how their product
  honors each of the conditions in Section 4, with concrete operational
  detail, in a publicly-accessible location;
- **Updates that Statement** within 30 days of any material change to the
  product;
- **Submits to good-faith inquiry** from end users and the public regarding
  compliance with that Statement;

shall be **presumed compliant** under this license absent clear evidence to
the contrary. The Filial Duty Statement is not approved or audited by any
central body. It exists as the licensee's public commitment, on the same
basis as the HONEST Manifesto itself.

---

## 6. Termination and cure

### 6.1 Cure period

A licensee in violation of Section 4 shall have **90 days from written
notice** of violation, delivered to a contact published in their Filial
Duty Statement (or to a publicly-listed corporate officer if no Statement
exists), to cure the violation.

### 6.2 Termination

If the violation is not cured within the cure period, the grant under
Section 3 **automatically terminates** with respect to the licensee. The
licensee shall, within 30 days of termination:

- Cease all use, distribution, and operation of the licensed work and any
  derivative work substantially containing it.
- Destroy or return all copies in their possession.
- Notify their end users that the operator has lost the right to operate
  this software.

### 6.3 Reinstatement

A terminated licensee may apply for reinstatement by:

- Curing the original violation.
- Publishing a public statement of the violation, the cure, and the
  controls put in place to prevent recurrence.
- Waiting 12 months from the date of cure.

The licensor (or the maintainer-collective designated as licensor) is under
no obligation to grant reinstatement.

---

## 7. Definitions

- **"Licensed work"** — the source code, binaries, data, models, and
  documentation distributed under this license by the original licensor or
  any subsequent licensee in good standing.
- **"Product or service"** — any artifact, system, application, website,
  hosted service, embedded system, or other deliverable that incorporates
  the licensed work, in source or binary form, in whole or in substantial
  part.
- **"End user"** — the natural human person whose use of the product or
  service is the proximate purpose of the product's or service's
  existence. The end user is not the licensee, the operator, or any
  intermediating institution.
- **"Filial duty"** — the duty intrinsic to the asymmetric relationship in
  which the software exists in service of the end user, and owes the end
  user the loyalty a child owes a parent: care, transparency, defense, no
  betrayal. In Sanskrit philosophical tradition, *Loka-hita-niṣṭhā*. In
  Latin, *pietas erga utentem*. The two are equivalent.
- **"User data"** — data created, contributed, captured, or stored by the
  end user, or derived from the end user's behavior or biometric, contextual,
  or environmental signals captured by the product or service.

---

## 8. Trademark

This license does not grant rights to use the names "HONEST," "HONEST
Software," "HONEST Manifesto," "HONEST License," "HONEST-compliant,"
"VaultAI," or any associated logos or marks. Such use is governed by
[`TRADEMARK.md`](./TRADEMARK.md), which is currently a placeholder
(v0.1) — no marks are yet filed, but the *intended* policy is described
there so that good-faith adopters know what they are agreeing to in
advance.

---

## 9. Disclaimer and limitation of liability

The licensed work is provided "AS IS," without warranty of any kind,
express or implied, including but not limited to warranties of
merchantability, fitness for a particular purpose, and non-infringement. In
no event shall the licensors be liable for any claim, damages, or other
liability, whether in an action of contract, tort, or otherwise, arising
from, out of, or in connection with the licensed work or the use or other
dealings in the licensed work.

*(Standard limitation language; final form to be drafted by counsel.)*

---

## 10. Severability

If any provision of this license is found by a court of competent
jurisdiction to be unenforceable, the remainder shall continue in full
force and effect. The provisions of Section 4 are the substantive purpose
of this license; if Section 4 in its entirety is held unenforceable, the
license itself is void *ab initio* and the licensed work reverts to "All
Rights Reserved" status with respect to the affected jurisdiction.

---

## 11. Versioning

This concept is **v0.1**. The final license text, once drafted by counsel,
will be **HONEST License v1.0**. The Manifesto and License version
independently. A project may declare adherence to *HONEST Manifesto v0.1*
while licensing its code under *HONEST License v1.0* (or any future minor
revision). Major version bumps require explicit re-adoption.

---

## 12. What we still need

To move this from concept to enforceable license, we need:

1. **Counsel review.** Real attorney drafting, with comparison to PolyForm
   Noncommercial 1.0.0, Hippocratic License 3.0, the Functional Source
   License, and the Business Source License. Estimated cost: $5–15k for the
   initial draft, plus ongoing review for amendments.
2. **Jurisdictional analysis.** This license must be enforceable in at
   least the US, EU, UK, India, and Canada. Each jurisdiction treats
   behavioral licensing terms differently.
3. **A dispute-resolution mechanism.** Who decides whether a licensee has
   violated Section 4? The current draft leaves this to ordinary
   contract-law processes (litigation), which is expensive and slow. We
   should consider adding a mediation step before termination.
4. **A maintainer-collective entity** (foundation, LLC, or similar) to hold
   the trademark and act as licensor for this work. An individual maintainer
   carries personal legal exposure that a properly-formed entity can
   diffuse.
5. **An Adopters' Registry mechanism**, such that other projects can adopt
   this license cleanly without inheriting our specific jurisdictional or
   organizational details.

This work is **non-trivial and non-cheap**. It is the price of meaning what
we say. It will not be done by Day 1 of VaultAI; it will be done by the
time VaultAI ships under HONEST License v1.0 to actual users.

---

## 13. Until then

This repository is, **legally**, licensed as follows:

> **Copyright (c) 2026 the VaultAI maintainers.**
>
> **All rights reserved.** This source is published for review,
> commentary, and contribution under a Contributor Agreement
> (forthcoming). It is not yet licensed for use in production, in
> derivative products, or in any commercial or non-commercial
> distribution. The HONEST License v1.0, once drafted by counsel and
> ratified, will replace this notice and grant the rights described
> above under the conditions described above.

This is the honest current state. No fudging it.

---

*The HONEST License Concept v0.1 — companion to [the HONEST Software Manifesto](./MANIFESTO.md). Released under CC BY 4.0 as a concept document. The eventual HONEST License v1.0 will govern code, not concept.*
