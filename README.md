# OpenAssurance

**Open assurance information that can move between organisations and systems.**

OpenAssurance is an open initiative to reduce duplication, platform lock-in, and repeated data entry in workplace assurance.

It is designed around a simple principle:

> **Assurance information should be portable, independently verifiable, and exchangeable without requiring every organisation to use the same software platform.**

OpenAssurance is not intended to replace competency-management, prequalification, contractor-management, training, or assurance platforms.

Those products can continue to compete on workflow, management, assessment, reporting, automation, and user experience.

The exchange layer should be open.

> **Compete on assurance management. Cooperate on assurance exchange.**

---

## The Problem

New Zealand organisations increasingly rely on digital systems to manage:

* worker qualifications;
* competency;
* training;
* licences;
* inductions;
* employer authorisations;
* contractor prequalification;
* health and safety assurance;
* insurance;
* organisational capability;
* supporting evidence.

These systems provide useful services, but assurance information is often trapped within the platform in which it was entered.

This creates duplication.

A contractor may already hold verified competency information for its workers but still need to recreate those workers and their records in a customer's required competency platform.

The same organisation may separately maintain similar prequalification information in:

* SiteWise;
* Tōtika;
* IMPAC PREQUAL;
* customer portals;
* procurement systems;
* internal systems.

The underlying information is often substantially the same.

Open data schemas alone do not solve this problem if organisations still need:

* an enterprise licence;
* membership of a specific platform;
* an account with the receiving platform;
* duplicate worker or company records;
* bilateral integrations between every software provider.

OpenAssurance exists to address that interoperability problem.

---

## The Goal

OpenAssurance aims to make this possible:

```text
Organisation A
    │
    │ OpenAssurance
    ▼
Organisation B
```

without requiring:

```text
Organisation A
    │
    ▼
Organisation B's software platform
    │
    ▼
Duplicate account
Duplicate records
Duplicate administration
```

A conforming assurance record should be capable of moving between different systems while preserving:

* who issued it;
* what was asserted;
* who or what it relates to;
* when it was issued;
* whether it remains current;
* supporting evidence where appropriate;
* cryptographic authenticity.

The receiving organisation remains responsible for deciding whether it accepts that information.

---

# Project Structure

OpenAssurance is the umbrella initiative.

The initial profiles are:

## OpenCompetency

**https://opencompetency.nz**

OpenCompetency covers assurance information about people, including:

* qualifications;
* licences;
* training;
* practical competency;
* assessments;
* employer attestations;
* experience;
* inductions;
* authorisations;
* competency evidence;
* issuer recognition.

Example:

```text
McLeod Cranes
      │
      │ issues / holds
      ▼
Worker competency records
      │
      │ OpenCompetency
      ▼
Customer's chosen system
```

The customer does not need to use the same competency-management platform as the employer.

---

## OpenPrequal

**https://openprequal.nz**

OpenPrequal covers assurance information about organisations, including:

* prequalification assessments;
* health and safety systems;
* risk-management capability;
* insurance;
* plant and equipment systems;
* training and competency systems;
* subcontractor management;
* incident management;
* worker engagement;
* organisational declarations;
* supporting evidence.

Example:

```text
Supplier
   │
   ├── SiteWise assessment
   ├── Tōtika assessment
   ├── Insurance
   ├── Policies
   └── Supporting evidence
            │
            │ OpenPrequal
            ▼
          Buyer
```

The aim is:

> **Assess once. Share anywhere.**

OpenPrequal does not require buyers to treat different assessment schemes as equivalent.

Each buyer remains free to determine what it requires and accepts.

---

# Core Principles

## 1. No Mandatory Platform

OpenAssurance compatibility must not require both parties to subscribe to the same commercial service.

A conforming sender should be able to provide assurance information to a conforming recipient regardless of which software either party uses.

---

## 2. No Mandatory Central Registry

OpenAssurance must not become a compulsory central database of workers or organisations.

No OpenAssurance-operated service should be required for a conforming assurance record to remain authentic.

---

## 3. Portable Records

Assurance records should remain portable between systems and hosting providers.

Changing software provider must not invalidate an assurance record.

---

## 4. Independent Verification

A recipient should be able to independently establish:

* who issued the record;
* whether it has been altered;
* whether it has expired;
* whether it has been revoked or suspended;
* what the issuer actually asserted.

Verification should not require a subscription to the platform that created the record.

---

## 5. Local Acceptance

OpenAssurance does not determine whether:

* a worker is competent;
* an organisation is suitable;
* an assessor is acceptable;
* a qualification is sufficient;
* a prequalification result meets a buyer's requirements.

Those decisions remain with the organisation relying on the information.

A preferred result is therefore:

> **Meets Organisation X requirements**

rather than:

> **Competent**

or:

> **Approved**

---

## 6. Issuer Provenance

The source of an assertion must remain visible.

Examples:

```text
NZQA / Training Provider
        │
        ▼
Qualification
```

```text
Employer
   │
   ▼
Practical competency
```

```text
Supervisor
   │
   ▼
Attestation
```

```text
Assessment Provider
        │
        ▼
Prequalification assessment
```

A system sharing a credential does not become its issuer.

---

## 7. Open Exchange

OpenAssurance should support organisation-to-organisation exchange.

For example:

```text
Pulse
  │
  │ OpenAssurance
  ▼
JNCTN
```

or:

```text
Risk3y
  │
  │ OpenAssurance
  ▼
SAP
```

or:

```text
Hosted OpenAssurance service
          │
          ▼
     Customer system
```

No bilateral proprietary integration should be required where both systems support the open protocol.

---

## 8. Small Organisations Must Be Able to Participate

OpenAssurance must not assume every organisation has:

* an HRIS;
* a competency database;
* an API;
* an IT department;
* specialist assurance software.

A small business should be able to use a hosted OpenAssurance-compatible service while participating in exactly the same exchange ecosystem as a large organisation with its own systems.

Hosting must remain separate from ownership of the assurance record.

---

## 9. Reuse Existing Standards

OpenAssurance should prefer established open standards rather than create new ones unnecessarily.

This includes alignment with:

* W3C Verifiable Credentials;
* established digital credential standards;
* New Zealand digital identity infrastructure;
* existing New Zealand credential schemas such as `credentialschema.nz`;
* recognised qualification and assessment systems.

OpenAssurance should define new schemas only where there is a genuine workplace assurance gap.

---

# What OpenAssurance Is Not

OpenAssurance is not intended to be:

* a national worker database;
* a compulsory competency passport;
* a prequalification provider;
* a training provider;
* an accreditation authority;
* an assessment company;
* a central issuer registry;
* a replacement for NZQA;
* a replacement for SiteWise;
* a replacement for Tōtika;
* a replacement for IMPAC PREQUAL;
* a replacement for JNCTN;
* a replacement for commercial assurance software.

Existing providers should be able to implement OpenAssurance while retaining their own products, workflows, commercial models, and intellectual property.

---

# The Trust Model

OpenAssurance separates four questions.

## Is the record authentic?

Did the claimed issuer actually issue it?

## Is it current?

Has it expired, been suspended, or been revoked?

## Do we recognise the issuer?

The receiving organisation decides whether it trusts that issuer for the relevant purpose.

## Does it meet our requirements?

The receiving organisation decides whether the evidence is sufficient for the work, role, contract, site, or risk involved.

This means trust can remain decentralised.

Example:

```text
McLeod Cranes
      │
      │ issues crane operator competency
      ▼
Worker
      │
      ▼
Client
      │
      └── "We recognise McLeod for this purpose."
```

An industry body may also endorse an issuer, but no OpenAssurance central authority is required to do so.

---

# Employer Attestations

OpenAssurance recognises that workplace competence is not represented only by formal qualifications.

An employer, supervisor, assessor, or other suitable person may need to attest that:

> Jim performed X.

Example:

```text
Subject:
Jim Smith

Assertion:
Operated Liebherr LTM 1230-5.1 under normal working conditions.

Period:
March 2025 - August 2026

Basis:
Direct supervision

Attestor:
Authorised company representative

Organisation:
Employer
```

The recipient remains responsible for deciding how much weight to give that attestation.

---

# Requirement Profiles

Organisations should be able to define what they require without OpenAssurance imposing a universal competency model.

Example:

```text
Mobile Crane Operator

Requires:

- recognised crane qualification
- practical competency
- current employer authorisation
- applicable driver licence
- site induction where required
```

Another company may legitimately define different requirements.

OpenAssurance provides a common way to describe and evaluate those requirements.

---

# Open Exchange Requirement

A core OpenAssurance conformance rule is:

> **A conforming assurance record must be capable of being exported, transmitted, received, and independently verified without requiring the issuer, subject, holder, sender, and verifier to subscribe to the same commercial platform.**

A platform cannot meaningfully claim OpenAssurance compatibility if receiving a conforming record requires the sending organisation to become a customer or tenant of that platform.

---

# Example - Competency

Today:

```text
Employer already manages Jim
        │
        ▼
Customer mandates Platform X
        │
        ▼
Employer joins Platform X
        │
        ▼
Jim recreated
        │
        ▼
Evidence recreated
        │
        ▼
Duplicate administration
```

OpenAssurance:

```text
Employer system
      │
      │ OpenCompetency
      ▼
Customer system
      │
      ▼
Customer applies its own requirements
```

---

# Example - Prequalification

Today:

```text
Company evidence
   ├── Prequal system A
   ├── Prequal system B
   ├── Buyer portal C
   └── Buyer questionnaire D
```

OpenAssurance:

```text
Company assurance information
            │
            ▼
    OpenPrequal exchange
            │
       ┌────┼────┐
       ▼    ▼    ▼
     Buyer Buyer Buyer
       A    B    C
```

The evidence can be reused while each buyer retains control over its acceptance criteria.

---

# Initial Scope

The first OpenAssurance specification is expected to focus on:

### Common

* organisation identity;
* issuer identity;
* assurance record structure;
* evidence references;
* signatures;
* status;
* expiry;
* revocation;
* presentation;
* export and import;
* open exchange;
* recipient requirements;
* issuer recognition.

### OpenCompetency

* qualification;
* licence;
* training;
* assessment;
* practical competency;
* employer attestation;
* authorisation;
* induction;
* experience.

### OpenPrequal

* organisation assurance profile;
* prequalification assessment;
* insurance;
* declarations;
* assurance evidence;
* assessment-provider credentials;
* buyer requirement profiles.

---

# Non-Goals for v0.1

The initial project will not attempt to build:

* learning-management software;
* contractor-management software;
* workforce scheduling;
* payroll;
* recruitment;
* site access control;
* a universal occupational taxonomy;
* a universal competency score;
* a central worker database;
* a central supplier database;
* blockchain infrastructure.

These functions may exist in products that implement OpenAssurance.

---

# Governance

OpenAssurance intends to operate as an open, vendor-neutral initiative.

The project should govern:

* technical specifications;
* schemas;
* interoperability requirements;
* conformance tests;
* versioning;
* shared technical vocabulary.

The project should not govern:

* who is competent;
* who is an acceptable contractor;
* which commercial platform must be used;
* which assessment provider must be used;
* which organisation another business must trust.

Proposed changes should be developed openly through this repository.

---

# Repository Direction

The expected repository structure is:

```text
openassurance/
│
├── README.md
├── CHARTER.md
├── GOVERNANCE.md
├── CONTRIBUTING.md
│
├── docs/
│
├── specification/
│
├── profiles/
│   ├── competency/
│   └── prequal/
│
├── schemas/
│
└── examples/
```

Separate repositories may later contain:

* reference implementations;
* verifier tools;
* conformance tests;
* hosted services;
* websites.

The specification should remain independent from any reference implementation.

---

# Status

OpenAssurance is currently an early-stage New Zealand open standards initiative.

The immediate priorities are:

1. define the problem clearly;
2. validate the need with suppliers, buyers, regulators, industry bodies, and existing platform providers;
3. map existing New Zealand and international standards;
4. define the minimum open exchange protocol;
5. build small reference examples;
6. establish appropriate industry governance.

The project should be shaped with industry rather than presenting a completed solution before the problem and approach have been tested.

---

# Domains

* **OpenAssurance:** https://openassurance.nz
* **OpenCompetency:** https://opencompetency.nz
* **OpenPrequal:** https://openprequal.nz

---

# Core Proposition

> **OpenAssurance exists to prevent assurance information from becoming captive to a single platform.**

> **Define locally. Issue anywhere. Share anywhere. Verify anywhere.**

