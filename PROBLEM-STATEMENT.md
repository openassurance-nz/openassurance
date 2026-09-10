# OpenAssurance Problem Statement

**Status:** First draft

## 1. Summary

New Zealand organisations repeatedly recreate, upload, verify, and maintain substantially the same workplace assurance information across multiple systems.

The problem appears in at least two major areas:

1. worker competency and qualification management;
2. contractor and supplier prequalification.

The issue is not that assurance platforms provide no value.

The issue is that assurance exchange is often coupled to a particular platform, forcing organisations to duplicate information or join another system before information can be shared.

OpenAssurance proposes that the exchange layer should be open even where management platforms remain commercial.

## 2. Competency Duplication

An employer may already maintain detailed, verified information about its workers, including:

- qualifications;
- licences;
- practical assessments;
- experience;
- inductions;
- training;
- competency;
- internal authorisations.

A customer, asset owner, principal contractor, or industry scheme may then require that the same worker and evidence be entered into another nominated platform.

The result can be:

```text
Employer competency record
          |
          v
Customer requires separate platform
          |
          v
Employer creates another account
          |
          v
Worker recreated
          |
          v
Qualifications and evidence recreated
          |
          v
Two systems now need ongoing maintenance
```

This can create:

- duplicate administration;
- duplicate licensing costs;
- inconsistent records;
- expiry mismatches;
- mobilisation delays;
- additional privacy exposure;
- increased chance of stale information;
- more copies of personal information requiring separate access control and retention;
- dependency on a particular vendor ecosystem.

The privacy problem is structural as well as administrative. Recreating the same worker record across multiple systems increases the number of places where personal information can become stale, be retained unnecessarily, or be exposed through a security incident.

An open data schema does not fully solve the problem if sending or receiving the record still requires enterprise licensing, platform membership, or tenant setup.

## 3. Prequalification Duplication

The same structural problem exists at organisation level.

A supplier may repeatedly provide similar information to:

- prequalification schemes;
- customers;
- tender portals;
- procurement systems;
- contractor-management systems;
- principal contractors.

Typical evidence includes:

- health and safety policies;
- risk-management processes;
- insurance;
- training and competency arrangements;
- plant and equipment systems;
- incident information;
- worker engagement;
- subcontractor management;
- supporting documentation.

The current pattern may look like:

```text
Company evidence
   |
   +--> Assessment process A
   |
   +--> Assessment process B
   |
   +--> Customer portal C
   |
   +--> Tender questionnaire D
```

The evidence is repeatedly entered, reformatted, uploaded, or reassessed.

This creates cost without necessarily creating additional assurance.

## 4. The Structural Problem

The current ecosystem often mixes three separate things:

### Management

Software for storing, monitoring, and administering assurance information.

### Assessment

A person or organisation evaluating evidence and expressing an assessment or opinion.

### Exchange

Moving assurance information from one party to another.

Management and assessment can remain commercial and differentiated.

The exchange layer does not need to be captive to either.

## 5. Open Schemas Are Not Enough

A schema may be public while access remains closed.

For genuine interoperability, an organisation should be able to:

- export a conforming assurance record;
- transmit it to another organisation;
- preserve the original issuer;
- independently verify authenticity;
- check status;
- receive a conforming record into another compatible system.

These capabilities should not require both parties to become customers of the same platform.

## 6. Desired Future State

### Competency

```text
Employer or issuer
       |
       | OpenCompetency
       v
Receiving organisation
       |
       v
Receiving organisation applies
its own requirements
```

### Prequalification

```text
Supplier assurance information
          |
          | OpenPrequal
          v
Buyer or assessment provider
          |
          v
Buyer applies its own requirements
```

The receiving organisation remains responsible for acceptance.

OpenAssurance only makes the information portable, attributable, and verifiable.

For personal information, the preferred model is a purpose-specific presentation rather than unrestricted sharing of an individual's entire assurance history.

```text
Authoritative assurance records
          |
          v
Purpose-specific presentation
          |
          v
Required recipient
```

## 7. What Should Remain Local

OpenAssurance should not attempt to create universal answers to questions such as:

- What makes a person competent to perform a specific task?
- Which training provider should be trusted?
- Which prequalification score is sufficient?
- Which assessment schemes are equivalent?
- Which contractor is acceptable for a particular job?

Those decisions are contextual and should remain with the relevant organisation.

OpenAssurance should instead provide a common way to express:

- the evidence;
- the issuer;
- the assessment;
- the endorsement;
- the requirement;
- the resulting match.

## 8. Small Organisations

Many organisations do not operate specialist competency or assurance databases.

OpenAssurance therefore cannot assume that every participant:

- runs its own server;
- has an API;
- employs an IT team;
- operates specialist software.

Hosted OpenAssurance-compatible services should allow smaller organisations to participate in the same open exchange system.

The hosting provider should not become the owner of the assurance information or the trust relationship.

## 9. The Core Test

OpenAssurance should be judged against one practical question:

> **Can Organisation A send a valid assurance record to Organisation B when neither organisation is a customer of the other's software provider?**

If the answer is no, the exchange is still platform-dependent.

## 10. Intended Outcome

The intended outcome is not a single national assurance database.

It is an ecosystem in which different organisations and software providers can compete while exchanging the same open assurance records.

> **Define locally. Issue anywhere. Share anywhere. Verify anywhere.**
