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

Applied as a working assumption in `exchange-model.md` sections 6.1 and 8.1, with the attestation and authorisation types it leaves outside Open Badges defined in `exchange-model.md` sections 6.2 and 6.3.

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

This would change if the borrowed terms proved to describe the conditions for gaining a credential so closely that they do not fit a requirement written as guidance for an assessor's judgement, in which case OpenAssurance would define its own and record the mapping.

Status: open.

Applied as a working assumption in `exchange-model/extensions.md` section 3.

### D9. Verification over time

The question is how records remain verifiable after an issuer rotates keys or ceases to exist, beyond the conformance rules in `exchange-model.md` section 8.3.

Likely path: the conformance rules in `exchange-model.md` section 8.3 apply from v0.1; the enduring-party question is put to regulators and industry bodies during Phase 1 engagement; no ledger or central archive is proposed.

This would change if a regulator or industry body volunteered to publish endorsements of issuers' historic keys for its sector, in which case the Endorsement record would gain a scope value for that purpose.

Status: open.

Applied as a working assumption in `exchange-model.md` section 8.3.

### D10. Named persons: authority and approval

The question is how a record shows that a named person, such as the director who makes a declaration, held the role claimed and approved this exact record, when the organisation's signature proves neither.

Likely path: the record carries authority evidence and approval evidence separately; a check of a public register as at the date of the record, and an approval bound to a digest of the statement, are the floor for v0.1; a verifier reports both apart from the signature and apart from the truth of the statement; approvals signed by the person, or accompanied by a credential of their role, are extensions.

This would change if a credential proving a role in a public register, or delegated authority, became generally available, which the government wallet documentation lists among the credential types it expects, at which point the credentialed method would move into the core.[^wallettech]

Status: open.

Applied as a working assumption in `exchange-model.md` section 5.6, and in `exchange-model/extensions.md` section 9.

### D11. Requirements, assessments, and corrective actions

The question is whether a requirement is a set of machine rules that a system evaluates, or a statement of what is expected that an assessor judges evidence against.

Likely path: a requirement record states the outcome expected, gives guidance and non-exclusive examples of evidence, accepts equivalent evidence unless it expressly excludes it, writes any condition on who may issue the evidence as an objective criterion and never as an example, and marks only its objective criteria, such as thresholds, currency, periods, capacity, and accepted issuers, as checkable by a system; an assessment record identifies the exact requirement record it was made against and carries the assessor's determination for each requirement, in the assessor's own terms and in common words where the assessor maps them, with the evidence reviewed by reference, findings, and any qualification of the evidence; it states whether any corrective action request that affects it is unresolved, and how many are, and carries neither the requests nor their history; recommendations are advice to the organisation assessed, and are given outside the record or as claims the holder can withhold; a corrective action request is a record of its own that never changes, closed only by a further assessment from the issuer that raised it, with its state derived from the chain of records; when a request is raised or closed the assessor issues a replacement assessment, so that the current assessment, which is what a supplier normally presents, states the current position, and the history stays with the supplier and the assessor unless the supplier chooses to show it; terms follow established audit practice.

This would change if buyers and assessors, asked during Phase 1, wanted requirements they could evaluate entirely by machine, in which case the objective criteria would be extended and the judgement criteria left as they are.

An earlier draft had each assessment list the identifier of every corrective action request it raised, and that was set aside because it carried the audit history into a record meant for reuse.

The parts to test are whether a count of unresolved requests, without their identifiers, is enough for a relying organisation, and whether assessors will issue a replacement assessment each time a request is raised or closed; if they will not, a supplier would present the closure assessment beside the earlier assessment.

Status: open.

Applied as a working assumption in `exchange-model.md` section 6.4, and in `exchange-model/extensions.md` sections 3 and 10.

### D12. Request object and response binding

The question is how a relying organisation asks another organisation for assurance records without making an interactive protocol, a portal, or a shared platform a precondition.

Likely path: a small signed JSON request, delivered to the recipient's inbox or sent as a file, which states requirements and is never a questionnaire, identifies the requester and the recipient, carries a unique identifier, a nonce, a purpose, the engagement, and an expiry, and references the exact requirement records that apply by identifier and digest; a presentation made in response carries records the holder already holds, refers to the request and its nonce, and may map the records presented to individual requirement identifiers, as an index and never as a claim that a requirement is met; a response never restates the contents of those records in a structure made for one requester, so no response record type is defined; the relying organisation assesses what it was given, and a follow-up request refers to the earlier request, selects only the requirements that remain undemonstrated, and says what further assurance is sought; the request is not a verifiable credential; interactive implementations translate the same transaction into OpenID for Verifiable Presentations and DCQL, and no second requirement model is defined.

This would change if implementation showed that the OpenID request object could be used unchanged for a message delivered outside an OAuth exchange, in which case the separate request would be dropped.

Status: open.

Applied as a working assumption in `exchange-model/extensions.md` section 5, with the follow-up request in its section 5.7.

### D13. Delivery between systems

The question is how a record, a presentation, or a request gets from one organisation's system to another's without a person attaching, uploading, or re-entering anything, and without a hub that both must join.

Likely path: each organisation names an HTTPS inbox in a discovery record under its own domain; a sender posts the signed file to it with its registered media type, needs no account, key, or prior arrangement, and is told only that the file was taken; everything an inbox receives is signed, so the inbox authenticates nothing and the receiving system verifies what arrives as it would any file; the pattern is borrowed from W3C Linked Data Notifications, which cannot be used unchanged because it requires a JSON-LD body; a file sent by any other channel remains the floor for a party that has no system, and such a party may give an email address as its inbox.

Discovery and the inbox are part of the v0.1 core, because exchange between systems is the purpose of the model and a core that defined only a file could not move a record between two systems without a person carrying it; the signed request, approval for a period, and the interactive protocols remain extensions.

This would change if open inboxes proved unmanageable without knowing the sender, in which case an inbox would accept a file only with a signed request or presentation whose signature it had verified.

Status: open.

Applied as a working assumption in `exchange-model.md` sections 11.4 and 11.5, and in `exchange-model/extensions.md` section 5.6.

### D14. Forms and questionnaires

The question is how OpenAssurance relates to the forms through which most prequalification information is collected today, each with its own questions, inside the system of the buyer or scheme that asks.

Likely path: OpenAssurance exchanges assurance records and not completed forms, as `CHARTER.md` section 3.4 says; a user interface may use forms to create, review, or collect records, forms are not part of the exchange, and no particular form or portal is required for conformance; a form is treated as four separable things, which are what the asker needs demonstrated, the answering, the keeping of the answers, and the assessment; what the questions are after is expressed as requirements, self-asserted information that no other record already represents may be captured in one or more declarations, each grouping related statements and approved by an authorised person, and never as one record for each field of a form, an uploaded document is an evidence record, and the result is an assessment record, so no new record type is needed; a request states requirements and is never a questionnaire; the aim is that a thing is entered once and not that nothing is ever entered; a system built around a form adopts the model in three steps, each useful alone, which are giving back what was typed and the result as records, taking in records against requirements, and stating its requirements as a requirement record that reaches the suppliers who are asked; a requirement record need not be published and a scoring method need not be disclosed; a conforming system does not require what a record it has received already says to be entered again.

Where the information was typed into a relying organisation's system, that system can return it as a portable draft, and it becomes a declaration only when the supplier approves and signs it through a mechanism it has authorised, because the supplier and not the system that collected it is the party making the statement.

What is unsettled is the form of that draft.

This would change if scheme operators and buyers, asked during Phase 1, would not state their requirements to the suppliers they ask in a form another system can read, in which case the first two steps would stand alone and a supplier would map its records to each form by hand.

Status: open.

Applied as a working assumption in `exchange-model.md` section 11.3, in `exchange-model/extensions.md` sections 3 and 5.7, and in section 5.4 of the OpenPrequal profile.

### D15. The conformance boundary

The question is how to keep the core minimal without letting a system that only imports and verifies records present itself as removing duplication while it still sends holders through a questionnaire of its own.

Likely path: the core stays record exchange, which is records, signatures, status, presentations, delivery, and verification; a further conformance class, Request exchange, is layered on it, applies to both profiles, and is proposed for v0.1 alongside the core; the class requires requirement records that state what must be demonstrated, signed requests, submission maps, no response in a structure made for one requester, no questionnaire as a condition of responding, and follow-up only on what remains undemonstrated; a system that conforms only in the core classes is not described as supporting request exchange, and a claim of OpenPrequal or OpenCompetency request interoperability requires the class; the requirement record and the request stay drafted where they are, and are not moved into the core.

This would change if implementers found that record exchange and request exchange could not usefully be claimed apart, in which case the requirement record and the request would move into the core.

Status: open.

Applied as a working assumption in `exchange-model.md` sections 2.4 and 15.5, in `exchange-model/extensions.md` sections 1, 3, and 5, and in section 5.6 of the OpenPrequal profile.

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
- to the operators of existing prequalification schemes and to buyers that use their own forms: whether they would state what their questions are after as requirements, available to the suppliers they ask in a form another system can read, and on what terms;
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

[^wallettech]: Government Digital Delivery Agency, "Govt.nz app wallet technical guide". https://github.com/NZ-Digital-Public-Infrastructure/govt-nz-app-wallet
