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

Organisation:
Employer
```

The attestation records who made the assertion and why.

It does not force another organisation to accept that assertion.

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
