# OpenAssurance Standards Landscape

**Status:** First draft; the Phase 2 assessment of each item is in `standards-map.md`

## 1. Purpose

OpenAssurance should build on existing standards rather than create parallel mechanisms.

This document identifies standards and New Zealand initiatives that should be considered when defining OpenAssurance.

It is a starting point and requires further technical and legal review.

## 2. W3C Verifiable Credentials

W3C Verifiable Credentials provide a general model for cryptographically verifiable claims.

They provide concepts that are directly relevant to OpenAssurance, including:

- issuer;
- subject;
- holder;
- verifier;
- credential;
- presentation;
- proof;
- credential status.

OpenAssurance should align with W3C Verifiable Credentials unless a specific workplace assurance requirement requires a different representation.

## 3. Credential Status and Revocation

Portable records require a mechanism for determining whether an issuer has:

- revoked;
- suspended;
- replaced;
- expired

a credential.

OpenAssurance should adopt established W3C-compatible status mechanisms instead of defining a proprietary revocation protocol.

## 4. OpenID Credential Protocols

Existing OpenID specifications support digital credential issuance and presentation.

These standards should be evaluated for:

- issuing credentials to a holder;
- presenting credentials to a verifier;
- interoperating with digital wallets;
- supporting future New Zealand government credential infrastructure.

OpenAssurance should avoid creating equivalent proprietary issuance and presentation protocols.

## 5. Open Badges

Open Badges provides an established model for representing achievements and related evidence.

It may be useful for:

- learning achievements;
- competency;
- assessment;
- evidence;
- endorsements.

OpenAssurance should determine where Open Badges can be reused directly and where a workplace-specific profile is required.

## 6. New Zealand Credential Schemas

New Zealand already has published credential schemas, including material available through:

https://credentialschema.nz

These schemas include areas such as:

- qualifications;
- licences;
- courses;
- assessments;
- inductions.

OpenAssurance should prefer compatible existing New Zealand schemas where they adequately represent the required information.

OpenAssurance should not create a duplicate schema solely for branding or namespace ownership.

Reuse assessment should distinguish two separate questions.

The first is whether a schema is openly published and may be implemented by anyone.

The second is whether the tooling around it — issuing, presentation, status, and verification — is available on open terms, or only to licensees of a particular service.

A schema that anyone may read, implemented through tooling only licensees may use, does not by itself satisfy the open exchange requirement. Both questions should be answered before a schema is adopted.

## 7. New Zealand Digital Identity Infrastructure

New Zealand government digital identity standards and credential infrastructure should be treated as an important compatibility target.

OpenAssurance should align with established approaches to:

- credential issuance;
- verification;
- digital wallets;
- relying-party decisions;
- issuer trust;
- credential status.

The project should remain usable outside government-operated systems and should not depend on a central government wallet or registry.

## 8. Qualification Records

Formal qualifications and standards already have authoritative sources and established processes.

OpenAssurance should:

- preserve the original issuer;
- allow organisations to hold and present verified qualification evidence;
- avoid recreating authoritative qualification systems;
- provide mappings where required for exchange.

## 9. Workplace Attestations

A likely gap is a simple interoperable model for workplace attestations.

Examples include:

- employer confirmation of experience;
- supervisor confirmation of observed work;
- practical competency evidence;
- internal authorisation;
- equipment-specific competency;
- employer declarations.

OpenAssurance may need to define a workplace attestation profile where existing standards do not provide sufficient shared semantics.

## 10. Requirement Profiles

Another likely gap is a common machine-readable model for organisations to describe what they require.

Examples:

### Worker requirement

A registered nurse working across multiple client sites may require:

- a current practising certificate;
- a recognised qualification;
- employer authorisation;
- a driver licence where travel between sites is required;
- site induction.

### Supplier requirement

A supplier may require:

- current prequalification;
- specified insurance;
- critical-risk controls;
- competency-management evidence.

OpenAssurance should investigate whether an existing standards model can be reused before defining its own.

## 11. Endorsement and Recognition

OpenAssurance should distinguish:

- a credential being authentic;
- an issuer being recognised;
- an assertion being sufficient for a particular purpose.

Existing standards for endorsement should be reused where practical.

OpenAssurance may need to define how endorsement scope is expressed for workplace use.

## 12. Standards Principle

The project should adopt the following rule:

> **OpenAssurance must prefer an established open standard or schema over defining a new OpenAssurance-specific mechanism where the established standard can represent the requirement without loss of meaning.**

## 13. Independence Principle

Compatibility with an existing schema or standard must not create a dependency on a particular commercial platform.

> **OpenAssurance compatibility must not require use of a particular credential issuer, registry, wallet, host, or commercial platform.**


## 14. New Zealand Privacy Act 2020

OpenAssurance will process personal information when assurance records relate to identifiable individuals.

The design should therefore consider the Information Privacy Principles under the Privacy Act 2020, including:

- IPP 1 - purpose of collection and necessity;
- IPP 2 - source of personal information;
- IPP 3 and IPP 3A - transparency, including indirect collection;
- IPP 5 - storage and security;
- IPP 6 - access;
- IPP 7 - correction;
- IPP 9 - retention;
- IPP 11 - disclosure;
- IPP 12 - overseas disclosure;
- IPP 13 - unique identifiers.

OpenAssurance should support privacy compliance without assuming that consent is the only lawful basis for employer-to-customer assurance exchange.

The legal basis for collecting, using, and disclosing information remains the responsibility of participating organisations.

## 15. Privacy Impact Assessment

A formal Privacy Impact Assessment should be completed before the first stable OpenAssurance specification is finalised.

The assessment should examine:

- competency and qualification data flows;
- employer-to-customer sharing;
- indirect collection;
- hosted services;
- overseas hosting and disclosure;
- identity and identifier design;
- selective disclosure;
- retention;
- correction and supersession;
- revocation;
- onward sharing;
- audit and security requirements.

Privacy should be treated as an architectural requirement rather than an implementation appendix.

## 16. Next Research

The items listed here in the first draft have been examined, and the results are recorded in `standards-map.md`.

That document states a position on each candidate standard, scheme, register, and legal instrument, and identifies the smallest genuinely new layer OpenAssurance needs to define.

The questions that remain open after that assessment are listed in its section 18.

They concern the licence terms of published New Zealand credential schemas, the formats the government wallet will hold, machine-readable access to qualification and licence registers, and the willingness of insurers, assessors, and scheme operators to issue verifiable records.

This document remains the summary of what should be considered.

The map is where the assessment is kept current.
