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
