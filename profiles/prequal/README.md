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

A buyer asks for records with a small signed request that names the engagement and pins the exact version of the requirements it refers to, and it goes from the buyer's system to the supplier's, with nobody filling in a form.

Where either has no system, two files attached to an email are enough to carry it, which is the floor and not the intended experience.

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

It always says whether any corrective action is outstanding, and how many, because a supplier chooses what it presents, and it says no more about them than that.

A supplier that receives a corrective action request, fixes the issue, and has it closed by the assessor should be able to keep the whole chain: the assessment, the request, the evidence of what was done, and the closure.

Once the request is closed, the assessor issues a replacement assessment that states the position as it now is, and that is what the supplier normally presents.

> **OpenPrequal exchanges the current assurance state, and does not automatically expose the assurance history.**

The history exists for auditability, the current assessment exists for reuse, and the supplier may show the history to anyone it chooses.

A recommendation is advice from one assessor to the supplier, and it does not travel with the assessment.

That stops the same issue being rediscovered and reassessed by each buyer in turn, and stops a closed finding from following a supplier around.

A corrective action request never changes once issued, and whether it is open, overdue, or closed is read from the records that follow it.

The records are drafted in `docs/exchange-model/extensions.md` sections 3 and 10, and the request in its section 5, and the choices are decisions D11 and D12 in `docs/decisions.md`.

`docs/exchange-model/examples.md` sections 3.8 to 3.13 follow an assessment, a corrective action request, the supplier's evidence of correction, the closure, and the replacement assessment from start to finish.

### 5.3 Reuse by another buyer

An assessment that a supplier holds can be presented to a second buyer that took no part in it.

The first buyer's decision does not bind the second.

The second buyer decides whether it recognises the assessor, whether the assessment is current, whether its scope is relevant to the engagement, which of its own requirements the assessment helps to demonstrate, and what further evidence it still needs.

It may accept the assessment as evidence and ask for nothing more, or find it relevant and not enough, and ask only about the part it does not cover.

> **OpenPrequal is not mutual recognition by default. It is portable assurance evidence that lets the next buyer make an informed local decision without starting from zero.**

`docs/exchange-model/examples.md` section 4 works through both outcomes.

### 5.4 Forms and questionnaires

Most prequalification today is a form.

A supplier answers many of them, each with its own questions, and each inside the system of the buyer or scheme that asks.

```text
Buyer A's form    the supplier enters its information
Buyer B's form    the supplier enters substantially the same information again
Buyer C's form    the supplier enters it again
```

OpenPrequal exchanges assurance records, not completed forms.

> **A user interface may use forms to create, review, or collect assurance records, but forms are not part of the exchange, and no particular form or portal is required for conformance.**

A form bundles four things that are worth keeping apart.

- what the buyer or the scheme needs demonstrated, which today is written as questions;
- the answering, in which a person types statements and uploads documents;
- the keeping of the answers;
- the assessment of them.

The form itself is not the problem.

Someone has to say a thing the first time, and a form is a proper way for a person to do that, particularly in a small organisation with no system of its own.

Where a supplier holds no current declaration about its regulatory history, its own software may show a form in which a director makes one.

What results is a declaration record, the next buyer receives that record, and the director does not answer the same declaration again because the next buyer uses another system.

An insurance certificate is added once in the same way, carried as an evidence record, and reused until it expires or is replaced.

Systems built around forms also do real work in managing, reminding, and assessing, and OpenPrequal expects them to go on doing it.

The difficulty is structural, and it has three parts.

- what a buyer requires exists only as the questions of a form, inside the system that asks them;
- the answers stay in that system, so the next form starts empty;
- a record the supplier already holds cannot be given in place of typing.

Each part of a form corresponds to something the exchange model already has, so no new record type is needed.

```text
In a form today                     In OpenPrequal
What the questions are after        requirements, which state what must be demonstrated
A fact held in a public register    checked against the register, and not asked
A typed answer                      a declaration, made once by a named person
An uploaded document                an evidence record, or the source's own signed record
The score or result                 an assessment record, which is the certificate
Submitting the form                 a presentation, which maps requirements to the records presented
```

A request is not a questionnaire.

It does not say upload this policy, enter that insurance amount, and upload the training matrix.

It says that these are the requirements that apply to this engagement, and the supplier's system works out which of the records it already holds may be relevant.

A system built around a form can adopt this in three steps, each useful on its own, and none of them requires it to give up its form.

- give back: issue the result as an assessment record the supplier holds, and return what the supplier typed and uploaded in a form the supplier's own system can keep and reuse;
- take in: accept a record against a requirement, and ask a person only for what no record demonstrates;
- state the requirements: express what the questions are after as a requirement record that reaches the suppliers who are asked, so that a supplier's system can work out what it already holds before anyone types.

> **The aim is that a thing is entered once, and not that nothing is ever entered.**

Four limits should be stated plainly.

A narrative answer written for one buyer's question seldom fits another's exactly, so reuse is strongest for documents, register facts, and assessments, which is one more reason for a buyer to rely on an assessment by a party it recognises, as section 5.3 describes, and not to ask the narrative questions again.

What a buyer or a scheme requires may be its owner's intellectual property, and OpenPrequal needs only that it reaches the supplier who is asked, as it does on a screen today; it does not require a requirement record to be published, and it does not require a scoring method to be disclosed.

OpenPrequal does not write anyone's requirements, and a common set, such as WorkSafe New Zealand's template, would multiply reuse if its owner expressed it as a requirement record.

If a requirement record became one more form for a person to fill in, OpenPrequal would have failed its own core test, so a supplier's system answers from the records it holds first, and a person is asked only for the remainder.

How an answer typed into another party's form comes back to the supplier as a declaration the supplier issues is unsettled, and it is decision D14 in `docs/decisions.md`.

### 5.5 Only the gaps

A buyer assesses what it was given, requirement by requirement, and asks again only about what remains undemonstrated.

```text
The buyer has twenty requirements

Existing supplier assurance demonstrates    R1 to R17
Further assurance is needed for             R18, R19, and R20

The follow-up request covers                R18, R19, and R20 only
```

These are genuine reasons to ask for something again.

- an existing record has expired;
- a record has been revoked;
- the scope of a record does not cover the new work;
- the buyer's requirement has changed;
- the existing evidence does not adequately demonstrate the requirement;
- material new information is needed.

That the buyer uses a different system is not one of them.

Any new record made to close a gap joins what the supplier holds, so the next buyer may need less again, and a supplier becomes easier to assure over time.

`docs/exchange-model/extensions.md` section 5.7 drafts the follow-up request, and `docs/exchange-model/examples.md` section 3.14 works through an example.

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

The exchange is between systems, so nobody attaches, uploads, or re-enters anything.

The floor, for a party that has no system, is a signed file that any conforming system can export and import, as section 11 of the exchange model describes.

The simplest exchange is a single file.

A supplier that passes an assessment is normally given a certificate, and where the assessor issues it as a signed assessment record, the supplier's system can deliver it to the system of any buyer the supplier approves.

Nothing is attached, uploaded, or entered twice, and a renewed certificate follows the first without anyone chasing it.

The buyer's system checks that it is authentic, current, and from an assessor the buyer recognises, and the buyer decides for itself.

`docs/exchange-model/examples.md` section 5 shows that case, and what changes where the assessor still issues only a document.

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

> **Can a supplier meet a buyer's prequalification requirements with assurance it already holds, without both parties being customers of the same prequalification platform, and without recreating that information in the buyer's system?**

> **Where what the supplier holds is not enough, can the buyer ask only for what is missing?**

If yes to both, OpenPrequal is serving its purpose.
