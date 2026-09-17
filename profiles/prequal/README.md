# OpenPrequal

**Profile:** OpenAssurance for organisations and prequalification  
**Status:** First draft

## 1. Purpose

OpenPrequal is the OpenAssurance profile for exchanging organisation-level prequalification and assurance information.

It is intended to reduce the repeated recreation of substantially the same supplier information across multiple assessment providers, customer portals, procurement systems, and tender processes.

The objective is not to create one compulsory national prequalification scheme.

The objective is to make assurance information portable and reusable while allowing each buyer and assessment provider to retain its own requirements and methodology.

## 2. Problem

A supplier may repeatedly provide the same or similar information about:

- health and safety systems;
- risk management;
- critical risks;
- competency management;
- plant and equipment;
- insurance;
- worker engagement;
- incidents;
- subcontractors;
- policies;
- procedures;
- supporting evidence.

This information may be entered separately into multiple prequalification and customer systems.

The result is duplicated administration without necessarily improving the underlying assurance.

## 3. Evidence and Assessment Must Be Separate

OpenPrequal should distinguish between:

### Organisation evidence

The underlying information provided by the supplier.

Examples:

- policies;
- procedures;
- insurance certificates;
- incident information;
- competency processes;
- plant-management processes;
- risk-management evidence.

### Assessment

An assessment provider's evaluation of that evidence.

Example:

```text
Supplier evidence
      |
      +--> Assessment Provider A
      |       |
      |       v
      |   Assessment Credential A
      |
      +--> Assessment Provider B
              |
              v
          Assessment Credential B
```

The assessment provider owns its assessment or opinion.

The supplier retains the ability to hold and share its underlying assurance evidence.

The exchange model carries these as two different record types, evidence in its section 6.5 and assessment in its section 6.4, so that a buyer can always tell the supplier's own material from an assessor's opinion of it.

## 4. Initial Record Types

OpenPrequal should support or map to:

- organisation identity;
- insurance credential;
- prequalification assessment;
- declaration;
- policy evidence;
- competency-system evidence;
- risk-management evidence;
- incident-management evidence;
- worker-engagement evidence;
- plant and equipment evidence;
- subcontractor-management evidence;
- assessment-provider credential;
- buyer requirement profile.

The working draft in `docs/exchange-model.md` defines the credential types that carry these records.

Section 2 of `docs/standards-map/organisations.md` aligns the evidence categories to the twelve topics of WorkSafe New Zealand's risk-based prequalification template.

Who should make an organisation's declaration is discussed in section 4.2 of the OpenCompetency profile, and the record type is defined in section 6.6 of the exchange model.

## 5. Buyer Requirements

Different buyers may have different requirements.

Example:

```text
Buyer requirement:
- current prequalification assessment
- public liability insurance at specified limit
- critical-risk management evidence
- worker competency management
- specified declarations
```

OpenPrequal should allow the supplier to present existing assurance information against that requirement without completing an entirely new data-entry process.

Section 3 of `docs/exchange-model/examples.md` works through an example, with the buyer's result reported separately for authenticity, currency, recognition, and requirement.

### 5.1 A requirement is guidance for judgement, not a set of machine rules

Prequalification that works does something simple.

- it states the requirement clearly;
- it gives examples of acceptable evidence;
- it allows equivalent evidence where that is appropriate;
- it assesses the evidence provided;
- it asks for corrective action, or makes a recommendation, where one is needed.

OpenPrequal should carry exactly that, and should not recreate the pattern in which a supplier must put a particular document in a particular box.

Evidence examples in a requirement are guidance, and are not exclusive unless the requirement expressly says so.

A requirement states an outcome that is expected, and not a document that is requested.

Where a buyer genuinely needs evidence from a particular source, it says so as an objective criterion, and does not disguise a mandatory condition as an example.

Some parts of a requirement are objective, such as an insurance limit, that evidence is current, the period a declaration covers, or that a director made it, and those parts can be checked by a system.

The judgement stays with the assessor wherever judgement is what is needed.

A buyer asks for records with a small signed request that names the engagement and pins the exact version of the requirements it refers to, and two files attached to an email are enough to carry it.

The supplier's response maps the records it presents to the requirements they are offered against, as an index for the buyer and never as a claim that a requirement is met.

```text
Requirement
     |
     v
Evidence
     |
     v
Assessment
     |
     v
Corrective action or recommendation
     |
     v
Closure, where one is required
```

### 5.2 Corrective actions and recommendations

A corrective action request means something must be addressed to satisfy or maintain a requirement.

A recommendation is an opportunity for improvement, and does not imply that any requirement failed.

An assessment gives a determination for each requirement, in the assessor's own words and, where the assessor maps them, in common words, with the evidence reviewed and any limit on that evidence stated.

It always says which corrective action requests it raised, even when there were none, because a supplier chooses what it presents.

A supplier that receives a corrective action request, fixes the issue, and has it closed by the assessor should be able to keep and present the whole chain: the assessment, the request, the evidence of what was done, and the closure.

That stops the same issue being rediscovered and reassessed by each buyer in turn.

A corrective action request never changes once issued, and whether it is open, overdue, or closed is read from the records that follow it.

The records are drafted in `docs/exchange-model/extensions.md` sections 3 and 10, and the request in its section 5, and the choices are decisions D11 and D12 in `docs/decisions.md`.

`docs/exchange-model/examples.md` sections 3.8 to 3.13 follow an assessment, a corrective action request, the supplier's evidence of correction, the closure, and the replacement assessment from start to finish.

## 6. Assessment Schemes

OpenPrequal should not require different prequalification schemes to be treated as equivalent.

A buyer may decide to accept:

- one particular scheme;
- several alternative schemes;
- a direct assessment;
- specific standalone evidence;
- a combination of these.

OpenPrequal provides the exchange mechanism.

The buyer retains the acceptance decision.

## 7. Exchange Example

```text
Supplier
   |
   +-- organisation evidence
   +-- insurance
   +-- assessment credential
   +-- declarations
            |
            | OpenPrequal
            v
          Buyer
            |
            v
       Buyer applies
       its requirements
```

The buyer should be able to identify the original issuer of each record.

The floor for that exchange is a signed file that any conforming system can export and import, as section 11 of the exchange model describes.

## 8. Small Organisations

A supplier should not need specialist procurement or assurance software to participate.

A hosted compatible service may allow the supplier to:

- maintain an organisation profile;
- upload or receive credentials;
- hold assessment results;
- maintain evidence;
- respond to assurance requests;
- selectively share records;
- export its data.

The supplier should be able to move to another compatible service without recreating the underlying assurance information.

The exchange model makes that possible by identifying an issuer under its own domain name, which a hosted service serves on the supplier's behalf.


## 9. Organisation Information and Personal Information

OpenPrequal primarily concerns organisations, but prequalification evidence can still contain personal information.

Organisation-level information may include:

- insurance;
- policies;
- systems;
- assessment results;
- organisational declarations.

Personal information may include:

- named contacts;
- directors or officers;
- identifiable employees;
- CVs;
- assessor details;
- identifiable incident information.

OpenPrequal should prefer organisation-level evidence where it is sufficient and should avoid collecting or sharing personal information unnecessarily.

Where personal information is required, the general OpenAssurance privacy principles apply, including purpose limitation, minimum disclosure, appropriate retention, and controlled onward sharing.

## 10. Desired Outcome

The aim is:

> **Assess once. Share anywhere.**

This does not mean every buyer must accept every assessment.

It means a valid assessment or evidence item should be capable of being presented anywhere without forcing the supplier to join the recipient's platform or re-enter the same information.

## 11. Non-Goals

OpenPrequal is not intended to:

- become a compulsory national supplier database;
- replace prequalification assessment providers;
- prescribe one universal prequalification score;
- determine which supplier a buyer must accept;
- replace procurement platforms;
- replace contractor-management systems.

## 12. Core Test

> **Can a supplier present valid prequalification information to a buyer without both parties being customers of the same prequalification platform?**

If yes, OpenPrequal is serving its purpose.
