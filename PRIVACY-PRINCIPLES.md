# OpenAssurance Privacy Principles

**Status:** First draft

## 1. Purpose

OpenAssurance is intended to reduce unnecessary duplication of assurance information.

Where assurance information relates to an identifiable person, it is personal information and must be treated accordingly.

Privacy is therefore a core architectural requirement of OpenAssurance.

The project should seek to reduce unnecessary replication, retention, and disclosure of personal information while preserving the ability of organisations to exchange legitimate assurance evidence.

## 2. Privacy by Default

Personal assurance information should not be public by default.

A public issuer identity, schema, verification key, or status mechanism does not require the underlying worker record to be publicly discoverable.

## 3. Purpose-Bound Exchange

Personal assurance information should be exchanged for a defined assurance purpose.

A presentation should be capable of identifying:

- the intended recipient;
- the purpose;
- the assurance records or claims included;
- the issue time;
- an expiry or access period where appropriate.

Example:

```text
Purpose:
Verify eligibility to undertake mobile crane operations
for Contract ABC

Recipient:
Organisation X

Presented:
- crane qualification
- practical competency
- employer authorisation
```

## 4. Minimum Disclosure

Only the information reasonably required for the assurance purpose should be presented.

A request to verify one competency should not require disclosure of a worker's complete:

- qualification history;
- training history;
- competency history;
- employment record;
- medical information;
- unrelated licences or inductions.

## 5. Credential and Presentation Are Different

A credential or attestation may be long-lived.

A presentation is a purpose-specific sharing event.

```text
Credential
    |
    v
Holder
    |
    v
Presentation
    |
    v
Verifier
```

A holder may possess many credentials while presenting only the information required for a particular recipient and purpose.

## 6. No Universal Worker Identifier

OpenAssurance should not create a universal person identifier that enables unnecessary tracking across unrelated organisations.

Implementations should prefer, where practical:

- issuer-scoped identifiers;
- organisation-scoped identifiers;
- pairwise identifiers;
- privacy-preserving cryptographic identifiers.

Existing government, licence, tax, or qualification identifiers should not automatically become universal OpenAssurance person identifiers.

## 7. Issuer Provenance

Privacy controls must not obscure who made an assurance assertion.

A verifier should still be able to establish:

- who issued the record;
- what was asserted;
- when it was issued;
- whether it remains current.

The objective is minimum disclosure, not anonymous assurance.

## 8. Lawful Sharing

OpenAssurance should not assume that individual consent is the only lawful basis for sharing personal assurance information.

Employers, asset owners, training providers, and other organisations may collect, use, or disclose information under different lawful purposes and Privacy Act provisions.

Each participating organisation remains responsible for:

- identifying its lawful purpose;
- providing required privacy notices;
- determining whether disclosure is permitted;
- meeting any indirect collection obligations;
- maintaining appropriate records of its decision.

## 9. Access and Correction

Implementations should provide practical mechanisms that support a person's rights to access and seek correction of personal information.

Cryptographically signed records should not be silently edited after issue.

Where correction is required, the preferred mechanisms are:

- revocation;
- supersession;
- replacement;
- linked correction statement.

Example:

```text
Original credential
       |
       v
Superseded
       |
       v
Replacement credential
```

## 10. Retention

Receiving an assurance record does not justify indefinite retention.

Recipients should retain personal information only for as long as required for their lawful purpose and applicable legal obligations.

A credential may remain valid longer than a particular presentation or recipient's need to retain a copy.

## 11. Onward Sharing

Receiving a credential or presentation should not automatically grant an unrestricted right to redistribute the information.

Implementations should support controls or metadata that help recipients understand:

- the purpose for which information was shared;
- whether onward sharing is expected or restricted;
- when the presentation expires.

## 12. Security

Implementations handling personal information should apply appropriate security measures, including where relevant:

- encryption in transit;
- encryption at rest;
- access controls;
- secure signing-key management;
- authentication;
- audit logging;
- credential-status checking;
- revocation;
- incident response;
- backup and recovery controls.

Cryptographic authenticity does not remove the need for privacy and security controls around storage.

## 13. Hosted Services

A small organisation may use a hosted OpenAssurance-compatible service.

The use of a host does not remove the organisation's privacy responsibilities.

Hosting should remain separate from:

- ownership of the assurance record;
- issuer identity;
- acceptance decisions;
- legal accountability.

## 14. Overseas Hosting and Disclosure

OpenAssurance should not require New Zealand-only hosting.

Implementations should, however, make it possible for participating organisations to understand:

- where personal information is stored;
- which service providers process it;
- whether providers act only as agents;
- whether information may be disclosed overseas;
- what safeguards apply.

## 15. OpenPrequal

OpenPrequal should distinguish organisation information from personal information.

Where organisation-level evidence is sufficient, personal information should not be collected merely because a platform is capable of collecting it.

## 16. Privacy Impact Assessment

OpenAssurance should complete a formal Privacy Impact Assessment before the first stable specification is finalised.

The Privacy Impact Assessment should be updated when material changes are proposed to:

- identity;
- hosting;
- exchange;
- credential presentation;
- status;
- evidence handling;
- retention;
- third-party integrations.

## 17. Core Privacy Test

OpenAssurance should continue to ask:

> **Are we reducing the amount of personal information organisations need to duplicate and disclose, or are we creating another place to copy it?**

The design should favour the former.
