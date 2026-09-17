# OpenAssurance Minimum Exchange Model

**Status:** Working draft towards v0.1  
**Last reviewed:** September 2026

## 1. Purpose

Phase 3 of the OpenAssurance development path is to define the minimum exchange model.

This document is the first working draft of that model.

It states the least that two systems have to agree on for an assurance record issued in one to be received, verified, and relied on in the other, without either party joining the other's platform.

It builds directly on `standards-map.md`, which identifies the existing standards OpenAssurance adopts and the small layer it has to define for itself.

Where `decisions.md` states a likely path for an open decision, this draft takes that path as a working assumption and says so.

Nothing in this draft is final.

No system can claim conformance to it, and no schema, protocol, or conformance suite exists yet.

### 1.1 Summary

In plain words, the model says five things.

- a record is a signed statement by an identifiable organisation, in an open format, that anyone can check without asking that organisation's software provider;
- the organisation is identified by its own domain name, and that domain is tied to its New Zealand Business Number through the public register;
- a record says whether it is still current, and a withdrawn record shows as withdrawn to anyone who checks;
- records are shared as a presentation that names the recipient, the purpose, and an expiry, and the floor for sharing is a file that can travel by email;
- a system that receives a record reports four things separately: whether it is authentic, whether it is current, whether the receiver recognises the issuer, and whether it meets the receiver's requirement.

The last two of those are always the receiver's own decision.

Everything else in this document is the detail needed to make those five things testable.

Extensions drafted for later versions are in `exchange-model/extensions.md`, and worked examples for both profiles are in `exchange-model/examples.md`.

## 2. How to Read This Draft

### 2.1 Requirement words

The words MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are used as defined in BCP 14, and only when they appear in capitals.

They describe what v0.1 is expected to require once it is finalised.

Until then they are proposals, and each one can be challenged through the process in `CONTRIBUTING.md`.

### 2.2 Working assumptions

Statements marked **Working assumption** adopt the likely path of a decision recorded in `decisions.md`, and each names the decision it depends on.

Phase 3 must confirm or overturn each of them in writing before v0.1 is finalised.

### 2.3 Sources

Every external standard named here is assessed, dated, and sourced in `standards-map.md` and its parts.

Section 20 lists them by name for convenience and does not repeat the assessment.

### 2.4 Core and extensions

A peer review of the first draft found that it was not minimal.

This document is therefore the core only: what the two reference exchanges in Phase 4 need, and what is proposed for v0.1.

The extensions drafted alongside it, which are the endorsement and requirement types, discovery, request and response, approval for a period, the interactive protocols, and acceptance of government-issued credentials, are in `exchange-model/extensions.md` and are not proposed for v0.1.

Worked examples are in `exchange-model/examples.md`.

### 2.5 System requirements and operator obligations

A requirement in capitals is a requirement on a system, and is meant to be testable by a conformance suite.

An obligation on the organisation operating a system, such as how long it retains a record, cannot be tested that way.

Such obligations are stated in plain words, without capitals, and are collected in section 13.2.

## 3. Scope

### 3.1 What this model defines

- the common structure every OpenAssurance record shares;
- the record types, and the claims each one carries;
- how issuers, organisations, people, and records are identified, and how an issuer is bound to the organisation it claims to be;
- how a record is signed, and how a verifier finds the key;
- how currency, replacement, and correction are expressed;
- how records are packaged into a purpose-specific presentation;
- the floor for moving records between systems;
- the verification procedure, and the shape of its result;
- the privacy requirements that apply to all of the above;
- what each class of conforming system must do.

### 3.2 What this model does not define

- who is competent, which supplier is acceptable, or which issuer is trustworthy;
- any organisation's requirements, criteria, scoring, or methodology;
- a registry of people, organisations, issuers, or records;
- a wallet, a wallet protocol, or an identity system;
- a credential format, signature scheme, status protocol, or presentation protocol of its own;
- the workflow, user experience, reporting, or commercial model of any conforming system.

Section 18 returns to these limits.

## 4. Model Overview

An exchange has five steps, and the model standardises the first four.

```text
Issuer creates a record
        |
        v
Issuer signs it as a verifiable credential
        |
        v
Holder keeps it, and packages what a purpose needs into a presentation
        |
        v
Presentation moves as a file, or through an interactive protocol
        |
        v
Verifier answers: authentic?  current?
        |
        v
Relying organisation answers: issuer recognised?  requirement met?
        |
        v
Local decision
```

The first two verification questions have the same answer for everyone, and the model defines how to reach it.

The last two have a different answer for every relying organisation, and the model defines only how they are expressed and kept separate.

## 5. Records

### 5.1 Common structure

Every OpenAssurance record is a verifiable credential conforming to the W3C Verifiable Credentials Data Model 2.0.

A record MUST carry:

- `@context`, beginning with the data model's base context;
- `id`, a URL under the issuer's control that identifies this record and no other;
- `type`, including `VerifiableCredential` and exactly one OpenAssurance record type from section 6;
- `issuer`, identifying the party responsible for the assertion, as section 7 requires;
- `validFrom`;
- `credentialSubject`, carrying the claims the record type requires.

A record SHOULD carry `validUntil` wherever the assertion is not intended to stand indefinitely.

A record MUST carry `credentialStatus` where section 9 requires it.

A record MAY carry `credentialSchema`, `evidence`, `relatedResource`, and `termsOfUse`.

The `id` of a record need not resolve to anything, and a verifier MUST NOT require it to.

### 5.2 Issuer provenance

The `issuer` of a record is the party that made the assertion.

A system that stores, forwards, hosts, or presents a record MUST NOT alter its `issuer` and MUST NOT present itself as the issuer of a record it did not issue.

Where a host operates signing keys on behalf of an organisation, the organisation remains the issuer, and section 8.4 sets the conditions.

### 5.3 Timestamps

Timestamps MUST be expressed as the data model requires, in the RFC 3339 profile of ISO 8601, with an explicit time zone.

### 5.4 Personal names, dates, and addresses

Where a record carries a person's name, date of birth, or address as a claim, it SHOULD use the representations in the New Zealand mandated government data standards, so that records exchanged with government need no translation.

### 5.5 Binding a record to its subject

The issuer is responsible for making sure a record is about the right person.

An employer has usually sighted photo identification when it engaged the worker, and a training provider when it enrolled the learner.

A record about a person SHOULD state how the issuer confirmed the subject's identity, as a short claim such as "photo identification sighted by the issuer", without recording the document's number.

A record about a person MUST carry enough claims for a relying organisation to match it to the person in front of it, normally the person's name, and MAY carry a date of birth or the digest of a photograph where the purpose needs them.

Matching the record to a person at the point of reliance is the relying organisation's act, by its own means, which may be sighting photo identification or receiving a government-issued credential alongside the record.

None of this requires an identifier shared between issuers.

## 6. Record Types

The architecture overview names six record types.

The core defines six credential types, because an authorisation and a declaration are distinct enough from an attestation to need their own.

Endorsement and requirement records are extensions, in `exchange-model/extensions.md`.

Type names are provisional.

### 6.1 Achievement

An achievement record asserts that a person holds a qualification, licence, certification, training outcome, assessment result, or micro-credential.

**Working assumption, decision D4.**

An achievement record is an Open Badges 3.0 achievement credential, with the achievement type taken from the Open Badges vocabulary.

Section 8.1 deals with the difference between the Open Badges proof format and the envelope used for other records.

Where the achievement is listed on the New Zealand Qualifications and Credentials Framework, the record MUST align to it by framework number and version, using the Open Badges alignment mechanism, and SHOULD carry credential type, level, and credits as `standards-map/people.md` section 7 describes.

A record asserting a registered occupational status SHOULD identify the public register that is the authoritative source for its currency.

### 6.2 Attestation

An attestation record is a first-hand statement that a person performed, demonstrated, or maintained something.

Its subject MUST carry:

- the assertion, and the kind of statement being made;
- the scope: activity, equipment, conditions, and context where they matter;
- the period over which it was observed;
- the basis: direct observation, supervision, review of records, or assessment against stated criteria;
- the attestor's role, and either their name or an identifier scoped to the issuer.

It SHOULD carry the attestor's authority, as a reference to another record or to a public register.

An attestor is a person too, and their name is personal information sent to every recipient, which is why the issuer may identify them by role and scoped identifier instead.

It MAY carry an alignment to a standard, qualification, or internal procedure by identifier.

The reasoning behind this structure, and a worked example, are in section 4 of the OpenCompetency profile.

### 6.3 Authorisation

An authorisation record is a permission an organisation grants a person to do defined work.

Its subject MUST carry:

- the permission: the work, and the equipment, site, or context it applies to;
- any conditions attached;
- the role that granted it.

It SHOULD carry the prerequisites relied on, as references to the records that satisfied them.

An authorisation MUST carry `credentialStatus`, because an authorisation is withdrawn more often than it expires.

### 6.4 Assessment

An assessment record is an opinion formed by reviewing evidence, issued by the party that formed it.

Its subject MUST carry:

- what was assessed, and the organisation or person it concerns;
- the criteria or standard assessed against, with its version;
- the result, in the assessor's own terms;
- the date of assessment.

It SHOULD carry, where the assessor's scheme uses them, a category, a status, a score, and the scope of evidence reviewed, including whether a site visit took place.

The model carries an assessor's result without interpreting it.

It MUST NOT be read as making the results of different schemes equivalent.

### 6.5 Evidence

An evidence record is a statement by a holder about a document or dataset it holds.

Its subject MUST carry:

- what the document purports to be;
- its purported source;
- the date the holder obtained it.

The document itself MUST be linked through `relatedResource` with a digest, and a verifier that uses the document MUST check the digest.

An evidence record MUST state whether the document carries its source's own digital signature.

A verifier MUST NOT treat an evidence record as carrying the source's signature unless it has checked that signature itself.

An evidence record says only that the holder has held the document unaltered since the date it obtained it.

When the source later issues a signed record, that record replaces the evidence record as section 9.3 describes, and nothing else in the holder's records changes.

Personal information that the stated purpose does not need SHOULD be removed from a document before it is linked.

### 6.6 Declaration

A declaration record is a statement by an organisation or a person about itself.

Its issuer and its subject are the same party, and the record MUST say so.

An organisation's declaration SHOULD name the declarant, their role as director or officer, and the public register that lists them.

A self-declaration's value comes from corroboration by other records, and a verifier SHOULD present it as a self-declaration.

## 7. Identifiers

### 7.1 Issuers

**Working assumption, decision D2.**

An issuer is identified by an HTTPS URL, under a domain name the issuing organisation itself controls, that resolves to a controller document as defined by Controlled Identifiers 1.0.

An issuer MAY instead be identified by a `did:web` identifier that resolves to the same document.

A conforming system MUST NOT require an issuer identifier that depends on a ledger, a registry, or a network operated by a third party.

A domain name is a low bar to entry, it is what makes email portable between providers, and it does the same job here.

A host MAY serve the controller document and status lists on an organisation's behalf, under the organisation's domain, so that the organisation changes host by changing where its domain points.

A host MUST NOT issue records for an organisation under the host's own domain.

### 7.2 Organisations

**Working assumption, decision D6.**

A New Zealand organisation acting as an issuer, or as the subject of an organisation-level record, MUST be described with its New Zealand Business Number.

An organisation without one SHOULD be described with a Legal Entity Identifier where it holds one.

The identifier is a claim about the organisation, carried alongside its name, and is not the issuer identifier of section 7.1.

A sole trader's New Zealand Business Number identifies a person, and records carrying it are personal information.

### 7.3 People

A subject identifier for a person is OPTIONAL.

A person MAY be identified by claims alone.

Where an identifier is used it MUST be scoped to the issuer, to an organisation, or to a pair of parties, and MUST NOT be a government, licence, tax, or qualification number.

A licence number, a registration number, or a learner number MAY appear as a claim where the record is about that licence, registration, or achievement.

A conforming system MUST NOT require a person to have an identifier that is shared across unrelated issuers.

Section 5.5 deals with how a record is bound to its subject without one.

### 7.4 Records

Section 5.1 requires every record to have an `id`.

Replacement and correction, in section 9, depend on it.

### 7.5 Binding an issuer to an organisation

A valid signature proves control of a domain.

It does not prove that the domain belongs to the organisation named in the record.

The binding is made in two directions, using a register that already exists.

- the domain asserts the organisation: the issuer's controller document, or the discovery record drafted in `exchange-model/extensions.md`, states the organisation's New Zealand Business Number;
- the organisation asserts the domain: the website recorded against that number in the public NZBN Register is on the same domain.

Where both hold, a verifier reports the issuer binding as confirmed.

Where only the first holds, it reports the binding as asserted only.

The register entry is maintained by the organisation through its own authenticated access to the register, which is what gives the check its value.

The register is a statutory public register with a free interface, and is not an OpenAssurance registry.

The check gives moderate assurance and no more.

An organisation that has not recorded a website, or an overseas organisation, cannot be confirmed this way, and recognition remains the relying organisation's decision in every case.

A credential proving a person's authority to act for a business, of the kind the government is trialling, would give higher assurance, and SHOULD be accepted as confirmation once it exists.

## 8. Securing

### 8.1 Envelope

**Working assumption, decision D1.**

Every record MUST be secured as a JSON Web Signature in the manner defined by Securing Verifiable Credentials using JOSE and COSE.

The record is the payload, the `typ` header is `vc+jwt`, and the claim names `vc` and `vp` do not appear.

A record MAY instead be secured as a selectively disclosable JWT under the same specification, with `typ` of `vc+sd-jwt`, where section 13 calls for selective disclosure.

A record MAY additionally be made available secured with a Data Integrity proof.

A conforming verifier MUST verify the JSON Web Signature form, SHOULD verify the selectively disclosable form, and MAY verify the Data Integrity form.

An achievement record is the exception.

Open Badges 3.0 defines its own JSON Web Token proof format, which requires RS256 as a minimum, permits a `typ` of `JWT` only, and carries validity in the `nbf` and `exp` claims, and that format differs from the one above.

Until the two are aligned, a conforming verifier MUST also verify an achievement record secured in the Open Badges format, and an issuer of achievement records SHOULD use that format so that existing Open Badges tooling can read them.

### 8.2 Algorithms

**Proposed.**

A conforming verifier MUST support ES256, and MUST support RS256 for achievement records secured in the Open Badges format.

A conforming issuer SHOULD sign with ES256 and MAY sign with EdDSA.

This choice follows the algorithm in widest use across the adopted protocols and is open to challenge.

### 8.3 Keys

The `kid` header MUST identify a verification method in the issuer's controller document.

That verification method MUST be listed under the assertion relationship for a record, and under the authentication relationship for a presentation.

An issuer MUST retain a retired key in its controller document, marked with the time it ceased to be used, and MUST NOT delete it while any record it signed remains within its validity period.

A verifier MUST check that the key was valid at the time of signing, and MUST NOT accept a signature made at or after the time a key was revoked.

### 8.4 Hosts that sign for an issuer

A small organisation MAY use a hosted service that holds signing keys on its behalf.

The organisation remains the issuer.

The host MUST keep each organisation's keys separate, MUST NOT use them for any other organisation, and MUST give the organisation what it needs to move to another host without its issued records becoming unverifiable.

Section 7.1 requires the issuer identifier to sit under the organisation's own domain, which is what makes that move possible.

## 9. Status, Replacement, and Correction

### 9.1 Validity period

A record outside the period from `validFrom` to `validUntil` is not current.

It remains authentic as a historical assertion, and a verifier MUST report the two separately.

### 9.2 Status

A record that is valid for more than 72 hours MUST carry a Bitstring Status List entry.

An authorisation MUST carry one regardless of its validity period.

The status list MUST be published at a URL under the issuer's control and MUST remain published for the validity period of every record it covers.

The 72 hour threshold is the one the New Zealand Trust Framework Rules use, so that this model does not set a lower bar than they do.

### 9.3 Replacement and correction

A signed record MUST NOT be altered after issue.

A record that replaces an earlier one MUST reference the earlier record's `id`, and the issuer SHOULD mark the earlier record as revoked or as superseded through its status entry.

A correction statement is a record whose subject is an earlier record, stating what was wrong and what is correct.

A verifier that finds a replacement or a correction for a record it is verifying MUST report it.

Term names for replacement and correction are an open point in section 17.

## 10. Presentations

### 10.1 Structure

A presentation is a verifiable presentation under the data model, secured as a JSON Web Signature with `typ` of `vp+jwt`.

Each record inside it is embedded as an enveloped verifiable credential, as the securing specification requires.

A presentation is signed by the holder that assembled it.

A holder's signature on a presentation says that the holder assembled and sent it, and nothing about the records inside.

### 10.2 Recipient, freshness, and expiry

A presentation that contains personal information MUST identify its intended recipient in the `aud` claim and MUST carry an expiry in the `exp` claim.

A presentation made in an interactive exchange MUST carry the verifier's nonce.

The recipient is identified by its issuer identifier where it has one, and otherwise by its domain name.

A verifier MUST reject a presentation addressed to another recipient, and one that has expired.

### 10.3 Terms of use

A presentation that contains personal information MUST carry a terms-of-use statement giving:

- the purpose for which it is shared;
- whether onward sharing is expected, restricted to named parties, or not expected;
- a suggested retention period.

These terms inform the recipient and do not bind it technically.

The recipient's legal obligations are its own, and the model does not replace them.

### 10.4 Minimum disclosure

A holder SHOULD include in a presentation only the records the stated purpose needs.

Where a single record carries claims the purpose does not need, the issuer SHOULD issue it in the selectively disclosable form so that the holder can withhold them.

Issuer provenance MUST survive any disclosure control.

## 11. Exchange

### 11.1 The floor

The floor for exchange is a file.

A conforming system MUST be able to export any record it holds, and any presentation it assembles, as a file containing the compact serialisation of its JSON Web Signature, in one of the media types registered by the securing specification.

A conforming system MUST be able to import such a file, and the same content pasted as text.

**Proposed.**

The file extension is `.vc.jwt` for a record and `.vp.jwt` for a presentation.

A file MAY travel by any channel the parties choose.

A holder MUST be able to export everything it holds, so that changing system does not strand its records.

### 11.2 A rendering a person can read

The receiving organisation may have nothing but an email client.

An exporting system SHOULD therefore provide, alongside the file, a rendering that states the issuer, the subject, the record type, what is asserted, the validity period, and how the file can be verified.

The rendering MUST NOT name a particular verification service as the only way to verify, and carries no authority of its own.

### 11.3 What a receiving system must not require

A conforming system MUST NOT require the issuer, the subject, the holder, or the sender of a record to hold an account with it, to be a customer or tenant of its provider, or to install its software, as a condition of receiving and verifying that record.

This is the Charter's open exchange requirement stated as a conformance rule.

### 11.4 Beyond the floor

Discovery of where to send a presentation, a signed request for one, approval for a period, the interactive protocols, and acceptance of government-issued credentials are extensions, drafted in `exchange-model/extensions.md`.

None of them changes the floor.

## 12. Verification

### 12.1 Procedure

A conforming verifier answers the first two trust questions as follows.

1. Resolve the issuer identifier to its controller document.
2. Find the verification method named by `kid`, and confirm its relationship and its validity at the time of signing.
3. Verify the signature.
4. Check the issuer binding as section 7.5 describes.
5. Check `validFrom` and `validUntil` against the time of verification.
6. Where the record carries a status entry, fetch the status list, verify it as a record in its own right, and read the entry.
7. Look for a replacement or a correction the verifier already holds.
8. For each related resource the verifier uses, check the digest.

The third and fourth questions are answered by the relying organisation against its own recognition list and its own requirement.

A verifier MAY evaluate them on the relying organisation's behalf, using only what that organisation has configured.

Matching the subject of a record to a person who is present is outside verification, and section 5.5 leaves it with the relying organisation.

### 12.2 Result

A verification result MUST report the four questions separately, with authenticity in two parts.

- signature: verified, failed, or not checked, with the reason;
- issuer binding: confirmed, asserted only, or not checked;
- currency: current, not yet valid, expired, suspended, revoked, superseded, or unknown;
- recognition: recognised, not recognised, or not evaluated;
- requirement: met, not met, or not evaluated.

A conforming system MUST NOT present a single combined result without making each of the four available.

A verifier SHOULD keep a record of what it verified, against which key and which status list, and when, without retaining personal information beyond what section 13 allows.

### 12.3 When something cannot be fetched

If a controller document or a status list cannot be fetched, the corresponding result is not checked or unknown.

It is not a failure, and it is not a pass.

A verifier MAY rely on a copy it fetched earlier, and MUST then report the time of that copy.

## 13. Privacy Requirements

`PRIVACY-PRINCIPLES.md` is the reference, and this section applies it to the model.

### 13.1 System requirements

These can be tested.

- a system MUST NOT publish a record about a person, or make it discoverable, by default;
- a status list MUST meet the minimum size the Bitstring Status List specification sets, so that checking status does not reveal which record is being checked;
- a presentation containing personal information MUST meet sections 10.2 and 10.3;
- an issuing system MUST be able to give the subject of a record a copy of it, as section 15.1 requires;
- a holding system MUST be able to tell the subject of a record which presentations have included it, as section 15.2 requires;
- a verification log MUST NOT reproduce the claims verified, and records only that a verification happened, against what, and what it found.

A person's right to ask for records about themselves already exists under the Privacy Act 2020, and the model adds only that the answer can be given as a file any conforming system can read.

### 13.2 Operator obligations

These cannot be tested by a conformance suite, and they are the operator's responsibility whatever system it uses.

- an operator includes in a presentation only the records the stated purpose needs;
- an operator that receives a presented record keeps it no longer than the stated purpose requires, unless it has its own lawful basis;
- an operator does not treat a person's consent as the only lawful basis on which a record may be presented, and does not assume consent has been given because a record was received;
- an operator keeps personal information that the purpose does not need out of organisation-level records and evidence;
- an operator that names an attestor by role and scoped identifier can say who that person was, where a relying organisation with a proper reason asks;
- an operator satisfies itself that a person asking for records about themselves is that person, as the Privacy Act already requires;
- an operator identifies its own lawful basis, gives its own notices, including any required for indirect collection, and sets its own retention.

The Privacy Impact Assessment required before v0.1 is finalised has not been started, and this section will change as a result of it.

## 14. Vocabulary and Namespace

OpenAssurance terms will be published as a JSON-LD context and a set of JSON Schemas written in JSON Schema 2020-12.

The namespace has not been assigned.

Three rules apply whatever it is.

- a verifier MUST NOT need to fetch anything from an OpenAssurance address in order to verify a record, and implementations MUST carry the context with them;
- a published context MUST NOT change once published, and a change of terms means a new versioned context;
- the vocabulary MUST be specified as named claims independent of any container, so that the same record can be rendered into another credential format without changing its meaning.

The first rule is the Charter's requirement that verification never depends on openassurance.nz being available.

## 15. Conformance Classes

A system may conform in one or more classes.

### 15.1 Issuing system

- creates records that meet sections 5 to 9;
- publishes and maintains the controller document and status lists sections 8 and 9 require;
- delivers every record it issues to its holder as a file, whatever else it offers;
- gives the subject of a record a copy of it as a file, on request.

### 15.2 Holding system

- stores records without altering them;
- assembles presentations that meet section 10;
- exports everything it holds, as section 11.1 requires;
- tells the subject of a record, on request, which presentations have included it, with recipient, purpose, and date;
- never presents itself as the issuer of a record it holds.

### 15.3 Verifying system

- imports files as section 11.1 requires;
- carries out the procedure in section 12 and reports the result in its form;
- meets section 11.3.

### 15.4 Host

A host provides storage or services for another party's records.

- keeps each party's records and keys separate;
- lets each party leave with its records and, where the host signs for it, with what it needs to keep them verifiable;
- never becomes the issuer of a record by hosting it.

An optional class for accepting government-issued credentials is an extension.

Conformance tests are Phase 5 and do not exist yet.

## 16. Worked Examples

Worked examples for both profiles, and for discovery, keys, and issuer binding, are in `exchange-model/examples.md`.

They are illustrative and carry no requirements.

## 17. Open Points

These are unresolved in this draft and should be settled before v0.1 is finalised.

Choices between alternatives that the standards map bears on are recorded as decisions in `decisions.md`, and the points below are unfinished drafting and things only implementation can settle.

- **The Open Badges proof format.** Open Badges 3.0 requires RS256 as a minimum, a `typ` of `JWT`, and validity carried in the `nbf` and `exp` claims, none of which matches the envelope in section 8.1, and section 8.1 currently asks verifiers to accept both; whether that is tolerable, or whether achievement records should use the Open Badges vocabulary under the common envelope, needs settling by implementation, under decision D4;
- **A working spike.** None of this has been implemented, and one attestation issued, exported, and verified by two independent open-source libraries would settle more than further drafting;
- **Domain continuity.** A lapsed domain that is re-registered by someone else, while the register still lists it, would pass the binding check in section 7.5, and a verifier that has seen an issuer before SHOULD be warned when its keys change without continuity;
- **Signing time.** The time of signing is asserted by the signer, so a compromised key can backdate, and the rule in section 8.3 is weaker than it reads until trusted timestamps or re-issuance after compromise are addressed;
- **Attestor and issuer liability.** Any attestation carries the risk of being relied on, and that is as true of a reference letter as of a signed record; what is new is that a portable record travels further and lasts longer, and whether stating its scope, period, basis, and validity, with a status entry for withdrawal, keeps that risk where it is today deserves a legal view;
- **Bulk export.** Section 11.1 requires everything to be exportable, and whether that is a set of files, a single presentation, or a Comprehensive Learner Record is undecided;
- **Replacement and correction terms.** Section 9.3 needs term names, and a decision on whether the link is a claim or a typed related resource;
- **Algorithm choice.** Section 8.2 is a proposal;
- **Assessment result structure.** Section 6.4 lists what schemes commonly report, and needs testing with buyers and scheme operators as `decisions.md` section 3 describes;
- **Verification over time.** What happens when an issuer ceases to exist remains open as decision D9, and `standards-map/credential-layer.md` section 3.4 describes what the standards offer;
- **Privacy Impact Assessment.** Section 13 is provisional until it is done.

## 18. What This Model Does Not Do

The model does not decide anything on a relying organisation's behalf.

It does not rank issuers, schemes, or assessors, and it does not make different schemes' results equivalent.

It does not require any party to be accredited, registered, or listed anywhere in order to issue, hold, present, or verify a record.

It does not create an identifier for people.

It does not require a wallet, and it does not prevent one.

It does not operate a service through which people request records about themselves, and a service that helps them make and authenticate such requests may be built by anyone, as an ordinary participant.

It does not replace the management, assessment, and workflow products that organisations already use, and a product that implements it keeps everything that distinguishes it.

It does not replace the duty of organisations with overlapping health and safety duties to consult, cooperate, and coordinate.

## 19. Design Test

> **Can a record issued by a system its recipient has never heard of be received as a file, verified against the issuer's own published key, checked for currency, and assessed against the recipient's own requirement, without the recipient creating an account anywhere or asking anyone's permission?**

If the answer is no for any conforming pair of systems, the model has failed at the thing it exists to do.

## 20. Standards Referenced

Assessment, status, and sources for each of these are in `standards-map.md` and its parts.

- W3C Verifiable Credentials Data Model 2.0, <https://www.w3.org/TR/vc-data-model-2.0/>;
- W3C Securing Verifiable Credentials using JOSE and COSE, <https://www.w3.org/TR/vc-jose-cose/>;
- W3C Verifiable Credential Data Integrity 1.0, <https://www.w3.org/TR/vc-data-integrity/>;
- W3C Bitstring Status List 1.0, <https://www.w3.org/TR/vc-bitstring-status-list/>;
- W3C Controlled Identifiers 1.0, <https://www.w3.org/TR/cid-1.0/>;
- IETF RFC 9901, Selective Disclosure for JSON Web Tokens, <https://www.rfc-editor.org/rfc/rfc9901.html>;
- IETF BCP 14, RFC 2119 and RFC 8174, <https://www.rfc-editor.org/info/bcp14>;
- IETF RFC 3339, Date and Time on the Internet, <https://www.rfc-editor.org/info/rfc3339>;
- 1EdTech Open Badges 3.0, <https://www.imsglobal.org/spec/ob/v3p0/>.
