# Contributing to OpenAssurance

**Status:** First draft

## 1. Purpose

OpenAssurance is an open standards initiative rather than a software product.

Contributions are proposals about how workplace assurance information should be described, exchanged, and verified.

This document sets out how proposals are made and the standards they are expected to meet.

## 2. Who Should Contribute

Participation is sought from:

- employers;
- workers;
- buyers;
- suppliers;
- regulators;
- qualification organisations;
- industry bodies;
- assessment providers;
- technology providers;
- small businesses;
- large organisations.

Technology providers are explicitly welcome. Commercial interest in this work is legitimate and expected.

## 3. Neutrality

OpenAssurance argues that assurance exchange should not depend on any single commercial platform.

The project's documents must therefore be neutral themselves.

### 3.1 No vendor-specific content

Project documents must not contain:

- the name of a commercial platform, product, service, or software provider;
- a description specific enough that a particular product is identifiable without being named;
- a claim that an existing scheme, assessor, or platform is inadequate, non-compliant, or obstructive;
- an endorsement, ranking, or implied preference between existing providers.

The problem is described structurally. It is a consequence of exchange being coupled to platform membership, licensing, and tenancy, not the fault of any identifiable organisation.

Existing providers should be able to read these documents and implement the standard without being positioned as the problem.

### 3.2 No organisation-specific content

Project documents must not contain material specific to any single participating organisation, including:

- an organisation's internal systems, registers, or templates;
- an organisation's procedures, document structures, or internal terminology;
- named staff, customers, sites, or suppliers;
- content that positions the initiative as one organisation's project.

This applies whichever organisation a contributor works for, including organisations contributing significant effort.

### 3.3 Examples should span industries

Worked examples should be concrete, because abstract examples are difficult to evaluate.

Examples should be drawn from a range of industries rather than concentrated in one. A document whose examples all come from a single sector reads as that sector's initiative.

Where an example names a role, qualification, or requirement, it is illustrative only. It does not assert what any organisation should require.

## 4. Proposal Tests

A proposal should be able to answer these questions before it is submitted.

### Open exchange

> Can a record issued in one compatible environment be received and independently verified in another compatible environment without either party joining the other's platform?

### Independence

> Can two organisations exchange and verify assurance information even when neither organisation is a customer of the other's software provider?

### Privacy

> Are we reducing the amount of personal information organisations need to duplicate and disclose, or are we creating another place to copy it?

### Reuse

> Can an established open standard represent this without loss of meaning?

Where an existing standard is sufficient, OpenAssurance should reuse it rather than define a parallel mechanism.

## 5. Scope Limits

A proposal will not be accepted where it would require:

- all participants to subscribe to the same commercial platform;
- a compulsory central registry of people, organisations, issuers, or records;
- openassurance.nz to remain available in order to verify a record;
- a universal person identifier;
- OpenAssurance to determine competency, acceptability, or issuer trustworthiness on a participant's behalf.

These limits are set by the Charter. A proposal that requires one of them is a proposal to change the Charter and should be made as such.

## 6. Privacy

Assurance records about people are personal information.

Any proposal affecting personal information should be consistent with `PRIVACY-PRINCIPLES.md`, and should preserve:

- the distinction between a long-lived credential and a purpose-specific presentation;
- minimum disclosure;
- issuer provenance, which must survive any privacy control;
- the separation between organisation information and personal information.

Contributions must not include real personal information. Examples must use fictional people, organisations, and records.

## 7. Document Style

The project documents follow a consistent style. Contributions should match it.

- New Zealand English.
- One sentence per paragraph, separated by a blank line.
- Numbered `##` sections, with `###` sub-sections.
- Bullet lists using `-`, each item ending in a semicolon and the final item ending in a full stop.
- Blockquotes for central propositions and tests.
- Fenced `text` blocks for diagrams. No images.
- Plain, declarative language. No marketing tone.

Documents state what the project is not as explicitly as what it is. Those sections should be preserved.

Line endings are LF. This is enforced by `.gitattributes`.

## 8. How to Propose a Change

Open an issue for a question, a problem, or a proposal that needs discussion before drafting.

Open a pull request for a specific change to a document, describing:

- what problem the change addresses;
- which of the tests in section 4 it satisfies;
- whether it affects personal information;
- whether it introduces a dependency on any external service, registry, or provider.

Small corrections do not require prior discussion.

## 9. Current Stage

OpenAssurance is at the problem definition and standards mapping stage.

No exchange protocol, schema, or conformance suite exists yet. Contributions that assume one exists will be difficult to evaluate.

The most useful contributions at this stage are:

- evidence about where duplication actually occurs;
- identification of existing standards that already solve part of the problem;
- practical constraints from organisations that would have to implement this;
- privacy analysis;
- reasons why the approach will not work.

The last of these is genuinely welcome.

## 10. Licence

Contributions are made under the Apache License 2.0, as set out in `LICENSE`.
