# OpenAssurance Charter

**Status:** First draft

## 1. Purpose

OpenAssurance exists to prevent workplace assurance information from becoming captive to a single software platform.

Organisations increasingly depend on digital systems to manage worker competency, qualifications, contractor prequalification, organisational assurance, and supporting evidence. These systems provide value, but the exchange of assurance information is often tied to platform membership, licensing, tenancy, or proprietary integrations.

Open schemas alone are not sufficient if organisations still need to buy access to a particular platform or duplicate records into that platform before information can be shared.

OpenAssurance seeks to establish an open, vendor-neutral exchange layer for workplace assurance.

## 2. Mission

OpenAssurance aims to make assurance records portable, independently verifiable, reusable, and exchangeable between organisations regardless of which software, service provider, or hosting arrangement each party uses.

A holder should be able to meet a new request with assurance it already holds, and should not have to recreate it because another organisation uses another system.

The project will focus on interoperability.

It will not determine who is competent, which contractor is acceptable, or which issuer another organisation must trust.

## 3. Founding Principles

### 3.1 No mandatory platform

No conforming OpenAssurance exchange should require all participants to subscribe to the same commercial platform.

### 3.2 No mandatory central registry

OpenAssurance must not become a compulsory central database of people, organisations, issuers, or assurance records.

A conforming record should not depend on OpenAssurance.nz remaining available in order to establish the authenticity of the original assertion.

### 3.3 Portability

Assurance records should remain portable between compatible systems and service providers.

A change of software or host should not invalidate an assurance record.

### 3.4 Reuse before recreation

OpenAssurance exchanges assurance records, not completed forms.

A relying organisation states what it needs demonstrated.

Where a holder already possesses assurance records relevant to those requirements, those records should be capable of being presented directly, without recreating their contents as answers in the relying organisation's system.

The relying organisation assesses whether they are sufficient.

Additional information should be requested only where existing assurance is insufficient, no longer current, or does not cover the applicable requirement or scope.

Any new assurance record created to address a genuine gap should remain reusable for later assurance requests.

Forms may be used by software as an interface for creating, reviewing, or collecting records, but forms are not the interoperability model.

A new relying organisation should not reset a holder to zero.

### 3.5 Independent verification

A recipient should be able to establish who issued a record, whether it has been altered, and whether it remains current without needing a subscription to the original issuing platform.

### 3.6 Local acceptance

The organisation relying on information decides:

- which issuers it recognises;
- which evidence it accepts;
- what requirements apply;
- whether a person or organisation meets those requirements.

OpenAssurance provides information and verification mechanisms. It does not make the final acceptance decision.

### 3.7 Issuer provenance

The original source of an assertion must remain clear.

A system that stores, forwards, or presents a credential does not become the issuer of that credential.

### 3.8 Open participation

Organisations of different sizes should be able to participate.

A small business should be able to use a hosted OpenAssurance-compatible service, while a larger organisation may implement the protocol directly in its own systems.

Both should participate in the same exchange ecosystem.

### 3.9 Open exchange

A conforming sender should be able to provide a conforming assurance record to a conforming recipient without first becoming a tenant or customer of the recipient's platform provider.

### 3.10 Reuse existing standards first

OpenAssurance should prefer established open standards where they can represent the required information without loss of meaning.

The project should avoid creating new identity, credential, signature, wallet, or status mechanisms where suitable standards already exist.

### 3.11 Vendor neutrality

Commercial services are expected and encouraged to compete on:

- user experience;
- assessment;
- workflow;
- reporting;
- automation;
- compliance management;
- contractor management;
- competency management;
- integrations;
- analytics.

The exchange layer should remain open.

> **Compete on assurance management. Cooperate on assurance exchange.**

### 3.12 Privacy by design

OpenAssurance should reduce unnecessary replication of personal information.

Personal assurance information should be private by default and exchanged only where there is a defined purpose, an appropriate basis for sharing, and a legitimate recipient.

### 3.13 Minimum disclosure

OpenAssurance should support presentation of only the information required for a particular assurance purpose.

A request to verify one competency should not require disclosure of a person's complete competency, employment, training, or qualification history.

### 3.14 Purpose-bound exchange

Where personal information is exchanged, the presentation should be capable of identifying:

- the intended recipient;
- the purpose of the exchange;
- the records or claims being presented;
- any appropriate expiry or access limitation.

### 3.15 No universal person identifier

OpenAssurance should not create a universal worker identifier that enables unnecessary tracking of an individual across unrelated organisations and systems.

Implementations should support scoped, pairwise, issuer-specific, or otherwise privacy-preserving identifiers where practical.

### 3.16 Access, correction, and supersession

Implementations should support appropriate access and correction processes.

Where signed assurance records require correction, implementations should preserve cryptographic integrity by supporting revocation, supersession, replacement, or linked correction statements rather than silently altering previously issued records.

### 3.17 Limited retention and onward sharing

Receiving an assurance record does not create an unrestricted right to retain or redistribute personal information indefinitely.

Implementations should support proportionate retention and controls on onward sharing consistent with the purpose for which information was received.

## 4. Initial Profiles

### OpenCompetency

OpenCompetency applies OpenAssurance principles to people and workplace competency, including qualifications, licences, training, assessments, practical competency, employer attestations, experience, inductions, and authorisations.

### OpenPrequal

OpenPrequal applies OpenAssurance principles to organisations and prequalification, including organisational assurance evidence, health and safety systems, insurance, assessments, declarations, and buyer requirements.

## 5. What OpenAssurance Will Govern

OpenAssurance may define and maintain:

- technical specifications;
- assurance record profiles;
- schemas;
- exchange conventions;
- interoperability requirements;
- conformance tests;
- versioning;
- shared technical vocabulary;
- reference examples;
- open-source reference implementations.

## 6. What OpenAssurance Will Not Govern

OpenAssurance should not become responsible for:

- deciding who is competent;
- deciding which business is safe or suitable;
- accrediting all issuers;
- approving all assessors;
- requiring use of a particular assessment scheme;
- requiring use of a particular software product;
- maintaining a compulsory worker or supplier register;
- setting universal role requirements.

These decisions remain with regulators, qualification authorities, industry bodies, employers, PCBUs, asset owners, buyers, assessment providers, and other organisations with the relevant responsibility.

## 7. Open Exchange Requirement

The following principles are foundational:

> **A conforming assurance record must be capable of being exported, transmitted, received, and independently verified without requiring the issuer, subject, holder, sender, and verifier to subscribe to the same commercial platform.**

> **A holder must be able to meet a request with conforming records it already holds, without recreating their contents in the relying organisation's system, and a relying organisation must be able to ask only for what those records do not demonstrate.**

An implementation should not claim OpenAssurance compatibility where interoperability exists only between customers of its own service.

An implementation that accepts conforming records, and still requires what they say to be completed again in a questionnaire of its own, should not claim to support OpenAssurance requests.

## 8. Development Approach

OpenAssurance should be developed openly.

Proposals should be testable against real workplace use cases and should prefer the smallest practical standard that solves the interoperability problem.

The project should seek participation from:

- employers;
- workers;
- buyers;
- suppliers;
- regulators;
- qualification organisations;
- industry bodies;
- assessment providers;
- technology providers;
- small businesses;
- large organisations.

## 9. Long-Term Test

OpenAssurance should continue to satisfy these questions:

> **Can two organisations exchange and verify assurance information even when neither organisation is a customer of the other's software provider?**

> **Can a holder satisfy a new assurance request using assurance it already holds, without recreating substantially the same information in another system?**

> **Where existing assurance is insufficient, does the exchange allow the relying organisation to ask only for the additional assurance needed to address the genuine gap?**

The first is necessary and is not enough, because a system could exchange conforming records and still make a supplier enter everything again in a new questionnaire.

If any answer becomes no, the project has departed from its founding purpose.
