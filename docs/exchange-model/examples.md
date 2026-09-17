# OpenAssurance Minimum Exchange Model: Worked Examples

**Part of:** `exchange-model.md`  
**Status:** Illustrative, not normative  
**Last reviewed:** September 2026

## 1. Purpose

These examples show the minimum exchange model at work, and they carry no requirements.

Every name, address, and identifier in them is fictional, the context address is a placeholder, and the term names are provisional.

One example is given for each profile, because Phase 4 calls for a reference exchange in each, a third shows the prequalification assessment reused by a second buyer, a fourth shows a certificate shared on its own, and a fifth shows discovery, keys, and issuer binding.

The requirements they illustrate are in `exchange-model.md`, and the fifth example also uses the discovery record drafted in `extensions.md`.

A reader who wants the simplest case first should start with section 5.

## 2. OpenCompetency: An Attestation About a Person

The first example is from food manufacturing, and shows the attestation from section 4.5 of the OpenCompetency profile as the payload of a JSON Web Signature.

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://example.org/openassurance/v0.1"
  ],
  "id": "https://records.harbourbeverages.example/attestations/2026-0417",
  "type": ["VerifiableCredential", "AttestationCredential"],
  "issuer": {
    "id": "https://harbourbeverages.example/issuer",
    "name": "Harbour Beverages Limited",
    "nzbn": "illustrative"
  },
  "validFrom": "2026-07-01T00:00:00+12:00",
  "validUntil": "2028-06-30T23:59:59+12:00",
  "credentialSubject": {
    "id": "urn:uuid:6f1c2f0e-0000-4000-8000-000000000000",
    "name": "A. Worker",
    "identityConfirmation": "Photo identification sighted by the issuer",
    "assertion": "Operated the depalletiser on packaging line 2 under normal production conditions, including start-up, jam clearing, and end-of-shift isolation",
    "statementKind": "performed",
    "scope": {
      "activity": "Depalletiser operation",
      "context": "Packaging line 2"
    },
    "period": {
      "from": "2026-03-01",
      "to": "2026-06-30"
    },
    "basis": "directObservation",
    "attestor": {
      "name": "T. Ngata",
      "role": "Packaging Shift Supervisor",
      "authorityEvidence": {
        "type": "AuthorisationRecord",
        "record": "https://records.harbourbeverages.example/authorisations/2025-0093"
      },
      "approvalEvidence": {
        "method": "authenticated",
        "authentication": "Signed in to the employer's system with a second factor",
        "approvedAt": "2026-06-30T15:40:00+12:00",
        "statementDigest": "sha256-illustrativeDigestValueOnly"
      }
    }
  },
  "credentialStatus": {
    "type": "BitstringStatusListEntry",
    "statusPurpose": "revocation",
    "statusListIndex": "94567",
    "statusListCredential": "https://harbourbeverages.example/status/3"
  }
}
```

The subject identifier is scoped to the employer and means nothing to anyone else, and the record says how the employer confirmed who the worker is without recording the document's number.

The attestor's authority is another record, the authorisation that made him a workplace assessor, and his approval is asserted by the employer and bound to a digest of the statement, as `exchange-model.md` section 5.6 describes.

A customer receiving this record in a presentation would see, in the presentation's own claims, that it was addressed to that customer, when it expires, and the purpose for which it was shared.

```json
{
  "type": "OpenAssurancePresentationTerms",
  "purpose": "Confirm eligibility to operate packaging equipment on the customer's site under contract 2026-118",
  "onwardSharing": "notExpected",
  "suggestedRetention": "P12M"
}
```

## 3. OpenPrequal: A Buyer Requests Assurance From a Supplier

The second example is from cold-chain logistics, and every organisation and person in it is fictional.

Tidewater Cold Storage Limited operates cold stores and is considering engaging Ridgeline Refrigeration Limited to maintain industrial refrigeration plant.

Fernbank Safety Assessors Limited has already assessed the supplier's health and safety management.

The example follows one transaction from start to finish, and sections 3.9 to 3.13 follow a second path in which a requirement is only partially met.

```text
Requirement record
     |
     v
Request
     |
     v
Presentation
     |
     v
Assessment
     |
     +---- Recommendation
     |
     +---- Corrective action request
                |
                v
           Evidence of correction
                |
                v
           Closure assessment
                |
                v
           Replacement assessment
```

The requirement record, the request, and the corrective action request are extensions drafted in `extensions.md`, and every other record is in the core.

A buyer that asks only to see a certificate needs none of this, and section 5 shows that case.

### 3.1 The buyer's requirement record

Tidewater has a durable requirement set for this kind of work, which it issues as a record of its own.

The record's `id` identifies this immutable version, the subject's `id` identifies the set from one version to the next, and R1 to R4 identify the requirements within it.

**How to read a requirement.**

R1 is the one to read closely, because it calls for judgement.

The requirement is an outcome: the contractor manages the health and safety risks of industrial refrigeration work, including work on ammonia plant.

It is followed by examples of evidence that may demonstrate that outcome.

- an assessment by an assessor the buyer recognises;
- a management-system certification from an accredited certifier;
- the contractor's own health and safety procedures, supported by records and examples showing how they are applied;
- other evidence that demonstrates equivalent arrangements.

These are examples and not prescribed documents.

A contractor does not need to hold all of them, and evidence that is not listed may still demonstrate the requirement.

One contractor might present a recognised third-party assessment.

Another might present its own risk-management procedure, worker training records, inspection records, and examples from completed ammonia work.

The assessor considers whether the evidence as a whole demonstrates the requirement.

So the statement describes the outcome the buyer expects, and the evidence guidance helps a supplier understand what could demonstrate it.

The objective criteria are a different kind of thing.

Where Tidewater says that an assessment relied on must be current and must have included a site visit, those are facts a system can check.

Passing those checks does not establish that the contractor meets R1, and the assessment of health and safety capability still takes a person.

**An objective requirement, by contrast.**

R2 is different.

Tidewater requires at least NZD 10 million of current public liability cover.

A certificate of currency is an example of evidence, but what is required is the cover itself.

The amount and the dates are objective facts that a system can check.

The buyer still decides what provenance it accepts for that evidence, whether a record issued by the insurer, a broker's certificate, or a certificate the supplier holds.

That is why evidence guidance and objective criteria are kept apart.

**What this comes to.**

- a requirement states an expected outcome, and not a requested document;
- evidence examples are guidance, and not the kinds of file a system will accept;
- equivalent evidence is valid unless the requirement expressly excludes it;
- one piece of evidence, or several together, may demonstrate a requirement;
- objective criteria are facts a system can check, and never the whole assessment;
- the assessor's judgement stays explicit.

**The record.**

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://example.org/openassurance/v0.1"
  ],
  "id": "https://tidewatercoldstorage.example/requirements/ammonia/versions/3",
  "type": ["VerifiableCredential", "RequirementCredential"],
  "issuer": {
    "id": "https://tidewatercoldstorage.example/issuer",
    "name": "Tidewater Cold Storage Limited",
    "nzbn": "illustrative"
  },
  "validFrom": "2026-09-01T00:00:00+12:00",
  "credentialSubject": {
    "id": "https://tidewatercoldstorage.example/requirements/ammonia",
    "name": "Refrigeration maintenance contractors, ammonia plant",
    "version": "3",
    "appliesTo": {
      "activity": "Industrial refrigeration maintenance",
      "context": "Ammonia plant"
    },
    "requirements": [
      {
        "id": "R1",
        "title": "Health and safety capability",
        "mandatory": true,
        "statement": "The contractor manages the health and safety risks of industrial refrigeration work, including work on ammonia plant.",
        "evidenceGuidance": {
          "equivalentEvidenceAccepted": true,
          "examples": [
            {
              "description": "An assessment by an assessor the buyer recognises",
              "recordType": "AssessmentCredential"
            },
            {
              "description": "A management-system certification from an accredited certifier"
            },
            {
              "description": "The contractor's own procedures, records, and examples of practice",
              "recordType": "EvidenceCredential"
            }
          ]
        },
        "objectiveCriteria": [
          { "type": "current" },
          { "type": "siteVisitIncluded", "appliesTo": "AssessmentCredential" }
        ]
      },
      {
        "id": "R2",
        "title": "Public liability insurance",
        "mandatory": true,
        "statement": "The contractor holds public liability insurance adequate for the work.",
        "evidenceGuidance": {
          "equivalentEvidenceAccepted": true,
          "examples": [
            { "description": "A certificate of currency issued by an insurer or broker" }
          ]
        },
        "objectiveCriteria": [
          { "type": "minimumInsuranceLimit", "amount": 10000000, "currency": "NZD" },
          { "type": "currentAt", "event": "engagementStart" }
        ]
      },
      {
        "id": "R3",
        "title": "Regulator interventions",
        "mandatory": true,
        "statement": "The contractor discloses any regulator notices, warnings, or prosecutions in the previous five years.",
        "evidenceGuidance": {
          "equivalentEvidenceAccepted": true,
          "examples": [
            {
              "description": "A declaration made by a director",
              "recordType": "DeclarationCredential"
            }
          ]
        },
        "objectiveCriteria": [
          { "type": "lookbackPeriod", "duration": "P5Y" },
          { "type": "declarantCapacity", "value": "Director" }
        ]
      },
      {
        "id": "R4",
        "title": "Worker engagement",
        "mandatory": false,
        "statement": "The contractor involves its workers in managing risk.",
        "evidenceGuidance": {
          "equivalentEvidenceAccepted": true,
          "examples": [
            { "description": "Meeting notes, toolbox talks, or a description of how it is done" }
          ]
        }
      }
    ]
  },
  "credentialStatus": {
    "type": "BitstringStatusListEntry",
    "statusPurpose": "revocation",
    "statusListIndex": "7640",
    "statusListCredential": "https://tidewatercoldstorage.example/status/1"
  }
}
```

The record stands until Tidewater withdraws it, so it carries a status entry as `exchange-model.md` section 9.2 requires, and a later version leaves this one unaltered.

Each objective criterion is a named type and not an expression in a general language of paths and operators.

The supplier is not told which document to put in which box.

### 3.2 The buyer's request

The requirement record says what Tidewater requires of anyone.

The request says that Tidewater is asking Ridgeline to respond to it for one engagement.

It is signed JSON and not a record, and its header names the key that signed it.

```json
{
  "alg": "ES256",
  "typ": "oa-request+jwt",
  "kid": "https://tidewatercoldstorage.example/issuer#key-2026"
}
```

```json
{
  "iss": "https://tidewatercoldstorage.example/issuer",
  "aud": "https://ridgelinerefrigeration.example/issuer",
  "iat": 1789678800,
  "exp": 1790884800,
  "jti": "urn:uuid:ea7b55e0-0000-4000-8000-000000000000",
  "type": "OpenAssuranceRequest",
  "nonce": "N8g2FQe7YvS1mK4x",
  "subject": {
    "type": "Organization",
    "name": "Ridgeline Refrigeration Limited",
    "nzbn": "illustrative"
  },
  "engagement": {
    "reference": "2026-118",
    "activity": "Industrial refrigeration maintenance",
    "context": "Ammonia plant",
    "starts": "2026-10-01"
  },
  "requestedUse": {
    "purpose": "Prequalification for refrigeration maintenance under contract 2026-118",
    "onwardSharing": "notExpected",
    "suggestedRetention": "P12M"
  },
  "requirements": [
    {
      "id": "https://tidewatercoldstorage.example/requirements/ammonia/versions/3",
      "digestSRI": "sha384-illustrativeDigestValueOnly",
      "items": ["R1", "R2", "R3", "R4"]
    }
  ],
  "replyTo": "mailto:assurance@tidewatercoldstorage.example"
}
```

The request does not restate the requirements.

It pins the exact version by identifier and by a digest of the requirement record's file, and that file goes with it.

```text
prequalification-request.jwt                 the signed request
tidewater-ammonia-requirements-v3.vc.jwt     the requirement record it refers to
```

### 3.3 The supplier verifies the request

Ridgeline's system checks the request before anyone considers what to disclose.

```text
Signature                  verified against Tidewater's controller document
Requester's binding        confirmed against the NZBN Register
Audience                   names Ridgeline
Expiry and identifier      not expired; identifier not seen before
Requirement record         signature verified
Requirement digest         matches the request
```

A person at Ridgeline then decides to respond, and what to respond with.

### 3.4 The supplier finds what it holds

Ridgeline holds three records that bear on the requirements.

**The assessment, issued by the assessor.**

The assessor is the issuer, the supplier is the subject, and the result is carried in the assessor's own terms.

The statement that no corrective action is outstanding is deliberate: it is inside the record the assessor signed, so nothing can be hidden by leaving a record out.

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://example.org/openassurance/v0.1"
  ],
  "id": "https://fernbankassessors.example/assessments/2026-1182",
  "type": ["VerifiableCredential", "AssessmentCredential"],
  "issuer": {
    "id": "https://fernbankassessors.example/issuer",
    "name": "Fernbank Safety Assessors Limited",
    "nzbn": "illustrative"
  },
  "validFrom": "2026-05-12T00:00:00+12:00",
  "validUntil": "2027-05-11T23:59:59+12:00",
  "credentialSubject": {
    "organisation": {
      "name": "Ridgeline Refrigeration Limited",
      "nzbn": "illustrative"
    },
    "scope": {
      "activity": "Health and safety management for industrial refrigeration maintenance"
    },
    "criteria": {
      "name": "Fernbank contractor assessment criteria",
      "version": "4.2"
    },
    "result": {
      "outcome": "Meets criteria",
      "score": 86,
      "scale": "percent"
    },
    "supplierCategory": "Medium-sized, higher-risk activities",
    "evidenceScope": {
      "documentsReviewed": true,
      "siteVisit": true
    },
    "assessmentDate": "2026-05-08",
    "correctiveActionState": { "outstanding": false }
  },
  "credentialStatus": {
    "type": "BitstringStatusListEntry",
    "statusPurpose": "revocation",
    "statusListIndex": "20311",
    "statusListCredential": "https://fernbankassessors.example/status/1"
  }
}
```

**The insurance evidence, issued by the supplier about a document it holds.**

The insurer has not issued a signed record, so the supplier carries its certificate of currency as evidence.

The supplier signs the record, the certificate is hash-linked, and the record says plainly that the document carries no signature from its source.

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://example.org/openassurance/v0.1"
  ],
  "id": "https://records.ridgelinerefrigeration.example/evidence/2026-0031",
  "type": ["VerifiableCredential", "EvidenceCredential"],
  "issuer": {
    "id": "https://ridgelinerefrigeration.example/issuer",
    "name": "Ridgeline Refrigeration Limited",
    "nzbn": "illustrative"
  },
  "validFrom": "2026-04-02T00:00:00+13:00",
  "validUntil": "2027-03-31T23:59:59+13:00",
  "credentialSubject": {
    "documentKind": "Certificate of currency, public liability insurance",
    "purportedSource": "The supplier's insurance broker",
    "obtained": "2026-04-02",
    "sourceSigned": false,
    "summary": {
      "cover": "Public liability",
      "limit": "NZD 10,000,000",
      "periodEnd": "2027-03-31"
    }
  },
  "relatedResource": [
    {
      "id": "https://records.ridgelinerefrigeration.example/files/pl-certificate-2026.pdf",
      "mediaType": "application/pdf",
      "digestSRI": "sha384-illustrativeDigestValueOnly"
    }
  ],
  "credentialStatus": {
    "type": "BitstringStatusListEntry",
    "statusPurpose": "revocation",
    "statusListIndex": "4402",
    "statusListCredential": "https://ridgelinerefrigeration.example/status/2"
  }
}
```

**The declaration, made by a director.**

Its issuer and its subject are both the supplier, and the supplier's signature shows only that the supplier issued it.

It therefore names the declarant and carries evidence of her role and of her approval separately, as `exchange-model.md` section 5.6 requires.

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://example.org/openassurance/v0.1"
  ],
  "id": "https://records.ridgelinerefrigeration.example/declarations/2026-0044",
  "type": ["VerifiableCredential", "DeclarationCredential"],
  "issuer": {
    "id": "https://ridgelinerefrigeration.example/issuer",
    "name": "Ridgeline Refrigeration Limited",
    "nzbn": "illustrative"
  },
  "validFrom": "2026-09-17T10:20:00+12:00",
  "validUntil": "2027-09-16T23:59:59+12:00",
  "credentialSubject": {
    "name": "Ridgeline Refrigeration Limited",
    "nzbn": "illustrative",
    "selfDeclaration": true,
    "statement": {
      "text": "Ridgeline Refrigeration Limited has received no notices, warnings, or prosecutions from a health and safety regulator in the five years to the date of this declaration.",
      "periodFrom": "2021-09-17",
      "periodTo": "2026-09-17"
    },
    "declarant": {
      "name": "R. Hale",
      "capacity": "Director",
      "authorityEvidence": {
        "type": "PublicRegisterRole",
        "register": "New Zealand Companies Register",
        "organisationNzbn": "illustrative",
        "role": "Director",
        "appointmentDate": "2021-04-15",
        "checkedAt": "2026-09-17T10:12:00+12:00"
      },
      "approvalEvidence": {
        "method": "authenticated",
        "authentication": "Signed in to the supplier's system with a second factor",
        "approvedAt": "2026-09-17T10:14:22+12:00",
        "statementDigest": "sha256-illustrativeDigestValueOnly"
      }
    }
  },
  "credentialStatus": {
    "type": "BitstringStatusListEntry",
    "statusPurpose": "revocation",
    "statusListIndex": "4410",
    "statusListCredential": "https://ridgelinerefrigeration.example/status/2"
  }
}
```

The register shows that a person of that name was appointed a director of that company in 2021 and had not ceased by the date of the declaration, which anyone can check.

That she approved these exact words rests on the supplier's word, because the method is one the buyer cannot check for itself.

It is the only record of the three that contains personal information, so the presentation that carries them meets `exchange-model.md` sections 10.2 and 10.3 because of it.

### 3.5 The supplier's presentation

The presentation names Tidewater as its recipient, carries the request's nonce and identifier, and sets the holder's own terms.

Each record travels inside it in its signed form, shortened here.

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://example.org/openassurance/v0.1"
  ],
  "type": ["VerifiablePresentation"],
  "holder": "https://ridgelinerefrigeration.example/issuer",
  "aud": "https://tidewatercoldstorage.example/issuer",
  "nonce": "N8g2FQe7YvS1mK4x",
  "iat": 1790044200,
  "exp": 1798714799,
  "requestId": "urn:uuid:ea7b55e0-0000-4000-8000-000000000000",
  "termsOfUse": [
    {
      "type": "OpenAssurancePresentationTerms",
      "purpose": "Prequalification for refrigeration maintenance under contract 2026-118",
      "onwardSharing": "notExpected",
      "suggestedRetention": "P12M"
    }
  ],
  "verifiableCredential": [
    {
      "@context": "https://www.w3.org/ns/credentials/v2",
      "type": "EnvelopedVerifiableCredential",
      "id": "data:application/vc+jwt,eyJhbGciOiJFUzI1NiIs...assessment-2026-1182"
    },
    {
      "@context": "https://www.w3.org/ns/credentials/v2",
      "type": "EnvelopedVerifiableCredential",
      "id": "data:application/vc+jwt,eyJhbGciOiJFUzI1NiIs...evidence-2026-0031"
    },
    {
      "@context": "https://www.w3.org/ns/credentials/v2",
      "type": "EnvelopedVerifiableCredential",
      "id": "data:application/vc+jwt,eyJhbGciOiJFUzI1NiIs...declaration-2026-0044"
    }
  ],
  "submission": [
    {
      "requirement": "R1",
      "records": ["https://fernbankassessors.example/assessments/2026-1182"]
    },
    {
      "requirement": "R2",
      "records": ["https://records.ridgelinerefrigeration.example/evidence/2026-0031"]
    },
    {
      "requirement": "R3",
      "records": ["https://records.ridgelinerefrigeration.example/declarations/2026-0044"]
    }
  ]
}
```

The submission map does not say that Ridgeline considers R1 met.

It says that Ridgeline presents that record for Tidewater to consider against R1.

Ridgeline presents nothing against R4, so R4 is simply absent.

### 3.6 The buyer's system verifies the presentation

The system answers what a system can answer, and says plainly where a person is needed.

```text
Presentation             addressed to Tidewater; nonce and request identifier match; not expired
```

```text
Record                   Signature    Issuer binding   Current      Recognised
Assessment               verified     confirmed        current      recognised
Insurance evidence       verified *   confirmed        current **   not applicable
Director's declaration   verified     confirmed        current      self-declaration

*  the supplier's signature; the document carries no signature from its source
** the period stated in the document; the buyer may confirm it with the source
```

```text
Director's declaration, the named person

Declarant                  R. Hale, Director
Role at declaration date   confirmed by name against the Companies Register
Approval                   asserted by the issuer; digest matches the statement
Corroboration              none
```

```text
Requirement   Objective criteria                    Result
R1            current; site visit included          needs assessment by a person
R2            limit met; current at start           met, on the face of an unsigned document
R3            period covered; made by a director    met
R4            none                                  not evaluated; nothing was presented
```

The issuer binding column is what lets the buyer treat the names on the records as the organisations they claim to be, and each was confirmed against the NZBN Register.

However well the declarant's role and approval are evidenced, they show who said it, and never that what was said is true.

### 3.7 A person assesses

R1 calls for judgement, so the system does not report it as met.

Tidewater's contract manager reads the assessor's result, decides that it demonstrates R1, and telephones the broker to confirm the certificate behind R2.

### 3.8 The buyer's assessment record

Two assessments now exist, and they are different things.

Fernbank's assessment is evidence that Ridgeline presented.

Tidewater's assessment is Tidewater's own determination of whether the evidence presented demonstrates Tidewater's requirements, and Tidewater issues it because Tidewater is the party that reviewed the evidence.

Ridgeline can keep it and present it to anyone else.

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://example.org/openassurance/v0.1"
  ],
  "id": "https://tidewatercoldstorage.example/assessments/2026-0441",
  "type": ["VerifiableCredential", "AssessmentCredential"],
  "issuer": {
    "id": "https://tidewatercoldstorage.example/issuer",
    "name": "Tidewater Cold Storage Limited",
    "nzbn": "illustrative"
  },
  "validFrom": "2026-09-24T14:30:00+12:00",
  "validUntil": "2027-09-23T23:59:59+12:00",
  "credentialSubject": {
    "organisation": {
      "name": "Ridgeline Refrigeration Limited",
      "nzbn": "illustrative"
    },
    "assessmentDate": "2026-09-24",
    "scope": {
      "activity": "Industrial refrigeration maintenance",
      "context": "Ammonia plant",
      "engagementReference": "2026-118"
    },
    "evidenceScope": {
      "documentsReviewed": true,
      "siteVisit": false
    },
    "request": {
      "id": "urn:uuid:ea7b55e0-0000-4000-8000-000000000000"
    },
    "requirementSet": {
      "id": "https://tidewatercoldstorage.example/requirements/ammonia/versions/3",
      "subjectId": "https://tidewatercoldstorage.example/requirements/ammonia",
      "version": "3",
      "digestSRI": "sha384-illustrativeDigestValueOnly"
    },
    "determinations": [
      {
        "requirementId": "R1",
        "result": { "outcome": "Accepted", "commonResult": "met" },
        "evidenceReviewed": [
          {
            "recordId": "https://fernbankassessors.example/assessments/2026-1182",
            "recordType": "AssessmentCredential"
          }
        ],
        "finding": "The assessment covered health and safety management for industrial refrigeration maintenance, included a site visit, and was current at the date of review."
      },
      {
        "requirementId": "R2",
        "result": { "outcome": "Accepted", "commonResult": "met" },
        "evidenceReviewed": [
          {
            "recordId": "https://records.ridgelinerefrigeration.example/evidence/2026-0031",
            "recordType": "EvidenceCredential"
          }
        ],
        "finding": "The certificate presented states current public liability cover of NZD 10,000,000, and was confirmed with the broker.",
        "qualification": "The certificate is carried as supplier-held evidence and does not carry a digital signature from its purported source."
      },
      {
        "requirementId": "R3",
        "result": { "outcome": "Accepted", "commonResult": "met" },
        "evidenceReviewed": [
          {
            "recordId": "https://records.ridgelinerefrigeration.example/declarations/2026-0044",
            "recordType": "DeclarationCredential"
          }
        ],
        "finding": "A declaration covering the required five-year period was made by a declarant whose name matched a current director on the Companies Register.",
        "qualification": "The declaration remains a self-declaration. Evidence of the declarant's role and approval does not corroborate the truth of what was declared."
      },
      {
        "requirementId": "R4",
        "result": { "outcome": "Not assessed", "commonResult": "notAssessed" },
        "evidenceReviewed": [],
        "finding": "No evidence was presented. R4 is informational and does not affect the determination."
      }
    ],
    "correctiveActionState": { "outstanding": false }
  },
  "credentialStatus": {
    "type": "BitstringStatusListEntry",
    "statusPurpose": "revocation",
    "statusListIndex": "7702",
    "statusListCredential": "https://tidewatercoldstorage.example/status/1"
  }
}
```

**What each part is for.**

The request identifier gives the chain from request to presentation to assessment.

The scope of evidence reviewed says that Tidewater reviewed documents and did not visit a site, which a later reader needs in order to weigh the result.

The requirement set names the exact immutable version assessed, by record, by set, by version, and by digest, so that there is never doubt later about what was assessed.

There is one determination for each requirement the assessor considered.

The assessment does not simply say approved, because a future buyer should be able to see what was assessed and what supported each determination.

Each result keeps the assessor's own word beside the common one.

Another scheme might say conformance where Tidewater says accepted, or minor deficiency for a result it maps to partially met, and the mapping is always the assessor's.

Nothing here lets anyone infer that an 86 per cent result from one scheme equals a pass from another.

Evidence reviewed is referenced by identifier and never copied, so the original signed records stay authoritative and the result is a graph of signed records.

A finding explains why the assessor reached the result, and describes the organisation's systems or evidence, not individual workers.

A qualification records a limit on the evidence without changing the result.

R2's objective criteria pass, and the certificate is still a copy the supplier holds, so the assessment says both, and the buyer decides whether that is enough.

The corrective action state says that none is outstanding, which is different from not knowing.

Tidewater also has a recommendation for Ridgeline, and it is not in the record.

```text
Tidewater's note to Ridgeline, sent with the assessment and not part of it

Recommendation REC-1, relating to R4
Consider keeping examples of completed worker engagement activities with the
health and safety records presented at future reviews.
Effect on any determination: none
```

A recommendation is advice from one assessor to the supplier, so it stays with the two of them, and it does not follow Ridgeline to the next buyer unless Ridgeline chooses to show it.

### 3.9 A parallel case: a requirement partially met

The transaction above succeeds, so a second path exercises what happens when it does not.

Suppose instead that Ridgeline had no independent assessment, and presented its own competency system as evidence for R1.

Its evidence record over that system, numbered 2026-0052, is of the same kind as the insurance evidence in section 3.4 and is not shown.

Tidewater's first assessment, called A1 here, determines R1 as partially met and raises a corrective action request.

Its other three determinations are as in section 3.8 and are left out of this extract.

```json
{
  "id": "https://tidewatercoldstorage.example/assessments/2026-0458",
  "type": ["VerifiableCredential", "AssessmentCredential"],
  "credentialSubject": {
    "determinations": [
      {
        "requirementId": "R1",
        "result": { "outcome": "Improvement required", "commonResult": "partiallyMet" },
        "correctiveActionState": { "outstanding": true, "count": 1 },
        "evidenceReviewed": [
          {
            "recordId": "https://records.ridgelinerefrigeration.example/evidence/2026-0052",
            "recordType": "EvidenceCredential"
          }
        ],
        "finding": "The competency system identifies the training required for each role, but expiry dates for licences and authorisations are not consistently recorded or monitored."
      }
    ],
    "correctiveActionState": { "outstanding": true, "count": 1 }
  }
}
```

A1 does not name CAR-7.

A buyer shown A1 while the request is open can see that one corrective action is outstanding against R1, and learns no more than that unless it asks and Ridgeline agrees.

Ridgeline cannot hide it, because the statement is inside the record Tidewater signed.

### 3.10 The corrective action request

CAR-7 is a signed record of its own, drafted in `extensions.md` section 10.

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://example.org/openassurance/v0.1"
  ],
  "id": "https://tidewatercoldstorage.example/corrective-actions/CAR-7",
  "type": ["VerifiableCredential", "CorrectiveActionCredential"],
  "issuer": {
    "id": "https://tidewatercoldstorage.example/issuer",
    "name": "Tidewater Cold Storage Limited",
    "nzbn": "illustrative"
  },
  "validFrom": "2026-09-24T14:35:00+12:00",
  "credentialSubject": {
    "organisation": {
      "name": "Ridgeline Refrigeration Limited",
      "nzbn": "illustrative"
    },
    "assessment": {
      "id": "https://tidewatercoldstorage.example/assessments/2026-0458"
    },
    "requirement": {
      "set": "https://tidewatercoldstorage.example/requirements/ammonia/versions/3",
      "id": "R1"
    },
    "finding": "The competency system identifies the training required for each role, but expiry dates for licences and authorisations are not consistently recorded or monitored.",
    "requiredOutcome": "Expiry dates are recorded and actively monitored for every licence and authorisation relied on for the work.",
    "dueDate": "2026-11-30"
  },
  "credentialStatus": {
    "type": "BitstringStatusListEntry",
    "statusPurpose": "revocation",
    "statusListIndex": "7719",
    "statusListCredential": "https://tidewatercoldstorage.example/status/1"
  }
}
```

It has no field that says open or closed, and it never will.

Its status entry says only whether Tidewater has withdrawn the request, as it might where one was raised in error.

The signed record stays as it is, and its life is told by the records that follow it.

### 3.11 The supplier's evidence of correction

Ridgeline makes the change and issues an evidence record over what it did.

The documents carry no digital signature of their own, and here that matters less, because their source is the issuer of the evidence record and its signature covers their digests.

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://example.org/openassurance/v0.1"
  ],
  "id": "https://records.ridgelinerefrigeration.example/evidence/2026-0088",
  "type": ["VerifiableCredential", "EvidenceCredential"],
  "issuer": {
    "id": "https://ridgelinerefrigeration.example/issuer",
    "name": "Ridgeline Refrigeration Limited",
    "nzbn": "illustrative"
  },
  "validFrom": "2026-10-18T09:00:00+13:00",
  "credentialSubject": {
    "documentKind": "Corrective action evidence",
    "purportedSource": "Ridgeline Refrigeration Limited",
    "obtained": "2026-10-18",
    "sourceSigned": false,
    "relatesTo": "https://tidewatercoldstorage.example/corrective-actions/CAR-7",
    "summary": "Competency records now include licence and authorisation expiry dates, with a monthly expiry review."
  },
  "relatedResource": [
    {
      "id": "https://records.ridgelinerefrigeration.example/files/competency-matrix-2026-10.pdf",
      "mediaType": "application/pdf",
      "digestSRI": "sha384-illustrativeDigestValueOnly"
    },
    {
      "id": "https://records.ridgelinerefrigeration.example/files/expiry-report-2026-10.pdf",
      "mediaType": "application/pdf",
      "digestSRI": "sha384-illustrativeDigestValueOnly"
    },
    {
      "id": "https://records.ridgelinerefrigeration.example/files/expiry-review-procedure-v2.pdf",
      "mediaType": "application/pdf",
      "digestSRI": "sha384-illustrativeDigestValueOnly"
    }
  ],
  "credentialStatus": {
    "type": "BitstringStatusListEntry",
    "statusPurpose": "revocation",
    "statusListIndex": "4463",
    "statusListCredential": "https://ridgelinerefrigeration.example/status/2"
  }
}
```

Names of individual workers that the finding does not need are removed from the documents before they are linked.

### 3.12 The closure assessment

Tidewater reviews the evidence of correction.

No closure record type is needed, because an assessment already means a party reviewing evidence and forming an opinion, and that is what closure is.

This assessment, called A2 here, has the corrective action request as its subject.

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://example.org/openassurance/v0.1"
  ],
  "id": "https://tidewatercoldstorage.example/assessments/2026-0517",
  "type": ["VerifiableCredential", "AssessmentCredential"],
  "issuer": {
    "id": "https://tidewatercoldstorage.example/issuer",
    "name": "Tidewater Cold Storage Limited",
    "nzbn": "illustrative"
  },
  "validFrom": "2026-10-21T11:10:00+13:00",
  "credentialSubject": {
    "assessed": {
      "type": "CorrectiveActionCredential",
      "id": "https://tidewatercoldstorage.example/corrective-actions/CAR-7"
    },
    "organisation": {
      "name": "Ridgeline Refrigeration Limited",
      "nzbn": "illustrative"
    },
    "assessmentDate": "2026-10-21",
    "evidenceReviewed": [
      {
        "recordId": "https://records.ridgelinerefrigeration.example/evidence/2026-0088",
        "recordType": "EvidenceCredential"
      }
    ],
    "result": {
      "outcome": "Corrective action accepted",
      "closureResult": "accepted"
    },
    "finding": "The evidence demonstrates that expiry dates are now recorded for licences and authorisations and are included in a scheduled monthly review."
  },
  "credentialStatus": {
    "type": "BitstringStatusListEntry",
    "statusPurpose": "revocation",
    "statusListIndex": "7731",
    "statusListCredential": "https://tidewatercoldstorage.example/status/1"
  }
}
```

Had the evidence fallen short, the closure result would have been not accepted, with the assessor's own words for it, such as further evidence required.

CAR-7 would still not have changed, and it would have stayed open until a later closure assessment accepted it.

Only Tidewater can close CAR-7, because Tidewater raised it.

An accepted closure does not by itself change what A1 determined about R1.

### 3.13 The replacement assessment

With CAR-7 accepted, Tidewater issues a new assessment against the same requirement record, called A3 here, which replaces A1.

Issuing it is not optional, because `exchange-model.md` section 6.4 requires a replacement whenever a request that affects an assessment is raised or closed.

Its determinations of R2, R3, and R4 are as in section 3.8 and are left out here, and the name of the term that links it to A1 is provisional.

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://example.org/openassurance/v0.1"
  ],
  "id": "https://tidewatercoldstorage.example/assessments/2026-0533",
  "type": ["VerifiableCredential", "AssessmentCredential"],
  "issuer": {
    "id": "https://tidewatercoldstorage.example/issuer",
    "name": "Tidewater Cold Storage Limited",
    "nzbn": "illustrative"
  },
  "validFrom": "2026-10-21T11:30:00+13:00",
  "validUntil": "2027-09-23T23:59:59+12:00",
  "credentialSubject": {
    "organisation": {
      "name": "Ridgeline Refrigeration Limited",
      "nzbn": "illustrative"
    },
    "assessmentDate": "2026-10-21",
    "scope": {
      "activity": "Industrial refrigeration maintenance",
      "context": "Ammonia plant",
      "engagementReference": "2026-118"
    },
    "evidenceScope": {
      "documentsReviewed": true,
      "siteVisit": false
    },
    "requirementSet": {
      "id": "https://tidewatercoldstorage.example/requirements/ammonia/versions/3",
      "subjectId": "https://tidewatercoldstorage.example/requirements/ammonia",
      "version": "3",
      "digestSRI": "sha384-illustrativeDigestValueOnly"
    },
    "replaces": "https://tidewatercoldstorage.example/assessments/2026-0458",
    "determinations": [
      {
        "requirementId": "R1",
        "result": { "outcome": "Accepted", "commonResult": "met" },
        "evidenceReviewed": [
          {
            "recordId": "https://records.ridgelinerefrigeration.example/evidence/2026-0052",
            "recordType": "EvidenceCredential"
          },
          {
            "recordId": "https://records.ridgelinerefrigeration.example/evidence/2026-0088",
            "recordType": "EvidenceCredential"
          }
        ],
        "finding": "The competency system identifies the training required for each role, and records and monitors the expiry dates of the licences and authorisations relied on for the work."
      }
    ],
    "correctiveActionState": { "outstanding": false }
  },
  "credentialStatus": {
    "type": "BitstringStatusListEntry",
    "statusPurpose": "revocation",
    "statusListIndex": "7744",
    "statusListCredential": "https://tidewatercoldstorage.example/status/1"
  }
}
```

Tidewater marks A1 as superseded through its status entry, as `exchange-model.md` section 9.3 describes.

A1 remains authentic as a record of what was determined in September, and A3 is Tidewater's current determination.

A3 describes the position as it now is.

It does not mention CAR-7, it does not list the closure assessment among the evidence reviewed, and its finding says what the competency system does and not what it used to lack.

```text
Requirement set, version 3
        |
        v
Assessment A1              R1 partially met; one corrective action outstanding
        |
        +---- CAR-7
        |        |
        |        +---- Evidence 2026-0088, from the supplier
        |        |
        |        +---- Closure assessment A2: accepted
        v
Replacement assessment A3  R1 met; no corrective action outstanding
```

Ridgeline and Tidewater hold the whole chain, and anyone Ridgeline chooses to show it to can verify every link.

Of that chain, what Ridgeline normally presents is A3 alone, as section 4 shows, so the same issue is not rediscovered by each buyer in turn, and it does not follow Ridgeline around either.

### 3.14 What the transaction shows

Nothing has been re-entered, the supplier has joined nothing, and the decision is the buyer's.

Two files went one way, one came back, and the supplier kept the buyer's actual decision, any corrective action, and the evidence that it was accepted as closed.

The exchange does not stop when documents have moved.

These stay separate facts throughout.

- whether a record is authentic;
- whether it is current;
- whether the buyer recognises its issuer;
- what evidence was reviewed;
- what the assessor concluded;
- whether any corrective action is outstanding;
- what the assessor's current determination is.

Those who hold the chain can also see what was raised and whether it was accepted, and that history stays with them unless the supplier chooses to show it.

Carrying them separately, and not as one green or red status, is what makes the resulting assurance portable and understandable by someone who was not there.

If the insurer later issues a signed record, it replaces the evidence record for R2, the qualification on that determination falls away, and nothing else changes.

## 4. OpenPrequal: A Second Buyer Reuses an Assessment

The third example tests the proposition itself, and not only a first exchange.

It continues the parallel case in sections 3.9 to 3.13, in which Ridgeline holds no independent assessment, so Tidewater's assessment A3 is the only opinion of its health and safety management that Ridgeline holds.

Southmere Seafoods Limited, which is fictional, processes seafood, runs ammonia refrigeration for its blast freezers, and is considering engaging Ridgeline for scheduled maintenance of that plant.

Southmere took no part in Tidewater's assessment, and Tidewater takes no part in this exchange.

```text
Tidewater's requirement
        |
        v
Ridgeline's evidence
        |
        v
Tidewater's assessment, which Ridgeline keeps
        |
        v
Southmere requests assurance
        |
        v
Ridgeline presents Tidewater's assessment
        |
        v
Southmere decides
```

Southmere has five questions to answer, and the model answers none of them on its behalf.

- does Southmere recognise Tidewater as an assessor;
- is the assessment current;
- is its scope relevant to this engagement;
- which of Southmere's requirements does it help to demonstrate;
- what further evidence, if any, does Southmere still need.

### 4.1 The second buyer's requirement

Southmere's requirement record has the form shown in section 3.1, and two of its requirements are given here in outline.

```text
Southmere Seafoods, requirements for mechanical contractors, version 2

S1   The contractor demonstrates an effective health and safety management
     system appropriate to higher-risk mechanical work.

     Evidence that may demonstrate it:
     - an assessment by a party Southmere recognises
     - a management-system certification from an accredited certifier
     - the contractor's own procedures, with records showing their use
     - other evidence that demonstrates equivalent arrangements

     Objective criteria:
     - any assessment relied on is current

S2   The contractor holds public liability cover of at least NZD 5,000,000,
     current at the start of the engagement.
```

Southmere's request is of the kind shown in section 3.2, sent on 10 November 2026 for an engagement that starts on 1 December.

### 4.2 What Ridgeline presents

```text
Presented
- Tidewater's assessment A3, numbered 2026-0533
- Tidewater's requirement record, version 3
- Ridgeline's insurance evidence, numbered 2026-0031

Not presented
- the superseded assessment A1
- corrective action request CAR-7, the evidence of correction, and closure assessment A2
- Tidewater's recommendation
```

The requirement record goes with the assessment because A3 says that R1 is met and does not say what R1 is.

The digest in A3 lets Southmere confirm that the record presented is the exact version Tidewater assessed against.

Nothing in A3 mentions CAR-7, so Southmere does not learn that there was ever a corrective action, and it does not need to.

A3 says that it replaces an earlier assessment, which tells Southmere only that Tidewater has assessed Ridgeline before.

The submission map in the presentation is an index, as it was in section 3.5.

```json
{
  "submission": [
    {
      "requirement": "S1",
      "records": [
        "https://tidewatercoldstorage.example/assessments/2026-0533",
        "https://tidewatercoldstorage.example/requirements/ammonia/versions/3"
      ]
    },
    {
      "requirement": "S2",
      "records": ["https://records.ridgelinerefrigeration.example/evidence/2026-0031"]
    }
  ]
}
```

Presenting Tidewater's assessment tells Southmere that Tidewater is a customer of Ridgeline, and whether to disclose that is Ridgeline's decision.

### 4.3 What Southmere's system reports

```text
Record                          Signature    Issuer binding   Current      Recognised
Tidewater's assessment A3       verified     confirmed        current      recognised
Tidewater's requirements, v3    verified     confirmed        current      not applicable
Insurance evidence              verified *   confirmed        current **   not applicable

*  the supplier's signature; the document carries no signature from its source
** the period stated in the document; the buyer may confirm it with the source
```

```text
Tidewater's assessment A3, as it bears on S1

Assessor                  Tidewater Cold Storage Limited
Scope                     Industrial refrigeration maintenance; ammonia plant
Evidence reviewed         documents; no site visit
Requirement assessed      R1 of Tidewater's requirements, version 3
Requirement record        presented; digest matches the assessment
Assessor's result         Accepted; met
Assessment date           21 October 2026
Corrective actions        none outstanding
Superseded                no; this is the assessor's current assessment
Replaces                  an earlier assessment, which was not presented
```

```text
Requirement   Objective criteria                    Result
S1            the assessment relied on is current   needs assessment by a person
S2            limit met; current at start           met, on the face of an unsigned document
```

Southmere's recognition list is its own, and it lists Tidewater as an assessor of refrigeration contractors.

Had Southmere not recognised Tidewater, the assessment would still have been authentic and current, and a person could still have read it and given it what weight they chose.

Checking the status of A3 tells Tidewater nothing, because a status list is fetched whole and does not show which record was checked.

### 4.4 Southmere decides

A person at Southmere reads R1 beside S1, and reads the scope of A3 beside the engagement.

```text
Southmere requirement S1

Evidence presented              Tidewater's assessment A3
Assessor                        Tidewater Cold Storage Limited, recognised by Southmere
Assessment scope                Industrial refrigeration maintenance; ammonia plant
Requirement assessed            R1 of Tidewater's requirements, version 3
Assessment result               R1 met
Assessment date                 21 October 2026
Corrective actions              none outstanding
Southmere's determination       Accepted as evidence for S1
Additional evidence required    none
```

Tidewater's decision does not bind Southmere.

Southmere uses it as evidence, and does not repeat the assessment that produced it.

For S2, Southmere does not rely on Tidewater's determination of R2, which says what Tidewater concluded about a certificate.

The evidence record over the certificate says what the cover is, costs Ridgeline nothing more to present, and lets Southmere check the limit and the dates for itself.

Reuse is worth most where judgement was needed, and an objective fact is better checked from its own evidence.

### 4.5 Southmere's assessment record

Southmere records its determination as an assessment of its own.

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://example.org/openassurance/v0.1"
  ],
  "id": "https://southmereseafoods.example/assessments/2026-0067",
  "type": ["VerifiableCredential", "AssessmentCredential"],
  "issuer": {
    "id": "https://southmereseafoods.example/issuer",
    "name": "Southmere Seafoods Limited",
    "nzbn": "illustrative"
  },
  "validFrom": "2026-11-12T10:00:00+13:00",
  "validUntil": "2027-11-11T23:59:59+13:00",
  "credentialSubject": {
    "organisation": {
      "name": "Ridgeline Refrigeration Limited",
      "nzbn": "illustrative"
    },
    "assessmentDate": "2026-11-12",
    "scope": {
      "activity": "Scheduled maintenance of industrial refrigeration plant",
      "context": "Ammonia plant, seafood processing",
      "engagementReference": "SM-2026-41"
    },
    "evidenceScope": {
      "documentsReviewed": true,
      "siteVisit": false
    },
    "request": {
      "id": "urn:uuid:5c1d9a20-0000-4000-8000-000000000001"
    },
    "requirementSet": {
      "id": "https://southmereseafoods.example/requirements/mechanical/versions/2",
      "subjectId": "https://southmereseafoods.example/requirements/mechanical",
      "version": "2",
      "digestSRI": "sha384-illustrativeDigestValueOnly"
    },
    "determinations": [
      {
        "requirementId": "S1",
        "result": { "outcome": "Accepted as evidence", "commonResult": "met" },
        "evidenceReviewed": [
          {
            "recordId": "https://tidewatercoldstorage.example/assessments/2026-0533",
            "recordType": "AssessmentCredential"
          },
          {
            "recordId": "https://tidewatercoldstorage.example/requirements/ammonia/versions/3",
            "recordType": "RequirementCredential"
          }
        ],
        "finding": "A current assessment by another operator of ammonia plant, made against a requirement that matches S1 for this engagement, determined that requirement met with no corrective action outstanding.",
        "qualification": "This determination rests on another organisation's assessment, which reviewed documents without a site visit, and does not repeat it."
      },
      {
        "requirementId": "S2",
        "result": { "outcome": "Accepted", "commonResult": "met" },
        "evidenceReviewed": [
          {
            "recordId": "https://records.ridgelinerefrigeration.example/evidence/2026-0031",
            "recordType": "EvidenceCredential"
          }
        ],
        "finding": "The certificate presented states current public liability cover of NZD 10,000,000, which exceeds the limit required.",
        "qualification": "The certificate is carried as supplier-held evidence and does not carry a digital signature from its purported source."
      }
    ],
    "correctiveActionState": { "outstanding": false }
  },
  "credentialStatus": {
    "type": "BitstringStatusListEntry",
    "statusPurpose": "revocation",
    "statusListIndex": "1288",
    "statusListCredential": "https://southmereseafoods.example/status/1"
  }
}
```

The evidence reviewed names Tidewater's assessment, so a third buyer shown this record can see that Southmere's opinion rests on Tidewater's and is not a second independent look.

An opinion that rests on an opinion stays visible as one, however many times it is reused.

### 4.6 The same evidence, a different engagement

Suppose instead that the engagement was the replacement of two rooftop condensers, which have to be lifted into place.

The records Ridgeline presents are the same, and so is everything Southmere's system reports.

The person at Southmere reads the scope of A3 and the words of R1, and finds that neither covers lifting.

```text
Southmere requirement S1

Evidence presented              Tidewater's assessment A3
Southmere's determination       Relevant but insufficient
Reason                          The assessment covered refrigeration maintenance, and did not
                                assess the lifting operations this engagement requires
Additional evidence requested   Evidence of how lifting operations are planned, and of the
                                competency arrangements for those who plan and direct them
```

Nothing has been found wanting in Ridgeline, so this is not a corrective action request, as `extensions.md` section 10 explains.

Southmere has not yet formed its opinion, so it issues no assessment.

It sends a further request, which refers to the first and says what it still seeks, and only the fields that differ from a first request are shown.

```json
{
  "iss": "https://southmereseafoods.example/issuer",
  "aud": "https://ridgelinerefrigeration.example/issuer",
  "jti": "urn:uuid:5c1d9a20-0000-4000-8000-000000000002",
  "type": "OpenAssuranceRequest",
  "follows": "urn:uuid:5c1d9a20-0000-4000-8000-000000000001",
  "requirements": [
    {
      "id": "https://southmereseafoods.example/requirements/mechanical/versions/2",
      "digestSRI": "sha384-illustrativeDigestValueOnly",
      "items": ["S1"],
      "furtherEvidence": [
        {
          "item": "S1",
          "sought": "Evidence of how lifting operations are planned, and of the competency arrangements for those who plan and direct them."
        }
      ]
    }
  ]
}
```

Ridgeline responds with an evidence record over its lifting procedure and a completed lift plan, with the names of workers removed.

Southmere asked about arrangements, which are evidence about the organisation.

Had it needed to know that particular workers are competent, that would be a different exchange under the competency profile, with the privacy requirements that section 2 carries.

Southmere then forms its opinion, and its determination of S1 names both sources.

```json
{
  "requirementId": "S1",
  "result": { "outcome": "Accepted", "commonResult": "met" },
  "evidenceReviewed": [
    {
      "recordId": "https://tidewatercoldstorage.example/assessments/2026-0533",
      "recordType": "AssessmentCredential"
    },
    {
      "recordId": "https://tidewatercoldstorage.example/requirements/ammonia/versions/3",
      "recordType": "RequirementCredential"
    },
    {
      "recordId": "https://records.ridgelinerefrigeration.example/evidence/2026-0097",
      "recordType": "EvidenceCredential"
    }
  ],
  "finding": "Another operator's current assessment demonstrates the management of refrigeration and ammonia risks, and the contractor's lifting procedure and a completed lift plan demonstrate the planning of lifting operations, which that assessment did not cover."
}
```

Tidewater's assessment still saved both parties from starting again, because Southmere asked only about the part it did not cover.

This outcome matters as much as the first.

### 4.7 What the reuse shows

> **OpenAssurance is not mutual recognition by default. It is portable assurance evidence that lets the next buyer make an informed local decision without starting from zero.**

The example was also a test of whether an assessment carries enough to be reused by someone who was not there.

```text
What Southmere needed to know           Where it found it
Who assessed                            the issuer of A3, and its issuer binding
What was assessed                       the scope in A3
Against which requirement and version   the requirement set in A3, and the record presented, bound by digest
On what basis                           the scope of evidence reviewed in A3
When                                    the assessment date and the validity period
The assessor's conclusion               the determination of R1, and its finding
Whether it is still current             the validity period and the status entry
Whether anything is outstanding         the corrective action state in A3
```

Southmere did not need the history behind A3, and was not given it.

The test changed four things in the model.

- a holder presents the requirement record with the assessment, because the assessment identifies a requirement and does not restate it, which is now `extensions.md` section 10.5;
- Tidewater's assessments now say whether a site was visited, which `exchange-model.md` section 6.4 already asked for and the example had left out;
- a request may refer to an earlier request and say what further evidence is sought, which is now `extensions.md` section 5.1;
- evidence that is not enough is kept apart from an organisation that falls short, and only the second calls for a corrective action request.

One question remains open.

An assessment says what it was made for, through its scope and the engagement it names, and that bounds what anyone else can take from it.

Whether a buyer is content for its assessment to be relied on by others, and whether it may say so in the record, is an open point in `extensions.md` section 11.

## 5. OpenPrequal: Sharing a Certificate on Its Own

The fourth example is the simplest exchange in the profile, and probably the most common.

A supplier that passes a prequalification assessment is normally given a certificate, and the next buyer often asks for nothing more than to see it.

In the main path of section 3, Ridgeline holds Fernbank's assessment, and that record is the certificate.

Hollowford Estate Wines Limited, which is fictional, runs glycol refrigeration for its fermentation tanks, and asks its contractors whether they are prequalified and whether it may see the certificate.

There is no request, no requirement record, and no presentation.

```text
Assessor issues the certificate, once
        |
        v
Supplier keeps it
        |
        +---- sends it to one buyer
        +---- sends it to another
        +---- sends it to a third
                    |
                    v
             Each buyer verifies it, and decides for itself
```

### 5.1 What the assessor issues

When Ridgeline passed, Fernbank issued two files.

```text
ridgeline-assessment-2026-1182.vc.jwt    the certificate, as a signed assessment record
ridgeline-assessment-2026-1182.pdf       a rendering a person can read
```

The record is the one shown in full in section 3.4.

It is a certificate in the sense people already use the word: it states a conclusion, a scope, and a period, and it leaves out the findings, the recommendations, and the working papers behind them.

That is the current assurance state and nothing else, which is what `extensions.md` section 10 says should travel.

The rendering is what `exchange-model.md` section 11.2 asks for.

```text
Fernbank Safety Assessors Limited
Certificate of assessment

Organisation         Ridgeline Refrigeration Limited, NZBN illustrative
Assessed             Health and safety management for industrial refrigeration maintenance
Criteria             Fernbank contractor assessment criteria, version 4.2
Result               Meets criteria; 86 percent
Category             Medium-sized, higher-risk activities
Evidence reviewed    documents, and a site visit
Assessed on          8 May 2026
Valid                12 May 2026 to 11 May 2027, unless withdrawn or replaced
Corrective actions   none outstanding

This page carries no authority of its own.
The file ridgeline-assessment-2026-1182.vc.jwt carries the assessor's signature,
and any conforming verifier can check it.
```

### 5.2 What the supplier sends

Ridgeline attaches both files to an email.

The record carries no personal information, so it travels on its own, without a presentation, as `exchange-model.md` section 11.1 allows.

Ridgeline sends the same two files to every buyer that asks, and enters nothing into anyone's system.

The file can be forwarded by anyone, and that does no harm, because the record says which organisation it is about and cannot be passed off as another's.

### 5.3 What the buyer sees

A person at Hollowford who has only an email client opens the rendering, as they would today.

A system that can verify reads the other file, and answers what a system can answer.

```text
Record                   Signature    Issuer binding   Current      Recognised
Fernbank's assessment    verified     confirmed        current      recognised
```

```text
Fernbank's assessment

Assessor's result       Meets criteria; 86 percent
Category                Medium-sized, higher-risk activities
Evidence reviewed       documents, and a site visit
Corrective actions      none outstanding
Superseded              no; this is the assessor's current assessment
Requirement             not evaluated; Hollowford has configured none
```

Hollowford's rule is the one it has always used, which is a current certificate from an assessor on its own list.

With a PDF, that the certificate is genuine, that it came from the assessor named, and that it has not been withdrawn are assumed.

Here each is checked, and the decision is still a person's.

Current means more than the dates, because the status entry shows a certificate that has been withdrawn or replaced at Hollowford's next check, and Fernbank does not learn who checked.

Hollowford is not a customer of Fernbank, holds no account with it, and did not need one, which is `exchange-model.md` section 11.3.

The score is carried and not interpreted, so 86 percent from one assessor says nothing about 86 percent from another.

Whether Fernbank is on Hollowford's list is Hollowford's decision, and the model has no view.

A buyer that needs more than a certificate asks for it with a request, as Tidewater does in section 3, and the certificate is then one piece of evidence among others.

### 5.4 Where the assessor issues only a document

An assessor that does not yet issue signed records still issues a certificate, and the supplier still holds it.

Ridgeline carries it as an evidence record, exactly as it carries its insurance certificate in section 3.4.

```text
                         Signed assessment record        Document carried as evidence
Signature                the assessor's, verified        the supplier's, verified
Issuer binding           the assessor's, confirmed       the supplier's, confirmed
Current                  validity period and status      the period the document states
Recognised               checked against the buyer's     not applicable, because the source
                         own list                        is only purported
Left for the buyer       nothing further                 confirm with the assessor, as today
```

Nothing is lost compared with today, and the digest fixes the supplier's copy.

When the assessor later issues a signed record, it replaces the evidence record and nothing else changes, as `exchange-model.md` section 6.5 describes.

### 5.5 What the certificate case shows

Everything in this example is in the core, and no extension is used.

- the assessor issues one record, once;
- the supplier keeps it, and sends it as many times as it likes;
- each buyer verifies it without joining anything, and decides for itself.

It is also the smallest useful step for each party.

An assessor that does nothing more than issue its certificate as a signed record has made its result portable, a supplier needs only to keep two files, and a buyer needs only a verifier.

## 6. Discovery, Keys, and Issuer Binding

The fifth example follows the buyer in section 3 as it checks that the supplier's records come from the supplier.

Issuer binding in `exchange-model.md` section 7.5 is part of the core, and the discovery record in `extensions.md` section 4 is an extension, so the record format shown is a proposal.

**The supplier's discovery record.**

Ridgeline Refrigeration publishes one TXT record in the DNS zone for its own domain.

```text
_openassurance.ridgelinerefrigeration.example.  3600  IN  TXT  (
    "v=OA1; "
    "issuer=https://ridgelinerefrigeration.example/issuer; "
    "nzbn=(illustrative); "
    "inbox=mailto:assurance@ridgelinerefrigeration.example" )
```

Anyone who knows the supplier's domain can look it up, with no account and no intermediary.

```text
$ dig +short TXT _openassurance.ridgelinerefrigeration.example
"v=OA1; " "issuer=https://ridgelinerefrigeration.example/issuer; " "nzbn=(illustrative); " "inbox=mailto:assurance@ridgelinerefrigeration.example"
```

The record says where the supplier's keys are, which organisation it claims to be, and where a request or a presentation for it should be sent.

It carries no keys and no personal information.

**The controller document.**

The issuer address resolves over HTTPS to a controller document as defined by Controlled Identifiers 1.0.

```json
{
  "@context": "https://www.w3.org/ns/cid/v1",
  "id": "https://ridgelinerefrigeration.example/issuer",
  "verificationMethod": [
    {
      "id": "https://ridgelinerefrigeration.example/issuer#key-2026",
      "type": "JsonWebKey",
      "controller": "https://ridgelinerefrigeration.example/issuer",
      "publicKeyJwk": {
        "kty": "EC",
        "crv": "P-256",
        "x": "illustrative",
        "y": "illustrative"
      }
    },
    {
      "id": "https://ridgelinerefrigeration.example/issuer#key-2024",
      "type": "JsonWebKey",
      "controller": "https://ridgelinerefrigeration.example/issuer",
      "expires": "2026-01-31T23:59:59+13:00",
      "publicKeyJwk": {
        "kty": "EC",
        "crv": "P-256",
        "x": "illustrative",
        "y": "illustrative"
      }
    }
  ],
  "assertionMethod": [
    "https://ridgelinerefrigeration.example/issuer#key-2026",
    "https://ridgelinerefrigeration.example/issuer#key-2024"
  ],
  "authentication": [
    "https://ridgelinerefrigeration.example/issuer#key-2026"
  ]
}
```

The header of each record the supplier signs names one of these keys in its `kid`, which is how a verifier finds the right one.

The retired key stays in the document with the time it ceased to be used, as `exchange-model.md` section 8.3 requires, so that records signed before that time remain verifiable.

If the supplier uses a hosted service, the host serves this document and the supplier's status lists under the supplier's domain, and the supplier changes host by changing where its domain points.

**The binding check.**

A valid signature shows only that the record came from whoever controls the domain.

The buyer's system closes the gap in both directions.

```text
1. The issuer of the record is
   https://ridgelinerefrigeration.example/issuer
2. The discovery record for that domain states an NZBN
3. The public NZBN Register entry for that NZBN lists the website
   ridgelinerefrigeration.example
4. The domain is the same in both directions:
   issuer binding confirmed
```

Had the register listed no website, or a different one, the result would be "asserted only", and the buyer would decide for itself what weight to give the record.

The same check applies to the assessor in section 3, and to any organisation that sends the buyer a request under `extensions.md` section 5.

**Addressing the reply.**

The buyer publishes a discovery record of its own.

The supplier's system reads it, puts the buyer's issuer address in the `aud` claim of the presentation, and sends the presentation file to the buyer's inbox.

Neither organisation has joined anything, and the only infrastructure either needed was a domain name.

## 7. What the Examples Share

The two profile examples use the same record structure, the same envelope, the same file, and the same four-part result, the third shows one of those records reused, the fourth shows one sent on its own, and the fifth shows the issuer binding that all of them depend on.

They differ where the profiles differ.

The competency example identifies a person by a scoped identifier and carries personal information throughout, so every privacy requirement in `exchange-model.md` section 13 applies.

The prequalification example identifies organisations by a public identifier, keeps personal information to one named declarant, and separates the supplier's evidence from the assessor's opinion of it.

It also carries the buyer's determination, a corrective action request, and its closure as records the supplier holds, so the exchange does not end when documents have moved.

The reuse example shows the supplier presenting only the assessor's current assessment to a second buyer, who decides for itself what it demonstrates.

The certificate example needs nothing but the core: one signed record, sent as a file to any buyer that asks.

Phase 4 should demonstrate both exchanges between systems that share nothing but this model.
