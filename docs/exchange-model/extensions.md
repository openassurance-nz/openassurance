# OpenAssurance Minimum Exchange Model: Extensions

**Part of:** `exchange-model.md`  
**Status:** Working draft, not proposed for v0.1  
**Last reviewed:** September 2026

## 1. Purpose

The core of the minimum exchange model is in `exchange-model.md`.

This document holds the extensions that were drafted alongside it and are not proposed for v0.1.

They are kept so that the core does not foreclose them, and so that the thinking behind them is not lost.

Requirement words, working assumptions, and the split between system requirements and operator obligations are used as `exchange-model.md` section 2 defines them.

Nothing here is needed for the two reference exchanges in Phase 4.

Each extension reuses an existing mechanism before defining anything, and each is open to challenge through the process in `CONTRIBUTING.md`.

## 2. Endorsement

An endorsement record states that one party recognises another party, an achievement definition, or a particular record.

**Working assumption, decision D7.**

An endorsement record is an Open Badges 3.0 endorsement credential.

Its subject MUST carry a scope: what the endorsement covers, by record type, activity, category, or period.

An endorsement without a scope MUST be treated by a verifier as informational only.

## 3. Requirement

**Working assumption, decision D11.**

A requirement record is a signed statement by a relying organisation describing what it expects, together with guidance and examples of evidence that may demonstrate it.

It is not a rules engine.

Prequalification that works states a requirement clearly, shows what acceptable evidence looks like, allows equivalent evidence, and leaves the judgement to an assessor, and a requirement record is built to carry exactly that.

A requirement record MAY hold one requirement or a numbered set, and each requirement MUST carry:

- an identifier that stays the same between versions;
- what it applies to, such as a role, an activity, a contract, or a supplier category;
- the statement of what is expected, in words a person can assess against;
- whether it is mandatory or informational.

Three identifiers keep the history intelligible.

The `id` of the record identifies one immutable issued version, the `id` of its subject identifies the requirement set from one version to the next, and each requirement within the set has a short identifier of its own.

An assessment can then say exactly which requirement, in which version of which set, it was made against, and a later version that changes one requirement leaves the history of the others readable.

Each requirement SHOULD carry guidance, and examples of evidence that may demonstrate it.

Evidence examples are not exclusive unless the requirement expressly says so.

Accepting equivalent evidence is the normal posture for any requirement that is assessed on evidence.

A requirement states an outcome that is expected, and not a document that is requested.

A supplier is not asked to put a particular document in a particular box: it presents the evidence it has, and an assessor decides whether that evidence demonstrates the requirement.

A requirement MAY also carry objective criteria, which are the parts a system can check without judgement:

- a threshold, such as public liability insurance of at least a stated amount;
- currency, such as a licence or an assessment that has not expired;
- a period, such as a declaration covering the previous five years;
- a capacity, such as a declaration made by a director;
- an accepted issuer or endorsement, or one of several alternatives.

An objective criterion is a named type, such as a minimum insurance limit, a lookback period, or a declarant's capacity, and not an expression in a general language of paths, operators, and nested logic.

The list of types grows only where a genuinely objective test recurs.

A condition that only one source can satisfy, such as a practising licence issued by the Electrical Workers Registration Board, is a condition on who issued the evidence.

It MUST be written as an objective criterion, and never as an example of evidence.

That discipline is what stops a list of examples of acceptable evidence from quietly becoming the only files a portal accepts.

A conforming system MUST NOT reject a presentation, or report a requirement as not met, because the evidence presented is of a kind that is not listed among the examples.

A requirement record MAY be used to derive a DCQL query that helps a holder's system identify candidate records in an interactive exchange.

A DCQL match does not mean that a requirement is met.

Everything else is for a person, and a conforming system MUST NOT report a requirement as met on the strength of its objective criteria alone where the requirement also calls for judgement.

A requirement MAY name a category from a published set of topics, such as the twelve in WorkSafe New Zealand's risk-based prequalification template, so that evidence organised for one buyer can be found by another.

**Working assumption, decision D8.**

Terms that match the CTDL condition profile exactly are borrowed from it, and the rest are defined by OpenAssurance.

Publishing a requirement is optional, and a relying organisation MAY keep its requirements private.

`examples.md` section 3.1 shows how to read a requirement and how to write a good one, followed by a whole requirement record as JSON, and the outline below shows the shape of a single requirement.

An example, in outline and with every detail illustrative:

```text
Requirement R12, version 2

Applies to:
Suppliers carrying out physical work on site

Statement:
Workers are competent for the work they perform, and the licences,
qualifications, and authorisations the work needs remain current.

Mandatory:
Yes

Evidence that may demonstrate it, among other things:
- a competency matrix
- training records
- licences and qualifications
- employer authorisations
- competency assessments
- expiry and renewal records

Objective criteria:
- any licence relied on is current at the date of assessment
```

## 4. Discovery

**Proposed.**

An organisation SHOULD publish a DNS TXT record at the name `_openassurance` under its domain, giving its issuer identifier, its New Zealand Business Number, and the address at which it receives presentations and requests.

```text
_openassurance.harbourbeverages.example.  TXT  "v=OA1; issuer=https://harbourbeverages.example/issuer; nzbn=(number); inbox=mailto:assurance@harbourbeverages.example"
```

The pattern is the one DKIM and similar mechanisms use, it is familiar to anyone who has set up email for a domain, and it needs no website.

It lets a sender who knows only an organisation's domain find where to send a presentation, and it gives the `aud` claim of a presentation a value.

The inbox MAY be an email address, because the floor in `exchange-model.md` section 11.1 is a file that can travel by any channel, or an HTTPS address that accepts such a file.

Keys stay in the controller document and are not published in DNS.

`examples.md` section 6 works through an example, with the controller document and the binding check.

The record format, the behaviour of an HTTPS inbox, and whether a well-known address should be offered as an alternative are open points in section 11.

## 5. Request and Response

**Working assumption, decision D12.**

The floor lets a holder send a presentation unprompted.

The other pattern is a relying organisation asking for one, and that needs a transaction layer between a durable requirement and a supplier's presentation.

Four objects are involved, and each has one job.

```text
Requirement record      durable policy: what the relying organisation expects
        |
        v
Request                 this requester asking this recipient, now, for this engagement
        |
        v
Presentation            the holder's response, and the evidence it chooses to disclose
        |
        v
Assessment record       the determination of the relying organisation or its assessor
        |
        +--> Corrective action request, where one is required
```

A requirement record says what an organisation requires of anyone.

A request says that one organisation is asking another to respond to particular requirements for a particular engagement.

That is a passing message and not an enduring assertion, so a request is not a verifiable credential.

| Object | Meaning | Form |
|---|---|---|
| Requirement | What the relying organisation expects | Requirement record, a verifiable credential |
| Request | Please respond to these requirements for this engagement | Signed JSON, a JSON Web Signature |
| Query | Which held records may be relevant | DCQL, derived, interactive exchange only |
| Presentation | The evidence the holder chooses to disclose | Verifiable presentation |
| Assessment | Whether the evidence demonstrates the requirement | Assessment record, a verifiable credential |
| Corrective action | A specific deficiency to be put right | Corrective action request, a verifiable credential |

The genuinely new pieces are small: the requirement vocabulary, the request, and the map between requirement identifiers and the records presented.

Everything cryptographic, and most of the interactive exchange, is an existing standard.

### 5.1 The request

A request is a JSON object that MUST carry:

- `iss`, the requester's issuer identifier;
- `aud`, the recipient's issuer identifier, so that a request cannot be passed to another organisation as though it were addressed to it;
- `iat` and `exp`, so that an old request does not stay actionable;
- `jti`, an identifier for the transaction that every later record can refer to;
- `nonce`, which the presentation made in response carries back;
- the subject the request is about;
- the purpose, and the use the requester proposes to make of what it receives;
- the address to reply to.

It SHOULD carry the engagement that gives rise to it, such as a contract reference, an activity, a start date, and the period for which the records are needed, because that is what tells the recipient why these requirements apply and for how long.

The subject is either the recipient organisation itself, or a person whose records the recipient holds, identified by claims such as a name and the job concerned, and never by an identifier the requester was not given by the holder.

Where requirements apply, the request MUST reference each requirement record by its `id` and by a digest, and MAY select particular requirements from it by identifier.

A request MAY refer to an earlier request by its `jti`, and MAY say, against a requirement it selects, what further evidence the requester seeks, which is how a requester asks for more where what it was given is relevant and not enough.

The request does not restate the requirements.

The digest is computed over the secured form of the requirement record, which is the exact content of its file, so that no canonical form of JSON is needed and there can be no later doubt about what was asked.

A conforming exchange MUST NOT depend on fetching a requirement record from anywhere: the record accompanies the request, or the recipient already holds it.

A request MAY carry a DCQL query derived from the requirement records, as section 5.5 describes.

### 5.2 Securing the request

A request MUST be secured as a JSON Web Signature, signed with a key that the requester's controller document lists under the authentication relationship and that the `kid` header names.

**Proposed.**

The `typ` header is `oa-request+jwt`, and a conforming recipient MUST support ES256.

### 5.3 Verifying a request

A recipient checks the following, in this order, before it considers disclosing anything.

1. The signature, against the requester's controller document.
2. The requester's issuer binding, as `exchange-model.md` section 7.5 describes.
3. That `aud` names the recipient.
4. That the request has not expired, and that its `jti` has not been seen before.
5. The signature of each requirement record referenced.
6. That each requirement record matches the digest in the request.

The holder then decides.

It works out who or what the request concerns, decides whether it has a lawful basis and a proper purpose to disclose, and selects the minimum records.

A holder MUST NOT confirm or deny that it holds records about a person to a requester whose signature or issuer binding it cannot verify.

A holder MAY decline any request without giving a reason.

### 5.4 The response

A presentation made in response to a request MUST name the requester in `aud`, carry the request's `nonce`, refer to the request by its `jti`, and carry its own expiry and the holder's own terms of use.

The use a requester proposes is a proposal, and the terms that govern a presentation are the holder's.

The presentation SHOULD carry a submission map, which lists, for each requirement, the records the holder presents against it.

A submission map is an index and not a claim.

It says that the holder presents these records for the requester to consider against that requirement, and it MUST NOT be read as the holder asserting that the requirement is met.

A requirement for which the holder presents nothing is simply absent from the map.

### 5.5 Interactive exchange

Where both systems support OpenID for Verifiable Presentations, the same transaction is translated into it, and no second requirement model is defined.

- the nonce maps directly;
- candidate records are requested with a `dcql_query` derived from the requirement records;
- the requester is identified as that protocol requires, and the response is returned in its `vp_token`.

The request in section 5.1 is not an OpenID authorization request, because that format carries fields that belong to an OAuth exchange and mean nothing in a message that may travel by email.

A DCQL query helps a holder's system find candidate records.

A match does not mean that a requirement is met.

### 5.6 The file floor

Two files attached to an email are enough.

```text
prequalification-request.jwt                 the signed request
tidewater-ammonia-requirements-v3.vc.jwt     the requirement record it refers to
```

No portal is involved, and neither party joins anything.

`examples.md` section 3 works through a whole transaction, from the requirement to the assessment that closes it.

## 6. Approval for a Period

An engagement lasts weeks or years, and a relying organisation needs the records to stay current for that long.

Most of that need is already met without any further mechanism.

- the expiry of the presentation is the end of the period the holder approved;
- every record in it carries its own validity period and, where `exchange-model.md` section 9.2 requires one, a status entry;
- the relying organisation can check status again whenever it chooses, and the issuer does not learn which record was checked.

An authorisation withdrawn when a worker leaves, or a licence that lapses, therefore shows at the relying organisation's next check, with nothing sent by anyone.

What status cannot deliver is a record that did not exist when the presentation was made, such as a renewed licence, a new attestation, or a replacement.

For that, a holder MAY record its approval as a standing grant: for a stated requester, subject, requirement, purpose, and period, it sends a fresh presentation to the requester's inbox when a relevant record is issued, renewed, or replaced.

That is publish and subscribe without a broker.

The subscription is the holder's own approval, held by the holder, and it ends when the period ends or when the holder withdraws it.

A holder MAY also send a change notice, which says only that something covered by a grant has changed and that the relying organisation should verify again.

A change notice MUST NOT carry personal information and MUST NOT say what changed.

A conforming system MUST NOT require a broker, a hub, or a shared message service, because that would make a third party a precondition for exchange.

A grant is a disclosure like any other, so it appears in the list a subject can ask for under `exchange-model.md` section 15.2, and the relying organisation's retention runs from the end of the period.

Existing event formats, in particular the IETF security event token with its push and poll delivery, should be evaluated for the change notice before anything new is defined.

## 7. Interactive Exchange

Section 5.5 says how a request is translated when an exchange is interactive, and this section covers issuance and presentation in general.

Where both parties run systems that support them, records SHOULD be issued using OpenID for Verifiable Credential Issuance 1.0 and presented using OpenID for Verifiable Presentations 1.0, with requests expressed in DCQL.

A system that supports interactive exchange MUST still support the floor.

The credential format identifier that those protocols use for a record secured under `exchange-model.md` section 8.1 is an open point in section 11.

## 8. Government-Issued Credentials

**An optional conformance class, decision D3.**

A relying organisation's requirement may name a government-issued credential such as a driver licence.

The government issues such credentials in the mdoc format, with a status mechanism of its own.

A verifier that claims this optional class MUST be able to accept a presentation of such a credential in that format, including its status mechanism, and MUST NOT require it to be re-issued as an OpenAssurance record.

No conforming system is required to claim that class, and it is expected to matter once government-issued credentials are in general use.

## 9. Stronger Evidence of Role and Approval

**Decision D10.**

`exchange-model.md` section 5.6 lets a record carry a named person's authority and approval, and leaves two methods to this document because their formats are not settled.

A signed approval is a signature made with a key bound to the person, over the same statement digest the core requires, carried inside the record beside the organisation's own signature.

It shows that the holder of that key approved the statement, and it is only as strong as the binding between the key and the person.

A credentialed approval adds a credential issued by someone other than the organisation, establishing the person's identity and their role.

The government wallet documentation lists proof of role in a public register, and delegated authority, among the credential types it expects to hold.

An accredited provider could issue such a credential by establishing a person's identity and checking the Companies Register, without OpenAssurance operating anything.

No such credential is known to be available yet, and nothing in the core depends on one.

When one exists, a verifier SHOULD accept it as authority evidence in place of a register check, and SHOULD report the role as independently verified.

A conforming system MUST NOT require either method, because a small supplier must be able to make a declaration with nothing more than the core.

## 10. Corrective Action and Closure

**Working assumption, decision D11.**

An assessment that finds a requirement partially met or not met usually says what must be put right.

The terms follow established audit practice, in which a nonconformity calls for corrective action and an opportunity for improvement does not.

A corrective action request is for something the organisation must put right.

Where the evidence presented is simply not enough to decide, nothing has been found wanting, and the assessor asks for more with a further request as section 5.1 describes, and not with a corrective action request.

A recommendation is an opportunity for improvement, it is advice to the organisation assessed, and `exchange-model.md` section 6.4 keeps it out of the part of an assessment record that travels.

> **OpenAssurance exchanges the current assurance state, and does not automatically expose the assurance history.**

The history exists for auditability, and the current assessment exists for reuse.

### 10.1 The corrective action request

A corrective action request is a record issued by an assessor to the organisation assessed, and it MUST carry:

- its own identifier;
- the organisation it concerns;
- the assessment that raised it;
- the requirement it relates to, by the identifier of the requirement record, which names the version, and the identifier of the requirement within it;
- the finding;
- the outcome required;
- the date by which it is due.

The subject of a request, with every detail illustrative:

```json
{
  "organisation": {
    "name": "Ridgeline Refrigeration Limited",
    "nzbn": "illustrative"
  },
  "assessment": {
    "id": "https://tidewatercoldstorage.example/assessments/2026-0458"
  },
  "requirement": {
    "set": "https://tidewatercoldstorage.example/requirements/ammonia/versions/3",
    "id": "R1"
  },
  "finding": "The competency system identifies the training required for each role, but expiry dates for licences and authorisations are not consistently recorded or monitored.",
  "requiredOutcome": "Expiry dates are recorded and actively monitored for every licence and authorisation relied on for the work.",
  "dueDate": "2026-11-30"
}
```

The outcome required says what must be true, and not which document must be produced, for the reason section 3 gives for requirements.

The request points to the assessment that raised it, and the assessment does not point back, so an assessment that is presented discloses no more than how many requests are unresolved.

A signed record is never edited, so a corrective action request MUST NOT carry a field that is expected to change, such as a status of open or closed.

Its status entry under `exchange-model.md` section 9.2 says only whether the issuer has withdrawn the request, as it might where one was raised in error, and says nothing about progress.

### 10.2 The chain

The life of a request is a chain of records, each linked to the last by identifier.

```text
Assessment                  a requirement is partially met; one request is unresolved
     |
     v
Corrective action request   refers to the assessment; finding, outcome required, due date
     |
     v
Evidence                    refers to the request; held and signed by the supplier
     |
     v
Closure assessment          refers to the request and the evidence: accepted, or not accepted
     |
     v
Replacement assessment      replaces the first; the requirement is now met; none unresolved
```

The order is the order of events, and each record refers only to records that came before it.

The supplier's evidence of correction is an evidence record under `exchange-model.md` section 6.5, and it SHOULD name the request it relates to.

### 10.3 The closure assessment

A closure is an assessment record whose subject is the corrective action request, so no further record type is needed.

An assessment already means a party reviewing evidence and forming an opinion, and that is what closure is.

A closure assessment MUST carry:

- the corrective action request assessed, by type and identifier;
- the organisation it concerns;
- the evidence reviewed, as the identifier and type of each record;
- the result in the assessor's own terms, and a closure result of accepted or not accepted;
- a finding;
- the date of assessment.

The subject of a closure assessment, with every detail illustrative:

```json
{
  "assessed": {
    "type": "CorrectiveActionCredential",
    "id": "https://tidewatercoldstorage.example/corrective-actions/CAR-7"
  },
  "organisation": {
    "name": "Ridgeline Refrigeration Limited",
    "nzbn": "illustrative"
  },
  "assessmentDate": "2026-10-21",
  "evidenceReviewed": [
    {
      "recordId": "https://records.ridgelinerefrigeration.example/evidence/2026-0088",
      "recordType": "EvidenceCredential"
    }
  ],
  "result": {
    "outcome": "Corrective action accepted",
    "closureResult": "accepted"
  },
  "finding": "The evidence demonstrates that expiry dates are now recorded for licences and authorisations and are included in a scheduled monthly review."
}
```

Accepted means that the assessor accepts that the outcome required has been achieved.

Not accepted means that the evidence reviewed did not demonstrate the outcome required, the request stays open, and a later closure assessment may accept it.

The assessor's own words sit beside the closure result, as they do in any determination, so an assessor may say further evidence required where the closure result is not accepted.

A closure assessment MUST be issued by the issuer of the corrective action request.

An assessment of the request by anyone else is that party's opinion, which a relying organisation may weigh, and it closes nothing.

An accepted closure does not change the determination that raised the request.

The assessor's current determination is given by the replacement assessment that `exchange-model.md` section 6.4 requires, and until it is issued the earlier determination stands.

### 10.4 State is derived, and never stored

The request never changes, and its state is derived from the chain by whoever holds the chain.

- open, until a current closure assessment from its issuer accepts it;
- overdue, where it is open and its due date has passed;
- closed, once a current closure assessment from its issuer accepts it.

A system can derive state only from the records it holds.

The supplier and the assessor hold the chain, and a relying organisation normally does not.

What a relying organisation relies on is the assessor's current assessment, which states whether any request that affects it is unresolved, and how many are.

That statement is inside the record the assessor signed, so a supplier cannot hide an unresolved request by leaving a record out, and the assessor's current assessment remains the authority on what is outstanding.

### 10.5 What travels

A holder normally presents the assessor's current assessment, together with the requirement record it was made against, because the assessment identifies each requirement and does not restate it.

The following stay with the supplier and the assessor unless the holder deliberately chooses to present them.

- an assessment that has been superseded;
- a corrective action request that has been closed, its closure assessment, and the evidence of correction;
- the detail of a request that is unresolved, whose existence the current assessment already states;
- recommendations;
- an assessor's working notes.

A holding system MUST NOT add any of these to a presentation unless the holder selects them.

A relying organisation that needs the detail of an unresolved request asks for it, and SHOULD say why, and the holder decides as it does with any request.

A supplier may well choose to present a closed chain, because a finding that was dealt with promptly speaks well of it, and that is the supplier's choice to make.

Where an assessor has accepted a closure and has not yet issued the replacement assessment, the supplier MAY present the closure assessment beside the earlier assessment.

A recommendation does not become permanent baggage attached to an organisation each time its assessment is shared.

### 10.6 What a system reports

A system that shows an assessment MUST keep these apart, in addition to the questions in `exchange-model.md` section 12.2.

- what evidence was reviewed;
- what the assessor concluded, in its own terms, and in common words where it gave them;
- whether any corrective action request is unresolved: none, the number stated, or not stated;
- whether the assessment is the assessor's current one, or has been superseded.

A system that holds the chain also reports, for each request, whether a closure assessment from its issuer accepts it.

It MUST NOT collapse them into a single status.

### 10.7 Privacy

Findings SHOULD be written about an organisation's systems and not about named people, and personal information that a finding does not need SHOULD be left out, as `exchange-model.md` section 6.4 says of any finding.

Evidence of correction often comes from records about workers, and names that the finding does not need SHOULD be removed before a document is linked.

Keeping that evidence out of later presentations is one more reason for section 10.5.

Where the subject of an assessment is a person, a corrective action is sensitive information about them, and it SHOULD stay between that person, their employer, and the assessor.

`examples.md` sections 3.9 to 3.13 follow one request through the whole chain, with each record in full, and its section 4 shows what a second buyer is then given.

## 11. Open Points

These are unresolved in the extensions, and none of them holds up the core.

- **Requests.** Section 5 leaves open how one request is addressed to many recipients, as in a tender, how long a recipient remembers the identifiers it has seen, and how a request about a person names them without disclosing more than the requester was given;
- **The submission map and the terms of a response.** Section 5.4 needs term names, and a decision on where in a presentation they sit;
- **Corrective action terms.** Section 10 needs term names, a decision on whether a closure is an assessment as drafted or a record type of its own, a test of whether a count of unresolved requests without their identifiers is enough for a relying organisation, and a decision on whether a recommendation needs a record form of its own;
- **Reuse of an assessment.** `examples.md` section 4 shows a buyer's assessment reused by a second buyer, and whether an assessor may state terms for reliance by others, and whether a supplier may always pass on the requirement record it was assessed against, are undecided;
- **Grants and change notices.** Section 6 describes a standing grant and a content-free change notice, and neither has a format, so existing event formats need evaluating first;
- **The discovery record.** Section 4 proposes a DNS record, and its format, the behaviour of an HTTPS inbox, and a well-known address as an alternative are undecided;
- **Format identifier in the interactive protocols.** How the OpenID format identifiers for W3C credentials apply to a record secured under `exchange-model.md` section 8.1 needs confirming by implementation;
- **An mdoc rendering.** `exchange-model.md` section 14 keeps it possible, and whether to define one is decision D3, which depends on answers from the Government Digital Delivery Agency.

## 12. Standards Referenced

Assessment, status, and sources for each of these are in `standards-map.md` and its parts, and the standards the core relies on are listed in `exchange-model.md` section 20.

- IETF BCP 222, RFC 8552, underscored naming of DNS attribute leaves, <https://www.rfc-editor.org/info/rfc8552>;
- IETF RFC 8417, Security Event Token, with RFC 8935 and RFC 8936 for push and poll delivery, <https://www.rfc-editor.org/info/rfc8417>;
- OpenID for Verifiable Credential Issuance 1.0, <https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0-final.html>;
- OpenID for Verifiable Presentations 1.0, <https://openid.net/specs/openid-4-verifiable-presentations-1_0-final.html>;
- Credential Engine CTDL, <https://credreg.net/ctdl/handbook>.
