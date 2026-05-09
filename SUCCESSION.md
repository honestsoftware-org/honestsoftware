# Designed-In Succession — v0.1

> **The hardest case for *Inviolata*.**
>
> A system that holds no keys cannot grant access on the user's death. If
> we do not design an answer to this from Day 1, every future demand for a
> backdoor — *"surely you must have something for the dead-user case"* —
> becomes a wedge to break the architecture. **This document is the
> answer.**

---

## The problem, stated honestly

Three things are simultaneously true:

1. **No backdoor.** *Inviolata* commits us, in code and in policy, to never
   hold a master key, recovery key, or escrow key for end-user content.
   This is non-negotiable.
2. **People die.** Their families, executors, business partners, co-authors,
   research collaborators, and (if the user wishes) the public — may have
   legitimate, sometimes urgent, sometimes legally-mandated, claim to access
   the user's data after the user is gone.
3. **The maintainer cannot adjudicate this.** Even if we wanted to be the
   "trusted third party" who decides who gets access — we should not be.
   The decision belongs to the user, not us.

These three constraints rule out:
- ❌ Maintainer-held recovery keys *("just in case")*
- ❌ Maintainer-mediated dispute resolution *("contact us if a family member dies")*
- ❌ Court-orderable decryption from the operator *("we'll comply with valid orders")*
- ❌ "Account recovery" in any form that touches the maintainer
- ❌ Any mechanism whose existence becomes a target for legal compulsion

The only remaining design space is: **the user pre-decides their own
succession, and the cryptographic mechanism works without the maintainer
in the loop.**

This is a hard problem. It is also a tractable one. Below is the design.

---

## The principle: user-designed succession

> **The user designs the succession protocol. We provide the cryptographic
> primitives that make it enforceable without our participation.**

This means:

- The user chooses **who** their heirs are (one person, several, an
  institution, no one).
- The user chooses **how many** of those heirs must agree to act (any
  one of N, a quorum of K-of-N, all of N, or — explicitly — *none*: the
  vault dies with the user).
- The user chooses **what triggers** the succession protocol (death
  certificate, executor's affidavit, dead-man's-switch timeout,
  multi-party "we both agree this human is no longer responding," or
  combinations).
- The user chooses **what scope** the heirs receive (full access; specific
  compartments only — "medical to my doctor, financial to my executor,
  personal to my spouse"; time-limited access; read-only access).
- The user can **change any of the above** at any time, while alive.

The cryptographic mechanism executes the user's design. We do not
participate; we cannot override; we cannot revoke. The heirs do not
contact us.

---

## The cryptographic primitive: Shamir's Secret Sharing

The mathematical tool that makes user-designed succession work is
**Shamir's Secret Sharing** (Adi Shamir, 1979). It allows a secret to be
split into N shares such that any K shares can reconstruct it, but K-1
shares reveal nothing. K-of-N is configurable independently per share-set.

In our case, the "secret" is the user's vault master key (or, more
precisely, a *succession key* derived from it — see §"Key hierarchy"
below). The "shares" are distributed to designated heirs. The user
configures K and N when they set up succession.

Worked example:

> Alice configures **3-of-5 succession**:
> - Share 1 → her spouse Bob
> - Share 2 → her sister Carol
> - Share 3 → her attorney
> - Share 4 → her primary-care physician *(scoped: medical compartment only)*
> - Share 5 → a sealed envelope in her safe deposit box
>
> When Alice dies, **any 3 of those 5 share-holders** can combine their
> shares to reconstruct the succession key. The vault opens. Without 3
> shares, the vault remains sealed forever.

Shamir's scheme is mature, well-understood cryptography. It is used by
Bitcoin custody (Trezor's SLIP-39), HashiCorp Vault, and dozens of
production systems. It does *not* require a third-party server. It does
*not* require the maintainer's participation. **It is exactly the
primitive Inviolata needs.**

---

## The trigger problem (and how the user solves it)

Distributing key shares is the easy part. The hard part is: **what makes
the heirs decide it is time to combine their shares?**

This is where the design must avoid centralization. We cannot be the
party that says "Alice has died, Bob may now reconstruct." The user must
configure the trigger themselves.

Three trigger families are supported, in order from simplest to most
sophisticated. The user picks one or composes them.

### Trigger Family A — Out-of-band human protocol

**The default.** The user instructs their heirs in plain English: *"If I
die, take your shares, meet at the attorney's office, combine them."*
The heirs follow the instructions because the heirs are people who
loved or worked with the user, not because of any technical mechanism.

The cryptographic system **does not enforce a trigger**; it simply
makes the shares useless individually and useful collectively. Whether
collection happens is a human decision by the heirs.

**Pros:** Simple. No additional infrastructure. No attack surface.
Aligned with how families actually handle estates today.

**Cons:** Heirs may collude to act before the user has actually died.
*(The user mitigates this by selecting trustworthy heirs, by requiring
quorum, and optionally by adding Trigger Family B or C.)*

### Trigger Family B — Dead-man's-switch timeout

The user's vault sends a regular "I am still alive" heartbeat to the
heirs (encrypted, P2P, no maintainer involved). If the heartbeat stops
for a user-configured duration (30 days, 90 days, 1 year — user
chooses), the heirs are notified that the dead-man's-switch has
elapsed and they may proceed to combine shares.

Implementation note: the heartbeat is **outbound only from the user's
vault**, sent via federated peer protocol. It does not require any
central server. If the user is alive but their vault is offline (long
trip, hardware failure), the user can pre-emptively reset the timer
from any of their configured devices, or extend it for an upcoming
absence.

**Pros:** Fully automated. No human notification step required. The
switch elapses if the user genuinely cannot reach a device.

**Cons:** False positives (user is alive but offline). User must
configure a tolerance window appropriately.

### Trigger Family C — Oracle-witnessed events

The user designates one or more **oracles** — services that publish
verifiable facts the user trusts. Examples:

- **Government death-certificate registry** (where it exists publicly).
- **Funeral home cryptographic attestation** (an emerging standard).
- **Designated executor's signed declaration** (the executor holds a
  key; their signature on a "person is deceased" message is the
  trigger).
- **Multi-signature human-witness declaration** (e.g., 2-of-3
  designated witnesses sign "we attest this person is deceased").

The oracle's signed message is the trigger. The cryptographic protocol
verifies the oracle's signature against the user's pre-registered
oracle public keys before share-combination is considered valid.

**Pros:** Strong evidence. Hard to fake. Aligns with how legal
systems already verify death.

**Cons:** Depends on the oracle being available at trigger time.
Composes well with Trigger Family A and B as backups.

### Composition

Triggers compose. A user can specify:

> *"3-of-5 share quorum AND ((death-certificate-oracle signature) OR
> (90-day dead-man's-switch elapsed))."*

The cryptographic protocol enforces the boolean logic. The user defines
the logic in their succession config; we provide the verifier.

---

## Scope: not all heirs see everything

Modern people's data is heterogeneous. A spouse should arguably see
personal correspondence and family photos. A primary-care physician
should arguably see medical history but not financial records. An
executor should arguably see financial records but not personal
correspondence. *Designing succession in a way that respects these
distinctions* is part of honoring the user's wishes.

The vault is divided into **compartments**: medical, financial, personal,
professional, custom (user-defined). Each compartment has its own key.
The succession config can specify *per-compartment* share distributions:

> Alice's design:
>
> - **Personal & family** compartment: 2-of-3 (spouse Bob, sister Carol,
>   safe-deposit envelope)
> - **Financial** compartment: 2-of-3 (attorney, executor, safe-deposit envelope)
> - **Medical** compartment: 2-of-3 (spouse Bob, primary physician, attorney)
> - **Professional** compartment: 1-of-2 (her co-author, her university
>   archives) — for posthumous publication of unfinished work
> - **Truly private journal** compartment: **0-of-N**, i.e., dies with her

The cryptographic mechanism: each compartment's encryption key is
independently Shamir-split, with its own K-of-N parameters and its own
share recipients. A heir who holds shares for one compartment cannot
unlock a different compartment unless the user's design grants them
shares there too.

---

## The "dies with her" case

Some compartments — the user's *truly private* writing, perhaps — should
**never be readable by anyone after the user's death**. The user must be
able to specify this and have it enforced.

Mechanism: those compartments are encrypted with a key for which **no
shares exist**. The key lives only in the user's hardware-rooted custody.
On the user's death, with no shares to reconstruct from, the
ciphertext becomes mathematically inaccessible. Permanently.

This is a feature, not a bug. The user's right to have private thoughts
that die with them is part of the inviolate-home principle. We support
it explicitly.

---

## Key hierarchy (cryptographic detail)

For implementers, the key hierarchy is:

```
                    User Master Seed
                    (BIP-39 / hardware-bound;
                     never leaves user's custody)
                            |
        +-------------------+-------------------+
        |                                       |
  Compartment Keys                       Succession Key
  (one per compartment;                  (derived deterministically;
   used for daily operation)              used only for succession)
        |                                       |
   [encrypted user data]              Shamir-split N ways
                                              |
                              +---------+-----+----+----------+
                              |         |          |          |
                          Share 1   Share 2   Share 3 ... Share N
                          (Bob)    (Carol)  (Attorney)  (Safe deposit)
```

- The **User Master Seed** never leaves the user's hardware. It is
  generated on first boot, optionally written to a paper backup by the
  user, optionally protected by a hardware token.
- **Compartment Keys** are derived from the master seed via a
  deterministic KDF. Each compartment has a distinct key.
- The **Succession Key** is *also* derived from the master seed, but is
  the only key that gets Shamir-split. It is not used in normal vault
  operation; it is used *only* to derive the compartment keys when
  succession is invoked.
- **Shamir splitting** happens at the Succession Key level. The shares
  are distributed when the user sets up succession. Each share is a
  short string (or QR code, or NFC-readable token) that the heir holds
  off-line.
- When a quorum of share-holders combine their shares (per user's
  K-of-N configuration), they reconstruct the Succession Key, which
  unlocks the compartments the user assigned them.

---

## What the maintainer never sees, ever

Throughout the entire succession process, the maintainer (us, or any
operator of an Inviolata-honoring system) sees: **nothing**.

- We do not generate the master seed. The user's hardware does.
- We do not see compartment keys. They are computed locally.
- We do not see the Succession Key. It is derived locally, split locally.
- We do not distribute shares. The user does, off our infrastructure.
- We are not notified of the user's death. Heirs handle it.
- We do not validate triggers. The user's chosen oracles do.
- We do not unlock compartments. The reconstructed key does.

Our role is **publishing the open-source library** that implements
Shamir's scheme correctly, the trigger verifiers, the compartment
abstractions, and the audit log. Adherence is verifiable by inspection
of the code. We have no operational role.

This is what makes the no-backdoor commitment honest. **There is no
exception to be carved out for the dead-user case, because the dead-
user case never touches us.**

---

## What the user has to actually do

For the user, succession setup is a one-time-with-occasional-updates UX:

1. **Decide the model.** *("Who, how many, what triggers, what scope.")*
   The vault provides templates: "spouse + executor + sealed envelope,"
   "trusted family member only," "die-with-me," "professional executor"
   etc. The user can use a template or design custom.
2. **Identify the heirs.** Each heir gets one or more shares. The vault
   generates the shares; the user delivers them — printed paper, QR
   codes, NFC tokens, hardware-token enrollment, encrypted-to-recipient
   email.
3. **Configure the triggers.** Out-of-band only (default), dead-man's-
   switch (with timeout), oracle-witnessed (with chosen oracles), or
   composed.
4. **Test the recovery process.** Crucially: the vault provides a
   *dry-run* mode where heirs can verify they hold valid shares
   *without* the user being dead. This is the same UX 1Password Family
   Recovery uses; it works. Periodic re-tests are encouraged.
5. **Update on life events.** Marriage, divorce, death of an heir, new
   executor, change of attorney — the user updates the share assignment.
   Old shares are invalidated cryptographically (via re-keying); new
   shares are issued.

The vault makes step 4 ("dry-run") **mandatory at setup**: succession
is not "configured" until the user has watched their designated heirs
successfully reconstruct a test secret. This is the single most important
UX commitment, because succession plans that have never been tested are
the ones that fail when needed.

---

## Limitations and honest open questions

I want these documented before any code is written, so they can be
addressed deliberately rather than discovered at the worst possible time:

1. **Heir security education.** Heirs holding shares need to understand
   what they hold and how to protect it. A share written to paper and
   kept in a sock drawer is approximately as secure as the sock drawer.
   The vault must provide *guidance* to heirs, but cannot enforce their
   key-management practices.
2. **Heir mortality.** Heirs die too. The user must update their
   succession plan as heirs die. The vault should periodically prompt
   the user to verify their heirs are still alive and capable.
3. **Estranged-heir attack.** A divorced spouse who once held shares may
   try to combine them with another former-heir to recover the vault
   maliciously. The user must rotate succession shares at every
   relationship change. The vault should make this easy.
4. **Coerced heir.** A bad actor may threaten an heir to combine shares.
   This is the same problem physical-world succession faces; we offer
   no novel solution. Mitigation: K-of-N with K geographically
   distributed, K diverse-relationship, and the option of an institutional
   share (attorney, bank safe-deposit) that requires institutional
   process.
5. **Quorum lost (heir count drops below K).** Several heirs die before
   the user; quorum becomes mathematically unreachable. The vault must
   detect this and warn the user. Recovery: user re-keys with new shares.
6. **Cross-jurisdictional execution.** If heirs live in different
   countries, share-combination may need to happen in a single
   jurisdiction for legal recognition of the resulting access. This is
   an estate-planning question, not a cryptographic one — but the vault
   should help the user think about it.
7. **The pre-mortem incapacity case.** The user is alive but
   incapacitated (coma, advanced dementia). Trigger Family A relies on
   heirs deciding to act; Trigger Family B will trigger eventually but
   may be slow; Trigger Family C with a "designated medical proxy
   attestation" oracle is the cleanest answer. The user should configure
   this case explicitly.
8. **The vault's own failure mode.** If the user's vault hardware fails
   while they are alive, succession should *not* trigger. The vault must
   distinguish "user is dead" from "user's hardware died" — typically
   by sending heartbeats from multiple devices, or by the user keeping
   a recovery procedure separate from the succession procedure.

These are real problems. They have real answers. The first version of
the vault will not solve all of them perfectly. **The principle is to
make the user's design space rich enough that they can solve the case
that matters most to them, even if we cannot solve every case for every
user.**

---

## What this commits us to building

For the substrate engineers, this section enumerates Day-1 deliverables
that flow from this design:

1. A correct, audited implementation of **Shamir's Secret Sharing**, with
   support for any K-of-N up to a reasonable bound (say N≤16, K≤N).
   Reference: SLIP-39 specification, or libgfshare.
2. A **succession config schema** (declarative, signable, versionable)
   describing the user's design.
3. A **trigger verifier** for each Trigger Family (A: trivial; B:
   heartbeat protocol; C: oracle signature verification).
4. A **share generation, distribution, and storage UX** with multiple
   delivery formats (printed paper with QR, hardware tokens, encrypted
   email-to-recipient, NFC).
5. A **mandatory dry-run** flow that simulates succession with the heirs
   and the user alive, verifying that share reconstruction works
   end-to-end.
6. A **succession update flow** that rotates shares cleanly on relationship
   changes.
7. **Compartment-aware succession** — per-compartment key splitting and
   per-heir scope assignment.
8. **An audit log** of all succession-related events, queryable by the
   user during their lifetime, queryable by heirs after.
9. **Heir-side software** — a small, focused tool for heirs to combine
   their shares, present the trigger, and unlock the compartments they
   are entitled to. Critically: this software must work *without* the
   maintainer's infrastructure being available, since the maintainer
   may have ceased to exist by the time the user's heirs need it.
10. **An offline test-vector suite** so any third party can verify our
    Shamir implementation, our trigger verifiers, and our compartment
    abstractions correctly enforce the user's design.

This is **substantial engineering**. It is also non-negotiable. A vault
that does not offer designed-in succession is a vault that will
eventually be coerced into adding a backdoor.

---

## Versioning

This document is **v0.1**. Revisions will be needed as we encounter real
user designs that the current model cannot express, as cryptographic
primitives mature (post-quantum Shamir variants, threshold signatures,
witness encryption), and as the legal landscape around digital estate
inheritance evolves.

The principle — *the user designs their own succession; we provide
cryptographic primitives without operational involvement* — is intended
to remain stable across versions.

---

*Designed-In Succession v0.1 — companion to [`INVIOLATA.md`](./INVIOLATA.md), which is the constitutional layer of the [HONEST Software Manifesto](./MANIFESTO.md). Released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Adoption is free.*
