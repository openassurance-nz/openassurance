# OpenAssurance Standards Map

**Status:** Working draft, Phase 2 (map existing standards)  
**Last reviewed:** September 2026

## 1. Purpose

The OpenAssurance development path has six phases.

Phase 2 is to identify what already exists and should be adopted rather than recreated.

This document is the working record of that phase.

It assesses each candidate standard, scheme, register, and legal instrument against what OpenAssurance actually needs, and states a position on each.

Its output is a statement of the smallest genuinely new layer OpenAssurance has to define, which is the input to Phase 3.

`docs/standards-landscape.md` lists the candidates and the principles that govern reuse.

This document records the assessment.

Where the two differ, this document is the more recent and should be preferred until the landscape document is revised.

Nothing in this document is a specification.

Positions stated here are proposals for discussion, and every one of them can be challenged through the process in `CONTRIBUTING.md`.

## 2. How to Read the Positions

Each item is given one of five positions.

- **Adopt**: use as published; OpenAssurance will reference it normatively and add nothing;
- **Profile**: use as published, but OpenAssurance must choose among its options or add a small workplace vocabulary on top of it;
- **Evaluate**: a plausible fit whose stability or suitability is not yet established; a decision is required before v0.1 is finalised;
- **Reference**: context that records will point to, such as legislation, public registers, or classification schemes, that OpenAssurance neither implements nor governs;
- **Set aside**: considered and not taken forward for v0.1, with the reason stated.

"Set aside" is not a judgement on quality.

It means the item does not solve an OpenAssurance problem better than an alternative, or is not stable enough to build a national profile on yet.

Every position is dated.

Standards move, and a position recorded against a Working Draft should be revisited when that draft becomes a Recommendation.

## 3. Method

Each candidate was checked against its primary source in September 2026, and the status recorded here is the status on that date.

No vendor material was used as a source for any status or capability claim.

Each candidate was then assessed against five questions.

### 3.1 Reuse

> Can this standard represent the OpenAssurance requirement without loss of meaning?

### 3.2 Independence

> Does adopting this standard create a dependency on a particular platform, registry, wallet, or service?

### 3.3 Openness in two parts

The landscape document separates two questions that are often conflated.

The first is whether the specification is openly published and may be implemented by anyone.

The second is whether the tooling around it is available on open terms, or only to licensees of a particular service.

Both were asked of every candidate.

### 3.4 Stability

A candidate published as a W3C Recommendation, an IETF RFC, an OpenID Foundation Final Specification, or an ISO International Standard is treated as stable.

A Working Draft, Candidate Recommendation, Internet-Draft, Community Group report, or Technical Specification is treated as prospective, however widely deployed.

### 3.5 Privacy fit

> Does the standard support minimum disclosure, scoped identifiers, and status checking that does not reveal who is being checked?

A candidate that fails this question is not automatically excluded, but the gap is recorded.

## 4. The Layers of an Exchange

An OpenAssurance exchange involves several distinct layers, and most of them are already standardised.

```text
Requirement and recognition   what a relying organisation asks for, and whom it recognises
Workplace vocabulary          what a record means: competency, attestation, assessment, evidence
Credential data model         how a record is structured
Securing mechanism            how a record is signed and checked
Identifiers                   how issuers, subjects, and organisations are named
Status                        whether a record is still current
Presentation and exchange     how records move: issue, hold, present, receive
Legal and regulatory context  Privacy Act, trust framework, occupational registers
```

The lower five layers, from credential data model to presentation, are the subject of mature international standards and should be adopted or profiled, not redefined.

The top two layers, requirement and recognition and workplace vocabulary, are where existing standards stop short of what workplace assurance needs.

That is where OpenAssurance's own contribution sits.

The bottom layer is New Zealand law and public infrastructure, which OpenAssurance must align with and cannot change.

Sections 5 to 11 work through the international standards layer by layer.

Sections 12 and 13 cover the workplace vocabulary for people and for organisations.

Section 14 covers the New Zealand context.

Sections 15 to 19 summarise the map, state what remains genuinely new, and list the decisions still required.

## 5. Credential Data Model

### 5.1 W3C Verifiable Credentials Data Model 2.0

**Position: Adopt.**

The Verifiable Credentials Data Model v2.0 became a W3C Recommendation on 15 May 2025.[^vcdm2]

Version 1.1 now carries a notice that it is outdated, and the undated address for the data model serves version 2.0.[^vcdm11]

The data model defines the three-party pattern of issuer, holder, and verifier, and the concepts of credential and presentation.

Those map directly onto the OpenAssurance roles and onto the distinction between a long-lived credential and a purpose-specific presentation that the privacy principles depend on.

The core properties cover what the architecture overview requires of a record.

- `issuer` carries issuer provenance;
- `credentialSubject` carries who or what the record is about, with an optional identifier;
- `validFrom` and `validUntil` carry the period of validity;
- `credentialStatus` carries the pointer to a revocation or suspension mechanism;
- `credentialSchema` carries the pointer to a schema the record conforms to;
- `evidence` carries a description of the basis for the assertion;
- `relatedResource` carries a hash-linked reference to an external document such as a certificate;
- `termsOfUse` carries conditions attached to the credential or presentation.

The data model deliberately does not define how a record is signed, how it moves, or how a verifier decides whether a claim is acceptable.

Those are left to the securing specifications, the protocols, and the relying party respectively, which is exactly the separation OpenAssurance wants.

A Working Draft of version 2.1 was published on 13 September 2026.[^vcdm21]

It does not supersede 2.0 and should be tracked rather than depended on.

### 5.2 Verifiable Credentials JSON Schema

**Position: Adopt as prospective.**

The Verifiable Credentials JSON Schema Specification defines how a credential points at the JSON Schema it conforms to, either directly or as a schema wrapped in its own signed credential.[^vcjs]

It requires support for JSON Schema 2020-12.

It remains a Candidate Recommendation Draft dated 4 February 2025 and has not advanced since.

OpenAssurance record schemas should be written in JSON Schema 2020-12 regardless, and should be referenced through `credentialSchema` in the form this specification describes.

If the specification has not reached Recommendation when v0.1 is finalised, the profile should say so and reference it as prospective.

### 5.3 Alternative credential formats

Two other credential formats are in wide use and are supported by the same issuance and presentation protocols.

**IETF SD-JWT VC.**

**Position: Evaluate.**

SD-JWT-based Verifiable Digital Credentials is an Internet-Draft of the IETF OAuth Working Group, submitted to the IESG for publication as a Proposed Standard in August 2026.[^sdjwtvc]

It expresses a credential as plain JSON claims in a selectively disclosable JWT, without JSON-LD.

It is close to stable, and the European Digital Identity Wallet framework requires wallets to support it alongside mdoc, while treating the W3C data model as optional and describing it as the reference format for attestations in the education sector.[^arf]

It is not proposed as the OpenAssurance record format for v0.1, because the W3C data model is already a Recommendation and carries the evidence, related-resource, and terms-of-use properties workplace records need.

A conforming OpenAssurance verifier may in future need to accept SD-JWT VC presentations of credentials issued by others, but no New Zealand issuer of relevance has adopted the format, and section 14 shows the government has chosen mdoc instead.

**ISO/IEC 18013-5 and the ISO/IEC 23220 series.**

**Position: Evaluate, and Reference for government-issued credentials.**

ISO/IEC 18013-5:2021 defines the mobile driving licence and the underlying binary credential format known as mdoc, and a second edition is at Draft International Standard stage.[^mdl]

The ISO/IEC 23220 series generalises the same building blocks to other mobile documents.[^iso23220]

The format is designed for government-issued identity documents presented from a phone, with strong device binding, and is the format mobile driving licences use internationally.

It is also the format the New Zealand government has built its own credential infrastructure on.

The Trust Framework Rules permit an accredited credential to use the W3C data model, ISO/IEC 18013-5, or the ISO/IEC 23220 series, but the government wallet, the government issuance platform, the government trust list, and the government verifier app all implement mdoc, and none currently implements the W3C model.[^distfrules][^wallettech][^dciptech]

Section 14 sets this out in full.

Two consequences follow for OpenAssurance.

A relying organisation whose requirement includes a government-issued licence or an NZBN credential will receive it as an mdoc presentation, and a conforming OpenAssurance verifier must be able to accept that presentation without requiring re-issuance in another format.

An OpenAssurance record on the W3C data model can in principle be accredited under the Trust Framework, but cannot today be held in the government wallet.

OpenAssurance should keep the W3C data model as its record format, because its holders are as often organisations' systems as individuals' phones and because the vocabulary it needs already exists there.

It should also specify its vocabulary as a set of named claims that is independent of either container, so that the same record can be rendered as a W3C credential or as an mdoc namespace without changing its meaning.

Whether OpenCompetency then defines that mdoc rendering, so that a worker can carry a competency record in the government wallet alongside a driver licence, is listed as a decision in section 17.

The wallet's own documentation gives educational qualifications and licences as examples of the credentials it expects to hold from non-government issuers, so the question is one of format, not of eligibility.[^wallettech]

### 5.4 Loss-of-meaning check

Nothing in the record types the architecture overview lists is unrepresentable in the W3C data model.

A credential, an attestation, an assessment, and an endorsement are each a signed assertion by an identifiable issuer about an identifiable subject, which is what the data model exists to express.

Evidence and requirement are different in kind: evidence is dealt with in section 5.5 and requirement in section 11.

### 5.5 Evidence as a record type

Evidence is the one record type in the architecture overview whose signer is normally not its source.

A policy, a certificate, a training register, or an incident report is held by the organisation it concerns, and the party that can sign a record about it is the holder.

The data model provides two mechanisms.

The `evidence` property lets an issuer describe the basis for its own assertion inside the credential.[^vcdm2]

The `relatedResource` property lets any credential hash-link an external document by identifier, media type, and digest, and requires a verifier that uses the document to check the digest.[^vcrelres]

An OpenAssurance Evidence record is a credential issued by the holder about a document or dataset it holds, carrying:

- what the document purports to be;
- its purported source;
- the date the holder obtained it;
- the hash-link;
- the least description a relying organisation needs to decide whether to look at it.

The honesty rule is that a held copy never implies the source's signature.

A document that carries the source's own signature, such as a digitally signed PDF, is the one exception.

The Evidence record still says only that the holder holds it unaltered, but a verifier can check the document's signature against the source's certificate, and the profile should distinguish an issuer-signed document from an unsigned one.

A verifier treats an Evidence record as the holder's statement that the document is unaltered since the holder obtained it, and nothing more, and a relying organisation that needs certainty checks with the source.

Evidence should carry the least personal information that serves the purpose, and evidence about an organisation should have names and identifiers the purpose does not need removed before it is shared, which is what the cross-recognition scheme in section 13 already requires of its suppliers.

When the source later issues a signed record, the Evidence record is superseded by it through the linking terms in section 8.3, and nothing else in the holder's records changes.

That is the upgrade path section 16.8 relies on.

## 6. Securing Records

The data model leaves signing to two companion specifications, both W3C Recommendations of 15 May 2025.

They are alternatives, and a profile that mandates both doubles every verifier's obligations.

### 6.1 Securing Verifiable Credentials using JOSE and COSE

**Position: Profile, as the mandatory-to-implement baseline.**

This specification wraps an unmodified credential or presentation in a signed envelope using one of three IETF mechanisms: a JSON Web Signature, a selectively disclosable JWT, or a COSE structure.[^vcjose]

It registers the media types `application/vc+jwt`, `application/vp+jwt`, `application/vc+sd-jwt`, `application/vp+sd-jwt`, `application/vc+cose`, and `application/vp+cose`.

Selective disclosure inside the envelope relies on RFC 9901, Selective Disclosure for JSON Web Tokens, published as a Proposed Standard in November 2025.[^sdjwt]

The case for making this the baseline is practical.

- JOSE libraries exist for every mainstream language and are already used by most organisations' identity systems;
- no canonicalisation step is required, so there is less to implement and less to get wrong;
- selective disclosure, which the minimum-disclosure principle requires, is available through an RFC rather than a draft;
- a hosted service for small organisations can be built on commodity components.

### 6.2 Verifiable Credential Data Integrity 1.0

**Position: Profile, as an optional alternative.**

Data Integrity embeds a `proof` object in the credential itself, parameterised by a named cryptosuite.[^vcdi]

The EdDSA and ECDSA cryptosuites reached Recommendation on the same date, and the ECDSA suite includes a selective-disclosure variant.[^vcdieddsa][^vcdiecdsa]

A BBS cryptosuite offering unlinkable selective disclosure is a Candidate Recommendation Draft and is not yet stable.[^vcdibbs]

Embedded proofs keep the record readable as plain JSON-LD and support proof sets and chains, which suits records that will be countersigned.

They require RDF canonicalisation or JSON canonicalisation before hashing, which is the main implementation cost.

A conforming verifier should be permitted to accept Data Integrity proofs, and a conforming issuer permitted to produce them, without either being required.

### 6.3 Recommendation

v0.1 should aim to require the JOSE envelope for every conforming record, permit the SD-JWT envelope where selective disclosure is needed, and permit Data Integrity proofs as an option.

This is a decision for Phase 3 and is listed in section 17.

The trade-off runs one way only if implementation cost for small organisations is weighted heavily, which the Charter's open-participation principle requires.

### 6.4 Verification over time

Assurance records outlive the keys that signed them, and sometimes the issuers.

A qualification issued today may be presented in fifteen years, and the portability principle in the architecture overview says a record must not become invalid because its host closed or its issuer changed systems.

The adopted standards answer part of this.

Controlled Identifiers lets a verification method carry an `expires` or `revoked` timestamp, and expects a verifier not to accept proofs made at or after that time.[^cid]

It says nothing about proofs made before that time, and nothing about whether a retired key should be retained in the controller document rather than deleted.

A JOSE envelope carries the time of signing and a Data Integrity proof carries a `created` timestamp, so a verifier can in principle check that a key was valid when it was used, but only if the controller document still lists the key with its dates.[^vcjose][^vcdi]

`did:web` has no key history at all, because replacing the document replaces the keys.[^didweb]

When an issuer ceases to exist, its controller document and status list disappear with it, and a record that was verifiable the day before is not verifiable the day after.

Four mitigations exist, and none is complete on its own.

- an issuer retains retired keys in its controller document with their validity dates, and never deletes one;
- a verifier records what it verified, against which key and which status list, and when, so that its own decision remains auditable;
- a body that outlives the issuer, such as a regulator, an industry body, or a successor organisation, publishes an endorsement of the issuer's historic keys, which is the job the service status history in an ETSI trusted list does;[^etsi612]
- a successor re-issues the records.

**Position: define, as conformance rules and a Phase 3 design question.**

The profile should require issuers to retain retired keys with their dates, require status lists to remain published for the validity period of the records they cover, and recommend that verifiers keep a record of each verification.

How records survive an issuer's disappearance should be worked through with the bodies that could act as the enduring party, and is listed in section 17.

## 7. Identifiers

Three kinds of party need identifying, and they need different treatment.

### 7.1 Issuers

**Position: Adopt Controlled Identifiers 1.0; Evaluate DID methods as conventions.**

A verifier must be able to go from the issuer identifier in a record to the key that signed it, without asking anyone's permission.

Controlled Identifiers v1.0 became a W3C Recommendation on 15 May 2025.[^cid]

It defines a controller document, published at any URL, that lists an identifier's verification keys and what each may be used for.

It does not require the identifier to be a DID, so an issuer may be identified by an HTTPS URL it controls, with the controller document published under that URL.

That is enough to satisfy the independence test, because the issuer's own domain is the only infrastructure involved.

Decentralized Identifiers v1.0 has been a Recommendation since July 2022, and v1.1 is a Candidate Recommendation dated March 2026.[^did10][^did11]

The DID specifications deliberately define no DID method, and the two methods in common use for organisations are not on a standards track.

- `did:web` resolves to a document fetched over HTTPS from the issuer's domain, and is an unversioned Community Group draft;[^didweb]
- `did:key` encodes the public key in the identifier itself, has no rotation or deactivation, and is a Community Group draft at version 0.9.[^didkey]

Both are trivially implementable and widely deployed, and `did:web` adds nothing cryptographically beyond a TLS-hosted controller document.

The profile should permit `did:web` as a convention because much existing tooling expects DIDs, and should say plainly that it is a convention rather than a standard.

A DID method that depends on a ledger, registry, or network would fail the independence test and should not be required.

### 7.2 People

**Position: Profile, with no universal identifier.**

The data model makes the subject identifier optional, and OpenAssurance should keep it optional.[^vcdm2]

A person can be identified by claims inside the credential, such as name and date of birth as recorded by the issuer, without any identifier at all.

Where an identifier is used, the privacy principles require it to be issuer-scoped, organisation-scoped, pairwise, or otherwise privacy-preserving.

A government, licence, tax, or qualification number must not be used as the subject identifier, because that would turn a number issued for one purpose into a universal tracking key.

Privacy Act 2020 Information Privacy Principle 13 constrains the assignment and reuse of unique identifiers, and section 14 returns to it.

Correlation within one issuer's records is unavoidable and acceptable, because the issuer already holds them.

Correlation across unrelated issuers is what the identifier design must prevent.

The `licenseNumber` property that Open Badges 3.0 places on an achievement subject is a claim about a licence, not a subject identifier, and that distinction should be preserved when the profile is written.[^ob3]

### 7.3 Organisations

**Position: Adopt the New Zealand Business Number; Adopt the Legal Entity Identifier as an alternative.**

Organisations are not people, and the no-universal-identifier principle does not apply to them in the same way.

Organisation identifiers are public by design, and a stable public identifier is what makes an OpenPrequal record about a supplier unambiguous.

The New Zealand Business Number is the statutory identifier for New Zealand businesses under the New Zealand Business Number Act 2016, administered by the Ministry of Business, Innovation and Employment, which maintains the NZBN Register.[^nzbnact][^nzbnabout]

Companies receive an NZBN automatically, and sole traders, partnerships, and trusts may apply for one.[^nzbnget]

Public primary business data, including entity name, trading names, status, and industry classification, is searchable by anyone and available through a free API and as free bulk data.[^nzbnapi][^nzbnbulk]

The Act permits a government agency to use the NZBN in substitution for any other identifier, which is the closest thing New Zealand has to a statement that this is the organisation identifier.[^nzbnact]

Each NZBN is a GS1 Global Location Number, which sits within the ISO/IEC 6523 organisation-identifier framework under International Code Designator 0088, so an NZBN can be written as a globally unambiguous identifier without any OpenAssurance-specific scheme.[^nzbnabout][^gs1icd][^iso6523]

The Government has announced that the Ministry of Business, Innovation and Employment will trial issuing NZBN digital credentials through the government's credential issuance platform, so that a person can prove their identity and authority to act for a business.[^beehivedcip]

That is an organisation-identity credential of exactly the kind OpenPrequal would consume, and section 14 returns to the format it will use.

The Legal Entity Identifier under ISO 17442 identifies legal entities worldwide, is issued for an annual fee through accredited issuers, and its reference data is published as open data by the Global Legal Entity Identifier Foundation.[^lei][^leiopen]

Several thousand New Zealand entities already hold one, and the foundation recognises the Companies Register as the registration authority for them.[^leinz]

It is the right identifier for an overseas supplier or issuer that has no NZBN.

A verifiable form of the LEI, standardised as ISO 17442-3:2024, uses a credential format outside the W3C family and is noted for completeness rather than proposed for adoption.[^vlei]

One caution applies.

A sole trader's NZBN identifies a person, and records about a sole trader are personal information to which the privacy principles apply in full.

### 7.4 Records

Every record should carry its own `id` as a URL under the issuer's control, so that a replacement or correction statement has something to point to.

The identifier need not resolve to anything, and must not be required to.

## 8. Currency and Status

The second trust question is whether a record is still current.

Three mechanisms answer it at different levels.

### 8.1 Validity period

**Position: Adopt.**

`validFrom` and `validUntil` in the data model carry the period the issuer intended the record to be valid for.[^vcdm2]

Timestamps should use the RFC 3339 profile of ISO 8601.[^rfc3339]

An expired record is not invalid as a historical assertion; it is no longer current, which is a different thing, and the profile should say so.

### 8.2 Bitstring Status List v1.0

**Position: Adopt.**

Bitstring Status List became a W3C Recommendation on 15 May 2025.[^bsl]

Each credential carries a pointer to one position in a compressed bitstring that the issuer publishes as a signed credential of its own.

The list supports revocation and suspension as status purposes, and an extensible message mechanism for others.

Its privacy property matters for OpenAssurance.

A list must contain at least 131,072 entries, so fetching it reveals nothing about which credential the verifier is checking.

The issuer publishes the list at a URL of its choosing, so no registry is involved and the mechanism satisfies the independence test.

The profile should require that the list URL sits under an identifier the issuer controls, so that a change of host does not break status checking for records already issued.

### 8.3 Supersession, replacement, and correction

**Position: define, as a small OpenAssurance vocabulary.**

The privacy principles require that a signed record be corrected by revocation, supersession, replacement, or a linked correction statement, never by silent edit.

The data model has no property that says "this record replaces that one" or "this record was superseded on this date by that one".

Bitstring Status List's message purpose could carry a superseded flag, but not the link to the replacement.

This is a gap, and a small one.

OpenAssurance should define a handful of terms for a replacement record to reference the record it supersedes, and for a correction statement to reference the record it corrects.

They should be expressed as ordinary properties on the credential subject or as a typed `relatedResource`, so that no existing tooling is broken by their presence.

### 8.4 Public registers as currency sources

**Position: Reference.**

Many New Zealand licences and registrations already have an authoritative public register operated by the regulator, and section 12.6 lists the main ones.

For those licences, the register is the source of truth for currency, and a status list published by anyone else would be a copy.

A credential that asserts a registered status should identify the register it derives from, and a relying organisation that needs certainty should check the register.

Most registers are web lookups for people rather than status endpoints for systems.

Whether a regulator publishes machine-checkable status is the regulator's decision, and OpenAssurance should neither mirror registers nor assume they will change.

### 8.5 Status for other formats

The Bitstring mechanism is defined for the W3C data model.

The government's credential issuance platform uses the IETF Token Status List draft for revocation of mdoc credentials, and the Trust Framework Rules make revocation mandatory for any accredited credential valid for more than 72 hours.[^dciptech][^wallettech]

A conforming OpenAssurance verifier that accepts government-issued mdoc presentations, as section 5 concludes it must, will therefore need to check that mechanism as well as the Bitstring list.

That is an implementation cost to record, not a reason to change the OpenAssurance choice.

## 9. Presentation and Exchange

This layer covers how a record gets from an issuer to a holder, and from a holder to a verifier.

### 9.1 Verifiable Presentations

**Position: Adopt, with a small profile.**

The data model defines a verifiable presentation as a signed container for one or more credentials, or for claims derived from them, that a holder assembles for a verifier.[^vcdm2]

That is the OpenAssurance "presentation": a purpose-specific sharing event distinct from the credentials it contains.

When the presentation is secured as a JWT, the standard `aud`, `nonce`, and `exp` claims carry the intended recipient, freshness, and expiry that the privacy principles require a presentation to be capable of identifying.

Two things the privacy principles ask for are not carried by any standard property.

- the purpose of the presentation;
- whether onward sharing is expected or restricted.

`termsOfUse` is the data model's extension point for exactly this kind of statement, and OpenAssurance should define a small terms-of-use vocabulary for purpose, onward-sharing expectation, and suggested retention.

### 9.2 OpenID for Verifiable Credential Issuance 1.0

**Position: Adopt, profiled.**

OpenID4VCI became a Final Specification of the OpenID Foundation on 16 September 2025.[^oid4vci]

It defines an OAuth 2.0 protected API by which an issuer delivers a credential to a holder, with same-device and cross-device flows, a credential-offer mechanism, and format profiles for the W3C data model, SD-JWT VC, and mdoc.

It is the established way for a qualification provider, employer, or assessor to issue a record into a worker's or organisation's holder system or wallet.

OpenAssurance should adopt it and profile only the choice of credential format and the required issuer metadata.

### 9.3 OpenID for Verifiable Presentations 1.0

**Position: Adopt, profiled.**

OpenID4VP became a Final Specification on 9 July 2025.[^oid4vp]

It defines how a verifier requests, and a holder returns, a presentation in any of the same three formats.

The Final text uses the Digital Credentials Query Language, DCQL, as its only query language, and no longer references Presentation Exchange.

OpenAssurance should adopt it for interactive presentation, profile the credential formats and response modes, and inherit DCQL for transaction-time queries, as section 11 discusses.

### 9.4 Organisation-to-organisation transfer

**Position: define, as an exchange convention rather than a format.**

The dominant OpenAssurance flow is not a person presenting from a phone.

It is an employer's system sending its worker's records to a customer's system, or a supplier sending its assurance records to a buyer, often asynchronously and sometimes by a person attaching a file.

OpenID4VP handles this when both sides run compatible software, because a holder can be a system as well as a wallet.

It does not help a small organisation that has no such software and has been asked for evidence by email.

The floor for conformance should therefore be a file: a signed verifiable presentation in one of the registered media types from section 6, which can be produced by any conforming system, sent by any channel, and imported and verified by any other conforming system.

No new format is involved.

A conforming file must also be readable by a person, because the organisation receiving it may have nothing but an email client, so a rendering rule is part of the convention, and the data model's reserved render-method extension point and Open Badges' baked images are the existing options to draw on.[^vcdm2][^ob3]

The genuinely new content is the conformance rule that every conforming system must export and import such a file, and the conventions for doing so.

That rule is what makes the Charter's open exchange requirement testable.

### 9.5 Digital Credentials API

**Position: Evaluate.**

The W3C Digital Credentials API is a Working Draft, most recently dated 4 September 2026, that lets a web page ask the browser to mediate a credential request to whatever wallet the user has.[^dcapi]

It will matter for web-based issuance and presentation to individuals once it is stable and shipped.

It is not stable, and OpenAssurance should track it rather than depend on it.

### 9.6 ISO/IEC 18013-7

**Position: Reference.**

ISO/IEC TS 18013-7:2025 defines online presentation of a mobile driving licence, including a profile over OpenID4VP.[^mdl7]

It is a Technical Specification under revision, and matters only to the extent that relying organisations will receive government-issued licences from phones.

## 10. Recognition and Endorsement

The third trust question is whether the relying organisation recognises the issuer.

OpenAssurance does not answer that question and must not maintain the list that answers it.

It needs two things: a way for one party to state that it recognises another for a scope, and a way for a relying organisation to consume such statements.

### 10.1 Endorsement as a record

**Position: Profile Open Badges 3.0 EndorsementCredential.**

Open Badges 3.0 defines an EndorsementCredential, a verifiable credential whose subject is the thing endorsed, with an optional comment.[^ob3endorse]

An endorsement can be attached to an issuer profile, to an achievement definition, or to an individual achievement credential.

That covers the three OpenAssurance cases: an industry body recognising an issuer, a regulator recognising a course, and an assessor countersigning a particular record.

What it lacks is scope.

An endorsement of an issuer says nothing about which record types, occupations, risk categories, or periods the endorsement covers, and workplace recognition is almost always scoped.

OpenAssurance should profile the endorsement subject with a small scope vocabulary, expressed as ordinary properties so that unmodified Open Badges tooling still reads the credential.

The W3C data model has no endorsement concept of its own; the general pattern is simply a second credential whose subject is the first, which is what Open Badges formalises.[^vcvocab]

### 10.2 Publishing and consuming recognition

Three published patterns exist for a relying party to learn which issuers a trusted party recognises, and none is ready to be adopted outright.

**OpenID Federation 1.0.**

**Position: Evaluate.**

OpenID Federation became a Final Specification on 17 February 2026.[^oidfed]

Each entity publishes a signed configuration, superiors publish signed statements about their subordinates, and a relying party resolves a trust chain from an issuer to a trust anchor it has chosen.

Trust marks let an accreditation body assert that an entity meets a defined set of requirements.

Multiple anchors can coexist, so the mechanism does not imply a central registry.

A companion draft applies it to credential issuers, verifiers, and wallet providers.[^oidfedwallet]

The mechanism is stable, but it is framed around OAuth entities and carries more machinery than a small industry body or a single employer would want to run.

**Recognized Entities v1.0.**

**Position: Evaluate.**

This W3C Working Draft, most recently dated September 2026, expresses recognition as a verifiable credential listing which entities are recognised for which actions.[^recog]

It states explicitly that any body, from a government to an individual, may issue such a credential, and that no single registry is mandated.

Its own status section says it is experimental and not fit for production deployment.

It is the most natural fit for OpenAssurance because it uses the same data model as everything else, and it should be tracked closely.

**ETSI trusted lists.**

**Position: Reference.**

ETSI TS 119 612 defines the signed XML trusted lists used under the European eIDAS regulation, and its scope explicitly permits scheme operators outside the European Union to publish lists in the same form.[^etsi612]

ETSI TS 119 602, published November 2025, generalises the model into an abstract data model for lists of trusted entities in any community.[^etsi602]

Both are the mature reference for how a hierarchy of signed lists works, and neither is something a New Zealand workplace scheme would run.

**The government trust list.**

**Position: Reference.**

Three government lists now exist, and they do different jobs.

The Trust Framework Register is the statutory public register of accredited providers and services, and it is format-neutral because accreditation is.[^tfregister]

The wallet's trusted issuer list is an operational list of the certificate authorities and issuance addresses of accredited issuers, which the Government Digital Delivery Agency adds to after accreditation and onboarding.[^wallettech]

The Digital Trust Service is the machine-readable list for relying parties, published in the ISO/IEC 18013-5 form known as a VICAL, and the government verifier app checks presented credentials against it.[^dts]

The service states that it remains the relying party's responsibility to decide which credentials are legally applicable to its purpose, which is the local-acceptance principle in the government's own words.

The VICAL form is built around mdoc issuing-authority certificates, and no published mechanism was found for representing an issuer of W3C-model credentials in it, even though the Rules permit such credentials to be accredited.

That gap is the subject of the first question to the agency in section 18.

These are existing New Zealand recognition sources that a relying organisation may consult for government and accredited issuers.

None is a list of workplace issuers, and OpenAssurance should not expect any of them to become one.

### 10.3 The OpenAssurance position

A relying organisation's recognition list is local, and that is the end of the matter for v0.1.

The profile should define the Endorsement record and its scope vocabulary, so that endorsements can be issued, held, and presented like any other record.

It should state that a relying organisation may build its recognition list from any source it chooses, including endorsements it receives, lists it maintains, and accreditation it observes.

It should defer the choice of a publishing format for recognition lists until either OpenID Federation for wallets or Recognized Entities is stable enough to depend on, and should be written so that adopting either later changes nothing in the records.

### 10.4 Accreditation as one signal among several

Accreditation under the New Zealand Digital Identity Services Trust Framework, discussed in section 14, is voluntary.

Accreditation under an industry cross-recognition scheme, discussed in section 13, is likewise a choice the scheme's participants make.

Both are signals a relying organisation may weigh.

Neither may be a precondition for issuing, holding, presenting, or verifying an OpenAssurance record, because that would reintroduce the mandatory registry the Charter excludes.

## 11. Requirement Expression

The fourth trust question is whether a record meets the relying organisation's requirement.

OpenAssurance does not set requirements, but it must give organisations a common way to express them.

Two different things are easily confused here.

- a **query** is what a verifier asks a holder for in one transaction;
- a **requirement** is a durable, publishable statement of what a role, activity, contract, or supplier category needs.

### 11.1 Digital Credentials Query Language

**Position: Adopt, for transaction-time queries.**

DCQL is defined inside OpenID4VP 1.0 and is a JSON query that a verifier sends to request presentations matching it.[^oid4vp]

It arrives with the presentation protocol and is the right way to ask for records in an interactive exchange.

It is not a requirement model.

It has no way to say that a requirement applies to a role, that alternatives are acceptable, or that an issuer must be recognised for a scope, and it is not meant to be read by a person deciding what to require.

### 11.2 Presentation Exchange

**Position: Set aside.**

Presentation Exchange 2.1.1 is a ratified specification of the Decentralized Identity Foundation, dated April 2024.[^pe]

It defined the query and submission structures earlier drafts of OpenID4VP used.

The Final OpenID4VP text does not reference it, and a profile built on the Final protocol inherits DCQL instead.

The specification has not been withdrawn, and the position should be revisited if the protocols change.

### 11.3 Requirement vocabularies elsewhere

Section 12 examines whether a requirement model exists in the education-credential world.

The short answer is that the vocabularies found describe what a credential *is* and what it *requires of its holder* far more fully than what an organisation *requires of a person or supplier*.

### 11.4 What remains

**Position: define, as a small OpenAssurance record type.**

A Requirement record needs to say, for a named role, activity, contract, or supplier category:

- which record types satisfy it;
- which issuers or which endorsements of issuers it accepts;
- what currency it needs;
- which alternatives are acceptable;
- which conditions are mandatory and which are informational.

It should be publishable, signable as an ordinary credential whose subject is the requirement itself, and readable by a person.

It should also be mechanically translatable into a DCQL query for use at transaction time, so that a relying organisation maintains its requirement once and the query is derived.

This is the largest genuinely new item in the map, and it is still small.

## 12. Vocabulary for People: Competency Records

The data model says how a record is structured.

It does not say what a qualification, a licence, a practical competency, or an employer attestation *is*, and that is what OpenCompetency has to settle.

### 12.1 Open Badges 3.0

**Position: Profile, as the base vocabulary for achievement records.**

Open Badges Specification 3.0 reached Final Release on 17 June 2024 and is maintained by the 1EdTech Consortium, with errata revisions continuing through June 2026.[^ob3]

It is a profile of the W3C Verifiable Credentials Data Model 2.0, so an Open Badges credential is a W3C credential with a defined vocabulary inside it.

Its achievement type vocabulary already includes the types OpenCompetency needs.

- Certification;
- License;
- Competency;
- Assessment;
- Course and CertificateOfCompletion;
- MicroCredential;
- Membership;
- LearningProgram.

The vocabulary is extensible, so a workplace-specific type can be added without breaking conforming readers.[^ob3type]

The achievement subject can carry a licence number, a role, a term, activity start and end dates, a result, and a source, which between them cover most of what a licence, training, or assessment record needs.[^ob3subject]

An achievement definition can be aligned to an external framework by name, URL, and code, which is how a record will point at a New Zealand standard or qualification identifier.[^ob3align]

Evidence is described by URL and narrative; the class has no hash property, so hash-linking a document should use the data model's `relatedResource` instead.[^ob3evidence][^vcrelres]

The specification is licensed for implementation by anyone on a royalty-free basis, and does not require membership to implement.[^ob3licence]

Formal conformance certification is a separate programme that does require 1EdTech membership, and OpenAssurance conformance must not depend on it.[^ob3cert]

That passes both halves of the openness test, provided the profile relies on the specification and not on the certification programme.

### 12.2 Comprehensive Learner Record 2.0

**Position: Evaluate.**

CLR 2.0 reached Final Release on 26 February 2025 and wraps many achievement credentials from many issuers into one signed record about one person, preserving each inner credential's issuer signature.[^clr2]

That is close to what an employer's competency system holds for a worker.

A verifiable presentation already does the same job for a single exchange, and OpenCompetency's privacy principles favour presenting a few records over exporting a whole record.

CLR should be evaluated for bulk transfer when a worker changes employer or an employer changes system, and not used for day-to-day presentation.

### 12.3 Credential Transparency Description Language

**Position: Evaluate, for describing credential types and requirements.**

CTDL is an openly licensed vocabulary for describing credentials, organisations, competencies, assessments, and the conditions attached to them, maintained by Credential Engine and released under a Creative Commons Attribution licence.[^ctdl][^ctdllicence]

It describes what a credential *is* and what its holder had to satisfy to get it.

It explicitly places the description of a credential *awarded* to a person outside its scope, so it complements rather than competes with Open Badges.[^ctdlscope]

Two features matter for OpenAssurance.

- Open Badges alignment targets already include CTDL competencies and credentials, so the two vocabularies are designed to be used together;[^ob3aligntype]
- its condition profile is the only published data model found for stating that one thing requires another, with alternatives, experience, and jurisdiction, and section 11 identified requirement expression as a gap.[^ctdlcond]

Use of CTDL outside the United States could not be confirmed from primary sources, and the registry that surrounds it is not something OpenAssurance should depend on.

The vocabulary should be evaluated on its own, as a source of terms for issuer-published credential descriptions and for the Requirement record.

### 12.4 Schema.org

**Position: Reference.**

Schema.org provides lightweight web vocabulary that search engines and ordinary websites understand.[^schemaorg]

`EducationalOccupationalCredential` describes a credential definition, `Occupation` describes an occupation and its requirements, and `Certification`, added in 2024, describes an issued certification about a person, product, or organisation with issuer, status, and expiry.[^schemacert]

None of these carries proof, status, or holder binding, so none is a substitute for a verifiable credential.

They are the right vocabulary for an issuer's public web page describing what it issues, and for a hosted service's public listing of an organisation's certifications where the organisation chooses to publish one.

### 12.5 New Zealand credential schemas

**Position: Evaluate, pending answers on openness.**

Five credential schemas for induction, course, licence, qualification, and assessment records are published at https://credentialschema.nz, expressed on the W3C data model in JSON.

The landscape document already records the two questions that must be answered before any published schema is adopted: whether the schema itself may be implemented by anyone, and whether the tooling around it is available on open terms.

At the time of writing, the site states no licence terms for the schemas and describes no governance or change process.

Neither question can be answered from the published material alone, and both should be put to the publisher.

If the schemas are openly licensed and their maintenance is open to participation, OpenCompetency should prefer to align field names with them rather than diverge.

If they are not, OpenCompetency should define its own on the Open Badges base and should not create a competing namespace for its own sake.

That position is the one the landscape document already takes, restated for this phase.

### 12.6 New Zealand qualification and standard identifiers

**Position: Adopt as alignment targets.**

The New Zealand Qualifications and Credentials Framework has ten levels and lists qualifications, micro-credentials, and the standards that make them up.[^nzqcf]

Standards are the building blocks: achievement standards listed by the Ministry of Education, and unit standards and skill standards listed by industry standard-setting bodies, with skill standards progressively replacing unit standards.[^nzqastandards][^dassrules]

Each standard has a numeric identifier and a version number, and a listing status of current, expiring, or discontinued.[^dassrules]

Each qualification has a reference number, and each micro-credential a framework number.[^nzqasearch]

These identifiers are stable, public, and already used on every certificate and transcript in the country.

An OpenCompetency record that asserts a New Zealand standard, qualification, or micro-credential should align to it by that identifier and version, using the Open Badges alignment mechanism, and should not restate what the standard says.

The framework recognises eleven credential types: certificate, diploma, graduate certificate, graduate diploma, bachelor's degree, bachelor honours degree, postgraduate certificate, postgraduate diploma, master's degree, doctoral degree, and micro-credential, and one credit represents ten notional hours of learning and assessment.[^nzqatypes]

Those attributes map onto the Open Badges achievement definition without invention: the credential type onto the achievement type, credits onto the credits available, and the framework number, version, and level onto an alignment whose target framework is the New Zealand framework.[^ob3type][^ob3align]

The profile should publish that mapping once, so that every issuer describes a New Zealand qualification the same way.

Industry standard-setting moved on 1 January 2026 from Workforce Development Councils to eight Industry Skills Boards established under the Education and Training (Vocational Education and Training System) Amendment Act 2025, with the councils to be disestablished by the end of 2026.[^isbact][^isbs]

Standard identifiers survive that change, which is one reason to align to identifiers rather than to the bodies that issue them.

No public machine-readable register or API of the framework was found.

The framework is searchable on the web, per-standard documents are downloadable, and two static snapshots of the standards list were published as open data in 2019 and 2020.[^nzqaopendata]

That is a question for the New Zealand Qualifications Authority in section 18, and not a reason to build a mirror.

### 12.7 The New Zealand Record of Achievement

**Position: Reference.**

The Record of Achievement is the official transcript of a person's New Zealand qualifications, micro-credentials, and standards as reported by education providers.[^nzroa]

A digital copy is available to the learner as a PDF, and anyone holding the original can verify it through an online tool.[^nzroaverify]

The same service verifies two other Authority documents: the International Qualification Assessment, which states how an overseas qualification compares with the New Zealand framework, and the Overseas Study Assessment.[^nzqaverifydocs]

Verification works by uploading the unmodified original PDF, with its original filename, and the tool responds at once.[^nzqaverifydocs]

That is verification by the issuer's service rather than against a published key: it is independent of any platform, but not of the Authority's tool remaining available.

The mechanism behind the tool is not described publicly, and no publication by the Authority on verifiable credentials or Open Badges was found.

Two consequences follow for OpenCompetency.

An Evidence record that hash-links the unmodified original preserves exactly the property the tool depends on, so a holder's copy can be re-verified at the Authority at any time by anyone the holder shares it with.

The International Qualification Assessment is, in OpenAssurance terms, an Assessment issued by the Authority about an overseas qualification, and it is the authoritative record for a migrant worker whose qualification was gained abroad.

**University qualifications.**

**Position: Reference.**

For university qualifications, the Authority points verifiers to My eQuals and to the university itself.[^nzqacheck]

My eQuals is the tertiary credentials service for Australia and New Zealand, governed and operated by the participating education providers through a not-for-profit subsidiary of Universities Australia, and used by all public universities in both countries.[^myequals]

A graduate shares a document by a secure link or as a cryptographically signed PDF, and verification is free for the receiving organisation.[^myequalsverify]

The service runs on a commercial platform, which is not named here, and the link-sharing route is mediated by that platform.

The signed PDF is not: it carries the university's own signature and can be checked with ordinary document tooling by anyone who holds it.

That makes a New Zealand university qualification the clearest existing case in the country of an issuer-signed, holder-controlled, independently verifiable record, in document form rather than as structured data.

OpenCompetency should carry such a document as an issuer-signed document under section 5.5, with the university as the source, and should not expect universities to re-issue what they already sign.

For OpenCompetency, the Record of Achievement is the authoritative source for formal achievements, and the Authority is their issuer.

A worker or employer may hold and present verified qualification evidence derived from it, with the Authority identified as the original issuer, which is what the landscape document already requires.

Whether the Authority will issue achievements as verifiable credentials is its decision, and section 18 records the question.

### 12.8 Occupational licences and public registers

**Position: Reference, as authoritative currency sources.**

Many New Zealand occupational licences have a public online register operated by the regulator that an employer can search.

- electrical workers, searchable by name and licence type, showing whether a person is registered and licensed, with a digital licence that links by QR code to the register;[^ewrb]
- plumbers, gasfitters, and drainlayers, showing registration and licence status, conditions, and recent disciplinary history;[^pgdb]
- licensed building practitioners, searchable by name or practitioner number, showing licence class, status, and history under the Building Act 2004;[^lbp]
- health practitioners under the Health Practitioners Competence Assurance Act 2003, whose registers must record whether a practitioner holds a current practising certificate;[^hpca]
- asbestos removal and assessor licences, showing current, renewal in progress, suspended, expired, or cancelled status;[^asbestos]
- seafarer certificates, verifiable by certificate number.[^seacert]

Each register is a web page for a person to look at.

None offers a documented API, and each uses its own status vocabulary.

Some safety-critical competencies have no public register at all, and verification depends on the holder's consent or on contacting the issuer.

- certified handlers of hazardous substances are certified by compliance certifiers, and no public register of handlers exists;[^handlers]
- extractives certificates of competence are verified by the holder or employer writing to the Board of Examiners secretariat;[^extractives]
- aviation licences are verified by a letter the holder requests;[^caa]
- crane operation has no licence regime, and the approved code of practice describes unit standards as one way of demonstrating competency rather than a requirement.[^cranes]

Three conclusions follow.

Where a register exists, it is the source of truth for currency, and an OpenCompetency record asserting that licence should cite the register rather than claim to replace it.

Because status vocabularies differ by regime, the profile needs a small mapping from each regime's states onto the OpenAssurance notion of current, and should not impose one enumeration on regulators.

Where no register exists, a holder-presented, issuer-signed record with a status list is a strict improvement on the present position, and those regimes are where OpenCompetency's value is most immediate.

### 12.9 Driver licences

**Position: Reference.**

Driver licences have six classes and nine endorsements, and a card carries a licence number that stays the same across renewals and a version number that changes with each card.[^nztaclasses][^nztaexplained]

The licence number is a government identifier issued for one purpose, and section 7 rules it out as a subject identifier.

The Driver Licence Register is the national record, and employers may use a free service, with the driver's signed consent, to see classes, endorsements, conditions, and whether the licence is current, disqualified, suspended, revoked, or expired.[^dlr][^drivercheck]

Digital driver licences are now recognised in law, and the consultation on implementing rules proposed the ISO/IEC 18013-5 mobile driving licence standard.[^ddlact][^ddl]

That is the clearest case of a government-issued credential that a relying organisation will receive as an mdoc, and it is the reason section 5 requires conforming verifiers to accept that format.

### 12.10 Occupation classification

**Position: Reference, optional.**

Stats New Zealand's National Occupation List replaced the joint Australian and New Zealand classification for New Zealand use, with version 3.0 released on 1 January 2026 and concordances to the former classification and to ISCO-08.[^nol]

Where a Requirement record or an attestation names a role, the classification is a useful optional tag.

It should never be required, because most workplace roles are defined locally and more narrowly than any classification.

No New Zealand skills taxonomy was found.

### 12.11 Adoption elsewhere

No adoption of Open Badges, the Comprehensive Learner Record, or CTDL by a New Zealand government body was found.

Australia's proposed National Skills Passport reached a business-case stage in 2024, and no decision on it could be confirmed from official sources.[^skillspassport]

New South Wales issues an optional digital high-risk work licence with a public check by name or licence number, which is the closest operating example of a portable workplace licence in the region.[^nswhrwl]

None of this changes the positions above.

It confirms that OpenCompetency would not be duplicating a government programme, and that the vocabulary gap in section 16 is real.

## 13. Vocabulary for Organisations: Prequalification Records

No international data standard for contractor prequalification was found, and none was expected.

What exists in New Zealand is a regulator's position and template, an industry cross-recognition scheme, a number of commercial schemes, and a set of certifications and accreditations that buyers already accept.

Together they define the content OpenPrequal must be able to carry.

### 13.1 WorkSafe New Zealand's position and template

**Position: Reference, as the alignment target for OpenPrequal evidence categories.**

WorkSafe New Zealand's position statement, *The work health and safety information needed before hiring contractors*, states that WorkSafe expects a hiring business to request health and safety information from a contractor before engagement, that a formal prequalification process is one way of doing so, and that prequalification is not compulsory.[^wsposition]

It requires the amount of detail sought to be proportionate to the size, complexity, and risk of the work.

It notes that prequalification may be done "either through a formally recognised provider or through a simple conversation".

Alongside it, WorkSafe published a form titled *Risk-based health and safety pre-qualification information*, described as a template that "is not a checklist" and is intended to help small businesses bring together examples of their practice.[^wstemplate]

The template covers twelve topics.

1. business information;
2. key personnel;
3. sub-contractors;
4. associations, memberships, and competent advice and assessments;
5. health and safety record and regulator interventions over the last five years;
6. policy and procedures;
7. hazard identification and risk assessment;
8. worker engagement, participation, representation, and communication;
9. information, training, and supervision;
10. coordination;
11. emergency procedures and planning;
12. checking, investigating, and improving health and safety.

The Minister for Workplace Relations and Safety announced both documents on 20 August 2026, citing "a lack of consistency and duplication within New Zealand's prequalification systems", one submitter who had completed 76 prequalifications in a year, and an expectation that the template would be useful across government procurement so that "businesses do not need to complete multiple forms to 'prequalify' for working with different agencies".[^beehive2026]

An earlier announcement of 28 July 2025 had directed WorkSafe to revise its prequalification guidance, "including developing free-to-use templates to improve national consistency", and asked for an Approved Code of Practice on overlapping duties.[^beehive2025]

The template is a PDF form.

It defines no data format and says nothing about digital exchange, and WorkSafe states that it "does not manage how this template is used or see any user details".

That is exactly the point at which OpenPrequal can contribute.

OpenPrequal's evidence categories should map one-to-one onto the twelve topics, so that a supplier whose records are organised for OpenPrequal can answer the template, and a buyer who uses the template can receive the answer as verifiable records.

The topics are those of the July 2026 form, and the mapping is revised if the form is.

That is an alignment, not a dependency, and section 16.8 explains the difference.

### 13.2 An industry cross-recognition scheme

**Position: Reference, as an existing recognition arrangement OpenPrequal must be able to carry.**

Tōtika is a health and safety prequalification cross-recognition scheme governed by the board of trustees of Construction Health and Safety New Zealand, an industry-led charitable trust.[^totikarules][^chasnz]

Its published scheme rules describe a common standard for prequalification assessment, a register of assessed suppliers, cross-recognition of external audit effort, and a common supplier classification.

Several features are directly relevant to how OpenPrequal records should be modelled.

- suppliers are classified into a sole-trader category and three further categories by headcount, contract value, and whether their primary activity is on a high-risk or very-high-risk list;
- assessments are conducted by independently audited member schemes, which may be commercial or non-commercial, against a published core criteria and assessment standard;[^totikacore]
- a supplier's listing carries a status of performing or developing and a percentage score, and expires after one year, or two years for the smaller categories;
- external certifications are cross-recognised as an alternative to assessment where they are an ISO or New Zealand standard, or a scheme endorsed by a New Zealand regulator;
- uploaded certificates are checked for validity directly with the certifying body, and expired certificates cause the listing to lapse;
- buyers retain the right to use suppliers who are not listed;
- personal information not needed for assessment is to be removed from evidence before it is submitted.

Each of these has an OpenAssurance counterpart.

A member scheme's assessment is an Assessment record issued by that scheme, with category, status, score, and validity as claims.

The scheme's acceptance of a certification standard for a category is an Endorsement with a scope.

A buyer's requirement that suppliers hold a listing at a given category is a Requirement record.

The register is a Host and Holder of records that other parties issued, and holding them does not make it their issuer.

The manual check of an uploaded certificate against the certifying body is the authenticity and currency question that a signed record with a status list answers automatically.

The instruction to remove unneeded personal information is the minimum-disclosure principle applied to organisation evidence.

Two things should be said plainly.

OpenPrequal does not propose to replace this or any other scheme, and the Charter's non-goals exclude it from doing so.

Its proposal is that the records such a scheme produces, and the evidence its suppliers hold, should be portable and independently verifiable, so that a listing on one register can be presented to a buyer who uses another, and so that a certificate need not be re-verified by hand at every register that receives it.

### 13.3 Common questionnaire content

Prequalification questionnaires in commercial use in New Zealand were reviewed as background, and are not named here in keeping with the neutrality rule in `CONTRIBUTING.md`.

Their content overlaps heavily with the WorkSafe template and the cross-recognition scheme's core criteria.

The information categories that recur across all of them are:

- organisation details, size, and category;
- insurance, evidenced by certificates of currency;
- health and safety policy and procedures, or an external certification in their place;
- leadership and commitment;
- hazard and risk identification and controls, including a risk register and high-risk work;
- training, competency, and supervision, including a training register;
- incident and near-miss reporting, recording, and investigation;
- emergency management;
- worker engagement, participation, and communication;
- health monitoring and wellbeing;
- inspections and checking;
- subcontractor management;
- plant and equipment;
- hazardous substances;
- health and safety performance history and regulator interventions;
- declarations.

Three modelling conventions also recur.

- assessment results are expressed as a percentage score and a tier;
- validity periods are tiered by score or by category, from six months to two years;
- sharing of a result with more than one client is offered within a scheme's own platform.

The last convention is the structural problem the Charter describes, and it is stated here without attribution because every scheme reviewed shares it.

### 13.4 Certifications and accreditations buyers already accept

**Position: Reference.**

Several certification and accreditation outcomes are already accepted by buyers and by the cross-recognition scheme as evidence of a health and safety system.

- ISO 45001 certification, where the certifier is accredited by a member of the International Accreditation Forum;
- NZS 7901 certification of safety management systems for public safety in the electricity and gas industries;[^nzs7901]
- a SafePlus onsite assessment, the joint programme of WorkSafe, ACC, and the Ministry of Business, Innovation and Employment;[^safeplus]
- accreditation under the ACC Accredited Employers Programme;
- a Maritime Operator Safety System audit under Maritime New Zealand.

Each is an Assessment record whose issuer is the certifier, assessor, or regulator, and whose currency is defined by its own audit cycle.

Accreditation of the certifier, by JAS-ANZ or another accreditation body, is an Endorsement of the issuer that a relying organisation may require.

OpenPrequal needs to be able to carry these as records with their original issuer visible.

It does not need to define any of them.

### 13.5 Insurance

**Position: define, as a small record type.**

No New Zealand open data standard for a certificate of currency was identified.

Insurers and brokers issue certificates as documents, and buyers verify them by inspection or by contacting the insurer.

An insurance record in OpenPrequal is an ordinary credential issued by the insurer or broker about the insured organisation, carrying policy type, insured party, limit, period, and a hash-linked copy of the certificate through `relatedResource`.

Whether insurers will issue such records is a question for Phase 1 engagement.

Until they do, a supplier's hosted service may hold the certificate as Evidence with the insurer identified as the source, which is weaker but honest about who asserted what.

### 13.6 Declarations

A declaration is a signed statement by the supplier about itself, such as a statement that it has no undisclosed regulator interventions.

It is an Attestation whose issuer and subject are the same organisation.

The data model represents that without difficulty, and the profile only needs to say so.

### 13.7 What OpenPrequal has to define

Section 16 collects the gaps.

For organisations, the genuinely new content is a small vocabulary that:

- names the evidence categories, aligned to the WorkSafe template topics;
- separates supplier evidence from an assessor's assessment of it, as the profile already requires;
- expresses an assessment result with category, status, score, and validity in a scheme-neutral way;
- expresses a buyer requirement in terms of accepted assessments, accepted certifications, accepted endorsements, and required standalone evidence.

None of this replaces any scheme's methodology, scoring, or criteria, which remain the scheme's own.

## 14. New Zealand Legal and Government Context

OpenAssurance operates inside New Zealand law and alongside government digital identity infrastructure that has moved quickly since the landscape document was first drafted.

Nothing here is something OpenAssurance can adopt or profile in the technical sense.

It is what OpenAssurance must be consistent with.

### 14.1 Privacy Act 2020

**Position: Reference, and the subject of the Privacy Impact Assessment.**

The landscape document lists the Information Privacy Principles that bear on OpenAssurance, and `PRIVACY-PRINCIPLES.md` sets out the design response.

Two developments since then need recording.

Information Privacy Principle 3A, which requires an agency that collects personal information indirectly to take reasonable steps to make the individual aware of it, was enacted by the Privacy Amendment Act 2025 and came into force on 1 May 2026.[^ipp3a]

It applies to personal information collected from that date, and it contains a worked exception: the receiving agency need not notify where the original collector has already told the individual about the disclosure.[^ipp3a]

That exception is directly relevant to an employer presenting a worker's record to a customer, and the Privacy Impact Assessment should examine which party's notice covers which flow.

Information Privacy Principle 13 permits an agency to assign a unique identifier only where necessary for its functions, prohibits assigning an identifier that another agency has already assigned, and restricts requiring its disclosure.[^ipp13]

Section 7's identifier design is built to sit inside that principle, and section 18 records the question that should be put to the Office of the Privacy Commissioner.

The Office of the Privacy Commissioner publishes a Privacy Impact Assessment toolkit, revised in 2024, which is the method the required assessment should follow.[^piatoolkit]

### 14.2 Digital Identity Services Trust Framework

**Position: Reference, as a compatibility target and a voluntary accreditation signal.**

The Digital Identity Services Trust Framework Act 2023 came fully into force on 1 July 2024.[^distfact]

It establishes a Trust Framework Board, a Trust Framework Authority, an accreditation regime, a public register of accredited providers and services, and a rule-making power covering identification management, privacy, security, information and data management, and sharing.[^distfact]

Accreditation is voluntary.

A provider "may apply" to be accredited, a service may lawfully be provided without accreditation, and the rules apply only to accredited services.[^distfact]

The Trust Framework functions moved from the Department of Internal Affairs to the Government Digital Delivery Agency, established within the Public Service Commission on 1 April 2026.[^gdda]

Three things in the Trust Framework matter to OpenAssurance.

First, the Act's definition of a digital identity service expressly covers sharing organisational information as well as personal information, so an OpenPrequal service is within its scope.[^distfact]

Second, the Trust Framework Rules specify the credential formats an accredited credential service may use: the W3C Verifiable Credentials Data Model in its latest Recommendation, ISO/IEC 18013-5, or the ISO/IEC 23220 series.[^distfrules]

An OpenAssurance record on the W3C data model is therefore a format the Trust Framework already recognises.

Third, the Rules require revocation for any accredited credential valid for more than 72 hours, prohibit server retrieval during presentation, and discourage display-only credentials.[^distfrules][^dciptech]

They also require an accredited credential service to keep a distinct cryptographic trust chain, whose issuing and root certificates are not shared with any non-accredited service.[^distfrules]

Those constraints are consistent with the OpenAssurance design and should be treated as a floor, and the trust-chain rule is a design constraint for any hosted OpenAssurance service that intends to seek accreditation for some of its credentials and not others.

The framework is open to private providers as well as government agencies: the regulations require a provider to be a government agency or a New Zealand resident, which for an organisation means one formed or incorporated in New Zealand and carrying on business here.[^distfregs]

Accreditation expires three years after it is granted or renewed, and the 2026 amendment rules describe themselves as introducing emerging standards for interoperable verifiable credential presentation.[^distfregs][^distfaccred][^distfrules]

OpenAssurance must not require accreditation as a condition of participation, because the Act itself does not, and because doing so would make a voluntary government register a mandatory one for workplace records.

It should be designed so that a hosted OpenAssurance service could seek accreditation if its operator chose to.

### 14.3 The government wallet, issuance platform, and verifier

**Position: Reference, and the source of the decision in section 17.3.**

The Govt.nz app was released on 10 December 2025, and its digital wallet is now available, with accredited credentials expected to become available progressively from October 2026.[^govtapp][^govtwallet]

Participation is stated to be voluntary, credentials are stored on the device rather than in a central database, and signatures are verified against published issuer keys without contacting the issuer.[^govtwalletprivacy]

The Government Digital Delivery Agency publishes the technical guides for the wallet and for the government's credential issuance platform openly.[^wallettech][^dciptech]

They show a consistent design.

- credentials are mdoc, on ISO/IEC 18013-5 and the ISO/IEC 23220 series;
- issuance uses OpenID for Verifiable Credential Issuance;
- presentation uses ISO/IEC 18013-5 proximity flows and OpenID for Verifiable Presentations as profiled by ISO/IEC 18013-7;
- revocation uses the IETF Token Status List draft;
- the W3C Digital Credentials API is planned for online presentation;
- government agencies that issue credentials must use the government issuance platform, while other organisations run their own conformant issuance service and supply their certificate authority and issuance address for the wallet's trusted issuer list;
- the wallet is open to any organisation, government or private, whose credential is accredited.

The private-issuer pathway is no longer theoretical.

On 16 September 2026 the Trust Framework Register recorded the accreditation of a registered bank as a credential provider, with a business bank account credential issued into the Govt.nz app.[^tfregister]

The structure this produces is federated rather than centralised: government issuers use a shared platform, private accredited issuers use their own, and both meet at accreditation and the trust list.

That is consistent with the Charter, because it does not make government infrastructure a precondition for issuing a credential.

The NZ Verify app, released in May 2025, verifies Trust Framework accredited credentials and ISO/IEC 18013-5 mobile driving licences, checks the signature against the issuer's public key, checks expiry and revocation, and then checks acceptability for a selected purpose.[^nzverify][^nzverifytech]

It keeps no information after verification.

That three-step check is the OpenAssurance trust flow with the recognition question answered by the government trust list, and the acceptance question answered by the app's purpose templates.

Digital driver licences are now recognised in law alongside physical ones, and the implementing rules were consulted on in mid-2026.[^ddl]

The consequence for OpenAssurance is stated in section 5.

The government has chosen mdoc for the credentials it issues, the W3C data model is permitted but not implemented in government tooling, and the protocols in between are the same ones this map adopts.

OpenAssurance should adopt the shared protocols, keep the W3C data model for its own records, require its verifiers to accept government-issued mdoc presentations, and decide before v0.1 whether an mdoc representation of OpenCompetency records is worth defining.

### 14.4 Health and Safety at Work Act 2015

**Position: Reference.**

The Act's overlapping-duties provisions require persons conducting a business or undertaking with shared duties to consult, cooperate, and coordinate so far as is reasonably practicable, and WorkSafe's position is that a prequalification does not by itself discharge those duties.[^wsposition]

OpenAssurance records support the information exchange that consultation needs.

They do not replace it, and the profile should say so.

### 14.5 New Zealand Business Number Act 2016

**Position: Reference, with the identifier adopted in section 7.**

The Act's purposes include enabling businesses to interact more easily with each other, reducing transaction costs, and protecting the privacy of individuals in business.[^nzbnact]

Its public and non-public data classes, and its treatment of unincorporated entities, are the reason section 7 cautions that a sole trader's NZBN is personal information.

### 14.6 Mandated government data standards

**Position: Reference.**

The Government Chief Data Steward maintains a register of data standards mandated for public service departments, including person name, date of birth as ISO 8601-1:2019, and street address as ISO 19160-1:2015.[^mandated]

Where an OpenAssurance record carries a person's name or address as a claim, the profile should use those representations, so that records exchanged with government need no translation.

No mandated standard exists for organisation identity beyond the NZBN.

## 15. Summary Map

The table collects every position in this document, ordered by the layers in section 4.

Status is as verified on 16 September 2026.

| Need | Candidate | Status | Position |
|---|---|---|---|
| Record structure | W3C Verifiable Credentials Data Model 2.0 | Recommendation, May 2025 | Adopt |
| Record schema binding | W3C VC JSON Schema | Candidate Recommendation Draft | Adopt as prospective |
| Evidence held by a party other than its source | W3C VC `evidence` and `relatedResource` | Recommendation | Profile as Evidence record |
| Alternative record format | IETF SD-JWT VC | Internet-Draft, at IESG | Evaluate |
| Alternative record format | ISO/IEC 18013-5 and 23220 mdoc | International Standard and Technical Specifications | Evaluate; Reference for government-issued credentials |
| Signing, baseline | W3C VC-JOSE-COSE with RFC 9901 SD-JWT | Recommendation and RFC | Profile, mandatory to implement |
| Signing, alternative | W3C Data Integrity 1.0 with EdDSA and ECDSA cryptosuites | Recommendation | Profile, optional |
| Selective disclosure, unlinkable | W3C BBS cryptosuite | Candidate Recommendation Draft | Set aside for v0.1 |
| Issuer key discovery | W3C Controlled Identifiers 1.0 | Recommendation | Adopt |
| Verification after key rotation or issuer closure | Controlled Identifiers `expires` and `revoked`; ETSI trusted-list status history | Recommendation; Technical Specification | Define conformance rules |
| Issuer identifiers | W3C DIDs 1.0; `did:web`; `did:key` | Recommendation; Community Group drafts | Reference; Evaluate as conventions |
| Subject identifiers, people | none | | Profile: optional, scoped, never a government number |
| Organisation identifiers | New Zealand Business Number | Statutory, public API | Adopt |
| Organisation identifiers | Legal Entity Identifier, ISO 17442 | International Standard, open data | Adopt as alternative |
| Organisation identifiers | ISO/IEC 6523 and GS1 Global Location Number | International Standard | Reference |
| Validity period | `validFrom`, `validUntil`, RFC 3339 | Recommendation, RFC | Adopt |
| Revocation and suspension | W3C Bitstring Status List 1.0 | Recommendation | Adopt |
| Revocation for mdoc | IETF Token Status List | Internet-Draft, used by government platform | Reference, verifiers must check |
| Supersession and correction | none | | Define |
| Licence currency | regulator public registers | Web lookups, no API | Reference |
| Presentation container | W3C Verifiable Presentations | Recommendation | Adopt with terms-of-use profile |
| Issuance protocol | OpenID4VCI 1.0 | Final, September 2025 | Adopt, profiled |
| Presentation protocol | OpenID4VP 1.0 | Final, July 2025 | Adopt, profiled |
| Transaction query | DCQL | Part of OpenID4VP 1.0 | Adopt |
| Transaction query | DIF Presentation Exchange 2.1.1 | DIF Ratified, not referenced by OpenID4VP 1.0 | Set aside |
| Browser mediation | W3C Digital Credentials API | Working Draft | Evaluate |
| Online mdoc presentation | ISO/IEC TS 18013-7 | Technical Specification | Reference |
| Organisation-to-organisation transfer | none | | Define as exchange convention |
| Endorsement | Open Badges 3.0 EndorsementCredential | Final, June 2024 | Profile with scope |
| Recognition publishing | OpenID Federation 1.0 | Final, February 2026 | Evaluate |
| Recognition publishing | W3C Recognized Entities 1.0 | Working Draft | Evaluate |
| Recognition publishing | ETSI TS 119 612 and TS 119 602 | Technical Specifications | Reference |
| Recognition source | government trust list, VICAL | Operating, sandbox | Reference |
| Requirement expression | CTDL ConditionProfile | Stable vocabulary, CC BY | Evaluate |
| Requirement expression | none publishable and executable | | Define |
| Achievement vocabulary | Open Badges 3.0 | Final, June 2024 | Profile, base for achievements |
| Many achievements, one person | Comprehensive Learner Record 2.0 | Final, February 2025 | Evaluate for bulk transfer |
| Credential type descriptions | CTDL | Stable vocabulary, CC BY | Evaluate |
| Public web descriptions | Schema.org | Living vocabulary | Reference |
| New Zealand credential schemas | published schemas at credentialschema.nz | Licence and governance unstated | Evaluate, pending answers |
| Qualification and standard identifiers | NZQCF standard, qualification, and micro-credential numbers | Public, no API | Adopt as alignment targets |
| Formal achievement source | New Zealand Record of Achievement | PDF with online verification | Reference |
| University qualification documents | My eQuals, governed by participating providers | Operating; signed PDFs and shared links | Reference |
| Occupation classification | Stats NZ National Occupation List | Version 3.0, January 2026 | Reference, optional |
| Attestation and authorisation | none | | Define |
| Prequalification evidence categories | WorkSafe risk-based template, twelve topics | Published July 2026, PDF | Reference as alignment target |
| Prequalification recognition | industry cross-recognition scheme | Operating, published rules | Reference |
| Prequalification assessment and requirement structure | none | | Define |
| Certifications buyers accept | ISO 45001, NZS 7901, SafePlus, ACC AEP, MOSS | Operating | Reference |
| Insurance | none | | Define as small record type |
| Personal information | Privacy Act 2020, including IPP 3A from May 2026 | In force | Reference; PIA required |
| Trust framework | Digital Identity Services Trust Framework Act 2023 and Rules | In force, voluntary accreditation | Reference; compatibility target |
| Government wallet and verifier | Govt.nz app, issuance platform, NZ Verify | Operating, mdoc | Reference; verifiers accept mdoc |
| Person name, date, address | mandated government data standards | Mandated for departments | Reference |

Forty-seven of the fifty-four rows point at something that already exists.

Seven say "Define", and two more, endorsement scope and presentation terms of use, are profiles that add a small vocabulary of their own.

Section 16 describes what each of those requires.

## 16. What Remains Genuinely New

The purpose of this phase was to find the smallest layer OpenAssurance has to define itself.

Everything below the workplace vocabulary is covered by a stable standard, and the map adopts or profiles it.

What remains is short.

### 16.1 Workplace attestation and authorisation

Open Badges describes achievements: something a person completed, passed, or was awarded.

Workplace assurance also relies on two things that are not achievements.

An **attestation** is a statement by a supervisor, employer, or assessor that a person performed or demonstrated something, over a period, on a stated basis such as direct observation.

An **authorisation** is a permission an organisation grants a person to do defined work, under conditions, until withdrawn.

Neither has a home in any vocabulary examined.

OpenCompetency should define both as small credential types on the W3C data model.

**Three layers behind one signature.**

The paper world bundles authenticity, authorship, and authority into a single signature on a form.

A digital attestation should keep them apart.

- the **issuer** is the organisation whose key signs the record, identified by its NZBN or controller document, and authenticity is checked against that key;
- the **attestor** is the person inside the organisation who observed or decided something, named in the record with their role, and their identity is a claim the organisation makes and is accountable for;
- the **authority** is what entitles the attestor to make the statement, and it is a reference to another record or to a public register, not free text.

A relying organisation relies on the employer, not on a private individual, and that is why the organisation signs.

The authority reference is the useful design move.

The entitlement to attest is itself an OpenCompetency record: an employer's Authorisation designating a person as a workplace assessor for a scope, an assessor's own qualification, a professional register entry, or a director's listing on the Companies Register.

An attestation that references its attestor's authority can be checked to the same depth a relying organisation chooses to go, and no deeper.

**What an attestation carries.**

- the subject, by claims or by a scoped identifier as section 7 requires;
- the assertion: what was performed, demonstrated, or maintained, and the type of statement being made;
- the scope: activity, equipment, conditions, and site or context where that matters;
- the period over which it was observed;
- the basis: direct observation, supervision, review of records, or assessment against stated criteria;
- an optional alignment to a standard, qualification, or internal procedure by identifier;
- the attestor's name, role, and authority reference;
- validity, and a status entry so that it can be withdrawn.

**What an authorisation carries.**

- the subject;
- the permission: the work the person may do, and the equipment, site, or context it applies to;
- the conditions attached, such as supervision, hours, or exclusions;
- the prerequisites relied on, as references to the credentials and attestations that satisfied them;
- the granting role, and its authority reference where the organisation chooses to give one;
- validity, and a status entry, because an authorisation is revoked more often than it expires.

**Who may attest.**

A director is publicly listed against the NZBN, directors already sign tender declarations, and a false declaration by a director has consequences the law understands.

An organisation-level declaration in OpenPrequal should therefore carry the declarant's name, their role as director or officer, and the register that lists them, and the NZBN authority credential the government is trialling would be the machine-verifiable form of the same thing.

A director did not watch a worker operate a machine, and an attestation's value comes from proximity to the work.

Observed competency should be attested by the person who observed it, and requiring officer sign-off on such records would make them less informative rather than more.

An authorisation is an organisational act, so it should name the granting role, and a Requirement record may demand officer-level grant for high-risk work if the relying organisation wants that.

The standard should not fix the level; local acceptance does.

A Justice of the Peace witnessing a statutory declaration proves that the declarant signed and places them under the Oaths and Declarations Act 1957.

It says nothing about competency, and it does not scale to the volume of attestations a workplace produces.

Witnessing should not be built into the standard, and where a relying organisation requires a witnessed declaration it should be attached as hash-linked Evidence, as an insurance certificate is.

**Self-declaration.**

Where issuer, attestor, and subject are the same party, as they are for a sole trader, the record is a self-declaration and should say so.

Its value comes from corroboration by other records, not from its signature.

**Attestation is not assessment.**

An attestation is a first-hand statement by someone with direct knowledge.

An assessment is an opinion formed by reviewing evidence, and the architecture overview already keeps the two apart.

A record that mixes them, such as a supervisor's statement that also grades the worker against criteria, should be issued as an attestation with an alignment, not as an assessment.

**Worked example.**

The example is illustrative only, from food manufacturing, and every name, identifier, and role in it is fictional.

A supervisor at a beverage bottling plant observes a worker operating the depalletiser on one packaging line over four months.

```text
Attestation

Issuer:
Harbour Beverages Limited (NZBN, illustrative)

Subject:
Worker, identified by an employer-scoped identifier

Assertion:
Operated the depalletiser on packaging line 2 under normal
production conditions, including start-up, jam clearing, and
end-of-shift isolation

Period:
March 2026 to June 2026

Basis:
Direct observation during supervised shifts

Alignment:
Site procedure PL2-OP-04, version 3
NZQCF standard [identifier] version [n], illustrative

Attestor:
T. Ngata, Packaging Shift Supervisor

Authority:
Authorisation issued by Harbour Beverages Limited designating
T. Ngata as workplace assessor for packaging line equipment

Validity:
Until 30 June 2028, subject to status
```

On the strength of that attestation, the worker's forklift endorsement, and a site induction, the employer then grants an authorisation.

```text
Authorisation

Issuer:
Harbour Beverages Limited (NZBN, illustrative)

Subject:
Worker, identified by an employer-scoped identifier

Permission:
Operate the depalletiser and associated conveyors on packaging
line 2 without supervision

Conditions:
Not during clean-in-place cycles
Not while line guarding is removed for maintenance

Prerequisites relied on:
Attestation above
Driver licence F endorsement, current
Site induction, completed 2 March 2026

Granted by:
Production Manager

Validity:
Until 30 June 2027, subject to status
```

A customer that receives the authorisation can verify the employer's signature, check that neither record has been revoked, decide whether it recognises the employer as an issuer for this purpose, and apply its own requirement.

If its requirement asks for evidence of assessor competence, the authority reference leads to the supervisor's assessor authorisation, and the customer decides whether that satisfies it.

Nothing in either record needs the customer to be a tenant of the employer's system, or the employer of the customer's.

The July 2025 ministerial statement's observation that "on-the-job experience should be better recognised" and that there is confusion "about the distinction between qualifications and actual competency" is the policy case for this item.[^beehive2025]

### 16.2 Requirement expression

Section 11 found a query language and a descriptive condition vocabulary, and no publishable requirement model that translates into a query.

OpenAssurance should define a Requirement record and its translation to DCQL.

### 16.3 Endorsement scope

Section 10 found an endorsement credential without scope.

OpenAssurance should define the scope vocabulary.

### 16.4 Prequalification evidence, assessment, and requirement vocabulary

Section 13 found a public template, a cross-recognition scheme, and a set of accepted certifications, and no data model for any of them.

OpenPrequal should define the evidence categories, the assessment-result structure, and the buyer-requirement structure, aligned to the WorkSafe template and neutral between schemes.

It should also publish an illustrative Requirement record that expresses the six information areas in WorkSafe's position statement, as a starting template a buyer adapts, without implying that WorkSafe endorses it.[^wsposition]

### 16.5 Presentation terms of use

Section 9 found that recipient, freshness, and expiry are standard, and that purpose, onward-sharing expectation, and retention guidance are not.

OpenAssurance should define a terms-of-use vocabulary for presentations.

### 16.6 Supersession and correction linkage

Section 8 found revocation and suspension standardised, and no way to link a replacement or correction to the record it replaces.

OpenAssurance should define the linking terms.

### 16.7 Exchange conventions and conformance

Section 9 found stable protocols for issuance and interactive presentation, and no rule that guarantees a record can leave one system and enter another.

OpenAssurance should define the file-based floor, the import and export obligations, and the conformance tests that make the Charter's open exchange requirement checkable.

### 16.8 What depends on another party

None of the seven items above requires anyone outside OpenAssurance to act before it can be defined.

Several deliver more once a counterparty issues signed records, and the profile should state what it does until then.

- an assessment result from a prequalification scheme is defined from the scheme's published rules, and until the scheme issues it as a signed record it is carried as hash-linked Evidence held by the supplier, with the scheme identified as the source and not as the issuer;
- a certificate of currency is carried the same way, with the insurer or broker as the source;
- a formal achievement is carried the same way from the Record of Achievement, with the Qualifications Authority as the source and its own online verification alongside;
- a published New Zealand credential schema is bypassed on the Open Badges base if its licence terms prove not to be open;
- the government wallet affects only whether an mdoc rendering is defined, not the record itself.

In each case the fallback is what happens today, with structure, integrity, and purpose-bound presentation added, and with authenticity resting on the document rather than on a signature.

That is weaker, and the profile should say so plainly rather than let a held copy imply the issuer's signature.

The evidence layer, where most of the repeated data entry occurs, belongs to the supplier or the worker and needs no counterparty at all.

Where a counterparty does sign, the record moves from Evidence to Credential or Assessment without any change to the vocabulary, which is the upgrade path the profile should be designed around.

### 16.9 What is not on the list

The following were considered and are not needed, because a standard already covers them.

- a credential format;
- a signature scheme;
- a status or revocation protocol;
- an identifier scheme for issuers or organisations;
- an issuance protocol;
- a presentation protocol or query language;
- a trust-list format;
- a schema language;
- an achievement vocabulary.

If a later proposal reintroduces any of these, it should be tested against this section first.

## 17. Decisions Required Before v0.1

The following choices are open and are recorded here so that Phase 3 starts from them rather than rediscovers them.

Each is stated with the path v0.1 should take unless something changes, and with what would change it.

A likely path is a working assumption, not a decision, and Phase 3 should confirm or overturn each one in writing.

### 17.1 Securing baseline

The question is whether the JOSE envelope is the mandatory-to-implement mechanism with Data Integrity optional, or the reverse.

Likely path: the JOSE envelope is mandatory to implement, the SD-JWT envelope is permitted where selective disclosure is needed, and Data Integrity proofs are permitted but not required, as section 6 recommends.

This would change if the Trust Framework Rules came to mandate a securing mechanism, or if a major New Zealand issuer of workplace-relevant credentials adopted Data Integrity and interoperability with it mattered more than implementation cost.

### 17.2 Issuer identifier form

The question is whether to require an HTTPS URL with a controller document, permit `did:web` as a convention, or permit both.

Likely path: an HTTPS URL under the issuer's control, resolving to a Controlled Identifiers document, is the baseline; `did:web` is permitted as a convention that resolves to the same document; no DID method that depends on a ledger, registry, or network is required.

This would change if DIDs 1.1 and DID Resolution reached Recommendation and a DID method for organisations gained a standards-track home, at which point the convention could become a normative option.

### 17.3 Accepting and producing mdoc

The question is whether a conforming verifier must accept mdoc presentations of government-issued credentials, and whether OpenCompetency defines an mdoc namespace rendering of its own records.

Likely path: a conforming verifier must accept an mdoc presentation of any government-issued credential that a Requirement record names, such as a driver licence or an NZBN credential; OpenCompetency records stay on the W3C data model with their claims specified independently of either container; an mdoc rendering is not defined in v0.1.

This would change if the Government Digital Delivery Agency confirmed that the wallet will not hold W3C-model credentials and worker-held competency records in the government wallet became a priority use case, in which case the rendering would be defined as a v0.x addition without changing the vocabulary.

### 17.4 Open Badges as base

The question is whether every OpenCompetency record is an Open Badges credential, or only those that are achievements in the Open Badges sense.

Likely path: qualifications, licences, training, assessments, and certifications are Open Badges achievement credentials; attestations and authorisations are OpenAssurance types on the plain W3C data model, sharing subject and alignment claim names with the achievement records but not forced into an achievement shape.

This would change if 1EdTech added workplace attestation and authorisation semantics to Open Badges, in which case the OpenAssurance types would be re-based on them.

### 17.5 New Zealand credential schemas

The question is whether to align with the published schemas at credentialschema.nz, which depends on the openness answers in section 12.5.

Likely path: define on the Open Badges base without waiting, and use the published schemas' field names wherever the two coincide, which costs nothing.

This would change if the publisher confirmed open licence terms and an open change process, in which case OpenCompetency would align formally and say so.

### 17.6 Organisation identifier

The question is whether the NZBN is required for New Zealand organisations or merely preferred.

Likely path: the NZBN is required for a New Zealand organisation acting as an issuer, and for the subject of an OpenPrequal record; it is preferred elsewhere; the LEI is accepted for organisations without an NZBN; a sole trader's NZBN is handled as personal information.

This would change if the Privacy Impact Assessment found that requiring a sole trader's NZBN created a disclosure the purpose does not need, in which case the requirement would apply to incorporated entities only.

### 17.7 Recognition publishing format

The question is whether to defer a format for publishing recognition lists, or to adopt one of the two candidates as prospective.

Likely path: defer, as section 10 recommends; define the Endorsement record and require that it can be issued, held, and presented like any other record; leave list publication to a later version.

This would change when either Recognized Entities reaches Candidate Recommendation or OpenID Federation for wallet architectures reaches Final, whichever comes first, at which point that one is adopted as prospective.

### 17.8 CTDL terms

The question is whether to borrow condition-profile terms for the Requirement record or define OpenAssurance's own.

Likely path: borrow the CTDL terms that match exactly, such as those for alternative conditions, target credentials, target competencies, and years of experience, define the rest, and depend on the vocabulary alone rather than on the registry around it.

This would change if the borrowed terms proved to carry meaning that does not survive translation to a DCQL query, in which case OpenAssurance would define its own and record the mapping.

### 17.9 Verification over time

The question is how records remain verifiable after an issuer rotates keys or ceases to exist, beyond the conformance rules in section 6.4.

Likely path: the conformance rules in section 6.4 apply from v0.1; the enduring-party question is put to regulators and industry bodies during Phase 1 engagement; no ledger or central archive is proposed.

This would change if a regulator or industry body volunteered to publish endorsements of issuers' historic keys for its sector, in which case the Endorsement record would gain a scope value for that purpose.

## 18. Open Questions

These could not be settled from published material and should be put to the parties named.

- to the publisher of the New Zealand credential schemas: the licence terms and the process for proposing changes;
- to the Government Digital Delivery Agency: whether the Govt.nz wallet is intended to hold native W3C Verifiable Credentials Data Model 2.0 credentials in addition to mdoc, and if so, what trust-list mechanism and credential profile an accredited non-government issuer would need to meet;
- to the Government Digital Delivery Agency: whether the issuance platform is intentionally restricted to government agencies, or whether accredited private credential providers will become eligible for a hosted issuance tenancy;
- to New Zealand Government Procurement: whether a common structured form for health and safety prequalification is being developed for use across government agencies, as the Minister's statement of 20 August 2026 anticipated, and whether it will have a defined data structure;[^beehive2026]
- to occupational regulators: whether machine-checkable licence status is available or planned, and on what terms;
- to the New Zealand Qualifications Authority: whether the mechanism behind its document verification tool can be documented so that a hash-linked copy can be relied on, whether verifiable credential forms of the Record of Achievement and the International Qualification Assessment are planned, and whether standard and qualification identifiers are available as open data;
- to insurers and brokers: whether a verifiable certificate of currency is feasible;
- to buyers and relying organisations: what an assessment result must carry for them to accept it without access to the scheme that produced it, and which of those things they cannot get today;
- to the operators of existing prequalification schemes: whether they would issue their assessment result as a signed record the supplier holds, what it would carry, and on what commercial terms;
- to suppliers: whether they currently receive a copy of their own assessment result that they can give to anyone;
- to the Office of the Privacy Commissioner: whether the identifier approach in section 7 is consistent with Information Privacy Principle 13 as applied to employer-scoped identifiers;
- to the project's governance: how the standard should engage with te ao Māori approaches to identity and with Māori data governance, given that the Trust Framework Act's purposes expressly include the former.[^distfact]

The question to buyers is a requirement rather than a research item, and belongs with Phase 1 validation.

None of these answers is a precondition for Phase 3, for the reasons given in section 16.8.

## 19. Design Test

> **Can every part of a conforming record be validated using a published, openly licensed standard, with OpenAssurance defining only the workplace vocabulary, requirement expression, and exchange conventions that no existing standard provides?**

If a proposal adds to the list in section 16, it should show why the standards in this map cannot carry the requirement without loss of meaning.

If it removes from that list, it should show which existing standard now does the job.

## 20. Sources

Every status and date in this document was checked against the source listed on 16 September 2026.

References to external organisations, schemes, and government publications are provided as evidence of what exists. No such reference implies consultation, participation, support, or endorsement.

[^vcdm2]: W3C, "Verifiable Credentials Data Model v2.0", W3C Recommendation, 15 May 2025. https://www.w3.org/TR/vc-data-model-2.0/

[^vcdm11]: W3C, "Verifiable Credentials Data Model v1.1", W3C Recommendation, 3 March 2022, carrying a June 2025 status update that the version is outdated. https://www.w3.org/TR/2022/REC-vc-data-model-20220303/

[^vcdm21]: W3C, "Verifiable Credentials Data Model v2.1", W3C Working Draft, 13 September 2026. https://www.w3.org/TR/vc-data-model-2.1/

[^vcjs]: W3C, "Verifiable Credentials JSON Schema Specification", W3C Candidate Recommendation Draft, 4 February 2025. https://www.w3.org/TR/vc-json-schema/

[^sdjwtvc]: IETF OAuth Working Group, "SD-JWT-based Verifiable Digital Credentials (SD-JWT VC)", Internet-Draft draft-ietf-oauth-sd-jwt-vc-19, 31 August 2026, submitted to the IESG for publication. https://datatracker.ietf.org/doc/draft-ietf-oauth-sd-jwt-vc/

[^arf]: European Commission, "European Digital Identity Wallet Architecture and Reference Framework", release 3.0.0, July 2026, section on data model and data exchange protocols. https://eudi.dev/latest/main/05-data-model-and-data-exchange-protocols/

[^mdl]: ISO/IEC 18013-5:2021, "Personal identification — ISO-compliant driving licence — Part 5: Mobile driving licence (mDL) application", International Standard, with a second edition at Draft International Standard stage. https://www.iso.org/standard/69084.html

[^iso23220]: ISO/IEC 23220 series, "Cards and security devices for personal identification — Building blocks for identity management via mobile devices", Part 1 published 2023 as an International Standard, later parts published as Technical Specifications or in draft. https://www.iso.org/standard/74910.html

[^mdl7]: ISO/IEC TS 18013-7:2025, "Personal identification — ISO-compliant driving licence — Part 7: Mobile driving licence (mDL) add-on functions", Technical Specification, under revision. https://www.iso.org/standard/91154.html

[^vcjose]: W3C, "Securing Verifiable Credentials using JOSE and COSE", W3C Recommendation, 15 May 2025. https://www.w3.org/TR/vc-jose-cose/

[^sdjwt]: IETF, "Selective Disclosure for JSON Web Tokens (SD-JWT)", RFC 9901, Proposed Standard, November 2025. https://www.rfc-editor.org/rfc/rfc9901.html

[^vcdi]: W3C, "Verifiable Credential Data Integrity 1.0", W3C Recommendation, 15 May 2025. https://www.w3.org/TR/vc-data-integrity/

[^vcdieddsa]: W3C, "Data Integrity EdDSA Cryptosuites v1.0", W3C Recommendation, 15 May 2025. https://www.w3.org/TR/vc-di-eddsa/

[^vcdiecdsa]: W3C, "Data Integrity ECDSA Cryptosuites v1.0", W3C Recommendation, 15 May 2025. https://www.w3.org/TR/vc-di-ecdsa/

[^vcdibbs]: W3C, "Data Integrity BBS Cryptosuites v1.0", W3C Candidate Recommendation Draft, 10 September 2026. https://www.w3.org/TR/vc-di-bbs/

[^cid]: W3C, "Controlled Identifiers v1.0", W3C Recommendation, 15 May 2025. https://www.w3.org/TR/cid-1.0/

[^did10]: W3C, "Decentralized Identifiers (DIDs) v1.0", W3C Recommendation, 19 July 2022. https://www.w3.org/TR/did-core/

[^did11]: W3C, "Decentralized Identifiers (DIDs) v1.1", W3C Candidate Recommendation Snapshot, 5 March 2026. https://www.w3.org/TR/did-1.1/

[^didweb]: W3C Credentials Community Group, "did:web Method Specification", unofficial draft. https://w3c-ccg.github.io/did-method-web/

[^didkey]: W3C Credentials Community Group, "The did:key Method v0.9", Draft Community Group Report. https://w3c-ccg.github.io/did-key-spec/

[^gs1icd]: GS1, "GS1 Application Standard for the use of ISO/IEC 6523 International Code Designator (ICD)", assigning ICD 0088 to the Global Location Number. https://ref.gs1.org/standards/icd/

[^iso6523]: ISO/IEC 6523-1:2023, "Information technology — Structure for the identification of organizations and organization parts — Part 1: Identification of organization identification schemes". https://www.iso.org/standard/82246.html

[^lei]: Global Legal Entity Identifier Foundation, "Introducing the Legal Entity Identifier (LEI)". https://www.gleif.org/en/about-lei/introducing-the-legal-entity-identifier-lei

[^leiopen]: Global Legal Entity Identifier Foundation, "Open data", LEI reference data published under a CC0 licence. https://www.gleif.org/en/about/open-data

[^vlei]: ISO 17442-3:2024, "Financial services — Legal entity identifier (LEI) — Part 3: Verifiable LEIs (vLEIs)". https://www.iso.org/standard/85628.html

[^rfc3339]: IETF, "Date and Time on the Internet: Timestamps", RFC 3339, July 2002. https://www.rfc-editor.org/info/rfc3339

[^bsl]: W3C, "Bitstring Status List v1.0", W3C Recommendation, 15 May 2025. https://www.w3.org/TR/vc-bitstring-status-list/

[^oid4vci]: OpenID Foundation, "OpenID for Verifiable Credential Issuance 1.0", Final Specification, 16 September 2025. https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0-final.html

[^oid4vp]: OpenID Foundation, "OpenID for Verifiable Presentations 1.0", Final Specification, 9 July 2025. https://openid.net/specs/openid-4-verifiable-presentations-1_0-final.html

[^dcapi]: W3C, "Digital Credentials", W3C Working Draft, 4 September 2026. https://www.w3.org/TR/digital-credentials/

[^pe]: Decentralized Identity Foundation, "Presentation Exchange 2.1.1", DIF Ratified Specification, 25 April 2024. https://identity.foundation/presentation-exchange/spec/v2.1.1/

[^oidfed]: OpenID Foundation, "OpenID Federation 1.0", Final Specification, 17 February 2026. https://openid.net/specs/openid-federation-1_0-final.html

[^oidfedwallet]: OpenID Foundation, "OpenID Federation for Wallet Architectures 1.0", draft 05, 15 February 2026. https://openid.net/specs/openid-federation-wallet-1_0.html

[^recog]: W3C, "Recognized Entities v1.0", W3C Working Draft, 6 September 2026. https://www.w3.org/TR/vc-recognized-entities-1.0/

[^etsi612]: ETSI, "Electronic Signatures and Trust Infrastructures (ESI); Trusted Lists", ETSI TS 119 612 V2.4.1, August 2025. https://www.etsi.org/deliver/etsi_ts/119600_119699/119612/02.04.01_60/ts_119612v020401p.pdf

[^etsi602]: ETSI, "Electronic Signatures and Trust Infrastructures (ESI); Lists of trusted entities; Data model", ETSI TS 119 602 V1.1.1, November 2025. https://www.etsi.org/deliver/etsi_ts/119600_119699/119602/01.01.01_60/ts_119602v010101p.pdf

[^vcvocab]: W3C, "Verifiable Credentials Vocabulary v2.0". https://www.w3.org/2018/credentials/

[^ob3]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", Final Release, 17 June 2024, with errata to revision 1.6 of 29 June 2026. https://www.imsglobal.org/spec/ob/v3p0/

[^ob3type]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", AchievementType enumeration. https://www.imsglobal.org/spec/ob/v3p0/#achievementtype-enumeration

[^ob3subject]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", AchievementSubject. https://www.imsglobal.org/spec/ob/v3p0/#achievementsubject

[^ob3align]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", Alignment. https://www.imsglobal.org/spec/ob/v3p0/#alignment

[^ob3aligntype]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", AlignmentTargetType enumeration. https://www.imsglobal.org/spec/ob/v3p0/#alignmenttargettype-enumeration

[^ob3evidence]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", Evidence. https://www.imsglobal.org/spec/ob/v3p0/#evidence

[^ob3endorse]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", EndorsementCredential and Profile. https://www.imsglobal.org/spec/ob/v3p0/#endorsementcredential

[^ob3licence]: 1EdTech Consortium, "Specification Document License". https://www.1edtech.org/standards/specification-license

[^ob3cert]: 1EdTech Consortium, "Open Badges 3.0 Specification Conformance and Certification Guide", version 1.5, 15 June 2026. https://www.imsglobal.org/spec/ob/v3p0/cert/

[^vcrelres]: W3C, "Verifiable Credentials Data Model v2.0", section 5.3, Integrity of Related Resources. https://www.w3.org/TR/vc-data-model-2.0/#integrity-of-related-resources

[^clr2]: 1EdTech Consortium, "Comprehensive Learner Record Standard, Version 2.0", Final Release, 26 February 2025. https://www.imsglobal.org/spec/clr/v2p0/

[^ctdl]: Credential Engine, "Credential Transparency Description Language (CTDL) Handbook", schema release 28 August 2026. https://credreg.net/ctdl/handbook

[^ctdllicence]: Credential Engine, CTDL licensing statement, Creative Commons Attribution 4.0 International. https://credreg.net/ctdl/handbook

[^ctdlscope]: Credential Engine, "CTDL Handbook", scope statement placing description of credentials awarded to a person outside the language. https://credreg.net/ctdl/handbook

[^ctdlcond]: Credential Engine, "CTDL Terms", ConditionProfile. https://credreg.net/ctdl/terms

[^schemaorg]: Schema.org, release history, version 30.1, 16 September 2026. https://schema.org/docs/releases.html

[^schemacert]: Schema.org, "Certification", added in release 25.0, 22 January 2024. https://schema.org/Certification

[^wsposition]: WorkSafe New Zealand, "The work health and safety information needed before hiring contractors", WorkSafe position, June 2026, page last updated 20 August 2026. https://www.worksafe.govt.nz/laws-and-regulations/operational-policy-framework/worksafe-positions/work-health-safety-info-needed-before-hiring-contractors/ and https://www.worksafe.govt.nz/dmsdocument/72833-the-work-health-and-safety-information-needed-before-hiring-contractors/latest/

[^wstemplate]: WorkSafe New Zealand, "Risk-based health and safety pre-qualification information", form, 2026. https://www.worksafe.govt.nz/dmsdocument/73194-risk-based-health-and-safety-pre-qualification-information-template/latest/

[^beehive2026]: New Zealand Government, "New template to simplify prequalification process", 20 August 2026. https://www.beehive.govt.nz/release/new-template-simplify-prequalification-process

[^beehive2025]: New Zealand Government, "Clearer rules and prequalification guidance to support construction", 28 July 2025. https://www.beehive.govt.nz/release/clearer-rules-and-prequalification-guidance-support-construction

[^totikarules]: Tōtika, "Scheme Rules", version 3.3.9, 2 December 2024. https://www.totika.org/resources/totika-scheme-rules-v3.3.9.pdf

[^totikacore]: Tōtika, "Core Criteria and Assessment Standard", version 3.1.4, 10 December 2024. https://www.totika.org/resources/totika-core-criteria-and-assessment-standard-v3.1.4.pdf

[^chasnz]: Construction Health and Safety New Zealand, "About". https://www.chasnz.org/about

[^safeplus]: WorkSafe New Zealand, "About SafePlus", a joint programme of WorkSafe New Zealand, ACC, and the Ministry of Business, Innovation and Employment. https://www.worksafe.govt.nz/managing-health-and-safety/businesses/safeplus/about-safeplus/

[^nzs7901]: Standards New Zealand, NZS 7901:2014, "Electricity and gas industries — Safety management systems for public safety". https://www.standards.govt.nz/shop/nzs-79012014/

[^ipp3a]: Privacy Amendment Act 2025, 2025 No 53, Part 1, inserting Information Privacy Principle 3A with effect from 1 May 2026. https://www.legislation.govt.nz/act/public/2025/0053/latest/whole.html

[^ipp13]: Office of the Privacy Commissioner, "Principle 13: Unique identifiers". https://www.privacy.org.nz/privacy-principles/13/

[^piatoolkit]: Office of the Privacy Commissioner, "Privacy Impact Assessments", toolkit revised 2024. https://www.privacy.org.nz/responsibilities/privacy-impact-assessments/

[^distfact]: Digital Identity Services Trust Framework Act 2023, 2023 No 13, sections 3, 8, 10, 15, 18 to 23, 34, 43, and 58. https://www.legislation.govt.nz/act/public/2023/0013/latest/whole.html

[^distfregs]: Digital Identity Services Trust Framework Regulations 2024, SL 2024/197, as amended 28 May 2026, regulations 3, 5, 9, and 13. https://www.legislation.govt.nz/regulation/public/2024/0197/latest/whole.html

[^distfrules]: Digital Identity Services Trust Framework Rules 2024, version 2, 24 July 2025, rules 8 and 9, as mirrored on the government standards site; consolidated rules of 29 June 2026 published by the Government Digital Delivery Agency. https://standards.digital.govt.nz/nz/dia-distfr/2/en/ and https://www.publicservice.govt.nz/about-the-commission/government-digital-delivery-agency/trust-framework-for-digital-identity/about-digital-identity-services/trust-framework-legislation/trust-framework-rules

[^gdda]: Government Digital Delivery Agency, "Government Digital Delivery Agency established", 2026. https://www.digital.govt.nz/news/government-digital-delivery-agency-established

[^govtapp]: New Zealand Government, "Government app launched today", 10 December 2025. https://www.beehive.govt.nz/release/government-app-launched-today

[^govtwallet]: New Zealand Government, "Digital wallet and credentials", Govt.nz app, page last updated September 2026. https://www.govt.nz/about/the-govt-nz-app/features-and-releases/digital-wallet-and-credentials/

[^govtwalletprivacy]: New Zealand Government, "Privacy and security for your digital wallet", Govt.nz app. https://www.govt.nz/about/the-govt-nz-app/privacy-and-security/privacy-and-security-for-your-digital-wallet/

[^wallettech]: Government Digital Delivery Agency, "Govt.nz app wallet technical guide". https://github.com/NZ-Digital-Public-Infrastructure/govt-nz-app-wallet

[^dciptech]: Government Digital Delivery Agency, "Digital Credentials Technical Guide" and "DCIP Onboarding Guide", Digital Credential Issuance Platform. https://github.com/NZ-Digital-Public-Infrastructure/nz-digital-credential-issuance-platform

[^dts]: Government Digital Delivery Agency, "Digital Trust Service", trust list for relying parties. https://github.com/NZ-Digital-Public-Infrastructure/digital-trust-service

[^tfregister]: Trust Framework Authority, "Trust Framework Register", as at 17 September 2026. https://www.publicservice.govt.nz/about-the-commission/government-digital-delivery-agency/trust-framework-for-digital-identity/trust-framework-authority/trust-framework-register

[^distfaccred]: Trust Framework Authority, "Accreditation of digital identity providers and services". https://www.publicservice.govt.nz/about-the-commission/government-digital-delivery-agency/trust-framework-for-digital-identity/information-for-providers/accreditation-and-maintenance/accreditation-of-digital-identity-providers-and-services

[^nzverify]: New Zealand Government, "What you can do with NZ Verify". https://www.govt.nz/about/nz-verify-app/what-you-can-do-with-nz-verify/

[^nzverifytech]: Government Digital Delivery Agency, "NZ Verify", technical documentation. https://github.com/NZ-Digital-Public-Infrastructure/nz-verify

[^ddl]: New Zealand Government, "Kiwis asked to help shape digital driver licences", 2026. https://www.beehive.govt.nz/release/kiwis-asked-help-shape-digital-driver-licences

[^beehivedcip]: New Zealand Government, "Making it faster and easier to issue digital credentials", 17 November 2025. https://www.beehive.govt.nz/release/making-it-faster-easier-issue-digital-credentials

[^nzbnact]: New Zealand Business Number Act 2016, 2016 No 16, sections 3, 20 to 29. https://www.legislation.govt.nz/act/public/2016/0016/latest/whole.html

[^nzbnabout]: New Zealand Business Number, "About the NZBN". https://www.nzbn.govt.nz/whats-an-nzbn/about/

[^nzbnget]: New Zealand Business Number, "Get an NZBN". https://www.nzbn.govt.nz/get-an-nzbn/

[^nzbnapi]: Ministry of Business, Innovation and Employment, "NZBN API", developer portal. https://portal.api.business.govt.nz/api/nzbn

[^nzbnbulk]: New Zealand Business Number, "Bulk data". https://www.nzbn.govt.nz/using-the-nzbn/nzbn-services/bulk-data/

[^leinz]: Global Legal Entity Identifier Foundation, registration authority RA000466, Companies Register, New Zealand. https://api.gleif.org/api/v1/registration-authorities/RA000466

[^mandated]: Government Chief Data Steward, "Mandated data standards register". https://www.data.govt.nz/toolkit/data-standards/mandated-standards-register

[^nzqcf]: New Zealand Qualifications Authority, "About the New Zealand Qualifications and Credentials Framework". https://www2.nzqa.govt.nz/qualifications-and-standards/about-new-zealand-qualifications-credentials-framework/

[^nzqatypes]: New Zealand Qualifications Authority, "About qualifications and credentials". https://www2.nzqa.govt.nz/qualifications-and-standards/about-qualifications-and-credentials/

[^nzqastandards]: New Zealand Qualifications Authority, "About standards". https://www2.nzqa.govt.nz/qualifications-and-standards/about-standards/

[^dassrules]: New Zealand Qualifications Authority, "Directory of Assessment and Skill Standards Listing and Operational Rules 2026", in force 19 January 2026. https://www2.nzqa.govt.nz/about-us/rules-fees-policies/nzqa-rules/dass-rules/

[^nzqasearch]: New Zealand Qualifications Authority, framework search for standards, qualifications, and micro-credentials. https://www.nzqa.govt.nz/framework/search/index.do

[^isbact]: Education and Training (Vocational Education and Training System) Amendment Act 2025, 2025 No 56, and Schedule 6 clause 183. https://www.legislation.govt.nz/act/public/2025/0056/latest/whole.html

[^isbs]: Ministry of Education, "Redesign of the vocational education and training system". https://www.education.govt.nz/our-work/strategies-policies-and-programmes/tertiary-and-further-education/redesign-vocational-education-and-training-system

[^nzqaopendata]: New Zealand Qualifications Authority, "List of Standards by Category", open data snapshots 2019 and 2020, data.govt.nz. https://catalogue.data.govt.nz/api/3/action/package_search?q=organization:new-zealand-qualifications-authority

[^nzroa]: New Zealand Qualifications Authority, "New Zealand Record of Achievement". https://www2.nzqa.govt.nz/qualifications-and-standards/access-your-results/new-zealand-record-of-achievement/

[^nzroaverify]: New Zealand Qualifications Authority, "Verify a New Zealand Record of Achievement". https://www2.nzqa.govt.nz/qualifications-and-standards/access-your-results/verify/

[^nzqacheck]: New Zealand Qualifications Authority, "Check a New Zealand qualification". https://www2.nzqa.govt.nz/international/check-qual/check-nz-qual/

[^myequals]: My eQuals, "About". https://myequals.org/about/

[^myequalsverify]: My eQuals, "Verifiers". https://myequals.org/verifiers/

[^nzqaverifydocs]: New Zealand Qualifications Authority, "Verify NZQA documents", covering the Record of Achievement, the International Qualification Assessment, and the Overseas Study Assessment. https://www2.nzqa.govt.nz/international/check-qual/verify-nzqa-docs/

[^ewrb]: Electrical Workers Registration Board, public register search and licence identification. https://kete.mbie.govt.nz/EW/EWPRSearch/ and https://www.ewrb.govt.nz/licences/licence-information/licence-ids/

[^pgdb]: Plumbers, Gasfitters, and Drainlayers Board, "Public register policy". https://www.pgdb.co.nz/media/2vgdigsd/public-register-policy.pdf

[^lbp]: Ministry of Business, Innovation and Employment, Licensed Building Practitioners register search; Building Act 2004, sections 298 to 309. https://kete-lbp.mbie.govt.nz/advanced-building-practitioner-search/

[^hpca]: Health Practitioners Competence Assurance Act 2003, sections 136 to 150. https://www.legislation.govt.nz/act/public/2003/0048/latest/whole.html

[^asbestos]: WorkSafe New Zealand, "Licence holder register", asbestos. https://www.worksafe.govt.nz/topic-and-industry/asbestos/licensing/licence-holder-register/

[^seacert]: Maritime New Zealand, seafarer certificate verification. https://services.maritimenz.govt.nz/seacert-search/default.aspx

[^handlers]: WorkSafe New Zealand, "Certified handlers". https://www.worksafe.govt.nz/topic-and-industry/hazardous-substances/certification-authorisation-approvals-and-licensing/certification-of-people/certified-handlers/

[^extractives]: WorkSafe New Zealand, "Verify certificate of competence information", extractives. https://www.worksafe.govt.nz/topic-and-industry/extractives/cocs-and-cpd/verify-certificate-of-competence-information/

[^caa]: Civil Aviation Authority of New Zealand, form CAA603, "Application for licence verification of occurrences", August 2025. https://www.aviation.govt.nz/assets/forms/CAA603-App-for-licence-verification-of-occurrences.pdf

[^cranes]: WorkSafe New Zealand, "Approved Code of Practice for Cranes". https://www.worksafe.govt.nz/dmsdocument/410-approved-code-of-practice-for-cranes-cranes-1.pdf

[^nztaclasses]: NZ Transport Agency Waka Kotahi, "Factsheet 11: Driver licence classes", August 2026. https://www.nzta.govt.nz/assets/resources/factsheets/11/docs/11-driver-licence-classes.pdf

[^nztaexplained]: NZ Transport Agency Waka Kotahi, "Your driver licence explained". https://www.nzta.govt.nz/driver-licences/getting-a-licence/your-driver-licence-explained

[^dlr]: NZ Transport Agency Waka Kotahi, "The Driver Licence Register". https://www.nzta.govt.nz/driver-licences/the-driver-licence-register

[^drivercheck]: NZ Transport Agency Waka Kotahi, "About Driver Check". https://www.nzta.govt.nz/driver-licences/driver-check/about-driver-check

[^ddlact]: Regulatory Systems (Transport) Amendment Act 2026, 2026 No 21. https://www.legislation.govt.nz/act/public/2026/21/en/latest/

[^nol]: Stats NZ, "About the National Occupation List". https://www.stats.govt.nz/methods/about-the-national-occupation-list/

[^skillspassport]: Australian Government Department of Education, "National Skills Passport consultation". https://www.education.gov.au/national-skills-passport-consultation

[^nswhrwl]: SafeWork NSW, "High risk work licences", and Service NSW, "Check a high risk work licence". https://www.safework.nsw.gov.au/licences-and-registrations/licences/high-risk-work-licences and https://www.service.nsw.gov.au/transaction/check-a-high-risk-work-licence
