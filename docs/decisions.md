# OpenAssurance Decisions and Open Questions

**Status:** Working register  
**Last reviewed:** September 2026

## 1. Purpose

This register holds the decisions that are still open before OpenAssurance v0.1, and the questions that could not be settled from published material.

Each decision has an identifier, the question, the path v0.1 should take unless something changes, what would change it, and a status of open, confirmed, or overturned.

A likely path is a working assumption, not a decision.

The exchange model cites a decision by its identifier instead of restating it, so that a change is made here once and nowhere else.

The evidence behind each decision is in `standards-map.md` and its parts.

## 2. Decisions

### D1. Securing baseline

The question is whether the JOSE envelope is the mandatory-to-implement mechanism with Data Integrity optional, or the reverse.

Likely path: the JOSE envelope is mandatory to implement, the SD-JWT envelope is permitted where selective disclosure is needed, and Data Integrity proofs are permitted but not required, as `standards-map/credential-layer.md` section 3 recommends.

This would change if the Trust Framework Rules came to mandate a securing mechanism, or if a major New Zealand issuer of workplace-relevant credentials adopted Data Integrity and interoperability with it mattered more than implementation cost.

Status: open.

Applied as a working assumption in `exchange-model.md` section 8.1.

### D2. Issuer identifier form

The question is whether to require an HTTPS URL with a controller document, permit `did:web` as a convention, or permit both.

Likely path: an HTTPS URL under a domain the organisation itself controls, resolving to a Controlled Identifiers document, is the baseline, with a host serving it on the organisation's behalf under that domain where one is used; `did:web` is permitted as a convention that resolves to the same document; no DID method that depends on a ledger, registry, or network is required.

This would change if DIDs 1.1 and DID Resolution reached Recommendation and a DID method for organisations gained a standards-track home, at which point the convention could become a normative option.

Status: open.

Applied as a working assumption in `exchange-model.md` section 7.1.

### D3. Accepting and producing mdoc

The question is whether a conforming verifier must accept mdoc presentations of government-issued credentials, and whether OpenCompetency defines an mdoc namespace rendering of its own records.

Likely path: accepting an mdoc presentation of a government-issued credential, such as a driver licence or an NZBN credential, is an optional conformance class that a verifier may claim once such credentials are in general use; OpenCompetency records stay on the W3C data model with their claims specified independently of either container; an mdoc rendering is not defined in v0.1.

This would change if the Government Digital Delivery Agency confirmed that the wallet will not hold W3C-model credentials and worker-held competency records in the government wallet became a priority use case, in which case the rendering would be defined as a v0.x addition without changing the vocabulary.

Status: open.

Applied as a working assumption in `exchange-model.md` section 14 and in `exchange-model/extensions.md` section 8.

### D4. Open Badges as base

The question is whether every OpenCompetency record is an Open Badges credential, or only those that are achievements in the Open Badges sense.

Likely path: qualifications, licences, training, assessments, and certifications are Open Badges achievement credentials; attestations and authorisations are OpenAssurance types on the plain W3C data model, sharing subject and alignment claim names with the achievement records but not forced into an achievement shape.

Achievement records keep the Open Badges proof format for now, because it differs from the envelope in `standards-map/credential-layer.md` section 3.1, and the exchange model asks verifiers to accept both until implementation settles the question.

This would change if 1EdTech added workplace attestation and authorisation semantics to Open Badges, in which case the OpenAssurance types would be re-based on them.

Status: open.

Applied as a working assumption in `exchange-model.md` sections 6.1 to 6.3 and 8.1.

### D5. New Zealand credential schemas

The question is whether to align with the published schemas at credentialschema.nz, which depends on the openness answers in `standards-map/people.md` section 6.

Likely path: define on the Open Badges base without waiting, and use the published schemas' field names wherever the two coincide, which costs nothing.

This would change if the publisher confirmed open licence terms and an open change process, in which case OpenCompetency would align formally and say so.

Status: open.

Not yet applied anywhere.

### D6. Organisation identifier

The question is whether the NZBN is required for New Zealand organisations or merely preferred.

Likely path: the NZBN is required for a New Zealand organisation acting as an issuer, and for the subject of an OpenPrequal record; it is preferred elsewhere; the LEI is accepted for organisations without an NZBN; a sole trader's NZBN is handled as personal information.

This would change if the Privacy Impact Assessment found that requiring a sole trader's NZBN created a disclosure the purpose does not need, in which case the requirement would apply to incorporated entities only.

Status: open.

Applied as a working assumption in `exchange-model.md` section 7.2.

### D7. Recognition publishing format

The question is whether to defer a format for publishing recognition lists, or to adopt one of the two candidates as prospective.

Likely path: defer, as `standards-map/recognition-and-requirements.md` section 2 recommends; define the Endorsement record and require that it can be issued, held, and presented like any other record; leave list publication to a later version.

This would change when either Recognized Entities reaches Candidate Recommendation or OpenID Federation for wallet architectures reaches Final, whichever comes first, at which point that one is adopted as prospective.

Status: open.

Applied as a working assumption in `exchange-model/extensions.md` section 2.

### D8. CTDL terms

The question is whether to borrow condition-profile terms for the Requirement record or define OpenAssurance's own.

Likely path: borrow the CTDL terms that match exactly, such as those for alternative conditions, target credentials, target competencies, and years of experience, define the rest, and depend on the vocabulary alone rather than on the registry around it.

This would change if the borrowed terms proved to carry meaning that does not survive translation to a DCQL query, in which case OpenAssurance would define its own and record the mapping.

Status: open.

Applied as a working assumption in `exchange-model/extensions.md` section 3.

### D9. Verification over time

The question is how records remain verifiable after an issuer rotates keys or ceases to exist, beyond the conformance rules in `exchange-model.md` section 8.3.

Likely path: the conformance rules in `exchange-model.md` section 8.3 apply from v0.1; the enduring-party question is put to regulators and industry bodies during Phase 1 engagement; no ledger or central archive is proposed.

This would change if a regulator or industry body volunteered to publish endorsements of issuers' historic keys for its sector, in which case the Endorsement record would gain a scope value for that purpose.

Status: open.

Applied as a working assumption in `exchange-model.md` section 8.3.

## 3. Open Questions

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
- to the Office of the Privacy Commissioner: whether the identifier approach in `standards-map/credential-layer.md` section 4 is consistent with Information Privacy Principle 13 as applied to employer-scoped identifiers;
- to a lawyer with employment and tort experience: whether a portable attestation, which states its scope, period, basis, and validity and can be withdrawn, carries any more risk for an employer or a supervisor than the informal attestations they already give;
- to the project's governance: whether a specification-specific intellectual property policy is needed alongside the Apache License 2.0 before other organisations contribute;
- to the project's governance: how the standard should engage with te ao Māori approaches to identity and with Māori data governance, given that the Trust Framework Act's purposes expressly include the former.[^distfact]

The question to buyers is a requirement rather than a research item, and belongs with Phase 1 validation.

None of these answers is a precondition for Phase 3, for the reasons given in `standards-map.md` section 7.10.

## 4. Changing a Decision

A decision is confirmed or overturned through the process in `CONTRIBUTING.md`, with the reason recorded under the decision.

Where a decision is overturned, every section of `exchange-model.md` and its extensions that names it is revised in the same change.

A new decision takes the next identifier, and identifiers are never reused.

## 5. Sources

Every status and date in this part was checked against the source listed in September 2026.

References to external organisations, schemes, and government publications are provided as evidence of what exists. No such reference implies consultation, participation, support, or endorsement.

[^beehive2026]: New Zealand Government, "New template to simplify prequalification process", 20 August 2026. https://www.beehive.govt.nz/release/new-template-simplify-prequalification-process

[^distfact]: Digital Identity Services Trust Framework Act 2023, 2023 No 13, sections 3, 8, 10, 15, 18 to 23, 34, 43, and 58. https://www.legislation.govt.nz/act/public/2023/0013/latest/whole.html
