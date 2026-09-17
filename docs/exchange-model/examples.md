# OpenAssurance Minimum Exchange Model: Worked Examples

**Part of:** `exchange-model.md`  
**Status:** Illustrative, not normative  
**Last reviewed:** September 2026

## 1. Purpose

These examples show the minimum exchange model at work, and they carry no requirements.

Every name, address, and identifier in them is fictional, the context address is a placeholder, and the term names are provisional.

One example is given for each profile, because Phase 4 calls for a reference exchange in each, and a third shows discovery, keys, and issuer binding.

The requirements they illustrate are in `exchange-model.md`, and the third example also uses the discovery record drafted in `extensions.md`.

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

The empty list of corrective action requests is deliberate: it is what lets a reader see that none was raised and none has been left out.

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
    "recommendations": [],
    "correctiveActionRequests": []
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
    "recommendations": [
      {
        "id": "REC-1",
        "relatesTo": "R4",
        "statement": "Consider keeping examples of completed worker engagement activities with the health and safety records presented at future reviews.",
        "effectOnDetermination": "none"
      }
    ],
    "correctiveActionRequests": []
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

The recommendation states that it has no effect, and a receiving system must not turn it into a failed requirement or an outstanding corrective action.

The empty list of corrective action requests says that none was raised, which is different from not knowing.

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
        "evidenceReviewed": [
          {
            "recordId": "https://records.ridgelinerefrigeration.example/evidence/2026-0052",
            "recordType": "EvidenceCredential"
          }
        ],
        "finding": "The competency system identifies the training required for each role, but expiry dates for licences and authorisations are not consistently recorded or monitored."
      }
    ],
    "recommendations": [],
    "correctiveActionRequests": [
      "https://tidewatercoldstorage.example/corrective-actions/CAR-7"
    ]
  }
}
```

A buyer that is later shown A1 can see that CAR-7 exists, even if Ridgeline does not present it.

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

Its other three determinations are unchanged and are left out of this extract, and the name of the term that links it to A1 is provisional.

```json
{
  "id": "https://tidewatercoldstorage.example/assessments/2026-0533",
  "type": ["VerifiableCredential", "AssessmentCredential"],
  "validFrom": "2026-10-21T11:30:00+13:00",
  "credentialSubject": {
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
          },
          {
            "recordId": "https://tidewatercoldstorage.example/assessments/2026-0517",
            "recordType": "AssessmentCredential"
          }
        ],
        "finding": "The competency system now records and monitors expiry dates, following the closure of CAR-7."
      }
    ],
    "recommendations": [],
    "correctiveActionRequests": []
  }
}
```

Tidewater marks A1 as superseded through its status entry, as `exchange-model.md` section 9.3 describes.

A1 remains authentic as a record of what was determined in September, and A3 is Tidewater's current determination.

```text
Requirement set, version 3
        |
        v
Assessment A1              R1 partially met; raises CAR-7
        |
        +---- CAR-7
        |        |
        |        +---- Evidence 2026-0088, from the supplier
        |        |
        |        +---- Closure assessment A2: accepted
        v
Replacement assessment A3  R1 met; no corrective action requests
```

A future relying organisation can verify every link for itself, and the same issue is not rediscovered and reassessed by each buyer in turn.

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
- whether a corrective action was raised;
- whether that corrective action was later accepted;
- what the assessor's current determination is.

Carrying them separately, and not as one green or red status, is what makes the resulting assurance portable and understandable by someone who was not there.

If the insurer later issues a signed record, it replaces the evidence record for R2, the qualification on that determination falls away, and nothing else changes.

## 4. Discovery, Keys, and Issuer Binding

The third example follows the buyer in section 3 as it checks that the supplier's records come from the supplier.

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

## 5. What the Examples Share

The two profile examples use the same record structure, the same envelope, the same file, and the same four-part result, and the third shows the issuer binding that both depend on.

They differ where the profiles differ.

The competency example identifies a person by a scoped identifier and carries personal information throughout, so every privacy requirement in `exchange-model.md` section 13 applies.

The prequalification example identifies organisations by a public identifier, keeps personal information to one named declarant, and separates the supplier's evidence from the assessor's opinion of it.

It also carries the buyer's determination, a corrective action request, and its closure as records the supplier holds, so the exchange does not end when documents have moved.

Phase 4 should demonstrate both exchanges between systems that share nothing but this model.
