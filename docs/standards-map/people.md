# OpenAssurance Standards Map: People

**Part of:** `standards-map.md`  
**Status:** Working draft, Phase 2  
**Last reviewed:** September 2026

## 1. Purpose

This part of the standards map assesses the vocabularies, identifiers, and registers that describe what a person's record means.

The data model says how a record is structured.

It does not say what a qualification, a licence, a practical competency, or an employer attestation *is*, and that is what OpenCompetency has to settle.

The positions used here are defined in `standards-map.md` section 3, and the method in its section 4.

## 2. Open Badges 3.0

**Position: Profile, as the base vocabulary for achievement records.**

Open Badges Specification 3.0 reached Final Release on 17 June 2024 and is maintained by the 1EdTech Consortium, with errata revisions continuing through June 2026.[^ob3]

It is a profile of the W3C Verifiable Credentials Data Model 2.0, so an Open Badges credential is a W3C credential with a defined vocabulary inside it.

Its achievement type vocabulary already includes the types OpenCompetency needs.

- Certification;
- License;
- Competency;
- Assessment;
- Course and CertificateOfCompletion;
- MicroCredential;
- Membership;
- LearningProgram.

The vocabulary is extensible, so a workplace-specific type can be added without breaking conforming readers.[^ob3type]

The achievement subject can carry a licence number, a role, a term, activity start and end dates, a result, and a source, which between them cover most of what a licence, training, or assessment record needs.[^ob3subject]

An achievement definition can be aligned to an external framework by name, URL, and code, which is how a record will point at a New Zealand standard or qualification identifier.[^ob3align]

Evidence is described by URL and narrative; the class has no hash property, so hash-linking a document should use the data model's `relatedResource` instead.[^ob3evidence][^vcrelres]

Open Badges 3.0 also defines its own JSON Web Token proof format, which requires RS256 as a minimum, permits a `typ` of `JWT` only, and carries validity in the `nbf` and `exp` claims.[^ob3jwt]

That differs from the envelope in `credential-layer.md` section 3.1, and the exchange model records how the two are reconciled for now and why the question needs settling by implementation.

The specification is licensed for implementation by anyone on a royalty-free basis, and does not require membership to implement.[^ob3licence]

Formal conformance certification is a separate programme that does require 1EdTech membership, and OpenAssurance conformance must not depend on it.[^ob3cert]

That passes both halves of the openness test, provided the profile relies on the specification and not on the certification programme.

## 3. Comprehensive Learner Record 2.0

**Position: Evaluate.**

CLR 2.0 reached Final Release on 26 February 2025 and wraps many achievement credentials from many issuers into one signed record about one person, preserving each inner credential's issuer signature.[^clr2]

That is close to what an employer's competency system holds for a worker.

A verifiable presentation already does the same job for a single exchange, and OpenCompetency's privacy principles favour presenting a few records over exporting a whole record.

CLR should be evaluated for bulk transfer when a worker changes employer or an employer changes system, and not used for day-to-day presentation.

## 4. Credential Transparency Description Language

**Position: Evaluate, for describing credential types and requirements.**

CTDL is an openly licensed vocabulary for describing credentials, organisations, competencies, assessments, and the conditions attached to them, maintained by Credential Engine and released under a Creative Commons Attribution licence.[^ctdl][^ctdllicence]

It describes what a credential *is* and what its holder had to satisfy to get it.

It explicitly places the description of a credential *awarded* to a person outside its scope, so it complements rather than competes with Open Badges.[^ctdlscope]

Two features matter for OpenAssurance.

- Open Badges alignment targets already include CTDL competencies and credentials, so the two vocabularies are designed to be used together;[^ob3aligntype]
- its condition profile is the only published data model found for stating that one thing requires another, with alternatives, experience, and jurisdiction, and `recognition-and-requirements.md` section 3 identified requirement expression as a gap.[^ctdlcond]

Use of CTDL outside the United States could not be confirmed from primary sources, and the registry that surrounds it is not something OpenAssurance should depend on.

The vocabulary should be evaluated on its own, as a source of terms for issuer-published credential descriptions and for the Requirement record.

## 5. Schema.org

**Position: Reference.**

Schema.org provides lightweight web vocabulary that search engines and ordinary websites understand.[^schemaorg]

`EducationalOccupationalCredential` describes a credential definition, `Occupation` describes an occupation and its requirements, and `Certification`, added in 2024, describes an issued certification about a person, product, or organisation with issuer, status, and expiry.[^schemacert]

None of these carries proof, status, or holder binding, so none is a substitute for a verifiable credential.

They are the right vocabulary for an issuer's public web page describing what it issues, and for a hosted service's public listing of an organisation's certifications where the organisation chooses to publish one.

## 6. New Zealand credential schemas

**Position: Evaluate, pending answers on openness.**

Five credential schemas for induction, course, licence, qualification, and assessment records are published at https://credentialschema.nz, expressed on the W3C data model in JSON.

The landscape document already records the two questions that must be answered before any published schema is adopted: whether the schema itself may be implemented by anyone, and whether the tooling around it is available on open terms.

At the time of writing, the site states no licence terms for the schemas and describes no governance or change process.

Neither question can be answered from the published material alone, and both should be put to the publisher.

If the schemas are openly licensed and their maintenance is open to participation, OpenCompetency should prefer to align field names with them rather than diverge.

If they are not, OpenCompetency should define its own on the Open Badges base and should not create a competing namespace for its own sake.

That position is the one the landscape document already takes, restated for this phase.

## 7. New Zealand qualification and standard identifiers

**Position: Adopt as alignment targets.**

The New Zealand Qualifications and Credentials Framework has ten levels and lists qualifications, micro-credentials, and the standards that make them up.[^nzqcf]

Standards are the building blocks: achievement standards listed by the Ministry of Education, and unit standards and skill standards listed by industry standard-setting bodies, with skill standards progressively replacing unit standards.[^nzqastandards][^nzqaguidelines][^dassrules]

Each standard has a numeric identifier and a version number, and a listing status of current, expiring, or discontinued.[^dassrules]

Each qualification has a reference number, and each micro-credential a framework number.[^nzqasearch]

These identifiers are stable, public, and already used on every certificate and transcript in the country.

An OpenCompetency record that asserts a New Zealand standard, qualification, or micro-credential should align to it by that identifier and version, using the Open Badges alignment mechanism, and should not restate what the standard says.

The framework recognises eleven credential types: certificate, diploma, graduate certificate, graduate diploma, bachelor's degree, bachelor honours degree, postgraduate certificate, postgraduate diploma, master's degree, doctoral degree, and micro-credential, and one credit represents ten notional hours of learning and assessment.[^nzqatypes]

Those attributes map onto the Open Badges achievement definition without invention: the credential type onto the achievement type, credits onto the credits available, and the framework number, version, and level onto an alignment whose target framework is the New Zealand framework.[^ob3type][^ob3align]

The profile should publish that mapping once, so that every issuer describes a New Zealand qualification the same way.

Industry standard-setting moved on 1 January 2026 from Workforce Development Councils to eight Industry Skills Boards established under the Education and Training (Vocational Education and Training System) Amendment Act 2025, with the councils to be disestablished by the end of 2026.[^isbact][^isbs]

Standard identifiers survive that change, which is one reason to align to identifiers rather than to the bodies that issue them.

No public machine-readable register or API of the framework was found.

The framework is searchable on the web, per-standard documents are downloadable, and two static snapshots of the standards list were published as open data in 2019 and 2020.[^nzqaopendata]

That is a question for the New Zealand Qualifications Authority in `decisions.md` section 3, and not a reason to build a mirror.

## 8. The New Zealand Record of Achievement

**Position: Reference.**

The Record of Achievement is the official transcript of a person's New Zealand qualifications, micro-credentials, and standards as reported by education providers.[^nzroa]

A digital copy is available to the learner as a PDF, and anyone holding the original can verify it through an online tool.[^nzroaverify]

The same service verifies two other Authority documents: the International Qualification Assessment, which states how an overseas qualification compares with the New Zealand framework, and the Overseas Study Assessment.[^nzqaverifydocs]

Verification works by uploading the unmodified original PDF, with its original filename, and the tool responds at once.[^nzqaverifydocs]

That is verification by the issuer's service rather than against a published key: it is independent of any platform, but not of the Authority's tool remaining available.

The mechanism behind the tool is not described publicly, and no publication by the Authority on verifiable credentials or Open Badges was found.

Two consequences follow for OpenCompetency.

An Evidence record that hash-links the unmodified original preserves exactly the property the tool depends on, so a holder's copy can be re-verified at the Authority at any time by anyone the holder shares it with.

The International Qualification Assessment is, in OpenAssurance terms, an Assessment issued by the Authority about an overseas qualification, and it is the authoritative record for a migrant worker whose qualification was gained abroad.

**University qualifications.**

**Position: Reference.**

For university qualifications, the Authority points verifiers to My eQuals and to the university itself.[^nzqacheck]

My eQuals is the tertiary credentials service for Australia and New Zealand, governed and operated by the participating education providers through a not-for-profit subsidiary of Universities Australia, and used by all public universities in both countries.[^myequals]

A graduate shares a document by a secure link or as a cryptographically signed PDF, and verification is free for the receiving organisation.[^myequalsverify]

The service runs on a commercial platform, which is not named here, and the link-sharing route is mediated by that platform.

The signed PDF is not: it carries the university's own signature and can be checked with ordinary document tooling by anyone who holds it.

That makes a New Zealand university qualification the clearest existing case in the country of an issuer-signed, holder-controlled, independently verifiable record, in document form rather than as structured data.

OpenCompetency should carry such a document as an issuer-signed document under `credential-layer.md` section 2.5, with the university as the source, and should not expect universities to re-issue what they already sign.

For OpenCompetency, the Record of Achievement is the authoritative source for formal achievements, and the Authority is their issuer.

A worker or employer may hold and present verified qualification evidence derived from it, with the Authority identified as the original issuer, which is what the landscape document already requires.

Whether the Authority will issue achievements as verifiable credentials is its decision, and `decisions.md` section 3 records the question.

## 9. Occupational licences and public registers

**Position: Reference, as authoritative currency sources.**

Many New Zealand occupational licences have a public online register operated by the regulator that an employer can search.

- electrical workers, searchable by name and licence type, showing whether a person is registered and licensed, with a digital licence that links by QR code to the register;[^ewrb]
- plumbers, gasfitters, and drainlayers, showing registration and licence status, conditions, and recent disciplinary history;[^pgdb]
- licensed building practitioners, searchable by name or practitioner number, showing licence class, status, and history under the Building Act 2004;[^lbp]
- health practitioners under the Health Practitioners Competence Assurance Act 2003, whose registers must record whether a practitioner holds a current practising certificate;[^hpca]
- asbestos removal and assessor licences, showing current, renewal in progress, suspended, expired, or cancelled status;[^asbestos]
- seafarer certificates, verifiable by certificate number.[^seacert]

Each register is a web page for a person to look at.

None offers a documented API, and each uses its own status vocabulary.

Some safety-critical competencies have no public register at all, and verification depends on the holder's consent or on contacting the issuer.

- certified handlers of hazardous substances are certified by compliance certifiers, and no public register of handlers exists;[^handlers]
- extractives certificates of competence are verified by the holder or employer writing to the Board of Examiners secretariat;[^extractives]
- aviation licences are verified by a letter the holder requests;[^caa]
- crane operation has no licence regime, and the approved code of practice describes unit standards as one way of demonstrating competency rather than a requirement.[^cranes]

Three conclusions follow.

Where a register exists, it is the source of truth for currency, and an OpenCompetency record asserting that licence should cite the register rather than claim to replace it.

Because status vocabularies differ by regime, the profile needs a small mapping from each regime's states onto the OpenAssurance notion of current, and should not impose one enumeration on regulators.

Where no register exists, a holder-presented, issuer-signed record with a status list is a strict improvement on the present position, and those regimes are where OpenCompetency's value is most immediate.

## 10. Driver licences

**Position: Reference.**

Driver licences have six classes and nine endorsements, and a card carries a licence number that stays the same across renewals and a version number that changes with each card.[^nztaclasses][^nztaexplained]

The licence number is a government identifier issued for one purpose, and `credential-layer.md` section 4 rules it out as a subject identifier.

The Driver Licence Register is the national record, and employers may use a free service, with the driver's signed consent, to see classes, endorsements, conditions, and whether the licence is current, disqualified, suspended, revoked, or expired.[^dlr][^drivercheck]

Digital driver licences are now recognised in law, and the implementing rules were consulted on in mid-2026.[^ddlact][^ddl]

The government's issuance platform already lists the ISO/IEC 18013-5 mobile driving licence among the document types it issues.[^dciptech]

That is the clearest case of a government-issued credential that a relying organisation will receive as an mdoc, and it is the reason `credential-layer.md` section 2 expects a verifier that handles government-issued credentials to accept that format.

## 11. Occupation classification

**Position: Reference, optional.**

Stats New Zealand now maintains the National Occupation List, an independent New Zealand-focused occupation classification developed after joint custodianship of the Australian and New Zealand classification ended, with version 3.0 released on 1 January 2026 and concordances to the former classification and to ISCO-08.[^nol]

Where a Requirement record or an attestation names a role, the classification is a useful optional tag.

It should never be required, because most workplace roles are defined locally and more narrowly than any classification.

No New Zealand skills taxonomy was found.

## 12. Adoption elsewhere

No adoption of Open Badges, the Comprehensive Learner Record, or CTDL by a New Zealand government body was found.

Australia's proposed National Skills Passport reached a business-case stage in 2024, and no decision on it could be confirmed from official sources.[^skillspassport]

New South Wales issues an optional digital high-risk work licence with a public check by name or licence number, which is the closest operating example of a portable workplace licence in the region.[^nswhrwl]

None of this changes the positions above.

It confirms that OpenCompetency would not be duplicating a government programme, and that the vocabulary gap in `standards-map.md` section 7 is real.

## 13. Sources

Every status and date in this part was checked against the source listed in September 2026.

References to external organisations, schemes, and government publications are provided as evidence of what exists. No such reference implies consultation, participation, support, or endorsement.

[^ob3]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", Final Release, 17 June 2024, with errata to revision 1.6 of 29 June 2026. https://www.imsglobal.org/spec/ob/v3p0/

[^ob3type]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", AchievementType enumeration. https://www.imsglobal.org/spec/ob/v3p0/#achievementtype-enumeration

[^ob3subject]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", AchievementSubject. https://www.imsglobal.org/spec/ob/v3p0/#achievementsubject

[^ob3align]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", Alignment. https://www.imsglobal.org/spec/ob/v3p0/#alignment

[^ob3evidence]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", Evidence. https://www.imsglobal.org/spec/ob/v3p0/#evidence

[^vcrelres]: W3C, "Verifiable Credentials Data Model v2.0", section 5.3, Integrity of Related Resources. https://www.w3.org/TR/vc-data-model-2.0/#integrity-of-related-resources

[^ob3jwt]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", section 8.2, JSON Web Token Proof Format. https://www.imsglobal.org/spec/ob/v3p0/

[^ob3licence]: 1EdTech Consortium, "Specification Document License". https://www.1edtech.org/standards/specification-license

[^ob3cert]: 1EdTech Consortium, "Open Badges 3.0 Specification Conformance and Certification Guide", version 1.5, 15 June 2026. https://www.imsglobal.org/spec/ob/v3p0/cert/

[^clr2]: 1EdTech Consortium, "Comprehensive Learner Record Standard, Version 2.0", Final Release, 26 February 2025. https://www.imsglobal.org/spec/clr/v2p0/

[^ctdl]: Credential Engine, "Credential Transparency Description Language (CTDL) Handbook", schema release 28 August 2026. https://credreg.net/ctdl/handbook

[^ctdllicence]: Credential Engine, CTDL licensing statement, Creative Commons Attribution 4.0 International. https://credreg.net/ctdl/handbook

[^ctdlscope]: Credential Engine, "CTDL Handbook", scope statement placing description of credentials awarded to a person outside the language. https://credreg.net/ctdl/handbook

[^ob3aligntype]: 1EdTech Consortium, "Open Badges Specification, Version 3.0", AlignmentTargetType enumeration. https://www.imsglobal.org/spec/ob/v3p0/#alignmenttargettype-enumeration

[^ctdlcond]: Credential Engine, "CTDL Terms", ConditionProfile. https://credreg.net/ctdl/terms

[^schemaorg]: Schema.org, release history, version 30.1, 16 September 2026. https://schema.org/docs/releases.html

[^schemacert]: Schema.org, "Certification", added in release 25.0, 22 January 2024. https://schema.org/Certification

[^nzqcf]: New Zealand Qualifications Authority, "About the New Zealand Qualifications and Credentials Framework". https://www2.nzqa.govt.nz/qualifications-and-standards/about-new-zealand-qualifications-credentials-framework/

[^nzqastandards]: New Zealand Qualifications Authority, "About standards". https://www2.nzqa.govt.nz/qualifications-and-standards/about-standards/

[^nzqaguidelines]: New Zealand Qualifications Authority, "Guidelines for listing standards and consent and moderation requirements". https://www2.nzqa.govt.nz/tertiary/approval-accreditation-and-registration/listing-standards-and-cmrs/guidelines/

[^dassrules]: New Zealand Qualifications Authority, "Directory of Assessment and Skill Standards Listing and Operational Rules 2026", in force 19 January 2026. https://www2.nzqa.govt.nz/about-us/rules-fees-policies/nzqa-rules/dass-rules/

[^nzqasearch]: New Zealand Qualifications Authority, framework search for standards, qualifications, and micro-credentials. https://www.nzqa.govt.nz/framework/search/index.do

[^nzqatypes]: New Zealand Qualifications Authority, "About qualifications and credentials". https://www2.nzqa.govt.nz/qualifications-and-standards/about-qualifications-and-credentials/

[^isbact]: Education and Training (Vocational Education and Training System) Amendment Act 2025, 2025 No 56, and Schedule 6 clause 183. https://www.legislation.govt.nz/act/public/2025/0056/latest/whole.html

[^isbs]: Ministry of Education, "Redesign of the vocational education and training system". https://www.education.govt.nz/our-work/strategies-policies-and-programmes/tertiary-and-further-education/redesign-vocational-education-and-training-system

[^nzqaopendata]: New Zealand Qualifications Authority, "List of Standards by Category", open data snapshots 2019 and 2020, data.govt.nz. https://catalogue.data.govt.nz/api/3/action/package_search?q=organization:new-zealand-qualifications-authority

[^nzroa]: New Zealand Qualifications Authority, "New Zealand Record of Achievement". https://www2.nzqa.govt.nz/qualifications-and-standards/access-your-results/new-zealand-record-of-achievement/

[^nzroaverify]: New Zealand Qualifications Authority, "Verify a New Zealand Record of Achievement". https://www2.nzqa.govt.nz/qualifications-and-standards/access-your-results/verify/

[^nzqaverifydocs]: New Zealand Qualifications Authority, "Verify NZQA documents", covering the Record of Achievement, the International Qualification Assessment, and the Overseas Study Assessment. https://www2.nzqa.govt.nz/international/check-qual/verify-nzqa-docs/

[^nzqacheck]: New Zealand Qualifications Authority, "Check a New Zealand qualification". https://www2.nzqa.govt.nz/international/check-qual/check-nz-qual/

[^myequals]: My eQuals, "About". https://myequals.org/about/

[^myequalsverify]: My eQuals, "Verifiers". https://myequals.org/verifiers/

[^ewrb]: Electrical Workers Registration Board, public register search and licence identification. https://kete.mbie.govt.nz/EW/EWPRSearch/ and https://www.ewrb.govt.nz/licences/licence-information/licence-ids/

[^pgdb]: Plumbers, Gasfitters, and Drainlayers Board, "Public register policy". https://www.pgdb.co.nz/media/2vgdigsd/public-register-policy.pdf

[^lbp]: Ministry of Business, Innovation and Employment, Licensed Building Practitioners register search; Building Act 2004, sections 298 to 309. https://kete-lbp.mbie.govt.nz/advanced-building-practitioner-search/

[^hpca]: Health Practitioners Competence Assurance Act 2003, sections 136 to 150. https://www.legislation.govt.nz/act/public/2003/0048/latest/whole.html

[^asbestos]: WorkSafe New Zealand, "Licence holder register", asbestos. https://www.worksafe.govt.nz/topic-and-industry/asbestos/licensing/licence-holder-register/

[^seacert]: Maritime New Zealand, seafarer certificate verification. https://services.maritimenz.govt.nz/seacert-search/default.aspx

[^handlers]: WorkSafe New Zealand, "Certified handlers". https://www.worksafe.govt.nz/topic-and-industry/hazardous-substances/certification-authorisation-approvals-and-licensing/certification-of-people/certified-handlers/

[^extractives]: WorkSafe New Zealand, "Verify certificate of competence information", extractives. https://www.worksafe.govt.nz/topic-and-industry/extractives/cocs-and-cpd/verify-certificate-of-competence-information/

[^caa]: Civil Aviation Authority of New Zealand, form CAA603, "Application for licence verification of occurrences", August 2025. https://www.aviation.govt.nz/assets/forms/CAA603-App-for-licence-verification-of-occurrences.pdf

[^cranes]: WorkSafe New Zealand, "Approved Code of Practice for Cranes". https://www.worksafe.govt.nz/dmsdocument/410-approved-code-of-practice-for-cranes-cranes-1.pdf

[^nztaclasses]: NZ Transport Agency Waka Kotahi, "Factsheet 11: Driver licence classes", August 2026. https://www.nzta.govt.nz/assets/resources/factsheets/11/docs/11-driver-licence-classes.pdf

[^nztaexplained]: NZ Transport Agency Waka Kotahi, "Your driver licence explained". https://www.nzta.govt.nz/driver-licences/getting-a-licence/your-driver-licence-explained

[^dlr]: NZ Transport Agency Waka Kotahi, "The Driver Licence Register". https://www.nzta.govt.nz/driver-licences/the-driver-licence-register

[^drivercheck]: NZ Transport Agency Waka Kotahi, "About Driver Check". https://www.nzta.govt.nz/driver-licences/driver-check/about-driver-check

[^ddlact]: Regulatory Systems (Transport) Amendment Act 2026, 2026 No 21. https://www.legislation.govt.nz/act/public/2026/21/en/latest/

[^ddl]: New Zealand Government, "Kiwis asked to help shape digital driver licences", 2026. https://www.beehive.govt.nz/release/kiwis-asked-help-shape-digital-driver-licences

[^dciptech]: Government Digital Delivery Agency, "Digital Credentials Technical Guide" and "DCIP Onboarding Guide", Digital Credential Issuance Platform. https://github.com/NZ-Digital-Public-Infrastructure/nz-digital-credential-issuance-platform

[^nol]: Stats NZ, "About the National Occupation List". https://www.stats.govt.nz/methods/about-the-national-occupation-list/

[^skillspassport]: Australian Government Department of Education, "National Skills Passport consultation". https://www.education.gov.au/national-skills-passport-consultation

[^nswhrwl]: SafeWork NSW, "High risk work licences", and Service NSW, "Check a high risk work licence". https://www.safework.nsw.gov.au/licences-and-registrations/licences/high-risk-work-licences and https://www.service.nsw.gov.au/transaction/check-a-high-risk-work-licence
