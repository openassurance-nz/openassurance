# OpenAssurance Standards Map

**Status:** Working draft, Phase 2 (map existing standards)  
**Last reviewed:** September 2026

## 1. Purpose

The OpenAssurance development path has six phases.

Phase 2 is to identify what already exists and should be adopted rather than recreated.

This document is the working record of that phase.

It assesses each candidate standard, scheme, register, and legal instrument against what OpenAssurance actually needs, and states a position on each.

Its output is a statement of the smallest genuinely new layer OpenAssurance has to define, which is the input to Phase 3.

The first working draft of Phase 3 is `exchange-model.md`.

`docs/standards-landscape.md` lists the candidates and the principles that govern reuse.

This document is the index to the assessment: it summarises the findings, defines the positions and the method, and collects every position in one table.

The assessment itself is in the five parts listed in section 5, and the decisions and questions still open are in `decisions.md`.

Where the two differ, this document is the more recent and should be preferred until the landscape document is revised.

Nothing in this document is a specification.

Positions stated here are proposals for discussion, and every one of them can be challenged through the process in `CONTRIBUTING.md`.

## 2. Summary

Almost every layer of an assurance exchange is already covered by a stable open standard, and OpenAssurance should adopt those standards as they are.

- records are W3C verifiable credentials, signed in a JOSE envelope, with status published as a Bitstring Status List and keys found through a controller document on the issuer's own domain;
- presentations, issuance, and interactive requests use the W3C presentation model and the two OpenID protocols;
- organisations are identified by the New Zealand Business Number, people are given no shared identifier, and formal achievements align to New Zealand framework numbers through Open Badges.

Three findings shape everything else.

The New Zealand government has built its own credential infrastructure on the ISO mdoc format, so OpenAssurance keeps the W3C data model for its records and treats acceptance of government-issued credentials as an optional class.

WorkSafe New Zealand's 2026 prequalification template gives OpenPrequal a public set of twelve topics to align its evidence categories to, and an industry cross-recognition scheme shows how assessment, endorsement, and requirement already differ in practice.

Issuer-signed, holder-controlled, independently verifiable records already exist in New Zealand in document form, as the signed qualification documents universities issue, and that is the pattern OpenAssurance generalises.

Nine things remain for OpenAssurance to define, all small, and none of them needs anyone else to act first.

The exchange model divides them into a core proposed for v0.1 and extensions that are drafted but not proposed.

They are listed in section 7, and the working draft that defines them is `exchange-model.md`.

The decisions still open, each with a likely path, are in `decisions.md`.

## 3. How to Read the Positions

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

## 4. Method

Each candidate was checked against its primary source in September 2026, and the status recorded here is the status on that date.

No vendor material was used as a source for any status or capability claim.

Each candidate was then assessed against five questions.

### 4.1 Reuse

> Can this standard represent the OpenAssurance requirement without loss of meaning?

### 4.2 Independence

> Does adopting this standard create a dependency on a particular platform, registry, wallet, or service?

### 4.3 Openness in two parts

The landscape document separates two questions that are often conflated.

The first is whether the specification is openly published and may be implemented by anyone.

The second is whether the tooling around it is available on open terms, or only to licensees of a particular service.

Both were asked of every candidate.

### 4.4 Stability

A candidate published as a W3C Recommendation, an IETF RFC, an OpenID Foundation Final Specification, or an ISO International Standard is treated as stable.

A Working Draft, Candidate Recommendation, Internet-Draft, Community Group report, or Technical Specification is treated as prospective, however widely deployed.

### 4.5 Privacy fit

> Does the standard support minimum disclosure, scoped identifiers, and status checking that does not reveal who is being checked?

A candidate that fails this question is not automatically excluded, but the gap is recorded.

### 4.6 Verification level

The research behind this document was carried out largely by automated retrieval of primary sources on a single date.

Most claims were read from the retrieved page or document itself.

A peer review on 17 September 2026 identified three claims that had rested on search excerpts, and they were rechecked: one was confirmed, and two were reworded to what the sources support.

A person should spot-check the citations before anyone relies on a position recorded here, and corrections are welcome through the process in `CONTRIBUTING.md`.

## 5. The Layers of an Exchange, and Where to Find Them

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

The assessment is divided into five parts, so that a reader can go straight to the layer that concerns them.

- `standards-map/credential-layer.md` covers the credential data model, securing, identifiers, status, and presentation and exchange;
- `standards-map/recognition-and-requirements.md` covers endorsement, trust lists, and requirement expression;
- `standards-map/people.md` covers Open Badges, New Zealand qualification identifiers, the Record of Achievement, occupational registers, and driver licences;
- `standards-map/organisations.md` covers WorkSafe New Zealand's position and template, an industry cross-recognition scheme, common questionnaire content, accepted certifications, and insurance;
- `standards-map/new-zealand-context.md` covers the Privacy Act, the Trust Framework, the government wallet and verifier, and the New Zealand Business Number.

Each part carries its own sources.

Section 6 collects every position in one table, section 7 states what remains genuinely new, and `decisions.md` holds the decisions and questions still open.

## 6. Summary Map

The table collects every position in this document, ordered by the layers in section 5.

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
| Binding an issuer to an organisation | website recorded in the public NZBN Register | Statutory register, public interface | Define the check; Reference the register |
| Discovery of an issuer and its inbox | DNS TXT record at an underscored name, the DKIM pattern | Best Current Practice | Define, extension |
| Validity period | `validFrom`, `validUntil`, RFC 3339 | Recommendation, RFC | Adopt |
| Revocation and suspension | W3C Bitstring Status List 1.0 | Recommendation | Adopt |
| Revocation for mdoc | IETF Token Status List | Internet-Draft, used by government platform | Reference, for the optional mdoc class |
| Supersession and correction | none | | Define |
| Licence currency | regulator public registers | Web lookups, no API | Reference |
| Presentation container | W3C Verifiable Presentations | Recommendation | Adopt with terms-of-use profile |
| Issuance protocol | OpenID4VCI 1.0 | Final, September 2025 | Adopt, profiled |
| Presentation protocol | OpenID4VP 1.0 | Final, July 2025 | Adopt, profiled |
| Transaction query | DCQL | Part of OpenID4VP 1.0 | Adopt |
| Transaction query | DIF Presentation Exchange 2.1.1 | DIF Ratified, not referenced by OpenID4VP 1.0 | Set aside |
| Request for records | none for a file sent by email; the OpenID4VP request object when interactive | Final, July 2025 | Define a small signed request, extension, decision D12; translate when interactive |
| Browser mediation | W3C Digital Credentials API | Working Draft | Evaluate |
| Online mdoc presentation | ISO/IEC TS 18013-7 | Technical Specification | Reference |
| Organisation-to-organisation transfer | none | | Define as exchange convention |
| Change notices during an approved period | IETF Security Event Token, RFC 8417 | RFC | Evaluate, extension |
| Endorsement | Open Badges 3.0 EndorsementCredential | Final, June 2024 | Profile with scope |
| Recognition publishing | OpenID Federation 1.0 | Final, February 2026 | Evaluate |
| Recognition publishing | W3C Recognized Entities 1.0 | Working Draft | Evaluate |
| Recognition publishing | ETSI TS 119 612 and TS 119 602 | Technical Specifications | Reference |
| Recognition source | government trust list, VICAL | Operating, sandbox | Reference |
| Requirement expression | CTDL ConditionProfile | Stable vocabulary, CC BY | Evaluate |
| Requirement expression | none that states an expectation with evidence guidance and objective criteria | | Define, extension, decision D11 |
| Achievement vocabulary | Open Badges 3.0 | Final, June 2024 | Profile, base for achievements |
| Achievement record proof format | Open Badges 3.0 JSON Web Token proof format | Final, June 2024 | Accept alongside the common envelope, decision D4 |
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
| Findings, corrective actions, and recommendations | terms from ISO 19011, ISO 45001, and ISO/IEC 17021-1 | International Standards for audit practice, not data formats | Define, extension, borrowing the terms |
| Director or officer role behind a declaration | Companies Register roles data | Public, with appointment and cessation dates | Reference, the floor for authority evidence |
| Role or delegated authority as a credential | credential types the government wallet expects | Anticipated, not yet available | Evaluate, extension |
| Personal information | Privacy Act 2020, including IPP 3A from May 2026 | In force | Reference; PIA required |
| Trust framework | Digital Identity Services Trust Framework Act 2023 and Rules | In force, voluntary accreditation | Reference; compatibility target |
| Government wallet and verifier | Govt.nz app, issuance platform, NZ Verify | Operating, mdoc | Reference; optional mdoc acceptance class |
| Person name, date, address | mandated government data standards | Mandated for departments | Reference |

Fifty-one of the sixty-two rows point at something that already exists.

Eleven say "Define", and two more, endorsement scope and presentation terms of use, are profiles that add a small vocabulary of their own.

Section 7 describes what each of those requires.

## 7. What Remains Genuinely New

The purpose of this phase was to find the smallest layer OpenAssurance has to define itself.

Everything below the workplace vocabulary is covered by a stable standard, and the map adopts or profiles it.

What remains is short.

The exchange model divides these items into a core proposed for v0.1 and extensions, and says which is which.

### 7.1 Workplace attestation and authorisation

Open Badges describes achievements: something a person completed, passed, or was awarded.

Workplace assurance also relies on two things that are not achievements.

An **attestation** is a statement by a supervisor, employer, or assessor that a person performed or demonstrated something, over a period, on a stated basis such as direct observation.

An **authorisation** is a permission an organisation grants a person to do defined work, under conditions, until withdrawn.

Neither has a home in any vocabulary examined.

Both name a person, as a declaration does, and the exchange model carries evidence of that person's role and of their approval separately from the organisation's signature, under decision D10.

OpenCompetency should define both as small credential types on the W3C data model.

The record types are defined in `exchange-model.md` sections 6.2 and 6.3, and the reasoning behind them, with a worked example, is in section 4 of the OpenCompetency profile.

The July 2025 ministerial statement's observation that "on-the-job experience should be better recognised" and that there is confusion "about the distinction between qualifications and actual competency" is the policy case for this item.[^beehive2025]

### 7.2 Requirement expression

`standards-map/recognition-and-requirements.md` section 3 found a query language and a descriptive condition vocabulary, and no publishable requirement model that translates into a query.

OpenAssurance should define a Requirement record that states what is expected, gives non-exclusive examples of evidence, and marks the objective criteria a system can check.

A DCQL query derived from it helps find candidate records, and a match never means that a requirement is met.

A requirement is guidance for an assessor's judgement and not a rules engine, which is decision D11.

### 7.3 Endorsement scope

`standards-map/recognition-and-requirements.md` section 2 found an endorsement credential without scope.

OpenAssurance should define the scope vocabulary.

### 7.4 Prequalification evidence, assessment, and requirement vocabulary

`standards-map/organisations.md` found a public template, a cross-recognition scheme, and a set of accepted certifications, and no data model for any of them.

OpenPrequal should define the evidence categories, the assessment-result structure, and the buyer-requirement structure, aligned to the WorkSafe template and neutral between schemes.

It should also define a corrective action request, closed by a further assessment, so that a supplier can present a finding together with what was done about it and the assessor's acceptance, in the terms of established audit practice.

It should also publish an illustrative Requirement record that expresses the six information areas in WorkSafe's position statement, as a starting template a buyer adapts, without implying that WorkSafe endorses it.[^wsposition]

### 7.5 Presentation terms of use

`standards-map/credential-layer.md` section 6 found that recipient, freshness, and expiry are standard, and that purpose, onward-sharing expectation, and retention guidance are not.

OpenAssurance should define a terms-of-use vocabulary for presentations.

### 7.6 Supersession and correction linkage

`standards-map/credential-layer.md` section 5 found revocation and suspension standardised, and no way to link a replacement or correction to the record it replaces.

OpenAssurance should define the linking terms.

### 7.7 Exchange conventions and conformance

`standards-map/credential-layer.md` section 6 found stable protocols for issuance and interactive presentation, and no rule that guarantees a record can leave one system and enter another.

OpenAssurance should define the file-based floor, the import and export obligations, and the conformance tests that make the Charter's open exchange requirement checkable.

### 7.8 Issuer binding

`standards-map/credential-layer.md` section 4 found that a valid signature proves control of a domain, and nothing about which organisation controls it.

No existing standard binds a web address to a New Zealand legal entity.

OpenAssurance should define the two-way check in which the domain states a New Zealand Business Number and the public NZBN Register lists a website on that domain, and should report the result separately from the signature.

The register already exists, so nothing new is operated by anyone.

### 7.9 Discovery, request and response, and approval for a period

The file floor lets a holder send a presentation, and says nothing about how a sender finds where to send it, how a relying organisation asks for one, or how an approval that lasts for a contract period is kept current.

The exchange model drafts three extensions for these, in `exchange-model/extensions.md`: a DNS record on the pattern DKIM uses, a small signed request that pins the exact requirement records it refers to and is translated into the OpenID presentation request when the exchange is interactive, and a standing grant with a change notice that carries no personal information.

None is proposed for v0.1, and each reuses an existing mechanism before defining anything.

### 7.10 What depends on another party

None of the items above requires anyone outside OpenAssurance to act before it can be defined.

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

### 7.11 What is not on the list

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

## 8. Decisions and Open Questions

The choices still open before v0.1, each with the path it should take unless something changes, are recorded in `decisions.md`.

The same file lists the questions that could not be settled from published material, and the party each should be put to.

They are kept in one place so that the exchange model can cite a decision by its identifier instead of restating it, and a change is made once.

## 9. Design Test

> **Can every part of a conforming record be validated using a published, openly licensed standard, with OpenAssurance defining only the workplace vocabulary, requirement expression, and exchange conventions that no existing standard provides?**

If a proposal adds to the list in section 7, it should show why the standards in this map cannot carry the requirement without loss of meaning.

If it removes from that list, it should show which existing standard now does the job.

## 10. Sources

Every status and date in this part was checked against the source listed in September 2026.

References to external organisations, schemes, and government publications are provided as evidence of what exists. No such reference implies consultation, participation, support, or endorsement.

[^beehive2025]: New Zealand Government, "Clearer rules and prequalification guidance to support construction", 28 July 2025. https://www.beehive.govt.nz/release/clearer-rules-and-prequalification-guidance-support-construction

[^wsposition]: WorkSafe New Zealand, "The work health and safety information needed before hiring contractors", WorkSafe position, June 2026, page last updated 20 August 2026. https://www.worksafe.govt.nz/laws-and-regulations/operational-policy-framework/worksafe-positions/work-health-safety-info-needed-before-hiring-contractors/ and https://www.worksafe.govt.nz/dmsdocument/72833-the-work-health-and-safety-information-needed-before-hiring-contractors/latest/
