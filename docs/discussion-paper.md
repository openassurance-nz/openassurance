# OpenAssurance

## Reducing duplication and platform dependency in New Zealand workplace assurance

**Discussion Paper - Draft v0.1**  
**September 2026**

**OpenAssurance.nz**

---

## Executive Summary

New Zealand businesses increasingly exchange workplace assurance information through digital platforms.

This includes:

- worker qualifications;
- competency and training;
- licences and authorisations;
- contractor prequalification;
- insurance;
- health and safety systems;
- organisational capability;
- supporting evidence.

These systems provide valuable management, assessment, reporting, and verification services.

However, the way assurance information is exchanged can create significant duplication.

A contractor may already hold verified competency information for its workers but still need to recreate those workers and their records inside a customer's nominated system.

A supplier may maintain substantially the same organisational assurance information across several prequalification schemes, procurement systems, customer portals, and tender processes.

The underlying issue is not necessarily the quality of those systems.

It is that **the exchange of assurance information is often coupled to the platform used to manage it**.

OpenAssurance proposes a different approach:

> **Assurance information should be capable of moving between organisations and systems without requiring every participant to use the same software platform.**

The proposal is not to create another compulsory national database or another assurance platform.

It is to explore an **open, vendor-neutral exchange standard** that existing and future systems could support.

OpenAssurance would initially consider two related areas:

- **OpenCompetency** - assurance records concerning people, qualifications, competency, training, attestations, inductions, and authorisations.
- **OpenPrequal** - assurance records concerning organisations, prequalification, insurance, organisational systems, assessments, declarations, and supporting evidence.

The central proposition is:

> **Compete on assurance management. Cooperate on assurance exchange.**

This paper is intended to start a discussion about whether the problem has been correctly identified and whether an open exchange approach could reduce unnecessary duplication while retaining organisational responsibility, privacy, and choice.

---

## 1. The Issue

New Zealand organisations need reliable assurance information.

A business engaging a contractor needs confidence that the contractor can manage the risks associated with the work.

An asset owner may need confidence that individual workers have the qualifications, training, competency, and authorisations required for particular activities.

These are legitimate requirements.

The question is whether obtaining that assurance should require the same information to be repeatedly recreated in different systems.

### 1.1 Worker competency

Consider a contractor that already maintains verified information about a worker, including:

- formal qualifications;
- licences;
- practical assessments;
- experience;
- employer competency;
- inductions;
- internal authorisations.

A customer may then require that worker to be established inside another competency-management platform.

The contractor may be required to:

1. create another worker record;
2. enter the same identifying information;
3. upload the same qualifications;
4. reproduce competency records;
5. maintain expiry dates in both systems;
6. keep both systems current.

The result can be:

```text
Employer competency system
          |
          v
Customer requires another platform
          |
          v
Worker recreated
          |
          v
Evidence recreated
          |
          v
Two records now require maintenance
```

The additional administration does not necessarily create additional evidence of competency.

It may simply create another copy of the same evidence.

---

## 2. The Same Problem Exists in Prequalification

The problem is also visible at organisation level.

Contractors and suppliers may repeatedly provide similar information through:

- prequalification assessment schemes;
- contractor-management platforms;
- procurement systems;
- customer portals;
- tender questionnaires;
- direct customer assessments.

Typical information includes:

- health and safety policies;
- risk-management systems;
- worker engagement;
- competency-management processes;
- plant and equipment management;
- incident-management processes;
- subcontractor management;
- insurance;
- previous performance;
- supporting evidence.

On 20 August 2026 the Minister for Workplace Relations and Safety announced action on inconsistency and duplication in prequalification, citing one submitter who reported completing **76 prequalifications in a year**.[^1] WorkSafe has since released both a position statement and a common prequalification template intended to support a more consistent, risk-based approach.[^1]

This is an important step.

A common questionnaire can help organisations **ask more consistent questions**.

The next question is whether technology can help avoid asking for information again when valid, current information already exists and can be independently verified.

---

## 3. Management, Assessment and Exchange Are Different Things

A useful distinction is between three activities.

### Management

A software system may help an organisation:

- maintain worker competencies;
- track expiries;
- manage contractor records;
- configure requirements;
- run workflows;
- generate reports;
- automate reminders.

These are valuable product capabilities.

### Assessment

An assessment provider may examine evidence and issue an assessment, score, category, or other conclusion.

That assessment is the provider's professional or commercial output.

### Exchange

Exchange is simply the ability to move the resulting assurance information from one legitimate party to another.

OpenAssurance proposes that:

> **Management and assessment can remain differentiated and commercial. Exchange should be interoperable.**

A supplier should not necessarily need to adopt the buyer's management software in order to provide valid assurance information.

---

## 4. Open Does Not Only Mean an Open Schema

New Zealand already has openly published credential schemas, including for qualifications, licences, courses, assessments, and inductions, expressed using the W3C Verifiable Credentials data model.

This is useful infrastructure, and OpenAssurance should build on it rather than duplicate it.

However, an open data structure alone does not necessarily create open exchange.

A schema can be published openly while the operational pathway for issuing, sending, receiving, or verifying the information still requires:

- platform membership;
- enterprise licensing;
- tenant setup;
- proprietary integrations;
- duplicate records.

The distinction that matters is between a schema being readable and the exchange being usable. A specification anyone may read, implemented through tooling only licensees may use, leaves the interoperability problem where it was.

OpenAssurance therefore proposes a stronger interoperability test:

> **Can Organisation A send a valid assurance record to Organisation B when neither organisation is a customer of the other's software provider?**

If the answer is no, the information may use an open schema, but the exchange remains platform-dependent.

---

## 5. The Proposed Model

OpenAssurance would not be a central database.

Instead, it would define how assurance records can be issued, stored, shared, received, and independently verified.

The model could look like:

```text
Organisation A
      |
      | OpenAssurance
      v
Organisation B
```

Organisation A might use:

- its own internal system;
- a commercial assurance platform;
- a hosted OpenAssurance-compatible service;
- a simple service intended for small businesses.

Organisation B might use something entirely different.

The systems would not need a bespoke bilateral integration if both supported the same open exchange standard.

---

## 6. OpenCompetency

OpenCompetency would apply the OpenAssurance model to people.

Potential record types include:

- qualifications;
- licences;
- training;
- courses;
- assessments;
- practical competency;
- experience;
- inductions;
- employer authorisations;
- employer or supervisor attestations.

### 6.1 The issuer remains visible

Different records have different sources.

For example:

```text
Qualification provider
        |
        v
Formal qualification
```

```text
Employer
   |
   v
Practical competency
```

```text
Supervisor
   |
   v
Experience attestation
```

The fact that an employer shares a qualification does not make the employer the qualification issuer.

The original provenance remains intact.

### 6.2 Workplace attestations matter

Competency is not represented only by qualifications.

In real workplaces an employer, supervisor, assessor, or business owner may legitimately attest that a worker has:

- performed a task;
- accumulated experience;
- demonstrated practical ability;
- operated particular equipment;
- worked under supervision;
- satisfied an internal authorisation process.

OpenCompetency should be capable of representing these assertions clearly, including:

- who made the assertion;
- their organisation;
- what was asserted;
- the basis for the assertion;
- when it applied;
- any supporting evidence.

Another organisation remains free to decide whether that attestation is sufficient.

---

## 7. Trust Should Remain Local

OpenAssurance should not establish a central authority that decides which businesses or issuers everyone must trust.

Instead, each relying organisation determines:

- which issuers it recognises;
- which assessors it accepts;
- what evidence it requires;
- whether an endorsement is sufficient;
- whether a credential meets its requirements.

For example:

```text
Credential received
       |
       v
Is it authentic?
       |
       v
Is it current?
       |
       v
Do we recognise the issuer?
       |
       v
Does it satisfy our requirement?
       |
       v
Local decision
```

The preferred conclusion is therefore:

> **Meets Organisation X requirements**

rather than a universal statement such as:

> **Competent**

The organisation responsible for accepting the worker retains that decision.

---

## 8. OpenPrequal

OpenPrequal would apply the same principles to organisations.

The subject becomes the supplier or contractor rather than an individual worker.

Potential assurance records could include:

- prequalification assessment results;
- insurance;
- declarations;
- organisational systems;
- health and safety processes;
- risk-management evidence;
- competency-management evidence;
- incident-management evidence;
- plant-management evidence.

### 8.1 Evidence and assessment should remain separate

A supplier may hold underlying evidence such as:

```text
Supplier assurance evidence
        |
        +-- policies
        +-- procedures
        +-- insurance
        +-- risk-management information
        +-- competency systems
        +-- incident information
```

Different assessment providers could evaluate that evidence.

```text
                Supplier evidence
                      |
          +-----------+-----------+
          |                       |
          v                       v
   Assessment Provider A   Assessment Provider B
          |                       |
          v                       v
      Assessment A            Assessment B
```

Each provider retains ownership of its own assessment methodology and result.

OpenAssurance simply allows the resulting records and permitted evidence to move between organisations.

---

## 9. Assess Once, Share Anywhere Does Not Mean Accept Everything

A concern with portability may be that it forces buyers to accept assurance they consider inadequate.

That is not the proposal.

A buyer may decide:

- which prequalification schemes it accepts;
- the required insurance limits;
- what evidence must be current;
- which additional information is required for high-risk work;
- whether direct assessment is necessary.

WorkSafe guidance states that the level of detail required for prequalification should be appropriate to the type of project, taking its size and complexity into account.[^5]

OpenPrequal therefore means:

> **Do not recreate information unnecessarily.**

It does not mean:

> **Every organisation must accept the same result.**

---

## 10. Small Businesses Must Be Able to Participate

An open standard cannot assume every contractor has:

- specialist assurance software;
- an internal database;
- an API;
- an IT department.

A small business should be able to use a hosted OpenAssurance-compatible service.

For example:

```text
Small contractor
       |
       v
Chosen hosted provider
       |
       | OpenAssurance
       v
Customer
```

The important distinction is that the hosted provider is **replaceable**.

The organisation should be able to move to another provider without recreating all of its assurance information.

This is similar to other open communications systems: organisations can choose a service provider without that provider owning the underlying communication standard.

---

## 11. Privacy

Portability must not become uncontrolled distribution of personal information.

OpenAssurance should be designed to reduce unnecessary privacy exposure.

The existing duplication model may create:

```text
Worker information
    |
    +--> System A
    +--> System B
    +--> System C
    +--> Customer portal D
    +--> Industry platform E
```

Each additional copy creates another location requiring:

- access control;
- security;
- correction;
- retention;
- breach management;
- ongoing maintenance.

OpenAssurance should instead support **purpose-specific presentation**.

```text
Verified assurance records
          |
          v
Selected information
for defined purpose
          |
          v
Defined recipient
```

A customer needing evidence that a worker satisfies one role should not automatically receive the worker's complete competency and employment history.

Personal information should be private by default, selectively disclosed, and handled consistently with the Privacy Act 2020.

OpenAssurance should also avoid creating a universal worker identifier that unnecessarily enables individuals to be tracked across unrelated organisations.

A formal Privacy Impact Assessment should form part of the development of any stable specification.

---

## 12. We Should Reuse Existing Infrastructure

OpenAssurance should not create new technology where suitable standards already exist.

New Zealand and international infrastructure now includes:

- W3C Verifiable Credentials;
- established digital credential schemas;
- digital signature mechanisms;
- credential status and revocation models;
- digital presentation protocols;
- New Zealand digital identity infrastructure.

New Zealand's government digital credential ecosystem already demonstrates cryptographic verification of issuer authenticity and secure credential presentation.

The NZ Verify app checks a credential's digital signature against the issuing authority's public key, confirming it is genuine and unaltered, and separately checks validity and acceptability for a stated purpose.[^2] That three-part separation closely resembles the trust flow described in section 7.

Version 2.0 of the Govt.nz app, released on 31 March 2026, introduced a digital wallet, with accredited digital credentials becoming available progressively from late August 2026.[^3]

OpenAssurance should build on this work rather than duplicate it.

Its likely contribution is the **workplace assurance profile and open exchange conventions** connecting existing systems.

---

## 13. What OpenAssurance Is Not

OpenAssurance is not proposed as:

- another mandatory competency platform;
- another prequalification provider;
- a national worker database;
- a national contractor database;
- a compulsory worker passport;
- a training provider;
- an assessment provider;
- a universal competency authority;
- a central list of approved companies;
- a replacement for existing assurance products.

Existing products should be able to support OpenAssurance without abandoning their existing commercial models.

They could continue to provide:

- assessment;
- workflow;
- dashboards;
- expiry management;
- contractor management;
- training management;
- access control;
- reporting;
- analytics;
- integrations.

The difference is that the underlying assurance record could move.

---

## 14. Why This Matters for Health and Safety

The objective is not simply to reduce administration.

Duplicated assurance processes can draw resources toward maintaining systems rather than understanding and controlling actual risks.

They can also create uncertainty about:

- which copy of a record is current;
- whether expired information has been updated everywhere;
- who originally made an assertion;
- whether the evidence has changed;
- whether administrative status accurately reflects real capability.

New Zealand's health and safety framework also requires PCBUs with overlapping duties to consult, cooperate, and coordinate so far as is reasonably practicable.[^6]

Better assurance exchange should support that relationship, not replace it with a platform-generated green tick.

---

## 15. Why This May Need Collective Action

This problem is difficult for any one contractor, buyer, or software provider to solve alone.

A contractor can complain about duplicated systems, but cannot dictate what customers use.

A buyer can simplify its own process, but cannot remove duplication created elsewhere in the supply chain.

A software company can provide an API, but bilateral integrations between every product do not scale.

An open standard only becomes useful when multiple parties agree on the exchange boundary.

Bodies with an established supply-chain leadership focus already exist. The Business Leaders' Health and Safety Forum, for example, represents more than 440 CEOs, Managing Directors, and Country Heads of New Zealand organisations.[^4]

No organisation named in this paper has been consulted about OpenAssurance or has endorsed it. They are cited as evidence that the problem is recognised, not as supporters of this proposal.

OpenAssurance may therefore be better developed as an industry conversation than as a product developed by one organisation.

---

## 16. Proposed Founding Principles

The following principles are offered for discussion.

They summarise the principles set out in the project Charter, which remains the authoritative statement and expands several of them further.

1. **No mandatory platform**  
   Organisations should not need to subscribe to the same service to exchange a conforming assurance record.

2. **No mandatory central registry**  
   OpenAssurance should not become another central database.

3. **Portable records**  
   Changing software or hosting provider should not invalidate assurance information.

4. **Independent verification**  
   A recipient should be able to verify who issued a record and whether it remains current.

5. **Local acceptance**  
   The receiving organisation decides what it requires and accepts.

6. **Issuer provenance**  
   The original issuer remains identifiable when a record is shared by another party.

7. **Open exchange**  
   Conforming systems should exchange assurance records without bilateral proprietary integrations.

8. **Privacy by design**  
   Personal information should be purpose-bound and limited to what is necessary.

9. **No universal worker identifier**  
   Identifiers should not enable unnecessary tracking of individuals across unrelated organisations.

10. **Small organisations can participate**  
    Organisations should not need specialist IT infrastructure to use the standard.

11. **Reuse existing standards first**  
    Existing open standards should be preferred over creating new technical mechanisms.

12. **Vendor neutrality**  
    Commercial providers remain free to compete on services around the open exchange layer.

---

## 17. Questions for Industry

OpenAssurance is currently a proposal, not a completed standard.

The first stage should therefore test the problem and assumptions.

We would particularly value discussion around the following questions:

### The problem

- How much assurance information is currently duplicated across New Zealand organisations and systems?
- Where does duplication create the greatest cost or operational delay?
- Are competency and prequalification the right first use cases?

### Trust

- Who should be able to issue workplace attestations?
- How should organisations express which issuers they recognise?
- When should industry endorsement supplement direct organisational recognition?

### Exchange

- What is the minimum information that needs to move between systems?
- What should remain with the original issuer?
- What should be independently verifiable without platform membership?

### Privacy

- How can assurance information be exchanged while reducing unnecessary replication of personal information?
- What should be held long-term and what should only be presented temporarily?

### Existing providers

- How can existing competency, prequalification, assessment, and assurance platforms participate without losing the value of their own products?
- What would make OpenAssurance commercially practical to implement?

### Governance

- Who should steward an open New Zealand assurance standard?
- What governance model would retain industry confidence while preventing any single provider from controlling the exchange layer?

---

## 18. Proposed Next Steps

A possible development path is:

### Phase 1 - Validate the problem

Engage contractors, buyers, asset owners, regulators, industry organisations, assessment providers, and technology providers.

Quantify duplication where possible.

### Phase 2 - Map existing standards

Identify what already exists and should be adopted rather than recreated.

### Phase 3 - Define the minimum exchange model

Create a small OpenAssurance v0.1 specification covering only what is required for interoperability.

### Phase 4 - Demonstrate two reference exchanges

One OpenCompetency example.

One OpenPrequal example.

The objective should be to demonstrate that information created in one environment can be independently received and verified in another.

### Phase 5 - Develop conformance tests

Define what a system must support before it can claim OpenAssurance compatibility.

### Phase 6 - Establish longer-term governance

Determine the appropriate independent stewardship model based on industry participation and experience.

---

## 19. The Proposition

OpenAssurance starts with a simple question:

> **Why should valid assurance information have to be recreated simply because two organisations use different software?**

The objective is not to standardise every organisation's safety requirements.

It is not to require every organisation to trust the same providers.

It is not to replace existing commercial services.

It is to establish a common boundary where assurance information can move.

> **Define locally. Issue anywhere. Share anywhere. Verify anywhere.**

And:

> **Compete on assurance management. Cooperate on assurance exchange.**

---

## References

[^1]: New Zealand Government, "New Template To Simplify Prequalification Process", 20 August 2026. https://www.scoop.co.nz/stories/PA2608/S00188/new-template-to-simplify-prequalification-process.htm

[^2]: New Zealand Government, "NZ Verify app". https://www.govt.nz/browse/passports-citizenship-and-identity/proving-and-protecting-your-identity/nz-verify-app/

[^3]: New Zealand Government, "Digital credentials" and "About the Govt.nz app". https://www.govt.nz/browse/passports-citizenship-and-identity/proving-and-protecting-your-identity/digital-credentials/

[^4]: Business Leaders' Health and Safety Forum, "About". https://www.forum.org.nz/about/

[^5]: WorkSafe New Zealand, "Managing health and safety through the contracting chain". https://www.worksafe.govt.nz/dmsdocument/71748-part-a-managing-health-and-safety-through-the-contracting-chain/latest/

[^6]: WorkSafe New Zealand, "PCBUs working together: advice when contracting". https://www.worksafe.govt.nz/managing-health-and-safety/getting-started/understanding-the-law/overlapping-duties/pcbus-working-together-advice-when-contracting/

All sources were accessed on 11 September 2026.

References to external organisations, publications, and government initiatives are provided as evidence that the problem described in this paper is recognised. No such reference implies consultation, participation, support, or endorsement.

---

## About OpenAssurance

OpenAssurance is an early-stage New Zealand open standards initiative.

Initial areas of work are:

- **OpenCompetency** - https://opencompetency.nz
- **OpenPrequal** - https://openprequal.nz

Project:

**https://openassurance.nz**

GitHub:

**https://github.com/openassurance-nz**