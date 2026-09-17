# OpenCompetency

**Profile:** OpenAssurance for people and workplace competency  
**Status:** First draft

## 1. Purpose

OpenCompetency is the OpenAssurance profile for exchanging workplace competency information about people.

It is intended to allow an employer, qualification provider, assessor, industry body, customer, or other authorised party to issue, hold, present, and verify competency information without requiring all organisations to use the same competency-management platform.

OpenCompetency is not intended to be a compulsory worker passport.

The operational holder of a record may be the worker, employer, issuer, or another authorised party.

## 2. Problem

Employers may already maintain verified competency records for their workers but still be required to recreate those workers and records in a customer's nominated platform.

This leads to:

- duplicate worker records;
- duplicate qualification uploads;
- repeated verification;
- multiple expiry processes;
- additional licence costs;
- increased administration;
- inconsistent records;
- platform dependency.

OpenCompetency aims to make the competency evidence portable instead.

## 3. Initial Record Types

OpenCompetency should support or map to records such as:

- qualification;
- licence;
- training;
- course completion;
- assessment;
- practical competency;
- equipment-specific competency;
- employer attestation;
- experience;
- induction;
- employer authorisation;
- industry authorisation.

Existing open schemas should be reused where practical.

The working draft in `docs/exchange-model.md` defines the credential types that carry these records, and `docs/standards-map.md` records which existing standards they are built on.

## 4. Employer Attestations

Workplace competency is not represented only by formal qualifications.

An employer, supervisor, or assessor may legitimately need to attest that a person has performed, demonstrated, or maintained a particular capability.

Example:

```text
Subject:
Worker A

Assertion:
Operated Equipment X under normal working conditions.

Period:
January 2025 - August 2026

Basis:
Direct supervision

Attestor:
Authorised supervisor

Authority:
Employer authorisation designating the supervisor
as a workplace assessor for this equipment

Organisation:
Employer
```

The employer is the issuer and signs the record, the supervisor is the attestor named in it, and the authority line says what entitles the supervisor to attest.

The exchange model defines this structure in its section 6.2, and defines employer authorisation as a record type of its own in its section 6.3.

Sections 4.1 to 4.5 below give the reasoning behind that structure, and a fuller worked example.

The attestation records who made the assertion and why.

It does not force another organisation to accept that assertion.

### 4.1 Three layers behind one signature

The paper world bundles authenticity, authorship, and authority into a single signature on a form.

A digital attestation should keep them apart.

- the **issuer** is the organisation whose key signs the record, identified by its NZBN or controller document, and authenticity is checked against that key;
- the **attestor** is the person inside the organisation who observed or decided something, named in the record with their role, and their identity is a claim the organisation makes and is accountable for;
- the **authority** is what entitles the attestor to make the statement, and it is a reference to another record or to a public register, not free text.

A relying organisation relies on the employer, not on a private individual, and that is why the organisation signs.

The authority reference is the useful design move.

The entitlement to attest is itself an OpenCompetency record: an employer's Authorisation designating a person as a workplace assessor for a scope, an assessor's own qualification, a professional register entry, or a director's listing on the Companies Register.

An attestation that references its attestor's authority can be checked to the same depth a relying organisation chooses to go, and no deeper.

What an attestation and an authorisation each carry is defined in sections 6.2 and 6.3 of the exchange model, and is not repeated here.

### 4.2 Who may attest

A director is publicly listed against the NZBN, directors already sign tender declarations, and a false declaration by a director has consequences the law understands.

An organisation-level declaration in OpenPrequal should therefore carry the declarant's name, their role as director or officer, and the register that lists them, and the NZBN authority credential the government is trialling would be the machine-verifiable form of the same thing.

Naming a person proves neither their role nor their approval, and section 5.6 of the exchange model says how each is evidenced and reported.

A director did not watch a worker operate a machine, and an attestation's value comes from proximity to the work.

Observed competency should be attested by the person who observed it, and requiring officer sign-off on such records would make them less informative rather than more.

An authorisation is an organisational act, so it should name the granting role, and a Requirement record may demand officer-level grant for high-risk work if the relying organisation wants that.

The standard should not fix the level; local acceptance does.

A Justice of the Peace witnessing a statutory declaration proves that the declarant signed and places them under the Oaths and Declarations Act 1957.

It says nothing about competency, and it does not scale to the volume of attestations a workplace produces.

Witnessing should not be built into the standard, and where a relying organisation requires a witnessed declaration it should be attached as hash-linked Evidence, as an insurance certificate is.

### 4.3 Self-declaration

Where issuer, attestor, and subject are the same party, as they are for a sole trader, the record is a self-declaration and should say so.

Its value comes from corroboration by other records, not from its signature.

### 4.4 Attestation is not assessment

An attestation is a first-hand statement by someone with direct knowledge.

An assessment is an opinion formed by reviewing evidence, and the architecture overview already keeps the two apart.

A record that mixes them, such as a supervisor's statement that also grades the worker against criteria, should be issued as an attestation with an alignment, not as an assessment.

### 4.5 Worked example

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

## 5. Trust

OpenCompetency separates:

1. whether the record is authentic;
2. whether the record is current;
3. whether the receiving organisation recognises the issuer;
4. whether the record meets the receiving organisation's requirements.

This means an employer can recognise one issuer for one purpose without recognising that issuer for all purposes.

## 6. Requirement Profiles

An organisation should be able to define its own competency requirements.

Example:

```text
Role:
Registered Electrical Worker

Requires:
- current practising licence
- recognised qualification
- current employer authorisation
- site induction where required
```

OpenCompetency should not define a universal answer to what makes someone a competent electrical worker.

It should provide a common way to express and test the receiving organisation's requirements.

The requirement record drafted in `docs/exchange-model/extensions.md` section 3 is the working draft of that common way, and is not proposed for v0.1.

## 7. Exchange Example

```text
Qualification provider
        |
        v
Signed qualification record
        |
        v
Employer competency system
        |
        | OpenCompetency
        v
Customer system
        |
        v
Customer applies its own
competency requirements
```

The employer can also issue its own practical competency or attestation records.

The customer can independently identify each original issuer.

The floor for that exchange is a signed file that any conforming system can export and import, as section 11 of the exchange model describes.

## 8. Small Organisations

A business without a competency database should be able to use a hosted OpenCompetency-compatible service.

That service should provide simple functions such as:

- add person;
- receive credential;
- issue attestation;
- issue authorisation;
- share selected records;
- export records;
- verify received records.

The organisation should be able to change service provider without invalidating existing credentials.

The exchange model makes that possible by identifying an issuer under its own domain name, which a hosted service serves on the organisation's behalf.


## 9. Privacy and Worker Information

OpenCompetency handles personal information and should be designed accordingly.

The profile should:

- keep worker assurance information private by default;
- support selective and purpose-specific presentation;
- identify the intended recipient and purpose of a presentation where practical;
- avoid disclosing unrelated competencies, qualifications, medical information, or employment information;
- avoid a universal OpenCompetency worker number;
- support scoped or privacy-preserving subject identifiers;
- provide practical access and correction mechanisms;
- support revocation, supersession, replacement, and linked correction statements;
- support proportionate retention;
- avoid uncontrolled onward sharing.

OpenCompetency should not require worker consent as the only possible basis for sharing. Employers and other organisations may have other lawful bases for collecting or disclosing assurance information. The participating organisation remains responsible for determining and documenting its legal basis.

A worker may hold many credentials while presenting only those required for a specific purpose.

```text
Worker assurance records
          |
          v
Purpose-specific presentation
          |
          v
Customer or verifier
```

## 10. Non-Goals

OpenCompetency is not intended to:

- define all occupations;
- establish universal competency levels;
- replace qualification authorities;
- accredit all assessors;
- run training courses;
- become a compulsory worker database;
- force workers to maintain a particular passport application.

## 11. Core Test

> **Can an employer provide valid competency evidence to a customer without both organisations being customers of the same competency platform?**

If yes, OpenCompetency is serving its purpose.
