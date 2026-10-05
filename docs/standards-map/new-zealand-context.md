# OpenAssurance Standards Map: New Zealand Context

**Part of:** `standards-map.md`  
**Status:** Working draft, Phase 2  
**Last reviewed:** October 2026

## 1. Purpose

This part of the standards map records the New Zealand law and government infrastructure that OpenAssurance must be consistent with.

OpenAssurance operates inside New Zealand law and alongside government digital identity infrastructure that has moved quickly since the landscape document was first drafted.

Nothing here is something OpenAssurance can adopt or profile in the technical sense.

It is what OpenAssurance must be consistent with.

The positions used here are defined in `standards-map.md` section 3, and the method in its section 4.

## 2. Privacy Act 2020

**Position: Reference, and the subject of the Privacy Impact Assessment.**

The landscape document lists the Information Privacy Principles that bear on OpenAssurance, and `PRIVACY-PRINCIPLES.md` sets out the design response.

Two developments since then need recording.

Information Privacy Principle 3A, which requires an agency that collects personal information indirectly to take reasonable steps to make the individual aware of it, was enacted by the Privacy Amendment Act 2025 and came into force on 1 May 2026.[^ipp3a]

It applies to personal information collected from that date, and it contains a worked exception: the receiving agency need not notify where the original collector has already told the individual about the disclosure.[^ipp3a]

That exception is directly relevant to an employer presenting a worker's record to a customer, and the Privacy Impact Assessment should examine which party's notice covers which flow.

Information Privacy Principle 13 permits an agency to assign a unique identifier only where necessary for its functions, prohibits assigning an identifier that another agency has already assigned, and restricts requiring its disclosure.[^ipp13]

The identifier design in `credential-layer.md` section 4 is built to sit inside that principle, and `decisions.md` section 3 records the question that should be put to the Office of the Privacy Commissioner.

The Office of the Privacy Commissioner publishes a Privacy Impact Assessment toolkit, revised in 2024, which is the method the required assessment should follow.[^piatoolkit]

## 3. Digital Identity Services Trust Framework

**Position: Reference, as a compatibility target and a voluntary accreditation signal.**

The Digital Identity Services Trust Framework Act 2023 came fully into force on 1 July 2024.[^distfact]

It establishes a Trust Framework Board, a Trust Framework Authority, an accreditation regime, a public register of accredited providers and services, and a rule-making power covering identification management, privacy, security, information and data management, and sharing.[^distfact]

Accreditation is voluntary.

A provider "may apply" to be accredited, a service may lawfully be provided without accreditation, and the rules apply only to accredited services.[^distfact]

The Trust Framework functions moved from the Department of Internal Affairs to the Government Digital Delivery Agency, established within the Public Service Commission on 1 April 2026.[^gdda]

Three things in the Trust Framework matter to OpenAssurance.

First, the Act's definition of a digital identity service expressly covers sharing organisational information as well as personal information, so an OpenPrequal service is within its scope.[^distfact]

Second, the Trust Framework Rules specify the credential formats an accredited credential service may use: the W3C Verifiable Credentials Data Model in its latest Recommendation, ISO/IEC 18013-5, or the ISO/IEC 23220 series.[^distfrules]

An OpenAssurance record on the W3C data model is therefore a format the Trust Framework already recognises.

Third, the Rules require revocation for any accredited credential valid for more than 72 hours, prohibit server retrieval during presentation, and discourage display-only credentials.[^distfrules][^dciptech]

They also require an accredited credential service to keep a distinct cryptographic trust chain, whose issuing and root certificates are not shared with any non-accredited service.[^distfrules]

Those constraints are consistent with the OpenAssurance design and should be treated as a floor, and the trust-chain rule is a design constraint for any hosted OpenAssurance service that intends to seek accreditation for some of its credentials and not others.

The framework is open to private providers as well as government agencies: the regulations require a provider to be a government agency or a New Zealand resident, which for an organisation means one formed or incorporated in New Zealand and carrying on business here.[^distfregs]

Accreditation expires three years after it is granted or renewed, and the 2026 amendment rules describe themselves as introducing emerging standards for interoperable verifiable credential presentation.[^distfregs][^distfaccred][^distfrules]

OpenAssurance must not require accreditation as a condition of participation, because the Act itself does not, and because doing so would make a voluntary government register a mandatory one for workplace records.

It should be designed so that a hosted OpenAssurance service could seek accreditation if its operator chose to.

## 4. The government wallet, issuance platform, and verifier

**Position: Reference, and the source of decision D3 in `decisions.md`.**

The Govt.nz app was released on 10 December 2025, and its digital wallet is now available, with accredited credentials expected to become available progressively from October 2026.[^govtapp][^govtwallet]

Participation is stated to be voluntary, credentials are stored on the device rather than in a central database, and signatures are verified against published issuer keys without contacting the issuer.[^govtwalletprivacy]

The Government Digital Delivery Agency publishes the technical guides for the wallet and for the government's credential issuance platform openly.[^wallettech][^dciptech]

They show a consistent design.

- credentials are mdoc, on ISO/IEC 18013-5 and the ISO/IEC 23220 series;
- issuance uses OpenID for Verifiable Credential Issuance;
- presentation uses ISO/IEC 18013-5 proximity flows and OpenID for Verifiable Presentations as profiled by ISO/IEC 18013-7;
- revocation uses the IETF Token Status List draft;
- the W3C Digital Credentials API is planned for online presentation;
- government agencies that issue credentials must use the government issuance platform, while other organisations run their own conformant issuance service and supply their certificate authority and issuance address for the wallet's trusted issuer list;
- the wallet is open to any organisation, government or private, whose credential is accredited.

The private-issuer pathway is no longer theoretical.

On 16 September 2026 the Trust Framework Register recorded the accreditation of a registered bank as a credential provider, with a business bank account credential issued into the Govt.nz app.[^tfregister]

The structure this produces is federated rather than centralised: government issuers use a shared platform, private accredited issuers use their own, and both meet at accreditation and the trust list.

That is consistent with the Charter, because it does not make government infrastructure a precondition for issuing a credential.

The NZ Verify app, released in May 2025, verifies Trust Framework accredited credentials and ISO/IEC 18013-5 mobile driving licences, checks the signature against the issuer's public key, checks expiry and revocation, and then checks acceptability for a selected purpose.[^nzverify][^nzverifytech]

It keeps no information after verification.

That three-step check is the OpenAssurance trust flow with the recognition question answered by the government trust list, and the acceptance question answered by the app's purpose templates.

Digital driver licences are now recognised in law alongside physical ones, and the implementing rules were consulted on in mid-2026.[^ddl]

The consequence for OpenAssurance is stated in `credential-layer.md` section 2.

The government has chosen mdoc for the credentials it issues, the W3C data model is permitted but not implemented in government tooling, and the protocols in between are the same ones this map adopts.

OpenAssurance should adopt the shared protocols, keep the W3C data model for its own records, let its verifiers accept government-issued mdoc presentations as an optional class, and decide before v0.1 whether an mdoc representation of OpenCompetency records is worth defining.

## 5. Health and Safety at Work Act 2015

**Position: Reference.**

The Act's overlapping-duties provisions require persons conducting a business or undertaking with shared duties to consult, cooperate, and coordinate so far as is reasonably practicable, and WorkSafe's position is that a prequalification does not by itself discharge those duties.[^wsposition]

OpenAssurance records support the information exchange that consultation needs.

They do not replace it, and the profile should say so.

## 6. New Zealand Business Number Act 2016

**Position: Reference, with the identifier adopted in `credential-layer.md` section 4.**

The Act's purposes include enabling businesses to interact more easily with each other, reducing transaction costs, and protecting the privacy of individuals in business.[^nzbnact]

Its public and non-public data classes, and its treatment of unincorporated entities, are the reason `credential-layer.md` section 4 cautions that a sole trader's NZBN is personal information.

## 7. Mandated government data standards

**Position: Reference.**

The Government Chief Data Steward maintains a register of data standards mandated for public service departments, including person name, date of birth as ISO 8601-1:2019, and street address as ISO 19160-1:2015.[^mandated]

Where an OpenAssurance record carries a person's name or address as a claim, the profile should use those representations, so that records exchanged with government need no translation.

No mandated standard exists for organisation identity beyond the NZBN.

## 8. Identification Standards

**Position: Reference, with OpenAssurance's roles and its statements about identity aligned to them.**

The Government Digital Delivery Agency is responsible for the Identification Standards, which the Department of Internal Affairs developed and first published.[^idstds][^idoverview]

There are five standards, each with an implementation guide, and all five in their current versions took effect on 1 May 2026.[^idstds][^idia][^idcs][^idfs]

- the Information Assurance, Binding Assurance, and Authentication Assurance Standards, at version 3, apply to any relying party that enrols an entity;
- the Credential Service Standard applies to a party that issues credentials on which others rely;
- the Facilitation Service Standard applies to a party that facilitates the presentation of credentials.

The last two replace the Federation Assurance Standard of 1 October 2024, whose controls they carry forward with the same numbering.[^idcs][^idfs]

The standards are published under the Creative Commons Attribution 4.0 International licence.[^idstds]

Conformance is voluntary and judged against the levels a risk assessment indicates, unless contract, Cabinet mandate, or legislation requires it.[^idconform]

The one mandate the standards list is that Trust Framework accreditation requires conformance with one or more of the standards, so they sit beneath section 3: a hosted OpenAssurance service that sought accreditation would be assessed against them, and no other participant need be.[^idconform]

The Trust Framework Rules make the link explicit, requiring an accredited credential service to comply with the Credential Service Standard and an accredited facilitation service with the Facilitation Service Standard.[^distfrules]

The standards govern identification processes and not data formats, and they define no record, protocol, or schema that OpenAssurance could adopt.

Their subject is whether information about an entity is accurate, belongs to the entity using it, and stays under that entity's control.

Most OpenAssurance records are not identification credentials, because an attestation of competence says what a person can do and not who the person is.

The standards nonetheless reach into OpenAssurance's territory: the Information Assurance Standard applies to information collected to decide an entity's eligibility or capability, and the Credential Service and Facilitation Service Standards both name misrepresentation of abilities among the harms they address.[^idia][^idcs][^idfs]

A consolidated draft of the standards has also been published for consultation and is stated not to be an official publication, and this section relies only on the published standards.

### 8.1 Roles

The standards use four roles, and each maps onto OpenAssurance's, though not one to one.[^idoverview][^idconform]

- an Entity corresponds to the Subject, and the standards' holder is the Entity with whom a credential was first established, whereas an OpenAssurance Holder may be an organisation presenting a record about someone else;
- a Credential Provider corresponds to the Issuer;
- a Facilitation Provider, which facilitates presentation through an exchange, a hub, or a wallet, corresponds to a Host that presents records, and the standards make it accountable for the presentation without making it the credential provider, which is the distinction `architecture-overview.md` draws between a Host and an Issuer;
- a Relying Party combines the Verifier and the Relying Organisation, which OpenAssurance keeps apart because checking authenticity and deciding acceptance are different acts.

The guidance on authority to act uses "Subject" for the entity on whose behalf another acts, and "Agent" for the one who acts.[^idata]

OpenAssurance's Subject is the party a record is about, and its documents should not borrow the guidance's sense of the word.

### 8.2 Where the controls already agree

The controls of the Credential Service and Facilitation Service Standards match choices the exchange model has already made.[^idcs][^idfs]

- a credential provider must not put in a credential the identifier under which it holds the person's information, and a facilitation provider must not give the same persistent identifier to several relying parties, which is the scoped identifier of `exchange-model.md` section 7.3;
- credential providers must support partial presentation and derived values, and a presentation must carry only what the relying party asked for, which is the minimum disclosure of section 10.4;
- information should not go to a relying party that cannot give a purpose for collecting it, and an OpenAssurance presentation states its purpose under section 10.3;
- a presentation should carry issuance and expiry times, a means of checking revocation, and an identifier for the relying party, which the record's validity period and status and the presentation's `aud` claim provide;
- the standard also asks for a transaction identifier, which a core presentation does not carry and a presentation made in response to a signed request does, through the request's `jti`;
- credentials must be capable of suspension, revocation, and expiry, which is section 9;
- a credential provider must support every member of the population that needs its credential, which the floor in section 11.1 is designed to allow.

The Information Assurance Standard requires a relying party to store only what its purpose needs, and to discard information collected solely to verify something once the verification is done.[^idia]

That is the verify-rather-than-copy behaviour the privacy principles ask of a relying organisation, stated as a government control.

### 8.3 Levels of assurance

The standards express assurance as three separate levels, each from 1 to 4, for information, binding, and authentication, written as a three-part expression and never combined into a single number.[^idloa]

The expression applies to an individual piece of information and not to a whole credential, and a declaration of levels says whether it is self-attested or independently certified.[^idloa]

A credential provider must make its levels available, and a facilitation provider must pass them to the relying party or declare the lowest where a presentation cannot carry each one.[^idcs][^idfs]

`exchange-model.md` section 5.5 asks an issuer to state in words how it confirmed a person's identity, such as "photo identification sighted by the issuer".

Where an issuer has applied the standards, a levels expression is the New Zealand way of saying the same thing more precisely, and section 5.5 lets a record carry one for its identity claims alongside the words, with the basis of the declaration.

It is not required, because most issuers of workplace records have not assessed themselves against the standards, and requiring it would make a voluntary regime a condition of issuing.

`decisions.md` section 3 records the question for the Government Digital Delivery Agency.

### 8.4 Evidence quality and the value of a signed record

The Information Assurance Standard grades evidence by level.[^idia]

At level 3 a relying party must use at least a copy of an authoritative source, judged by manual identification or by security features that need proprietary knowledge to reproduce, which since version 3 need not be physical, and should check its status with the issuer.

At level 4 it must use the authoritative source itself or a continuously synchronised link to it, identified systematically and reached through a trusted channel, and must check whether it has been suspended or revoked.

An uploaded copy of a certificate, which OpenAssurance carries as an evidence record, offers neither systematic identification nor a status check.

A record signed by the party that is the authoritative source for its claims, verified against that party's published key and checked against its status list, is identified systematically and has its status checked, and is the closest thing to what level 4 describes.

Whether a signature verified against a published key meets the standard's trusted channel is a question for the Government Digital Delivery Agency, recorded in `decisions.md` section 3, and until it is answered this part claims no more than that.

The standard grades statements too: a statement at level 1 is taken at face value, at level 3 it must be a declaration carrying some penalty, and at level 4 a statutory declaration carrying severe penalties, with contradictory statements checked at levels 3 and 4.[^idia]

A declaration record under `exchange-model.md` section 6.6 says who declared and in what capacity, but not whether the declarant accepted any consequence for a false statement, which is what a relying party applying the standard needs to know.

Section 6.6 therefore lets a declaration state the basis on which it was made, inside the statement the declarant approves.

The standard's check for contradictions is the corroboration on which section 6.6 already says a self-declaration's value depends.

### 8.5 Authority to act

The guidance on authority to act separates role-based authority, held through a role such as director or treasurer and usually defined in legislation or policy, from delegated authority, granted by the holder of a power and never exceeding it.[^idata]

It says that evidence of a role-based authority, such as a director's entry in the companies register, normally gives information assurance only, and that binding it to the right person takes a separate process.[^idata]

That is the conclusion `exchange-model.md` section 5.6 reaches when it says a register check matches a name and no more, and the guidance supports keeping authority evidence and approval evidence apart under decision D10.

Delegated authority corresponds to an authorisation record under section 6.3 used as authority evidence.

The guidance recommends that the delegate acknowledge and accept a delegation, and that an authority be checked for currency before it is relied on.[^idata]

Section 5.6 already checks the role as at the date of the record, and under decision D10 an authorisation used as authority evidence for a delegation now carries the delegate's acceptance.

### 8.6 Where a hosted service would need care

The Facilitation Service Standard requires a facilitation provider to collect, for each presentation, its transaction identifier and time, an identifier for the holder and for the relying party, values and references describing the information presented, and the integrity mechanisms used.[^idfs]

The Credential Service Standard also requires a credential provider to log all activity in the service that establishes its credentials, including what each change altered.[^idcs]

A Host that sought accreditation as a facilitation provider would therefore keep a record of every presentation it facilitates, which is a further copy of who presented what to whom.

The Privacy Impact Assessment should examine whether references without values satisfy that control, and how long such a log need be kept, so that a hosted service can meet the standard without becoming a register of presentations, and `PRIVACY-PRINCIPLES.md` section 16 lists it in the assessment's scope.

## 9. Government API Standard

**Position: Reference, as a constraint on a government agency that operates an inbox or an issuing service.**

The Government Digital Delivery Agency publishes the API Standard, whose version of 1 September 2026 consolidates the 2022 API Guidelines into a single normative specification for the Digital Government Target State, written with RFC 2119 requirement words.[^apistd]

It applies to APIs developed by or on behalf of New Zealand government, and not to APIs an agency merely consumes.[^apistd]

A private organisation's inbox is outside it, and so is an agency sending a file to someone else's inbox.

An agency that receives files at its own inbox, as a relying organisation or as an issuer, would be building an API within its scope, and the model should let it do so without conflict.

The inbox in `exchange-model.md` section 11.5 already meets most of the standard.

- the standard requires TLS 1.2 or later, and the inbox is an HTTPS address;
- the standard requires APIs to be based on open or industry-accepted standards and not to expose proprietary formats, and everything an inbox receives is a file in a registered media type;
- the standard requires the major version in the URL path from first publication, and the inbox is whatever address the discovery record gives, so an agency can include a version in it.

Two points need attention.

First, the standard requires a machine-readable interface specification in the OpenAPI format.[^apistd]

`exchange-model.md` section 11.5 calls for an OpenAPI description of the inbox in v0.1, so that every agency's inbox is described the same way and no agency has to write its own.

Second, the standard requires OAuth 2.1 where a client must be authorised to use an API, while section 11.5 forbids an inbox to require an account, a key, or any prior arrangement.[^apistd]

The two need not conflict, because an inbox authorises no client: the integrity of what it receives comes from the signature on the file, and section 11.5 lets the receiving system accept or refuse each file according to whether it recognises the signer, without requiring the sender to register.

An agency's security assessment may still treat an endpoint that any sender can reach as a risk, and `decisions.md` section 3 records the question for the Agency.

The standard also points agencies to the Standard for information sharing with third parties, mandatory for public service agencies since 1 July 2025, which governs giving third parties access to personal information.[^apistd]

It bears on any agency that issues or receives records about people, and `PRIVACY-PRINCIPLES.md` section 16 lists it in the Privacy Impact Assessment's scope.

## 10. Sources

Every status and date in sections 2 to 7 was checked against the source listed in September 2026, and in sections 8 and 9 in October 2026.

Sections 8 and 9 cite the dated copies on the government standards site, which carry each document's version date in the address.

That site states that the versions on digital.govt.nz prevail over any inconsistency, and that its own copy of the API Standard is the authoritative one; the digital.govt.nz pages could not be read without completing a human-verification check.

References to external organisations, schemes, and government publications are provided as evidence of what exists. No such reference implies consultation, participation, support, or endorsement.

[^ipp3a]: Privacy Amendment Act 2025, 2025 No 53, Part 1, inserting Information Privacy Principle 3A with effect from 1 May 2026. https://www.legislation.govt.nz/act/public/2025/0053/latest/whole.html

[^ipp13]: Office of the Privacy Commissioner, "Principle 13: Unique identifiers". https://www.privacy.org.nz/privacy-principles/13/

[^piatoolkit]: Office of the Privacy Commissioner, "Privacy Impact Assessments", toolkit revised 2024. https://www.privacy.org.nz/responsibilities/privacy-impact-assessments/

[^distfact]: Digital Identity Services Trust Framework Act 2023, 2023 No 13, sections 3, 8, 10, 15, 18 to 23, 34, 43, and 58. https://www.legislation.govt.nz/act/public/2023/0013/latest/whole.html

[^gdda]: Government Digital Delivery Agency, "Government Digital Delivery Agency established", 2026. https://www.digital.govt.nz/news/government-digital-delivery-agency-established

[^distfrules]: Digital Identity Services Trust Framework Rules 2024, consolidated version in force from 29 June 2026, rules 8 and 9 and the history of amendments, compiled by the Government Digital Delivery Agency as a reference document; the rules as made are notified in the New Zealand Gazette. https://standards.digital.govt.nz/docref/digital-identity-services-trust-framework-rules-2024/2026-06-29/en/ and https://gdda.govt.nz/trust-framework

[^dciptech]: Government Digital Delivery Agency, "Digital Credentials Technical Guide" and "DCIP Onboarding Guide", Digital Credential Issuance Platform. https://github.com/NZ-Digital-Public-Infrastructure/nz-digital-credential-issuance-platform

[^distfregs]: Digital Identity Services Trust Framework Regulations 2024, SL 2024/197, as amended 28 May 2026, regulations 3, 5, 9, and 13. https://www.legislation.govt.nz/regulation/public/2024/0197/latest/whole.html

[^distfaccred]: Trust Framework Authority, "Accreditation of digital identity providers and services". https://www.publicservice.govt.nz/about-the-commission/government-digital-delivery-agency/trust-framework-for-digital-identity/information-for-providers/accreditation-and-maintenance/accreditation-of-digital-identity-providers-and-services

[^govtapp]: New Zealand Government, "Government app launched today", 10 December 2025. https://www.beehive.govt.nz/release/government-app-launched-today

[^govtwallet]: New Zealand Government, "Digital wallet and credentials", Govt.nz app, page last updated September 2026. https://www.govt.nz/about/the-govt-nz-app/features-and-releases/digital-wallet-and-credentials/

[^govtwalletprivacy]: New Zealand Government, "Privacy and security for your digital wallet", Govt.nz app. https://www.govt.nz/about/the-govt-nz-app/privacy-and-security/privacy-and-security-for-your-digital-wallet/

[^wallettech]: Government Digital Delivery Agency, "Govt.nz app wallet technical guide". https://github.com/NZ-Digital-Public-Infrastructure/govt-nz-app-wallet

[^tfregister]: Trust Framework Authority, "Trust Framework Register", as at 17 September 2026. https://www.publicservice.govt.nz/about-the-commission/government-digital-delivery-agency/trust-framework-for-digital-identity/trust-framework-authority/trust-framework-register

[^nzverify]: New Zealand Government, "What you can do with NZ Verify". https://www.govt.nz/about/nz-verify-app/what-you-can-do-with-nz-verify/

[^nzverifytech]: Government Digital Delivery Agency, "NZ Verify", technical documentation. https://github.com/NZ-Digital-Public-Infrastructure/nz-verify

[^ddl]: New Zealand Government, "Kiwis asked to help shape digital driver licences", 2026. https://www.beehive.govt.nz/release/kiwis-asked-help-shape-digital-driver-licences

[^wsposition]: WorkSafe New Zealand, "The work health and safety information needed before hiring contractors", WorkSafe position, June 2026, page last updated 20 August 2026. https://www.worksafe.govt.nz/laws-and-regulations/operational-policy-framework/worksafe-positions/work-health-safety-info-needed-before-hiring-contractors/ and https://www.worksafe.govt.nz/dmsdocument/72833-the-work-health-and-safety-information-needed-before-hiring-contractors/latest/

[^nzbnact]: New Zealand Business Number Act 2016, 2016 No 16, sections 3, 20 to 29. https://www.legislation.govt.nz/act/public/2016/0016/latest/whole.html

[^mandated]: Government Chief Data Steward, "Mandated data standards register". https://www.data.govt.nz/toolkit/data-standards/mandated-standards-register

[^idstds]: Government Digital Delivery Agency, "Identification Standards", version of 1 May 2026, licensed CC BY 4.0. https://standards.digital.govt.nz/docref/identification-standards/2026-05-01/en/ and https://www.digital.govt.nz/standards-and-guidance/identification-management/

[^idoverview]: Government Digital Delivery Agency, "Overview of the Identification Standards", version of 1 May 2026, roles, tables 1 to 3, and "Updating the standards". https://standards.digital.govt.nz/docref/overview-of-the-identification-standards/2026-05-01/en/

[^idia]: Government Digital Delivery Agency, "Information Assurance Standard", version 3, effective 1 May 2026, objectives 2 to 4; "Binding Assurance Standard" and "Authentication Assurance Standard", version 3, effective 1 May 2026. https://standards.digital.govt.nz/docref/information-assurance-standard/2026-05-01/en/

[^idcs]: Government Digital Delivery Agency, "Credential Service Standard", version 1, effective 1 May 2026, replacing Part 1 of the Federation Assurance Standard, controls FA2.02, FA3.01, FA3.02, FA4.01, FA4.02, and FA5.06 to FA5.08. https://standards.digital.govt.nz/docref/credential-service-standard/2026-05-01/en/

[^idfs]: Government Digital Delivery Agency, "Facilitation Service Standard", version 1, effective 1 May 2026, replacing Parts 2 and 3 of the Federation Assurance Standard, controls FA10.01 to FA10.03, FA11.03, FA11.04, FA11.06, and FA13.02. https://standards.digital.govt.nz/docref/facilitation-service-standard/2026-05-01/en/

[^idloa]: Government Digital Delivery Agency, "Levels of Assurance", version of 1 May 2026. https://standards.digital.govt.nz/docref/levels-of-assurance/2026-05-01/en/

[^idconform]: Government Digital Delivery Agency, "Conforming with the Identification Standards", version of 1 May 2026, "Conformance and mandates" and table 1. https://standards.digital.govt.nz/docref/conforming-with-the-identification-standards/2026-05-01/en/

[^idata]: Government Digital Delivery Agency, "Authority to act for another entity", guidance, version of 2 September 2026. https://standards.digital.govt.nz/docref/authority-to-act-for-another-entity/2026-09-02/en/

[^apistd]: Government Digital Delivery Agency, "API Standard", version of 1 September 2026, sections "About this Standard", "Scope", and the requirements on TLS, OAuth 2.1, versioning, and interface specifications. https://standards.digital.govt.nz/docref/api-standard/2026-09-01/en/
