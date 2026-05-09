# HONEST Manifesto Adopters' Registry — v0.1

> *A public list of projects, products, and individual practitioners who have
> declared adherence to [the HONEST Software Manifesto](./MANIFESTO.md).*

This is the **soft-power lever** of the HONEST movement. The Manifesto
declares values; the License operationalizes them legally; this Registry
makes adherence *visible*. It is the answer to "*who actually means what
they say?*"

The Registry is not a certification scheme. There is no committee, no
audit, no badge to buy, no fee to pay. It is a public commitment, on the
honor system, with the License's cure-and-termination process and the
Trademark Policy as backstops if the honor system fails.

---

## Status

**The Registry is open. There are currently zero declared adopters
beyond the reference implementation itself.**

This is the honest current state. We are publishing the Registry now,
even empty, so that:

1. The references to it in [`MANIFESTO.md`](./MANIFESTO.md) §Adoption are
   not dangling.
2. The mechanism for adoption exists *before* the first prospective
   adopter shows up, not after.
3. New adopters know exactly what they are agreeing to and what
   information they will publish.
4. The Registry's growth (or lack of it) is itself a public, honest
   signal about how the movement is doing.

---

## Adopters

### Reference implementation

| Project | Maintainer | Declared on | Filial Duty Statement | Notes |
|---|---|---|---|---|
| **[VaultAI](https://github.com/sgireddy/VaultAI)** | [@sgireddy](https://github.com/sgireddy) | — *(pending the implementation actually existing)* | *(pending — see §15.4 of [north-star-requirements.md](https://github.com/sgireddy/VaultAI/blob/main/docs/north-star-requirements.md))* | The first reference implementation. This entry will be filled in when VaultAI ships its first artifact; for now, it is the *intended* reference implementation, not an adopter that has met its own bar yet. |

### Independent adopters

*None yet.*

When the first independent adopter declares, this section will list:

| Project | Maintainer | Declared on | Filial Duty Statement | License | Manifesto version |
|---|---|---|---|---|---|

---

## How to declare adherence

Adoption is a public act. To add your project to this Registry:

### 1. Read the Manifesto and License Concept

[`MANIFESTO.md`](./MANIFESTO.md) and
[`LICENSE-CONCEPT.md`](./LICENSE-CONCEPT.md), in that order. Make sure
you genuinely agree with what's there. Adoption is not free in the
sense of cheap — it is free in the sense of voluntary. The cost is real:
you are committing to architectural constraints that will make some
things harder to build and some business models impossible.

### 2. Publish a Filial Duty Statement

A short public document, hosted somewhere stable (your project's repo,
your website, your blog), explaining how your project honors each of
the six HONEST pillars. The required content is described in
[`LICENSE-CONCEPT.md`](./LICENSE-CONCEPT.md) §5. Concretely, the
Statement should answer, in your own words and with operational detail:

- **H — Honest:** How does your project handle uncertainty? How does
  it cite evidence? Where would a user inspect what your model claimed
  vs. what it could defend?
- **O — Owned:** Who owns the user's data, derived state, and
  fine-tuned model adaptations? How does the user export them? What
  happens when the user requests deletion?
- **N — Network-free:** Does your project phone home? If so, when, why,
  and how does the user know?
- **E — Ephemeral:** What peripherals does your project access, and
  what is the lifecycle of that access?
- **S — Sealed:** What is the trust boundary of your project? How is it
  enforced (kernel sandbox, OS permission, application-level only)?
- **T — Transparent:** Is the source published? Are file formats
  documented? Can the user leave with everything intact?

A Filial Duty Statement does not need to claim perfection. It needs to
be *honest*. If your project falls short on a pillar, name the
shortfall and what you plan to do about it. The Manifesto explicitly
welcomes adopters who are publicly honest about their own limits over
adopters who claim more than they can defend.

### 3. License under terms compatible with the Manifesto

When [the HONEST License v1.0](./LICENSE-CONCEPT.md) exists, license
your project's code under it (or under another license whose terms are
at least as protective of the user). Until v1.0 exists, declare your
intent to migrate to it, and license interim work under whatever permits
that future migration without violating contributor expectations.

### 4. Open a pull request to this Registry

Add a row to the **Independent adopters** table above with:

- **Project name** (and link)
- **Maintainer** (GitHub handle, person, or organization)
- **Date of declaration** (ISO format)
- **Link to your Filial Duty Statement**
- **License** under which the project is distributed
- **Manifesto version** you are declaring adherence to (e.g., `v0.1`)

Sign the commit message with the line:

> *"I declare, on behalf of [project name], adherence to the HONEST Software Manifesto v[X.Y] under the principle of Loka-hita-niṣṭhā."*

The PR will be reviewed for one thing only: that the Filial Duty
Statement exists, is reachable, and addresses each of the six pillars.
The Registry maintainers do not adjudicate whether the *content* of
your Statement is sufficient — that is between you and your users. The
Registry is a public list, not a court.

---

## What being on the Registry means

- **You are publicly held to the principles you declared.** Anyone may
  read your Filial Duty Statement and challenge whether your product
  matches it. That accountability is the entire point.
- **You may use "HONEST-compliant"** in good standing as a description of
  your project, subject to [`TRADEMARK.md`](./TRADEMARK.md). Self-
  declaration is welcome and ungated for individual and non-commercial
  actors; commercial operators should publish the Filial Duty Statement
  before claiming the phrase publicly.
- **You are part of the movement.** Movements grow by the visible
  presence of practitioners. You being here is a signal to the next
  reader that the principles are not just one project's idiosyncrasy.
- **You can be removed.** If you stop honoring the principles, fail to
  cure a documented violation per the License's cure-and-termination
  process, or quietly drift away from the Statement without updating it,
  you can be removed from this Registry by majority vote of the Registry
  maintainers. Removal is not a punishment; it is an honest
  re-statement of the public record.

---

## What being on the Registry does NOT mean

- **It is not a certification.** No body has audited your project. No
  badge has been issued. The Registry does not vouch for your code; it
  vouches that you have publicly committed to a set of principles.
- **It is not a quality bar.** A small, rough, half-finished project
  whose maintainer is honest about its limits is a valid adopter. A
  polished commercial product whose Filial Duty Statement is corporate
  marketing is not.
- **It is not a competitive edge.** The Registry exists to make the
  movement visible, not to give adopters a marketing advantage over
  non-adopters. If your reason for adopting is the marketing benefit,
  please do not adopt.

---

## Removal and contestation

A project may be removed from the Registry by:

1. **Self-removal.** Open a PR removing your row, with a brief honest
   explanation of why. *"We can no longer honor the principles for the
   following reason"* is a respected entry, not a shameful one. Honesty
   about leaving is itself a form of honoring the manifesto.
2. **Public contestation.** Any reader may open an issue documenting a
   specific violation of an adopter's Filial Duty Statement. The issue
   triggers the cure-and-termination process from
   [`LICENSE-CONCEPT.md`](./LICENSE-CONCEPT.md) §6. If the violation is
   uncured after 90 days, the adopter is removed from the Registry.
3. **Maintainer initiative.** If the Registry maintainers become aware
   of a sustained, willful, public violation, they may initiate the
   cure-and-termination process directly.

In all cases, removal is a matter of public record. The Registry keeps
a `HISTORY.md` of all additions and removals, with reasons. Forgetting
the past would defeat the Registry's purpose.

---

## Versioning

This Registry document is **v0.1**. It will be revised as adopters
arrive, edge cases are encountered, and the maintainer-collective entity
takes on responsibility for stewarding it. The *adopter rows themselves*
are versioned by the Manifesto version they declare adherence to: a
project may be on the Registry under Manifesto v0.1 and need to
re-declare under Manifesto v1.0.

---

## Versioning policy for adopters

When the Manifesto bumps a major version (v0.1 → v1.0; v1.0 → v2.0), all
adopters are *not* automatically bumped. Each adopter must explicitly
re-declare adherence to the new version, optionally documenting any
disagreement with new clauses. Adopters who do not re-declare within 90
days of a major version bump are moved to a **Historical adopters**
section of the Registry — preserved as audit trail, not as current
endorsement.

This protects the movement from claiming endorsements that the adopters
did not actually grant, and protects the adopters from being held to
principles they did not explicitly accept.

---

## A note on growth

If this list is empty for a long time, that is a useful signal — both to
us and to readers. It means either:

1. The movement's reach is still small (likely, on Day 1).
2. The bar for adoption is correctly calibrated; nobody has been able to
   meet it yet.
3. The bar is too high; we should reconsider the principles.
4. The bar is at the right height but the cost of declaring is too low
   to overcome inertia.

We will not pad the list. If on Day 365 the list is still only the
reference implementation, we will say so honestly. The point is not to
have many adopters. The point is to have *real* adopters, and to be
*honest* about how many real adopters exist.

---

*Adopters' Registry v0.1 — companion to [`MANIFESTO.md`](./MANIFESTO.md), [`LICENSE-CONCEPT.md`](./LICENSE-CONCEPT.md), and [`TRADEMARK.md`](./TRADEMARK.md). Released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).*
