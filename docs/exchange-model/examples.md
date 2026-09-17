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
      "authority": "https://records.harbourbeverages.example/authorisations/2025-0093"
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

The subject identifier is scoped to the employer and means nothing to anyone else.

A customer receiving this record in a presentation would see, in the presentation's own claims, that it was addressed to that customer, when it expires, and the purpose for which it was shared.

```json
{
  "type": "OpenAssurancePresentationTerms",
  "purpose": "Confirm eligibility to operate packaging equipment on the customer's site under contract 2026-118",
  "onwardSharing": "notExpected",
  "suggestedRetention": "P12M"
}
```

## 3. OpenPrequal: A Supplier Presenting to a Buyer

The second example is from cold-chain logistics, and every organisation in it is fictional.

Ridgeline Refrigeration Limited maintains industrial refrigeration plant.

Tidewater Cold Storage Limited operates cold stores and is considering engaging it.

Fernbank Safety Assessors Limited has assessed the supplier's health and safety management.

The supplier holds three records and presents them together.

**The assessment, issued by the assessor.**

The assessor is the issuer, the supplier is the subject, and the result is carried in the assessor's own terms.

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
    "name": "Ridgeline Refrigeration Limited",
    "nzbn": "illustrative",
    "assessed": "Health and safety management for industrial refrigeration maintenance",
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
    "assessmentDate": "2026-05-08"
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
  ]
}
```

**The declaration, made by a director.**

The third record is a declaration that the supplier has had no regulator notices, warnings, or prosecutions in the last five years.

Its issuer and its subject are both the supplier, it names the declarant and her role as director, and it identifies the Companies Register as the register that lists her.

It is the only record of the three that contains personal information, so the presentation that carries them meets `exchange-model.md` sections 10.2 and 10.3 because of it.

**The buyer's requirement.**

The requirement is shown in outline, because its structure is the least settled part of the model.

```text
Requirement:
Refrigeration maintenance contractors, ammonia plant

Issued by:
Tidewater Cold Storage Limited

All of:
1. One of:
   - a current assessment that included a site visit, from an
     assessor the buyer recognises
   - current ISO 45001 certification from an accredited certifier
2. Public liability insurance of at least NZD 10,000,000, current
3. A declaration on regulator interventions in the last five
   years, made by a director

Informational:
- worker engagement arrangements
```

**What the buyer's system reports.**

```text
Record                   Authentic    Current      Recognised          Requirement
Assessment               verified     current      recognised          condition 1 met
Insurance evidence       verified *   current **   not applicable      condition 2 met on its face
Director's declaration   verified     current      self-declaration    condition 3 met

*  the supplier's signature; the document carries no signature from its source
** the period stated in the document; the buyer may confirm it with the source
```

The issuer binding of all three issuers is confirmed against the NZBN Register, which is what lets the buyer treat the names on the records as the organisations they claim to be.

The buyer sees at once which of the three rests on an independent issuer, which on the supplier's own word, and which on a document it may want to confirm.

Nothing has been re-entered, the supplier has joined nothing, and the decision is the buyer's.

If the insurer later issues a signed record, it replaces the evidence record, the first asterisk disappears, and nothing else changes.

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

Phase 4 should demonstrate both exchanges between systems that share nothing but this model.
