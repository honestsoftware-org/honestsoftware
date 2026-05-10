# The Federation Concept — *Owner-Sovereign Federation*

**Version 0.1 (Concept)** — *companion to [`MANIFESTO.md`](./MANIFESTO.md), [`INVIOLATA.md`](./INVIOLATA.md), and [`SUCCESSION.md`](./SUCCESSION.md). Released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) so other projects may adopt the same architectural direction.*

> ***Owner-Sovereign Federation*** *— each vault is a first-class peer. No node is more authoritative than any other for its own data. All trust between vaults is graph-shaped, user-owned, scoped, time-bounded, and revocable. There is no Identity Provider. There is no operator-mediated lookup. There is no central directory. There is no node whose absence breaks anyone else's vault.*

This document is a **concept**, not a wire protocol. It declares the *shape* federation must have to compose with the [Inviolata Principle](./INVIOLATA.md) — a centralized identity layer or operator-mediated trust directory would silently undo every architectural commitment Inviolata makes — and the *direction* a wire protocol drafted later must satisfy.

The purpose of writing it now, *before* a single byte of federation code is shipped, is the same as the purpose of writing Inviolata before a single backdoor demand is received: **decisions made under pressure are different from decisions made on the merits.** Federation, especially, is the layer where every privacy commitment is most easily silently compromised. Hence: pre-stated, in writing, in the public record.

---

## 1. What this document is, and what it is not

**This document is** the architectural-layer commitment that VaultAI, and any HONEST-aligned project that follows the same direction, will federate vaults *peer-to-peer with user-owned trust graphs* and **never** via a central identity provider, a central directory, an operator-held trust ledger, or any equivalent mechanism that would re-introduce the very class of dependency Inviolata exists to refuse.

**This document is not:**

- A **wire protocol specification.** Specific cryptographic primitives, transport choices, message formats, and key-rotation algorithms are deferred to a separate Federation Protocol Specification.
- A **scheduling commitment.** Federation between vaults is not a Day-1 deliverable for VaultAI. The Manifesto's *N* (Network-free) pillar makes federation an *opt-in capability* that must compose with the kernel-enforced phase separation (FR-55), never become ambient.
- A **guarantee that federation is even desirable for every user.** Many users will run a single vault on a single machine, federate with no one, and that is the supported and architecturally-blessed default. Federation must reward those who opt into it without penalizing those who do not.
- The **trust-graph schema.** That document will be drafted as part of the broader *agent tool contract / memory schema* work-stream (per `docs/north-star-requirements.md` §15 open question 4), and will live in `docs/` as an implementation-near artifact rather than a movement-level concept.

What this document **does** declare: the principle, the structural requirements, the worked examples, the open design questions, and the architectural failures that must be foreclosed in advance.

---

## 2. The federation failures we refuse, by name

Federation is a wide design space. The HONEST direction is defined as much by what it refuses as by what it commits to. Three named failure modes:

### 2.1 Centralized identity (the Apple-ID model)

A single operator (Apple, Google, Microsoft, Meta) issues identities. Every cross-device trust relationship is mediated through that operator's servers. The operator can:

- Lock the user out of their own data
- Reveal the social graph to any state actor with sufficient legal leverage
- Be compelled to introduce silent identity-spoofing (so that an "authenticated" peer is actually law enforcement)
- Discontinue service unilaterally and strand every relationship
- Charge rent on the social graph in perpetuity

This is not federation. It is **operator-mediated centralization wearing the costume of federation**. The HONEST direction refuses it categorically.

### 2.2 Federated-but-leaky (the homeserver model)

Better than 2.1, but not enough. Mastodon, Matrix, email, and similar federated protocols permit users to choose their server-operator — but the server-operator still:

- Sees everyone's social graph at that server
- Sees timing, volume, and recipient metadata of every message
- Holds keys to the server's identity (so server-takeover means user-impersonation)
- Becomes a single point of legal compulsion for that fraction of the network
- Concentrates by default into a few mega-servers, recreating 2.1 in slow motion

A user choosing matrix.org over WhatsApp is making a real privacy improvement, but the architecture is not Inviolata-compatible: an operator-mediated trust directory still exists; only its tenancy is different. **The HONEST direction requires that no peer learns more than the cryptographic floor of who-talks-to-whom**, and the cryptographic floor is approached, not circumvented, by mixnet-style techniques (FR-97).

### 2.3 Distributed-but-leaky (the public-blockchain model)

A category sometimes proposed as the answer to centralization. It is not the answer Inviolata accepts: writing every trust grant, every revocation, every metadata change to a public ledger that anyone can read, in perpetuity, is *the opposite* of metadata minimization (FR-97) and zero-knowledge-to-non-participants (FR-90). The HONEST direction is **owner-sovereign**, which means: by default, *no one* learns about a trust grant except its participants. A public ledger is a permanent, queryable inversion of that property.

### 2.4 What this leaves

The remaining design space is small and well-understood by the cryptographic community: peer-to-peer trust grants with end-to-end encryption, opaque relays (mixnet, sealed-sender, onion-routed), per-user choice of relay operator (or none — direct peer connections when feasible), and **no global directory of any kind**. It is not theoretically novel. It is, however, *unusually difficult to ship as a finished product* — which is why most "private messenger" projects compromise on one or more axes. The HONEST direction asks the maintainers, and any adopter, to refuse those compromises in writing in advance.

---

## 3. The principle

> **Owner-Sovereign Federation Principle.** *Each vault is a first-class peer. No node is more authoritative than any other for its own data. All trust between vaults is expressed as a typed, scoped, time-bounded, and revocable grant in a graph owned by the granting user. There is no Identity Provider. There is no operator-mediated lookup. There is no central directory. There is no node whose unavailability breaks anyone else's vault. There is no global authority that can be compelled to reveal the network's structure, because no global authority exists.*

The principle has five load-bearing properties; each is a specific failure refused.

| Property | What it refuses | Why it matters |
|---|---|---|
| **First-class peer** | Asymmetric "client/server" roles in which one node holds keys for another, or "syncs" another's data through itself. | Asymmetry is where compulsion attaches. A node that holds another's data is a wedge. |
| **Self-authoritative** | Any node that "issues" identity to another. | The moment one node certifies another's identity, that node becomes the legal target for "tell us who is who." |
| **Graph-shaped trust** | Flat lists ("contacts"), or trust as a binary ("friend / not friend"). | Trust is multi-dimensional in real life; flat models force the user to over-grant access. |
| **User-owned graph** | Operator-held trust ledgers; "social graph as a service." | A graph the user does not own is a graph someone else can sell, leak, or be compelled to disclose. |
| **No directory** | A queryable global "phonebook" of vaults. | Discovery is the most under-considered metadata leakage in federated systems. A directory is a register of who exists; that register is a target. |

The principle composes with Inviolata. Specifically:

- *FR-90 (zero-knowledge)* — Federation messages, including trust grants and revocations, are end-to-end encrypted and zero-knowledge to all non-participants, including any relay operator.
- *FR-93 (transparency log)* — The user's *local* audit log records every grant and revocation. There is no central transparency log of grants, because grants are not events the network needs to know about; they are events the *user* needs to remember.
- *FR-97 (metadata minimization in federation)* — Federation transports use padding, sealed-sender, and (eventually) mixnet routing. Day-1 implementations may not deploy all techniques; the design must accommodate them progressively, never foreclose them by architectural lock-in.
- *FR-99 (no lawful-intercept architecture, ever)* — Because no central authority exists, no central authority can be compelled. A jurisdiction wishing to force exceptional access has no party to serve a warrant on except the individual user, restoring the constitutional condition Inviolata is named for.

---

## 4. The trust graph

### 4.1 Nodes and edges

**Nodes** in the trust graph are vaults. A vault may correspond to:

- A natural person (the common case)
- A household, treated as a single vault with multiple users (a married couple sharing a vault is supported, with internal multi-user discipline; this is a Day-N feature, not Day-1)
- An organization (an attorney's office, a clinic, a charity) running its own HONEST-aligned vault
- An automation (a backup service, a publication node) running a vault with narrow capabilities

A vault has a **stable cryptographic identity** — a long-lived public key, hardware-rooted where the user's device permits (FR-91). A vault is *not* identified by a username, an email address, a phone number, a DNS name, or any operator-controlled handle. Human-meaningful names exist in each user's *local* contact list and may differ between users; there is no global namespace.

**Edges** in the trust graph are **trust grants**. A trust grant is a structured, signed, locally-stored statement by one vault about another, of the shape:

```
GRANT
  by:               <granting-vault-public-key>
  to:               <grantee-vault-public-key>
  trust-levels:     [family/spouse, professional/attorney, ...]
  compartments:     [personal, financial, medical-emergency-only, ...]
  capabilities:     [read, propose, attest, ...]
  conditions:       [time-bounded(30 days), revoke-on-(...) , transitive(...)]
  audit:            <granting-vault's local audit-log entry id>
  signature:        <signed by granting-vault>
```

The grant's authoritative copy lives in the granting user's vault. A *cryptographic capability* derived from the grant is delivered to the grantee's vault, scoped to exactly what the grant permits. The grantee cannot extend the grant, only exercise it; revocation is one-sided (the granter can revoke at any time; the grantee cannot "lock in" the grant).

This shape is recognizable from the broader capability-systems literature (object capabilities, macaroons, biscuit tokens, Tahoe-LAFS-style sharecaps). It is not novel. The novelty is in **wiring it to a user-owned trust graph at the application layer with explicit trust-level taxonomy**, rather than at the storage layer alone.

### 4.2 Trust levels (an example taxonomy, not a fixed schema)

The trust graph's edges carry typed, possibly multiple, **trust levels**. A worked example taxonomy (which a real implementation would refine by user research and adopter input):

| Trust level | Typical relations | Default scope |
|---|---|---|
| `family/spouse` | Married/civil-partner | Broad, durable, includes co-decision capabilities |
| `family/parent` | Parent of minor child | Scoped to child's vault; sunsets at age of majority |
| `family/adult-child` | Adult child | Narrower than spouse; succession-relevant |
| `family/sibling` | Sibling | Mutual-aid scope |
| `household` | Roommate, live-in caregiver | Scoped to shared-context items only |
| `professional/attorney` | Personal attorney | Privileged compartment access; protected by law in most jurisdictions |
| `professional/physician` | Primary care physician | Medical compartment; emergency-extensible (see §6) |
| `professional/accountant` | Personal accountant | Financial compartment, time-bounded to engagement |
| `professional/clergy` | Religious counselor | Confessional compartment in jurisdictions that recognize it |
| `transactional/merchant` | One-off counterparty | Single-purpose, single-transaction, auto-expiring |
| `social/friend` | Close friend | Scoped, no fiduciary capabilities |
| `social/acquaintance` | Casual contact | Minimal, mostly contact-routing |
| `public/published` | Public projection | Read-only public posture, not really "trust" — the boundary case |
| `revoked` | Former relationship now ended | Tombstoned; remains in audit log; cannot be re-promoted without explicit user act |

A node may carry **multiple** trust levels simultaneously. Your spouse who is also your attorney is `family/spouse + professional/attorney`. Your doctor who is also your friend is `professional/physician + social/friend`. The grant compositor takes the **union of capabilities** in the levels granted, modulated by the **intersection of compartments** the user explicitly scopes.

### 4.3 Compartments

The compartment concept is shared with [`SUCCESSION.md`](./SUCCESSION.md) §3.3, where compartments enable per-heir scoping. In federation, compartments enable per-grant scoping, with the same data-shape:

- **Personal** — daily reasoning, journal, correspondence
- **Financial** — banking metadata, holdings, transaction history
- **Medical** — health records, medications, allergies, providers, advance directives
- **Medical-emergency-only** — a specifically-narrowed slice of medical, intended for short-window emergency-room style reveal
- **Legal** — wills, contracts, attorney-privileged correspondence
- **Professional** — work artifacts, project memory
- **Confessional** — clergy- or therapist-protected
- **Truly private** — never shared with anyone, ever (the 0-of-N succession compartment from `SUCCESSION.md`; in federation terms, no grant can ever access this)

Compartments are user-extensible. The above is a starter set; an organizational vault would have entirely different compartments. The architectural commitment is that compartments are **first-class**, not bolt-on; the trust graph's edges *cannot* express "everything" — they must always be scoped to one or more named compartments, and "all current compartments" is itself an explicit, dated, revocable choice rather than an implicit one.

### 4.4 Conditions

Every grant carries optional conditions. The starter set (extensible):

- **Time-bounded** — expires automatically at a wall-clock time
- **Use-bounded** — N uses then expires (single-use is a special case)
- **Revoke-on-event** — auto-revokes on a designated event (e.g., revoke spouse on divorce-decree-witnessed; revoke attorney on engagement-ended)
- **Transitive(depth, scope)** — the grantee may delegate a *subset* of the grant to another node, to a maximum depth, scoped to a maximum compartment intersection
- **Quorum-required** — the grant only activates when M-of-N other named nodes co-sign within a window (composes with `SUCCESSION.md` §4.1.1)
- **Geofenced** — the grant only activates when the grantee's vault is within a declared jurisdiction (composes with FR-98 jurisdictional posture)
- **Co-witness-required** — the grant only activates when a named witness vault is online and counter-signs (composes with `SUCCESSION.md` §4.1.3 oracle-witnessed triggers)

Conditions compose. A grant may be `time-bounded(30 days) + revoke-on-event(divorce) + transitive(depth=1, medical-emergency-only-compartment)` simultaneously.

### 4.5 The grant lifecycle

```
DRAFT (in granting user's vault, not yet delivered)
    ↓ user reviews, signs
ACTIVE (delivered as capability to grantee; both sides have it in their audit log)
    ↓ time-bound / use-bound / revoke-on-event triggers
EXPIRED (auto, mechanical)  or  REVOKED (explicit user act)
    ↓
TOMBSTONED (remains in granting vault's audit log forever; cannot be silently un-revoked)
```

Revocation is **one-sided and immediate from the granter's perspective**, but **propagation latency exists**: a grantee whose vault has been offline for a week may not learn of revocation until it comes online. This is the federated-system equivalent of certificate-revocation latency. Mitigations are the same: short time-bounds by default, soft online-check where feasible, hard-fail on capability use beyond expected horizon, and a published *negative cache* (the granter's vault publishes "as of timestamp T, no new grants and no revocations are pending for these recipients" — a kind of warrant canary at the grant-graph level).

---

## 5. The family graph as a worked example

The earliest, most-needed concrete trust graph is the family graph. Its shape:

```
         [me / VaultAI primary]
              │
   ┌──────────┼──────────────────────────────┐
   │          │                              │
 spouse    adult-child            (two designated heir-only nodes from SUCCESSION.md)
 (broad)   (narrower)                          │
   │          │                                ↓
   │     spouse-of-adult-child             professional/attorney
   │       (very narrow,                       (legal compartment,
   │      household-only)                       privileged)
   │
 spouse-of-spouse's-physician
 (medical-emergency-only,
  transitive depth=0)
```

Properties of the family graph in the HONEST direction:

- **Each person is a peer.** My spouse's vault is not a sub-vault of mine. We may share a household compartment, but each of us holds our own keys, our own truly-private compartment, and our own succession quorum.
- **Trust levels are typed and multi-edged.** My spouse is `family/spouse` *and* (because we co-parent) holds parental capabilities over our minor child's vault — those capabilities sunset at the child's age of majority, mechanically, without anyone needing to remember.
- **Compartments are explicit.** My truly-private journal is not in *any* family edge. My financial compartment is shared with spouse but not with adult-child until I explicitly extend it. My medical-emergency-only compartment is shared more broadly because the cost of unavailability is high (a physician needs allergies and medications NOW; the cost of broad share is low because the compartment itself is narrow).
- **Succession overlays.** The succession quorum (`SUCCESSION.md`) typically draws its members from the family graph, but with an important twist: succession quorum members hold *Shamir shares*, not *active grants*. An heir who is also an active family-graph node has both: an active grant (current trust) and a Shamir share (latent succession trust that activates on triggers). The two are independent; revoking active grants does not revoke the Shamir share, and vice versa.
- **Graph is asymmetric.** My spouse trusts me at `family/spouse` and my adult-child trusts me at `family/parent`, both of whom in their own vaults make their own grants back to me with their own scoping. Each is sovereign. There is no merged "household graph" — there are overlapping, peer-coherent local graphs.

The family graph also reveals the load-bearing role of **transitive grants with scope and depth limits**: my spouse may grant her physician access to her medical compartment. That physician now has a capability over my spouse's vault, derived from my spouse's grant — but **not** over mine, because no transitivity flows up, only outward, and only within the scope my spouse's grant explicitly permits. The physician is a peer to my spouse, and a stranger to me, even though my spouse and I are intimate peers.

---

## 6. The doctor scenario (the load-bearing probe case)

The federation concept must answer a specific concrete case, similar in load-bearing role to "the user dies" for `SUCCESSION.md`:

> *I am unconscious in an emergency room. The attending physician needs my medications, allergies, recent diagnoses, and any advance directives. They need it in minutes, not hours. They have never seen my vault before. There is no operator I can call. My phone is locked. My family has not arrived.*

Without a designed-in answer, every "no central directory" promise becomes a wedge to introduce one — *"surely there must be SOME way to look up a patient's medical record in an emergency."* This section is the answer.

### 6.1 The answer in shape

The HONEST direction must enable this case **without** any of the following:

- A central medical-records directory
- An operator-held trust ledger that an emergency-room workstation queries
- A government identity-card system that resolves to a vault address
- Any maintainer involvement at all

What it **does** require:

1. **A federation-aware emergency credential** that the user has pre-arranged
2. **Multiple delivery channels** for that credential, because *we don't get to choose which one is available in the emergency*

### 6.2 Three modalities for the doctor case

| Modality | What the user does in advance | What the doctor / ER does in the moment |
|---|---|---|
| **Pre-shared physical token** | Print a wallet-sized card containing a *medical-emergency-only-compartment* capability token. The token authorizes read-only access to the medical-emergency-only compartment, time-bounded 24h from first use, single-issue. | Doctor scans the QR / NFC of the card; their organizational vault (or a dedicated ER kiosk vault) presents the capability to the user's vault address (also on the card) and retrieves the medical-emergency slice. |
| **Spouse / heir grants emergency access** | Spouse or designated emergency contact already has a `family/spouse` or `family/emergency` edge in the trust graph with the *capability-to-extend-medical-emergency-only* condition. | Hospital contacts spouse; spouse uses their vault to grant the ER's organizational vault a transitive, time-bounded, single-incident grant of the medical-emergency-only compartment. |
| **Pre-designated ER node in the graph** | User has, in advance, granted their primary care physician (and that physician's affiliated hospital network) a standing `professional/physician + condition: emergency-trigger-required` grant. | ER staff invoke the emergency-trigger condition (with the physician or hospital co-witnessing per the user's pre-set policy); the standing grant activates and the ER can read the emergency compartment. |

All three modalities **compose** — a user may have all three in place simultaneously, on the principle that a Day-1 unconscious-in-the-ER scenario is exactly the case where redundancy pays off. Crucially, *all three* terminate at the medical-emergency-only compartment unless the user has explicitly broadened scope. The doctor cannot, through any of these paths, read the user's journal or financial compartment.

### 6.3 What the doctor scenario forecloses

By committing to this design pre-emptively, in writing, in this document, the project forecloses:

- *"You need to add a hospital-readable backdoor for emergencies"* — pre-empted. The pre-shared token exists. The spouse-grant exists. The standing-grant-with-emergency-trigger exists. None of these is a backdoor; all of them are user-controlled, scoped, audited, and revocable.
- *"You need to register with our Health Information Exchange"* — pre-empted. The Exchange's organizational vault, if HONEST-aligned, can be granted access by the user; if not HONEST-aligned, the user has the same three modalities to give an HIE the capability without joining its operator-mediated ecosystem.
- *"You need a recovery procedure for forgotten medical compartment passwords"* — pre-empted. The medical-emergency-only compartment uses a *separately-scoped* succession quorum (typically smaller and faster than the full vault succession), so quorum-based recovery is available even when the user is alive but incapacitated.

This is the same pattern as Inviolata more broadly: **pre-commit to the architecture; pre-state the answer in writing; the demand for the backdoor arrives to find the answer already there.**

---

## 7. Composing with Inviolata, Succession, and the License

### 7.1 With `INVIOLATA.md`

Federation, done as specified here, *strengthens* Inviolata rather than weakening it. Each of the seven architectural commitments (`INVIOLATA.md` §3) is checkable against this design:

| Inviolata commitment | Federation discipline |
|---|---|
| Zero-knowledge architecture | Grants and revocations are E2E encrypted; no relay learns content |
| User-controlled keys, hardware-rooted | Every vault holds its own keys; identity is a public key, not an operator handle |
| Reproducible builds | Federation client is part of the substrate; no separate "federation server" exists |
| Transparency log | Each user's local audit log is the canonical record of their own grants; no central log |
| Tamper-evident next-boot | Inbound grants and capability uses are logged; malicious modification would re-key the audit log |
| No backdoor, ever | No central authority exists *to* be backdoored |
| Designed-in succession | Succession quorum is implemented over the federation peer protocol — see §7.2 |

### 7.2 With `SUCCESSION.md`

Federation and succession are deliberately the same architectural primitive used at different timescales:

- **Active federation** = trust grants in use *now*, mediated by capabilities, expressed as graph edges.
- **Succession** = latent trust held as Shamir shares, activated by triggers, expressed as a quorum.

Both ride the **same wire protocol** — there is no separate "succession protocol" to design. A succession reveal-ping (`SUCCESSION.md` §6.2) is, mechanically, a federation message of a special type. A heir's vault is, mechanically, a federation peer with a latent share. This is intentional: every line of federation code we write is also succession code, and the audit and red-team of one is the audit and red-team of the other.

Specifically:

- A **dead-man's-switch trigger** (`SUCCESSION.md` §4.1.2) propagates as a federation message from the user's vault to designated heirs.
- An **out-of-band trigger** (`SUCCESSION.md` §4.1.1) is initiated by an heir's vault sending a federation message to a quorum of co-heirs to begin reveal.
- An **oracle-witnessed trigger** (`SUCCESSION.md` §4.1.3) involves the named oracle's vault as a federation peer of the user, signing a federation-format attestation.

Therefore the **federation protocol's safety properties are the load-bearing properties of succession also**. We do not have the option of shipping "best-effort" federation; we are shipping the rails that the succession quorum runs on.

### 7.3 With `LICENSE-CONCEPT.md`

`LICENSE-CONCEPT.md` §4.8 (Federation discipline) was reserved as a placeholder pending this document. It can now be filled in substantively, on the following terms — each operationalizing a section of this document into license language:

- **Owner-Sovereign Federation requirement** — A licensee operating a federation-capable HONEST vault may not introduce a centralized identity provider, an operator-mediated directory, or any architectural element that gives the licensee a position from which they can be compelled to disclose the social graph or its structure.
- **No operator-held trust ledger** — A licensee may not hold a copy of any user's trust graph except (a) for the duration of relay transit, (b) as cryptographic ciphertext to which they have no key, and (c) for the minimum metadata floor needed to deliver the message.
- **No global directory** — A licensee may not operate a queryable directory mapping user-meaningful handles (names, emails, phone numbers) to vault public keys, except as a wholly user-side, vault-local index. Cross-user discovery may only proceed via the user's own contacts, mutual-introduction handshakes, or out-of-band channels.
- **Revocation honoring** — A licensee operating a relay may not retain message bodies or capability uses past the standard relay lifetime, and may not reject or delay revocation propagation as a service feature.

These terms compose with §4.9 (Inviolata clause) and §4.9.1 (Lavabit clause) — a relay operator compelled to retain or reveal federation traffic shall cease operating in the compelling jurisdiction, exactly as a vault operator under §4.9.1.

### 7.4 With `docs/north-star-requirements.md`

FR-97 (metadata minimization in federation) becomes a *direction* that a future Federation Protocol Specification must satisfy. The path is:

| Phase | What ships |
|---|---|
| Phase 0 (now) | This document. No federation code. Architecture pre-committed. |
| Phase 1 (post-Day-1) | Federation Protocol Specification draft (separate document, in `docs/`). Reviewed against this concept. |
| Phase 2 | Reference implementation of one peer-to-peer transport (likely [Noise Protocol](https://noiseprotocol.org/) over QUIC). Single-relay, sealed-sender, padding. No mixnet yet. |
| Phase 3 | Multiple relay options; user-owned relay; first audit. |
| Phase 4 | Mixnet integration (Nym, Loopix, or successor). Anonymous-by-traffic-analysis. |
| Phase 5 | Hardware attestation of relay non-logging (TEE-based; aspirational). |

Phases 2–5 are *not* committed-to schedules. They are the **direction**. A user who never enables federation never depends on any of them.

---

## 8. Open design questions

These genuinely need answers before the Federation Protocol Specification can be written.

### 8.1 Bootstrapping a peer relationship

How do two users who do not yet share a trust graph establish a first edge?

- **Out-of-band public-key exchange** — QR code in person, public key on a business card, NFC tap. Privacy-strong, UX-weak for distant relationships.
- **Mutual-introduction handshake** — a third user who already trusts both introduces them. Privacy-medium, UX-strong, but requires a pre-existing graph to seed it.
- **Web-of-trust seed** — a small pre-loaded set of high-trust public introducers (e.g., a maintainer-collective entity's public-attestation node). Privacy-weak in adversarial cases (the introducer becomes a target).
- **Out-of-band channel with cryptographic continuity** — exchange via Signal / iMessage / similar, with the federation client doing key-pinning verification afterward. Privacy depends on the OOB channel's privacy.

The HONEST direction probably requires **multiple bootstrapping modalities to be supported**, with the user choosing which is acceptable per-relationship. Default UX should make the in-person QR-code / NFC path one tap.

### 8.2 Discovery without a directory

How does a user find their spouse's *new* vault address after the spouse replaces hardware?

- **Last-known-address with cryptographic continuity** — a vault re-keys on hardware swap, but signs the new public key with the old one's key (or with succession shares); peers automatically follow the rotation.
- **Designated-rotation-authority node** — the user has nominated one or more nodes in their graph as "rotation announcers"; those nodes propagate the new key.
- **Out-of-band confirmation** — peers receive an automated re-introduction request, but require the user to manually confirm.

The HONEST direction must provide for cryptographic continuity (so that hardware loss doesn't strand every relationship), without recreating an "identity provider" by the back door. The boundary case to design carefully: **a malicious actor who steals a user's old hardware should not be able to cryptographically continue that user's identity to peers**. This requires either (a) succession-quorum involvement in identity rotation, or (b) hardware-attested re-keying. Both need design work.

### 8.3 Sybil resistance without central authority

How does a relationship-graph maintain integrity against an attacker who spawns thousands of fake vault identities?

- **Cost-imposing primitive** at vault creation (proof-of-work, proof-of-stake-of-something-non-monetary, hashcash). Has a long history of failure modes.
- **Web-of-trust depth limit** — accept only nodes within depth-N of one's own graph. Doesn't prevent Sybil; it prevents Sybil from being noticed by anyone outside the attacker's bubble. May be enough in many cases.
- **No solution** — accept that a personal-vault use case doesn't have the cross-stranger interaction patterns where Sybil matters most. *This is plausible* and is the honest current position.

### 8.4 Revocation latency

Acceptable bound? Mitigations? Already discussed in §4.5; specific numbers TBD.

### 8.5 Cross-jurisdictional grants

A user's attorney lives in Switzerland. The user lives in the US. A US warrant is served on the user. Does the attorney-grant survive? *Probably yes* — the attorney's vault holds a capability, not a copy of the user's data; the user retains the right to revoke; the warrant cannot reach the Swiss vault without an MLAT request which is the proper constitutional channel. But the answer needs to be worked through with counsel for several scenarios (US/EU, US/CH, US/IS, EU/IN, etc.).

### 8.6 UX collapse under trust-level granularity

Granular trust is principled and also a UX disaster if presented as a 14-checkbox grid every time the user adds a contact. The design must provide **sensible defaults per trust level**, **template grants** (the spouse template, the attorney template), and **review prompts on edge changes** (when expanding scope, the UX must surface what is changing and why). UX research is part of the Federation Protocol Specification, not this concept document.

### 8.7 Organizational vaults

A clinic, an attorney's office, a charity wishing to participate in HONEST federation as a peer. They have multiple staff, possibly turnover, possibly auditors. *They are vaults, but they are not individuals.* The architecture must permit them as peers without requiring they collapse into a single person's keys. Multi-user vaults, role-segregated capabilities within an organizational vault, time-bounded staff access — all are open design questions.

### 8.8 Is the trust graph itself a compartment?

Should the trust graph be backed up, recovered, or revealed under succession the way other compartments are? *Probably yes*, but with **strong revocation hygiene** — heirs should *not* automatically inherit the user's trust grants, only the user's data; specific grants extending across the user's death (spouse's continued access, perhaps) need explicit user act in advance. The interaction between succession and federation is *non-trivial* and merits its own design pass.

---

## 9. What this document is NOT and what is deferred

To be unambiguous on scope:

- **No wire protocol.** This document declares the shape; the bytes are deferred to a Federation Protocol Specification.
- **No cryptographic primitive selection.** Noise / Signal-protocol / Ratchet / MLS / similar — all deferred.
- **No code.** Not a single line of federation code is committed to any HONEST project on the basis of this document alone; this is a planning artifact.
- **No timeline commitment.** Federation is a Day-N capability for the [first reference implementation](https://github.com/sgireddy/VaultAI); the Mars Test (see [VaultAI's `docs/north-star-requirements.md` §0.2](https://github.com/sgireddy/VaultAI/blob/main/docs/north-star-requirements.md)) requires that a vault function fully without federation. Adopting projects set their own schedules.
- **No implication that federation is "the" answer for HONEST projects generally.** A perfectly HONEST project could choose to never federate. This document only constrains *how* federation is done if it is done.

---

## 10. Why pre-state this in writing now

The same logic as `INVIOLATA.md` §6 and `SUCCESSION.md` §10:

- The **decisions made under pressure** to ship a federated feature are different from the decisions made on the merits in a planning document. Federation pressure will arrive (users will ask; competitors will ship; regulators will assume there is one). The pre-stated answer is: *yes, federated; here is the shape; no, we will not centralize anything.*
- The **demand for a directory** will arrive before the demand for a backdoor. *"Just a search to find users by email"* is the camel's nose. The pre-stated answer is: no.
- The **demand for an Identity Provider** will arrive disguised as an ergonomic improvement. *"Let users log in with Sign-in-with-Apple."* The pre-stated answer is: no.
- The **demand for a 'lawful access' channel at the relay** will arrive whenever a state actor's interests align. The pre-stated answer is the Lavabit stance, scoped to the relay layer specifically.

Each of these refusals is harder to make once a system exists than once a document exists. We are writing the document.

---

## 11. Versioning

This document is **v0.1 (concept)**. The intended trajectory:

| Version | Status | Contents |
|---|---|---|
| **0.1** | **This document** | Principle, trust graph shape, doctor scenario, open questions |
| 0.2 | Possible | Refinements after community / adopter feedback |
| 1.0 | Aspirational | Frozen concept; companion to first Federation Protocol Specification |

The Manifesto is at v0.1; Inviolata at v0.1; Succession at v0.1; License Concept at v0.1; Federation Concept at v0.1. They will move in concert.

---

*The Federation Concept v0.1 — released under [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/). You may copy, modify, and republish, including under a different name, with attribution to the source. The principle of Owner-Sovereign Federation belongs to whoever wishes to honor it.*

*Federation, done with discipline, makes Inviolata stronger. Federation, done with operator mediation, undoes everything. The discipline is non-negotiable; the choice of whether to federate at all remains, always, the user's.*
