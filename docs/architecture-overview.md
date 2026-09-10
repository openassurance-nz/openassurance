# OpenAssurance Architecture Overview

**Status:** First draft

## 1. Objective

OpenAssurance provides a common exchange model for workplace assurance information.

It separates:

- the subject of an assurance record;
- the issuer making an assertion;
- the holder storing or presenting the record;
- the host providing technical storage or services;
- the verifier checking authenticity;
- the relying organisation deciding whether the information is acceptable.

This separation is intended to prevent platform ownership from becoming part of the trust model.

## 2. Conceptual Architecture

```text
                         OPENASSURANCE
                         shared standard
                               |
             +-----------------+-----------------+
             |                                   |
             v                                   v
       OpenCompetency                       OpenPrequal
           people                           organisations
             |                                   |
             +-----------------+-----------------+
                               |
                               v
                        Assurance Records
                               |
          +--------------------+--------------------+
          |                    |                    |
          v                    v                    v
       Issuers              Holders              Verifiers
          |                    |                    |
          +--------------------+--------------------+
                               |
                               v
                       Local acceptance rules
```

## 3. Core Roles

### Subject

The person or organisation that an assurance record concerns.

Examples:

- a worker;
- a contractor;
- a supplier;
- an employer.

### Issuer

The party responsible for the assertion.

Examples:

- qualification authority;
- training provider;
- employer;
- assessor;
- supervisor;
- prequalification provider;
- insurer;
- industry body.

### Holder

A party legitimately storing or presenting a record.

The holder may be:

- the subject;
- an employer;
- a contractor;
- a hosted service;
- another authorised organisation.

Holding or presenting a record does not make the holder its issuer.

### Host

A technical service that stores or facilitates records.

Hosting is separate from trust.

A host may change without changing the underlying issuer or assurance record.

### Verifier

A system or person checking:

- issuer identity;
- signature;
- integrity;
- expiry;
- status;
- evidence references.

### Relying Organisation

The organisation deciding whether the assurance information is sufficient for its purpose.

## 4. Core Record Types

The initial OpenAssurance model is expected to include:

### Credential

A signed assertion of qualification, training, competency, assessment, status, or similar achievement.

### Attestation

A signed statement that a person or organisation observed, performed, maintained, or satisfied something.

### Evidence

Supporting information that may underpin an assertion or assessment.

### Assessment

An evaluation or opinion issued after reviewing evidence.

### Endorsement

A statement that one party recognises another issuer, assessor, record, or capability for a defined scope.

### Requirement

A statement of what a receiving organisation expects for a role, activity, supplier category, contract, or risk.

## 5. Trust Flow

OpenAssurance separates four questions:

```text
Incoming assurance record
          |
          v
Is the record authentic?
          |
          v
Is the record current?
          |
          v
Do we recognise the issuer?
          |
          v
Does it meet our requirement?
          |
          v
Local decision
```

The final decision is always local.

## 6. Exchange Model

The preferred model is direct standards-based exchange rather than a compulsory central hub.

```text
Organisation A system
        |
        | OpenAssurance
        v
Organisation B system
```

Where an organisation does not have its own system:

```text
Small organisation
        |
        v
Hosted compatible service
        |
        | OpenAssurance
        v
Receiving organisation
```

The hosted service is replaceable.

## 7. Portability

A valid assurance record should not become invalid because:

- the original host closes;
- the holder changes software;
- the subject changes employer;
- the receiving organisation changes platform.

Authenticity should derive from the issuer and the signed record, not from continued tenancy in a particular platform.

## 8. Multi-Hosting

The same signed record may be stored in more than one place:

```text
               Signed Record
                    |
        +-----------+-----------+
        |           |           |
        v           v           v
     Issuer      Employer     Recipient
     storage      storage      cache
```

The copies remain the same assertion.

## 9. Privacy

OpenAssurance should not create a public searchable database of worker or supplier assurance information by default.

The architecture should support selective presentation and sharing.

Public information may include:

- issuer identity;
- public verification information;
- public schemas;
- public endorsements where intended;
- status mechanisms.

Private information may include:

- worker records;
- underlying evidence;
- assessments;
- employment information;
- detailed supplier documentation.

## 10. Existing Standards

OpenAssurance should use established standards wherever practical for:

- verifiable credentials;
- digital signatures;
- credential status;
- presentation;
- identity;
- JSON schemas;
- interoperability.

OpenAssurance should focus on the workplace assurance profile and exchange rules that are not already adequately covered elsewhere.

## 11. Initial Technical Boundary

OpenAssurance v0.1 should aim to define:

- common assurance record semantics;
- minimum metadata;
- issuer provenance;
- requirement expression;
- recognition and endorsement scope;
- exchange expectations;
- import/export expectations;
- conformance rules.

It should avoid creating:

- a new blockchain;
- a new general-purpose wallet protocol;
- a new national identity system;
- a compulsory OpenAssurance registry.

## 12. Design Test

Any proposed architecture should pass this test:

> Can a record issued in one compatible environment be received and independently verified in another compatible environment without either party joining the other's platform?
