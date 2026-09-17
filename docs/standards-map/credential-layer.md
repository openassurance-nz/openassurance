# OpenAssurance Standards Map: The Credential Layer

**Part of:** `standards-map.md`  
**Status:** Working draft, Phase 2  
**Last reviewed:** September 2026

## 1. Purpose

This part of the standards map assesses the standards that carry a record: its data model, how it is signed, how parties are identified, how currency is checked, and how it moves.

The positions used here are defined in `standards-map.md` section 3, and the method in its section 4.

These are the layers where mature international standards exist, and the conclusion throughout is to adopt or profile them, not to redefine them.

## 2. Credential Data Model

### 2.1 W3C Verifiable Credentials Data Model 2.0

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

Those are left to the securing specifications, the protocols, and the relying organisation respectively, which is exactly the separation OpenAssurance wants.

A Working Draft of version 2.1 was published on 13 September 2026.[^vcdm21]

It does not supersede 2.0 and should be tracked rather than depended on.

### 2.2 Verifiable Credentials JSON Schema

**Position: Adopt as prospective.**

The Verifiable Credentials JSON Schema Specification defines how a credential points at the JSON Schema it conforms to, either directly or as a schema wrapped in its own signed credential.[^vcjs]

It requires support for JSON Schema 2020-12.

It remains a Candidate Recommendation Draft dated 4 February 2025 and has not advanced since.

OpenAssurance record schemas should be written in JSON Schema 2020-12 regardless, and should be referenced through `credentialSchema` in the form this specification describes.

If the specification has not reached Recommendation when v0.1 is finalised, the profile should say so and reference it as prospective.

### 2.3 Alternative credential formats

Two other credential formats are in wide use and are supported by the same issuance and presentation protocols.

**IETF SD-JWT VC.**

**Position: Evaluate.**

SD-JWT-based Verifiable Digital Credentials is an Internet-Draft of the IETF OAuth Working Group, submitted to the IESG for publication as a Proposed Standard in August 2026.[^sdjwtvc]

It expresses a credential as plain JSON claims in a selectively disclosable JWT, without JSON-LD.

It is close to stable, and the European Digital Identity Wallet framework requires wallets to support it alongside mdoc, while treating the W3C data model as optional and describing it as the reference format for attestations in the education sector.[^arf]

It is not proposed as the OpenAssurance record format for v0.1, because the W3C data model is already a Recommendation and carries the evidence, related-resource, and terms-of-use properties workplace records need.

A conforming OpenAssurance verifier may in future need to accept SD-JWT VC presentations of credentials issued by others, but no New Zealand issuer of relevance has adopted the format, and `new-zealand-context.md` shows the government has chosen mdoc instead.

**ISO/IEC 18013-5 and the ISO/IEC 23220 series.**

**Position: Evaluate, and Reference for government-issued credentials.**

ISO/IEC 18013-5:2021 defines the mobile driving licence and the underlying binary credential format known as mdoc, and a second edition is at Draft International Standard stage.[^mdl]

The ISO/IEC 23220 series generalises the same building blocks to other mobile documents.[^iso23220]

The format is designed for government-issued identity documents presented from a phone, with strong device binding, and is the format mobile driving licences use internationally.

It is also the format the New Zealand government has built its own credential infrastructure on.

The Trust Framework Rules permit an accredited credential to use the W3C data model, ISO/IEC 18013-5, or the ISO/IEC 23220 series, but the government wallet, the government issuance platform, the government trust list, and the government verifier app all implement mdoc, and none currently implements the W3C model.[^distfrules][^wallettech][^dciptech]

`new-zealand-context.md` sets this out in full.

Two consequences follow for OpenAssurance.

A relying organisation whose requirement includes a government-issued licence or an NZBN credential will receive it as an mdoc presentation, and a verifier that handles such credentials must accept that presentation without requiring re-issuance in another format, which the exchange model treats as an optional conformance class.

An OpenAssurance record on the W3C data model can in principle be accredited under the Trust Framework, but cannot today be held in the government wallet.

OpenAssurance should keep the W3C data model as its record format, because its holders are as often organisations' systems as individuals' phones and because the vocabulary it needs already exists there.

It should also specify its vocabulary as a set of named claims that is independent of either container, so that the same record can be rendered as a W3C credential or as an mdoc namespace without changing its meaning.

Whether OpenCompetency then defines that mdoc rendering, so that a worker can carry a competency record in the government wallet alongside a driver licence, is listed as a decision in `decisions.md`.

The wallet's own documentation gives educational qualifications and licences as examples of the credentials it expects to hold from non-government issuers, so the question is one of format, not of eligibility.[^wallettech]

### 2.4 Loss-of-meaning check

Nothing in the record types the architecture overview lists is unrepresentable in the W3C data model.

A credential, an attestation, an assessment, and an endorsement are each a signed assertion by an identifiable issuer about an identifiable subject, which is what the data model exists to express.

Evidence and requirement are different in kind: evidence is dealt with in section 2.5 and requirement in `recognition-and-requirements.md` section 3.

### 2.5 Evidence held by a party other than its source

**Position: Profile.**

The `evidence` property lets an issuer describe the basis for its own assertion inside the credential.[^vcdm2]

The `relatedResource` property lets any credential hash-link an external document by identifier, media type, and digest, and requires a verifier that uses the document to check the digest.[^vcrelres]

Together they are enough to carry a document that a holder has and its source has not signed.

The record type built on them is defined in `exchange-model.md` section 6.5, including the rule that a held copy never implies the source's signature and the distinction between an issuer-signed document and an unsigned one.

## 3. Securing Records

The data model leaves signing to two companion specifications, both W3C Recommendations of 15 May 2025.

They are alternatives, and a profile that mandates both doubles every verifier's obligations.

### 3.1 Securing Verifiable Credentials using JOSE and COSE

**Position: Profile, as the mandatory-to-implement baseline.**

This specification wraps an unmodified credential or presentation in a signed envelope using one of three IETF mechanisms: a JSON Web Signature, a selectively disclosable JWT, or a COSE structure.[^vcjose]

It registers the media types `application/vc+jwt`, `application/vp+jwt`, `application/vc+sd-jwt`, `application/vp+sd-jwt`, `application/vc+cose`, and `application/vp+cose`.

Selective disclosure inside the envelope relies on RFC 9901, Selective Disclosure for JSON Web Tokens, published as a Proposed Standard in November 2025.[^sdjwt]

The case for making this the baseline is practical.

- JOSE libraries exist for every mainstream language and are already used by most organisations' identity systems;
- no canonicalisation step is required, so there is less to implement and less to get wrong;
- selective disclosure, which the minimum-disclosure principle requires, is available through an RFC rather than a draft;
- a hosted service for small organisations can be built on commodity components.

### 3.2 Verifiable Credential Data Integrity 1.0

**Position: Profile, as an optional alternative.**

Data Integrity embeds a `proof` object in the credential itself, parameterised by a named cryptosuite.[^vcdi]

The EdDSA and ECDSA cryptosuites reached Recommendation on the same date, and the ECDSA suite includes a selective-disclosure variant.[^vcdieddsa][^vcdiecdsa]

A BBS cryptosuite offering unlinkable selective disclosure is a Candidate Recommendation Draft and is not yet stable.[^vcdibbs]

Embedded proofs keep the record readable as plain JSON-LD and support proof sets and chains, which suits records that will be countersigned.

They require RDF canonicalisation or JSON canonicalisation before hashing, which is the main implementation cost.

A conforming verifier should be permitted to accept Data Integrity proofs, and a conforming issuer permitted to produce them, without either being required.

### 3.3 Recommendation

v0.1 should aim to require the JOSE envelope for every conforming record, permit the SD-JWT envelope where selective disclosure is needed, and permit Data Integrity proofs as an option.

This is a decision for Phase 3 and is listed in `decisions.md`.

The trade-off runs one way only if implementation cost for small organisations is weighted heavily, which the Charter's open-participation principle requires.

### 3.4 Verification over time

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

**Position: define, as conformance rules.**

The rules are in `exchange-model.md` section 8.3, and what happens when an issuer ceases to exist is decision D9 in `decisions.md`.

## 4. Identifiers

Three kinds of party need identifying, and they need different treatment.

### 4.1 Issuers

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

A valid signature proves control of a domain, and not that the domain belongs to the organisation named in a record.

The exchange model closes that gap with a two-way check against a register that already exists: the domain asserts the organisation's New Zealand Business Number, and the website recorded against that number in the public NZBN Register is on the same domain.[^nzbnact]

It also proposes a DNS record, on the pattern DKIM uses, for discovering an organisation's issuer identifier and the address at which it receives presentations.

### 4.2 People

**Position: Profile, with no universal identifier.**

The data model makes the subject identifier optional, and OpenAssurance should keep it optional.[^vcdm2]

A person can be identified by claims inside the credential, such as name and date of birth as recorded by the issuer, without any identifier at all.

Where an identifier is used, the privacy principles require it to be issuer-scoped, organisation-scoped, pairwise, or otherwise privacy-preserving.

A government, licence, tax, or qualification number must not be used as the subject identifier, because that would turn a number issued for one purpose into a universal tracking key.

Privacy Act 2020 Information Privacy Principle 13 constrains the assignment and reuse of unique identifiers, and `new-zealand-context.md` returns to it.

Correlation within one issuer's records is unavoidable and acceptable, because the issuer already holds them.

Correlation across unrelated issuers is what the identifier design must prevent.

The `licenseNumber` property that Open Badges 3.0 places on an achievement subject is a claim about a licence, not a subject identifier, and that distinction should be preserved when the profile is written.[^ob3]

### 4.3 Organisations

**Position: Adopt the New Zealand Business Number; Adopt the Legal Entity Identifier as an alternative.**

Organisations are not people, and the no-universal-identifier principle does not apply to them in the same way.

Organisation identifiers are public by design, and a stable public identifier is what makes an OpenPrequal record about a supplier unambiguous.

The New Zealand Business Number is the statutory identifier for New Zealand businesses under the New Zealand Business Number Act 2016, administered by the Ministry of Business, Innovation and Employment, which maintains the NZBN Register.[^nzbnact][^nzbnabout]

Companies receive an NZBN automatically, and sole traders, partnerships, and trusts may apply for one.[^nzbnget]

Public primary business data, including entity name, trading names, status, and industry classification, is searchable by anyone and available through a free API and as free bulk data.[^nzbnapi][^nzbnbulk]

The Act permits a government agency to use the NZBN in substitution for any other identifier, which is the closest thing New Zealand has to a statement that this is the organisation identifier.[^nzbnact]

Each NZBN is a GS1 Global Location Number, which sits within the ISO/IEC 6523 organisation-identifier framework under International Code Designator 0088, so an NZBN can be written as a globally unambiguous identifier without any OpenAssurance-specific scheme.[^nzbnabout][^gs1icd][^iso6523]

The Government has announced that the Ministry of Business, Innovation and Employment will trial issuing NZBN digital credentials through the government's credential issuance platform, so that a person can prove their identity and authority to act for a business.[^beehivedcip]

That is an organisation-identity credential of exactly the kind OpenPrequal would consume, and `new-zealand-context.md` returns to the format it will use.

The Legal Entity Identifier under ISO 17442 identifies legal entities worldwide, is issued for an annual fee through accredited issuers, and its reference data is published as open data by the Global Legal Entity Identifier Foundation.[^lei][^leiopen]

Several thousand New Zealand entities already hold one, and the foundation recognises the Companies Register as the registration authority for them.[^leinz]

It is the right identifier for an overseas supplier or issuer that has no NZBN.

A verifiable form of the LEI, standardised as ISO 17442-3:2024, uses a credential format outside the W3C family and is noted for completeness rather than proposed for adoption.[^vlei]

One caution applies.

A sole trader's NZBN identifies a person, and records about a sole trader are personal information to which the privacy principles apply in full.

### 4.4 Records

Every record should carry its own `id` as a URL under the issuer's control, so that a replacement or correction statement has something to point to.

The identifier need not resolve to anything, and must not be required to.

## 5. Currency and Status

The second trust question is whether a record is still current.

Three mechanisms answer it at different levels.

### 5.1 Validity period

**Position: Adopt.**

`validFrom` and `validUntil` in the data model carry the period the issuer intended the record to be valid for.[^vcdm2]

Timestamps should use the RFC 3339 profile of ISO 8601.[^rfc3339]

An expired record is not invalid as a historical assertion; it is no longer current, which is a different thing, and the profile should say so.

### 5.2 Bitstring Status List v1.0

**Position: Adopt.**

Bitstring Status List became a W3C Recommendation on 15 May 2025.[^bsl]

Each credential carries a pointer to one position in a compressed bitstring that the issuer publishes as a signed credential of its own.

The list supports revocation and suspension as status purposes, and an extensible message mechanism for others.

Its privacy property matters for OpenAssurance.

A list must contain at least 131,072 entries, so fetching it reveals nothing about which credential the verifier is checking.

The issuer publishes the list at a URL of its choosing, so no registry is involved and the mechanism satisfies the independence test.

The profile should require that the list URL sits under an identifier the issuer controls, so that a change of host does not break status checking for records already issued.

### 5.3 Supersession, replacement, and correction

**Position: define, as a small OpenAssurance vocabulary.**

The privacy principles require that a signed record be corrected by revocation, supersession, replacement, or a linked correction statement, never by silent edit.

The data model has no property that says "this record replaces that one" or "this record was superseded on this date by that one".

Bitstring Status List's message purpose could carry a superseded flag, but not the link to the replacement.

This is a gap, and a small one.

OpenAssurance should define a handful of terms for a replacement record to reference the record it supersedes, and for a correction statement to reference the record it corrects.

They should be expressed as ordinary properties on the credential subject or as a typed `relatedResource`, so that no existing tooling is broken by their presence.

### 5.4 Public registers as currency sources

**Position: Reference.**

Many New Zealand licences and registrations already have an authoritative public register operated by the regulator, and `people.md` section 9 lists the main ones.

For those licences, the register is the source of truth for currency, and a status list published by anyone else would be a copy.

A credential that asserts a registered status should identify the register it derives from, and a relying organisation that needs certainty should check the register.

Most registers are web lookups for people rather than status endpoints for systems.

Whether a regulator publishes machine-checkable status is the regulator's decision, and OpenAssurance should neither mirror registers nor assume they will change.

### 5.5 Status for other formats

The Bitstring mechanism is defined for the W3C data model.

The government's credential issuance platform uses the IETF Token Status List draft for revocation of mdoc credentials, and the Trust Framework Rules make revocation mandatory for any accredited credential valid for more than 72 hours.[^dciptech][^wallettech]

A conforming OpenAssurance verifier that accepts government-issued mdoc presentations, as section 2 describes, will therefore need to check that mechanism as well as the Bitstring list.

That is an implementation cost to record, not a reason to change the OpenAssurance choice.

## 6. Presentation and Exchange

This layer covers how a record gets from an issuer to a holder, and from a holder to a verifier.

### 6.1 Verifiable Presentations

**Position: Adopt, with a small profile.**

The data model defines a verifiable presentation as a signed container for one or more credentials, or for claims derived from them, that a holder assembles for a verifier.[^vcdm2]

That is the OpenAssurance "presentation": a purpose-specific sharing event distinct from the credentials it contains.

When the presentation is secured as a JWT, the standard `aud`, `nonce`, and `exp` claims carry the intended recipient, freshness, and expiry that the privacy principles require a presentation to be capable of identifying.

Two things the privacy principles ask for are not carried by any standard property.

- the purpose of the presentation;
- whether onward sharing is expected or restricted.

`termsOfUse` is the data model's extension point for exactly this kind of statement, and OpenAssurance should define a small terms-of-use vocabulary for purpose, onward-sharing expectation, and suggested retention.

### 6.2 OpenID for Verifiable Credential Issuance 1.0

**Position: Adopt, profiled.**

OpenID4VCI became a Final Specification of the OpenID Foundation on 16 September 2025.[^oid4vci]

It defines an OAuth 2.0 protected API by which an issuer delivers a credential to a holder, with same-device and cross-device flows, a credential-offer mechanism, and format profiles for the W3C data model, SD-JWT VC, and mdoc.

It is the established way for a qualification provider, employer, or assessor to issue a record into a worker's or organisation's holder system or wallet.

OpenAssurance should adopt it and profile only the choice of credential format and the required issuer metadata.

### 6.3 OpenID for Verifiable Presentations 1.0

**Position: Adopt, profiled.**

OpenID4VP became a Final Specification on 9 July 2025.[^oid4vp]

It defines how a verifier requests, and a holder returns, a presentation in any of the same three formats.

The Final text uses the Digital Credentials Query Language, DCQL, as its only query language, and no longer references Presentation Exchange.

OpenAssurance should adopt it for interactive presentation, profile the credential formats and response modes, and inherit DCQL for transaction-time queries, as `recognition-and-requirements.md` section 3 discusses.

### 6.4 Organisation-to-organisation transfer

**Position: define, as an exchange convention rather than a format.**

The dominant OpenAssurance flow is not a person presenting from a phone.

It is an employer's system sending its worker's records to a customer's system, or a supplier sending its assurance records to a buyer, often asynchronously and sometimes by a person attaching a file.

OpenID4VP handles this when both sides run compatible software, because a holder can be a system as well as a wallet.

It does not help a small organisation that has no such software and has been asked for evidence by email.

The floor for conformance should therefore be a file: a signed verifiable presentation in one of the registered media types from section 3, which can be produced by any conforming system, sent by any channel, and imported and verified by any other conforming system.

No new format is involved.

A conforming file must also be readable by a person, because the organisation receiving it may have nothing but an email client, so a rendering rule is part of the convention, and the data model's reserved render-method extension point and Open Badges' baked images are the existing options to draw on.[^vcdm2][^ob3]

The genuinely new content is the conformance rule that every conforming system must export and import such a file, and the conventions for doing so.

That rule is what makes the Charter's open exchange requirement testable.

The exchange model also drafts, as extensions, a discovery record, a signed request, and approval for a period, none of which changes the floor.

### 6.5 Digital Credentials API

**Position: Evaluate.**

The W3C Digital Credentials API is a Working Draft, most recently dated 4 September 2026, that lets a web page ask the browser to mediate a credential request to whatever wallet the user has.[^dcapi]

It will matter for web-based issuance and presentation to individuals once it is stable and shipped.

It is not stable, and OpenAssurance should track it rather than depend on it.

### 6.6 ISO/IEC 18013-7

**Position: Reference.**

ISO/IEC TS 18013-7:2025 defines online presentation of a mobile driving licence, including a profile over OpenID4VP.[^mdl7]

It is a Technical Specification under revision, and matters only to the extent that relying organisations will receive government-issued licences from phones.

## 7. Sources

Every status and date in this part was checked against the source listed in September 2026.

References to external organisations, schemes, and government publications are provided as evidence of what exists. No such reference implies consultation, participation, support, or endorsement.

[^vcdm2]: W3C, "Verifiable Credentials Data Model v2.0", W3C Recommendation, 15 May 2025. https://www.w3.org/TR/vc-data-model-2.0/

[^vcdm11]: W3C, "Verifiable Credentials Data Model v1.1", W3C Recommendation, 3 March 2022, carrying a June 2025 status update that the version is outdated. https://www.w3.org/TR/2022/REC-vc-data-model-20220303/

[^vcdm21]: W3C, "Verifiable Credentials Data Model v2.1", W3C Working Draft, 13 September 2026. https://www.w3.org/TR/vc-data-model-2.1/

[^vcjs]: W3C, "Verifiable Credentials JSON Schema Specification", W3C Candidate Recommendation Draft, 4 February 2025. https://www.w3.org/TR/vc-json-schema/

[^sdjwtvc]: IETF OAuth Working Group, "SD-JWT-based Verifiable Digital Credentials (SD-JWT VC)", Internet-Draft draft-ietf-oauth-sd-jwt-vc-19, 31 August 2026, submitted to the IESG for publication. https://datatracker.ietf.org/doc/draft-ietf-oauth-sd-jwt-vc/

[^arf]: European Commission, "European Digital Identity Wallet Architecture and Reference Framework", release 3.0.0, July 2026, section on data model and data exchange protocols. https://eudi.dev/latest/main/05-data-model-and-data-exchange-protocols/

[^mdl]: ISO/IEC 18013-5:2021, "Personal identification — ISO-compliant driving licence — Part 5: Mobile driving licence (mDL) application", International Standard, with a second edition at Draft International Standard stage. https://www.iso.org/standard/69084.html

[^iso23220]: ISO/IEC 23220 series, "Cards and security devices for personal identification — Building blocks for identity management via mobile devices", Part 1 published 2023 as an International Standard, later parts published as Technical Specifications or in draft. https://www.iso.org/standard/74910.html

[^distfrules]: Digital Identity Services Trust Framework Rules 2024, version 2, 24 July 2025, rules 8 and 9, as mirrored on the government standards site; consolidated rules of 29 June 2026 published by the Government Digital Delivery Agency. https://standards.digital.govt.nz/nz/dia-distfr/2/en/ and https://www.publicservice.govt.nz/about-the-commission/government-digital-delivery-agency/trust-framework-for-digital-identity/about-digital-identity-services/trust-framework-legislation/trust-framework-rules

[^wallettech]: Government Digital Delivery Agency, "Govt.nz app wallet technical guide". https://github.com/NZ-Digital-Public-Infrastructure/govt-nz-app-wallet

[^dciptech]: Government Digital Delivery Agency, "Digital Credentials Technical Guide" and "DCIP Onboarding Guide", Digital Credential Issuance Platform. https://github.com/NZ-Digital-Public-Infrastructure/nz-digital-credential-issuance-platform

[^vcrelres]: W3C, "Verifiable Credentials Data Model v2.0", section 5.3, Integrity of Related Resources. https://www.w3.org/TR/vc-data-model-2.0/#integrity-of-related-resources

[^vcjose]: W3C, "Securing Verifiable Credentials using JOSE and COSE", W3C Recommendation, 15 May 2025. https://www.w3.org/TR/vc-jose-cose/

[^sdjwt]: IETF, "Selective Disclosure for JSON Web Tokens (SD-JWT)", RFC 9901, Proposed Standard, November 2025. https://www.rfc-editor.org/rfc/rfc9901.html

[^vcdi]: W3C, "Verifiable Credential Data Integrity 1.0", W3C Recommendation, 15 May 2025. https://www.w3.org/TR/vc-data-integrity/

[^vcdieddsa]: W3C, "Data Integrity EdDSA Cryptosuites v1.0", W3C Recommendation, 15 May 2025. https://www.w3.org/TR/vc-di-eddsa/

[^vcdiecdsa]: W3C, "Data Integrity ECDSA Cryptosuites v1.0", W3C Recommendation, 15 May 2025. https://www.w3.org/TR/vc-di-ecdsa/

[^vcdibbs]: W3C, "Data Integrity BBS Cryptosuites v1.0", W3C Candidate Recommendation Draft, 10 September 2026. https://www.w3.org/TR/vc-di-bbs/

[^cid]: W3C, "Controlled Identifiers v1.0", W3C Recommendation, 15 May 2025. https://www.w3.org/TR/cid-1.0/

[^didweb]: W3C Credentials Community Group, "did:web Method Specification", unofficial draft. https://w3c-ccg.github.io/did-method-web/

[^etsi612]: ETSI, "Electronic Signatures and Trust Infrastructures (ESI); Trusted Lists", ETSI TS 119 612 V2.4.1, August 2025. https://www.etsi.org/deliver/etsi_ts/119600_119699/119612/02.04.01_60/ts_119612v020401p.pdf

[^did10]: W3C, "Decentralized Identifiers (DIDs) v1.0", W3C Recommendation, 19 July 2022. https://www.w3.org/TR/did-core/

[^did11]: W3C, "Decentralized Identifiers (DIDs) v1.1", W3C Candidate Recommendation Snapshot, 5 March 2026. https://www.w3.org/TR/did-1.1/

[^didkey]: W3C Credentials Community Group, "The did:key Method v0.9", Draft Community Group Report. https://w3c-ccg.github.io/did-key-spec/

[^nzbnact]: New Zealand Business Number Act 2016, 2016 No 16, sections 3, 20 to 29. https://www.legislation.govt.nz/act/public/2016/0016/latest/whole.html

[^ob3]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", Final Release, 17 June 2024, with errata to revision 1.6 of 29 June 2026. https://www.imsglobal.org/spec/ob/v3p0/

[^nzbnabout]: New Zealand Business Number, "About the NZBN". https://www.nzbn.govt.nz/whats-an-nzbn/about/

[^nzbnget]: New Zealand Business Number, "Get an NZBN". https://www.nzbn.govt.nz/get-an-nzbn/

[^nzbnapi]: Ministry of Business, Innovation and Employment, "NZBN API", developer portal. https://portal.api.business.govt.nz/api/nzbn

[^nzbnbulk]: New Zealand Business Number, "Bulk data". https://www.nzbn.govt.nz/using-the-nzbn/nzbn-services/bulk-data/

[^gs1icd]: GS1, "GS1 Application Standard for the use of ISO/IEC 6523 International Code Designator (ICD)", assigning ICD 0088 to the Global Location Number. https://ref.gs1.org/standards/icd/

[^iso6523]: ISO/IEC 6523-1:2023, "Information technology — Structure for the identification of organizations and organization parts — Part 1: Identification of organization identification schemes". https://www.iso.org/standard/82246.html

[^beehivedcip]: New Zealand Government, "Making it faster and easier to issue digital credentials", 17 November 2025. https://www.beehive.govt.nz/release/making-it-faster-easier-issue-digital-credentials

[^lei]: Global Legal Entity Identifier Foundation, "Introducing the Legal Entity Identifier (LEI)". https://www.gleif.org/en/about-lei/introducing-the-legal-entity-identifier-lei

[^leiopen]: Global Legal Entity Identifier Foundation, "Open data", LEI reference data published under a CC0 licence. https://www.gleif.org/en/about/open-data

[^leinz]: Global Legal Entity Identifier Foundation, registration authority RA000466, Companies Register, New Zealand. https://api.gleif.org/api/v1/registration-authorities/RA000466

[^vlei]: ISO 17442-3:2024, "Financial services — Legal entity identifier (LEI) — Part 3: Verifiable LEIs (vLEIs)". https://www.iso.org/standard/85628.html

[^rfc3339]: IETF, "Date and Time on the Internet: Timestamps", RFC 3339, July 2002. https://www.rfc-editor.org/info/rfc3339

[^bsl]: W3C, "Bitstring Status List v1.0", W3C Recommendation, 15 May 2025. https://www.w3.org/TR/vc-bitstring-status-list/

[^oid4vci]: OpenID Foundation, "OpenID for Verifiable Credential Issuance 1.0", Final Specification, 16 September 2025. https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0-final.html

[^oid4vp]: OpenID Foundation, "OpenID for Verifiable Presentations 1.0", Final Specification, 9 July 2025. https://openid.net/specs/openid-4-verifiable-presentations-1_0-final.html

[^dcapi]: W3C, "Digital Credentials", W3C Working Draft, 4 September 2026. https://www.w3.org/TR/digital-credentials/

[^mdl7]: ISO/IEC TS 18013-7:2025, "Personal identification — ISO-compliant driving licence — Part 7: Mobile driving licence (mDL) add-on functions", Technical Specification, under revision. https://www.iso.org/standard/91154.html
