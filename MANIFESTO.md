# The HONEST Software Manifesto

**Version 0.1 (Draft) · Released under CC BY 4.0 · Adoption is free**

> *Rooted in the principle of **Loka-hita-niṣṭhā*** — *steadfast devotion to the welfare of all who use.*
> *Carried in the Latin tradition as **pietas erga utentem*** — *duty toward the user.*

---

## Preamble

The age of *yester-day-ta-centers* is ending.

For a generation, software has converged on a single shape: centralize the data, harvest the attention, optimize for engagement, lock in the user, monetize behavior, and grow at any cost. The user has become the input device of a remote machine. Their thoughts, their photographs, their conversations, their habits, their sleep — all flow upward to data centers owned by someone else, processed by intelligence that does not belong to them, and returned in the form of advertisements, addictions, and assessments. The user has been told this is normal. It is not. It is a choice. And it is ending.

We declare what comes next.

Software has a duty to the human who runs it. The user gives the software existence, attention, data, and trust. In return, the software owes the user the loyalty a child owes a parent — care, transparency, defense, no betrayal, no selling out the family, no bringing strangers home. **This is not a contract; it is a duty intrinsic to the relationship.** We call this duty *Loka-hita-niṣṭhā* in the Sanskrit philosophical tradition, and *pietas erga utentem* in the Latin. They are the same thing. Both predate computing by millennia. They are older, deeper, and truer than any platform's terms of service, and they are what software has always owed and rarely paid.

We will build only software that pays this debt. We will declare it openly so others can hold us to it. We will license our work in a way that prevents its capture by the architecture we are replacing. And we will measure ourselves, in public, against the principles that follow.

---

## Three eras

| Era | Architecture | Status |
|---|---|---|
| **The age of yester-day-ta-centers** | User as input device for centralized compute. Data flows up. Intelligence happens elsewhere. Attention is the product. | Obsolescent. Already a fossil; not yet aware of it. |
| **The transition** | Cloud-personal hybrid. Some compute local, most still remote. User data still leaks. Privacy is marketed but not delivered. | Today. |
| **The HONEST era** | Compute happens at the user's machine. Data never leaves. Intelligence belongs to the operator. The data center dissolves into the user's silicon. | What we are declaring. What we are building. |

We do not predict this transition; we make it. The HONEST era arrives because practitioners build under HONEST principles, ship under HONEST licenses, and refuse to participate in the architecture they are replacing — not because corporations decide, of their own accord, to behave better. They will not. They have not.

---

## The Six Pillars

Software adhering to this manifesto is **HONEST**:

### H — Honest

**Uncertainty is a first-class answer.** The system cites its evidence. It calibrates its confidence. It refuses to assert what it cannot defend. *"I don't know"* is not a failure; it is a feature. Where models speculate, the speculation is labeled. Where evidence conflicts, the conflict is surfaced, never silently resolved.

### O — Owned

**The user owns everything the system produces from the user's data.** Code, schemas, indices, embeddings, fine-tuned weights, and the corpus itself remain under the user's control, on the user's machine, exportable in open formats. Walking away leaves no hostage state behind. There is no second master. The system has no advertiser, no platform, no upstream interest competing with the user's.

### N — Network-free

**The system does not phone home, does not phone elsewhere, and does not extract.** No telemetry, even "anonymous." No analytics. No model-improvement data collection. No background sync. No accounts, no identity servers, no upstream reachability requirement. Network capability is denied at the kernel level during normal operation. *Yester-day-ta-centers do not exist for HONEST software.*

### E — Ephemeral

**Peripherals are opened on invocation and released; nothing is held ambient.** The system does not hold open the microphone, the camera, the screen-capture, the clipboard, the accessibility APIs. It does not subscribe to push streams. It does not run a background "always-listening" agent. It is silent until invoked, present when needed, and immediately gone when its use is done.

### S — Sealed

**The system chooses what it ingests, what it computes, and what it emits.** Every input, output, and computation is the result of a deliberate, scoped, audit-logged decision. Nothing happens reactively. Nothing happens behind the user's back. The trust boundary is physical; the kernel enforces it; the audit log proves it.

### T — Transparent

**The source is auditable; the formats are portable; the door out is unlocked.** Code is published. File formats are documented and standard. Every derived state is regenerable from the user's primary data. The user's right to leave — with everything they value, in formats they can use — is a load-bearing requirement, not a marketing promise.

---

## What this means in practice

A project adhering to the HONEST Manifesto declares, by its very existence, that it does not and will not:

- Collect telemetry, even "anonymous" or "performance" telemetry.
- Require accounts, identity, network reachability, or DNS to function.
- Measure DAU, MAU, time-in-app, retention, or engagement of any kind.
- Notify the user except when the user has asked to be notified.
- Auto-update; updates are user-invoked and signature-verified.
- Hold open peripherals (microphone, camera, screen, clipboard) ambiently.
- Assert facts without citations into evidence the user can inspect.
- Encode facts about the user in proprietary formats.
- Optimize models for engagement; optimize them for correctness, brevity, and refusal.
- Lock the user in — including by training on their data without giving them the trained weights.
- Carry advertising, sponsored content, paid placement, or "promoted" results.
- Use dark patterns ("are you sure you want to leave?", streaks, FOMO triggers, scarcity prompts, infinite scroll, autoplay).
- Train on user data outside the user's machine, ever, under any pretext.
- Sell, share, or transmit user data to any third party for any reason.

These are not marketing claims. They are architectural constraints. The HONEST License operationalizes them.

---

## The Inviolata Principle — *domus inviolata*

Beyond the Six Pillars stands a commitment of a different kind. The Pillars describe what HONEST software *does*. **Inviolata describes what HONEST software *will not betray under any pressure.***

***Inviolata*** — Latin: *the inviolate home* — declares that the user's vault is protected with the same architectural rigor that constitutional democracies extend to the physical home. **Extrajudicial access is foreclosed in code. Lawful access requires due process between the user and the state, not between the operator and the state.**

The principle has four-thousand-year heritage in legal doctrine:

- **Fourth Amendment**, US Constitution (1791) — *"the right of the people to be secure in their persons, houses, papers, and effects, against unreasonable searches and seizures."*
- **Article 8**, European Convention on Human Rights (1950) — *"everyone has the right to respect for his private and family life, his home and his correspondence."*
- **Article 12**, Universal Declaration of Human Rights (1948) — *"no one shall be subjected to arbitrary interference with his privacy, family, home or correspondence."*
- ***Unverletzlichkeit der Wohnung*** — German Basic Law, Article 13.

The digital home of the AI era — the personal data vault that holds a human's writing, conversations, health, finances, relationships, and the AI that has learned them — must be protected by an equivalent architectural commitment. *Inviolata* is the name we give to that commitment.

It is not a synonym for "private." Privacy is what we *want*. Inviolata is what we *enforce in code*, with mechanisms that survive bad-faith demands by anyone — including the operator, the maintainer, the investor, the host, and the state.

### What Inviolata commits us to architecturally

Seven commitments. Detailed in [`INVIOLATA.md`](./INVIOLATA.md):

1. **Zero-knowledge architecture.** The maintainer cannot read user content under any circumstance — including circumstances where the maintainer is legally compelled to. We hold no master key, no escrow, no recovery key.
2. **User-controlled keys, hardware-rooted where available.** Apple Secure Enclave, Windows TPM, Linux TPM2, Snapdragon SPU. Software-only key custody is the floor for early releases on platforms where hardware roots are unavailable; hardware roots of trust are the target as platforms support them.
3. **Reproducible builds and transparency log.** Every release binary verifiable against published source. Release hashes logged in an append-only public log. Silent push of "special builds" to individual users is mechanically detectable.
4. **No backdoor, no lawful intercept, no exceptional access, no key escrow — ever.** Under any name, for any reason, at any layer. *This commitment is non-negotiable and pre-stated.*
5. **Metadata minimization.** Federation protocols designed to minimize traffic-analysis information.
6. **Tamper-evident architecture.** Modifications to the user's binary or trust enclave are detectable on next boot.
7. **Designed-In Succession.** The hardest case for Inviolata is *the user dies; heirs need access; we hold no keys.* Without a designed-in answer, every "no backdoor" promise becomes an excuse for a backdoor later. We refuse that excuse. The user — not the maintainer — pre-designs their own succession protocol. We provide the cryptographic primitives (Shamir's Secret Sharing, configurable triggers, compartment-aware key splitting). We do not participate. **The detailed design is in [`SUCCESSION.md`](./SUCCESSION.md), and it is load-bearing for the credibility of every other commitment in this section.**

### What Inviolata commits us to politically

If a jurisdiction mandates a backdoor, lawful-intercept capability, key-escrow system, or any equivalent — including under the names "exceptional access," "responsible encryption," "child-safety access," "national-security access," or any other characterization — **the project will cease operating in that jurisdiction rather than comply.**

This is the **Lavabit stance**, named after Ladar Levison's 2013 decision to shut down Lavabit rather than hand the US government Snowden's email keys. We pre-commit to it publicly, in writing, before it is needed — so that it is not seen as a panicked retreat when the time comes, and so that no government can quietly extract a partial concession by escalating gradually.

We accept the costs this commitment imposes:

- **We will face legal and political pressure.** The UK's *Investigatory Powers Act*, Australia's *TOLA Act*, China's *Cybersecurity Law*, India's IT Rules 2021 traceability mandate, and periodic EU "Chat Control" proposals are hostile to this stance.
- **We may face market exit** in jurisdictions that mandate backdoors. We accept this as the cost of meaning what we say.
- **Personal legal exposure for maintainers**, particularly during the period before the maintainer-collective entity is formed.
- **The "going dark" framing** by some law-enforcement and political actors. We answer with the lock analogy: *locks on physical homes protect every honest occupant; the unavoidable cost is that bad actors also benefit from locks; the alternative — a master key for authorities — protects no one because the master key inevitably leaks.*

### Jurisdictional posture

The maintainer-collective entity (when formed) is chartered in the **United States** as primary jurisdiction (for First Amendment protection of code-as-speech and the legal precedent of *Apple v. FBI*, 2016) and **Switzerland or Iceland** as secondary jurisdiction (for strong privacy constitutional traditions and operational independence from US dependencies). If the primary jurisdiction's posture deteriorates, operations migrate to the secondary without compromising the principle.

### Real-world precedent we stand on

We are not alone in this stance. We join a tradition:

| Precedent | What it established |
|---|---|
| **Apple v. FBI** *(San Bernardino, 2016)* | A company can refuse to write a backdoor, even on a single device, even with a court order, even for terrorism investigation. |
| **Signal** | A service can architect itself such that the only data it has to surrender under subpoena is "registration date and last seen." |
| **Lavabit** *(2013)* | A service can shut itself down rather than comply with a demand for SSL keys. The "Lavabit stance" is named for this precedent. |
| **WhatsApp v. India** *(2021–ongoing)* | A service can refuse to comply with traceability demands, accepting potential market exit as the cost. |
| **Tutanota / Threema / ProtonMail / Tresorit** | E2E-encrypted services routinely refuse to provide content because they architecturally cannot. |

Inviolata is **the constitutional layer** of the HONEST movement. Below the Six Pillars in this document; *above* them in priority when they conflict.

---

## Honest exceptions

A small number of operations require contact with the outside world. We confine these to **explicit, user-invoked, time-bounded phases.**

1. **Update phase** — signature-verified downloads of model bundles or substrate releases, on user invocation, with a hard timeout back to offline operation.

That is the entire list. **Sync of files** into the user's chosen folder is performed by the user's chosen sync mechanism (iCloud Drive, Dropbox, Syncthing, none) — *outside* the trust boundary. We never contact a network on the user's behalf during normal operation. *Yester-day-ta-centers do not exist for us.*

---

## Adoption

Projects, products, and individual practitioners may declare adherence to this manifesto. Adherence is not a certification — there is no committee — it is a *public commitment, and an invitation to be measured by it.*

To declare adherence:

1. State publicly that your project follows **the HONEST Software Manifesto v0.1** (or the current version), and link to its canonical text.
2. License your code under **the HONEST License**, or under another license whose terms are at least as protective of the user. The Manifesto is the values; the License is one way of operationalizing them.
3. **Document where, if anywhere, you fall short**, and what you plan to do about it. Honest about being honest.
4. Accept that compromise on these pillars is a **regression**, to be reverted or justified in public, not silently absorbed.

We will fail at this sometimes. We are humans, building software, in a world that has been organized against this stance for a generation. The remedy when we fail is to *name the failure, fix it, and answer to the user* — not to redefine the principle.

---

## What this is not

- This is **not** a certification scheme. There is no body to issue stamps. There are no audits we sell. There is no "HONEST-Certified" sticker. Adherence is self-declared and publicly held.
- This is **not** a religion or a sect. *Loka-hita-niṣṭhā* and *pietas* are philosophical heritage, not articles of faith. We cite them because the duty they describe is older, deeper, and truer than the venture-backed software industry, and because every successful movement carries a tradition older than itself.
- This is **not** anti-corporate. It is anti-extractive. Corporations may build HONEST software. They will, if they choose, find that their users trust them more for it.
- This is **not** complete. This document is v0.1. The principles will be sharpened by adversarial argument and by the hard cases that real implementations encounter. Versioning matters. Manifestos are living documents.

---

## Signature

> *We hold these principles to be the duty owed by software to the human who runs it.
> We declare them openly so others may hold us to them.
> We refuse the architecture of the yester-day-ta-centers.
> We build, instead, software that is its operator's loyal servant —
> Honest, Owned, Network-free, Ephemeral, Sealed, Transparent.*

— Initial signatories: *The maintainers of [VaultAI](https://github.com/sgireddy/VaultAI), the first reference implementation.*

Add your name and your project's name to the [Adopters' Registry](./ADOPTERS.md) when you are ready to declare publicly. The Registry is open and currently lists only the reference implementation; that is the honest current state.

---

## Where this Manifesto lives

**This is the canonical home** of the HONEST Software Manifesto, the Inviolata Principle, the License Concept, and the Adopters' Registry: the movement repository at **[github.com/honestsoftware-org/honestsoftware](https://github.com/honestsoftware-org/honestsoftware)**, served at **[honestsoftware.org](https://honestsoftware.org)** (website to be built at an appropriate time).

These movement-level documents are deliberately separate from any product implementation. *VaultAI is one reference implementation; HONEST is the movement.* The Manifesto is mirrored in adopting projects' repositories (including the [VaultAI repository](https://github.com/sgireddy/VaultAI)) for self-containment, but **this repository is canonical** for any future amendments. Adopters are encouraged to mirror; mirrors should reference this repository as canonical.

---

*The HONEST Software Manifesto v0.1 — released under [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/). You may copy, modify, and republish, including under a different name, with attribution to the source. Adoption is free. Forking is welcome. The Manifesto becomes stronger every time it is read aloud and meant.*
