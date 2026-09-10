# OpenAssurance

**Open assurance information that can move between organisations and systems.**

OpenAssurance is an open initiative to reduce duplication, platform lock-in, and repeated data entry in workplace assurance.

It is based on a simple principle:

> **Assurance information should be portable, independently verifiable, and exchangeable without requiring every organisation to use the same software platform.**

OpenAssurance is not intended to replace competency management, prequalification, contractor management, training, assessment, or assurance platforms.

Those products and services can continue to compete on workflow, management, assessment, reporting, automation, and user experience.

The exchange layer should be open.

> **Compete on assurance management. Cooperate on assurance exchange.**

## The Problem

New Zealand organisations increasingly rely on digital systems to manage:

- worker qualifications;
- competency;
- training;
- licences;
- inductions;
- employer authorisations;
- contractor prequalification;
- health and safety assurance;
- insurance;
- organisational capability;
- supporting evidence.

These systems provide useful services, but assurance information is often confined to the platform in which it was entered.

This creates duplication.

A contractor may already hold verified competency information for its workers but still be required to recreate those workers and their records in a customer's nominated system.

An organisation may also be required to provide substantially the same prequalification and assurance information repeatedly to:

- assessment providers;
- customers;
- principal contractors;
- procurement systems;
- contractor portals;
- tender processes.

The underlying information is often substantially the same.

Open data schemas alone do not solve this problem if organisations still require:

- an enterprise licence;
- membership of a specific platform;
- an account with the receiving platform;
- duplicate worker or company records;
- bilateral integrations between software providers.

OpenAssurance exists to address that interoperability problem.

## The Goal

OpenAssurance aims to make this possible:

```text
Organisation A
      |
      | OpenAssurance
      v
Organisation B
```

regardless of which systems either organisation uses.

A conforming assurance record should be capable of moving between different systems while preserving:

- who issued it;
- what was asserted;
- who or what it relates to;
- when it was issued;
- whether it remains current;
- supporting evidence where appropriate;
- cryptographic authenticity.

The receiving organisation remains responsible for deciding whether it accepts that information.

For personal assurance information, OpenAssurance should support purpose-specific presentation rather than unnecessary disclosure of a person's complete record.

## Project Structure

OpenAssurance is the umbrella initiative.

Its initial profiles are:

### OpenCompetency

OpenCompetency covers assurance information about people, including qualifications, licences, training, practical competency, assessments, employer attestations, experience, inductions, authorisations, competency evidence, and issuer recognition.

The receiving organisation does not need to use the same competency-management system as the employer or issuer.

Website: https://opencompetency.nz

### OpenPrequal

OpenPrequal covers assurance information about organisations, including prequalification assessments, health and safety systems, risk-management capability, insurance, plant and equipment systems, competency systems, subcontractor management, incident management, worker engagement, declarations, and supporting evidence.

The aim is:

> **Assess once. Share anywhere.**

OpenPrequal does not require buyers to treat different assessment schemes as equivalent. Each buyer remains free to determine what it requires and accepts.

Website: https://openprequal.nz

## Core Principles

1. **No mandatory platform** - OpenAssurance compatibility must not require both parties to subscribe to the same commercial service.
2. **No mandatory central registry** - OpenAssurance must not become a compulsory central database of workers or organisations.
3. **Portable records** - Changing software provider must not invalidate an assurance record.
4. **Independent verification** - Verification should not require a subscription to the platform that created the record.
5. **Local acceptance** - The receiving organisation decides what evidence and issuers it accepts.
6. **Issuer provenance** - A system sharing a credential does not become its issuer.
7. **Open exchange** - Conforming systems should exchange assurance records without bilateral proprietary integrations.
8. **Small organisations can participate** - A business should not need specialist software or its own database to use the standard.
9. **Reuse existing standards first** - OpenAssurance should align with established international and New Zealand standards wherever practical.
10. **Privacy by design** - Personal assurance information should be private by default, purpose-bound, and limited to the minimum information required.
11. **No universal worker identifier** - OpenAssurance should avoid identifiers that enable unnecessary tracking of individuals across organisations.

## What OpenAssurance Is Not

OpenAssurance is not intended to be:

- a national worker database;
- a compulsory competency passport;
- a prequalification provider;
- a training provider;
- an accreditation authority;
- an assessment company;
- a central issuer registry;
- a replacement for qualification authorities;
- a replacement for existing assessment schemes;
- a replacement for competency-management platforms;
- a replacement for commercial assurance software.

Existing providers should be able to implement OpenAssurance while retaining their own products, workflows, commercial models, and intellectual property.

## Open Exchange Requirement

A core OpenAssurance conformance rule is:

> **A conforming assurance record must be capable of being exported, transmitted, received, and independently verified without requiring the issuer, subject, holder, sender, and verifier to subscribe to the same commercial platform.**

A platform cannot meaningfully claim OpenAssurance compatibility if receiving a conforming record requires the sending organisation to become a customer or tenant of that platform.

## Status

OpenAssurance is currently an early-stage New Zealand open standards initiative.

The immediate priorities are:

1. define the problem clearly;
2. validate the need with suppliers, buyers, regulators, industry bodies, and existing service providers;
3. map existing New Zealand and international standards;
4. define the minimum open exchange protocol;
5. build small reference examples;
6. establish appropriate industry governance;
7. complete a Privacy Impact Assessment before the first stable specification is finalised.

## Domains

- OpenAssurance: https://openassurance.nz
- OpenCompetency: https://opencompetency.nz
- OpenPrequal: https://openprequal.nz

## Core Proposition

> **OpenAssurance exists to prevent assurance information from becoming captive to a single platform.**

> **Define locally. Issue anywhere. Share anywhere. Verify anywhere.**
