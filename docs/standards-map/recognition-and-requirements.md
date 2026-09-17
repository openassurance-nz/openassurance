# OpenAssurance Standards Map: Recognition and Requirements

**Part of:** `standards-map.md`  
**Status:** Working draft, Phase 2  
**Last reviewed:** September 2026

## 1. Purpose

This part of the standards map assesses how a relying organisation learns which issuers a trusted party recognises, and how it expresses what it requires.

The positions used here are defined in `standards-map.md` section 3, and the method in its section 4.

These are the third and fourth trust questions, where existing standards stop short of what workplace assurance needs.

## 2. Recognition and Endorsement

The third trust question is whether the relying organisation recognises the issuer.

OpenAssurance does not answer that question and must not maintain the list that answers it.

It needs two things: a way for one party to state that it recognises another for a scope, and a way for a relying organisation to consume such statements.

### 2.1 Endorsement as a record

**Position: Profile Open Badges 3.0 EndorsementCredential.**

Open Badges 3.0 defines an EndorsementCredential, a verifiable credential whose subject is the thing endorsed, with an optional comment.[^ob3endorse]

An endorsement can be attached to an issuer profile, to an achievement definition, or to an individual achievement credential.

That covers the three OpenAssurance cases: an industry body recognising an issuer, a regulator recognising a course, and an assessor countersigning a particular record.

What it lacks is scope.

An endorsement of an issuer says nothing about which record types, occupations, risk categories, or periods the endorsement covers, and workplace recognition is almost always scoped.

OpenAssurance should profile the endorsement subject with a small scope vocabulary, expressed as ordinary properties so that unmodified Open Badges tooling still reads the credential.

The W3C data model has no endorsement concept of its own; the general pattern is simply a second credential whose subject is the first, which is what Open Badges formalises.[^vcvocab]

### 2.2 Publishing and consuming recognition

Three published patterns exist for a relying organisation to learn which issuers a trusted party recognises, and none is ready to be adopted outright.

**OpenID Federation 1.0.**

**Position: Evaluate.**

OpenID Federation became a Final Specification on 17 February 2026.[^oidfed]

Each entity publishes a signed configuration, superiors publish signed statements about their subordinates, and a relying party resolves a trust chain from an issuer to a trust anchor it has chosen.

Trust marks let an accreditation body assert that an entity meets a defined set of requirements.

Multiple anchors can coexist, so the mechanism does not imply a central registry.

A companion draft applies it to credential issuers, verifiers, and wallet providers.[^oidfedwallet]

The mechanism is stable, but it is framed around OAuth entities and carries more machinery than a small industry body or a single employer would want to run.

**Recognized Entities v1.0.**

**Position: Evaluate.**

This W3C Working Draft, most recently dated September 2026, expresses recognition as a verifiable credential listing which entities are recognised for which actions.[^recog]

It states explicitly that any body, from a government to an individual, may issue such a credential, and that no single registry is mandated.

Its own status section says it is experimental and not fit for production deployment.

It is the most natural fit for OpenAssurance because it uses the same data model as everything else, and it should be tracked closely.

**ETSI trusted lists.**

**Position: Reference.**

ETSI TS 119 612 defines the signed XML trusted lists used under the European eIDAS regulation, and its scope explicitly permits scheme operators outside the European Union to publish lists in the same form.[^etsi612]

ETSI TS 119 602, published November 2025, generalises the model into an abstract data model for lists of trusted entities in any community.[^etsi602]

Both are the mature reference for how a hierarchy of signed lists works, and neither is something a New Zealand workplace scheme would run.

**The government trust list.**

**Position: Reference.**

Three government lists now exist, and they do different jobs.

The Trust Framework Register is the statutory public register of accredited providers and services, and it is format-neutral because accreditation is.[^tfregister]

The wallet's trusted issuer list is an operational list of the certificate authorities and issuance addresses of accredited issuers, which the Government Digital Delivery Agency adds to after accreditation and onboarding.[^wallettech]

The Digital Trust Service is the machine-readable list for relying parties, published in the ISO/IEC 18013-5 form known as a VICAL, and the government verifier app checks presented credentials against it.[^dts]

The service states that it remains the relying party's responsibility to decide which credentials are legally applicable to its purpose, which is the local-acceptance principle in the government's own words.

The VICAL form is built around mdoc issuing-authority certificates, and no published mechanism was found for representing an issuer of W3C-model credentials in it, even though the Rules permit such credentials to be accredited.

That gap is the subject of the first question to the agency in `decisions.md` section 3.

These are existing New Zealand recognition sources that a relying organisation may consult for government and accredited issuers.

None is a list of workplace issuers, and OpenAssurance should not expect any of them to become one.

### 2.3 The OpenAssurance position

A relying organisation's recognition list is local, and that is the end of the matter for v0.1.

The profile should define the Endorsement record and its scope vocabulary, so that endorsements can be issued, held, and presented like any other record.

It should state that a relying organisation may build its recognition list from any source it chooses, including endorsements it receives, lists it maintains, and accreditation it observes.

It should defer the choice of a publishing format for recognition lists until either OpenID Federation for wallets or Recognized Entities is stable enough to depend on, and should be written so that adopting either later changes nothing in the records.

### 2.4 Accreditation as one signal among several

Accreditation under the New Zealand Digital Identity Services Trust Framework, discussed in `new-zealand-context.md`, is voluntary.

Accreditation under an industry cross-recognition scheme, discussed in `organisations.md`, is likewise a choice the scheme's participants make.

Both are signals a relying organisation may weigh.

Neither may be a precondition for issuing, holding, presenting, or verifying an OpenAssurance record, because that would reintroduce the mandatory registry the Charter excludes.

## 3. Requirement Expression

The fourth trust question is whether a record meets the relying organisation's requirement.

OpenAssurance does not set requirements, but it must give organisations a common way to express them.

Two different things are easily confused here.

- a **query** is what a verifier asks a holder for in one transaction;
- a **requirement** is a durable, publishable statement of what a role, activity, contract, or supplier category needs.

### 3.1 Digital Credentials Query Language

**Position: Adopt, for transaction-time queries.**

DCQL is defined inside OpenID4VP 1.0 and is a JSON query that a verifier sends to request presentations matching it.[^oid4vp]

It arrives with the presentation protocol and is the right way to ask for records in an interactive exchange.

It is not a requirement model.

It has no way to say that a requirement applies to a role, that alternatives are acceptable, or that an issuer must be recognised for a scope, and it is not meant to be read by a person deciding what to require.

### 3.2 Presentation Exchange

**Position: Set aside.**

Presentation Exchange 2.1.1 is a ratified specification of the Decentralized Identity Foundation, dated April 2024.[^pe]

It defined the query and submission structures earlier drafts of OpenID4VP used.

The Final OpenID4VP text does not reference it, and a profile built on the Final protocol inherits DCQL instead.

The specification has not been withdrawn, and the position should be revisited if the protocols change.

### 3.3 Requirement vocabularies elsewhere

`people.md` examines whether a requirement model exists in the education-credential world.

The short answer is that the vocabularies found describe what a credential *is* and what it *requires of its holder* far more fully than what an organisation *requires of a person or supplier*.

### 3.4 What remains

**Position: define, as a small OpenAssurance record type.**

A requirement is not a set of machine rules.

Prequalification that works states what is expected, shows what acceptable evidence looks like, allows equivalent evidence, and leaves the judgement to an assessor, which is how the template recorded in `organisations.md` section 2 describes itself when it says it is not a checklist.

A Requirement record therefore needs to say, for a named role, activity, contract, or supplier category:

- what is expected, in words a person can assess against;
- guidance, and examples of evidence that may demonstrate it, which are not exclusive unless it says so;
- any objective criteria, such as a threshold, currency, a period, a capacity, or an accepted issuer or endorsement;
- which alternatives are acceptable;
- whether it is mandatory or informational.

It should be publishable, signable as an ordinary credential whose subject is the requirement itself, and readable by a person.

Only the objective criteria translate into a DCQL query for use at transaction time, and the rest is judged by an assessor, whose determination is carried in an Assessment record.

The design, and the corrective action record that follows from it, are decision D11 in `decisions.md`.

This is the largest genuinely new item in the map, and it is still small.

## 4. Sources

Every status and date in this part was checked against the source listed in September 2026.

References to external organisations, schemes, and government publications are provided as evidence of what exists. No such reference implies consultation, participation, support, or endorsement.

[^ob3endorse]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", EndorsementCredential and Profile. https://www.imsglobal.org/spec/ob/v3p0/#endorsementcredential

[^vcvocab]: W3C, "Verifiable Credentials Vocabulary v2.0". https://www.w3.org/2018/credentials/

[^oidfed]: OpenID Foundation, "OpenID Federation 1.0", Final Specification, 17 February 2026. https://openid.net/specs/openid-federation-1_0-final.html

[^oidfedwallet]: OpenID Foundation, "OpenID Federation for Wallet Architectures 1.0", draft 05, 15 February 2026. https://openid.net/specs/openid-federation-wallet-1_0.html

[^recog]: W3C, "Recognized Entities v1.0", W3C Working Draft, 6 September 2026. https://www.w3.org/TR/vc-recognized-entities-1.0/

[^etsi612]: ETSI, "Electronic Signatures and Trust Infrastructures (ESI); Trusted Lists", ETSI TS 119 612 V2.4.1, August 2025. https://www.etsi.org/deliver/etsi_ts/119600_119699/119612/02.04.01_60/ts_119612v020401p.pdf

[^etsi602]: ETSI, "Electronic Signatures and Trust Infrastructures (ESI); Lists of trusted entities; Data model", ETSI TS 119 602 V1.1.1, November 2025. https://www.etsi.org/deliver/etsi_ts/119600_119699/119602/01.01.01_60/ts_119602v010101p.pdf

[^tfregister]: Trust Framework Authority, "Trust Framework Register", as at 17 September 2026. https://www.publicservice.govt.nz/about-the-commission/government-digital-delivery-agency/trust-framework-for-digital-identity/trust-framework-authority/trust-framework-register

[^wallettech]: Government Digital Delivery Agency, "Govt.nz app wallet technical guide". https://github.com/NZ-Digital-Public-Infrastructure/govt-nz-app-wallet

[^dts]: Government Digital Delivery Agency, "Digital Trust Service", trust list for relying parties. https://github.com/NZ-Digital-Public-Infrastructure/digital-trust-service

[^oid4vp]: OpenID Foundation, "OpenID for Verifiable Presentations 1.0", Final Specification, 9 July 2025. https://openid.net/specs/openid-4-verifiable-presentations-1_0-final.html

[^pe]: Decentralized Identity Foundation, "Presentation Exchange 2.1.1", DIF Ratified Specification, 25 April 2024. https://identity.foundation/presentation-exchange/spec/v2.1.1/
