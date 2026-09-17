# OpenAssurance Standards Map: Organisations

**Part of:** `standards-map.md`  
**Status:** Working draft, Phase 2  
**Last reviewed:** September 2026

## 1. Purpose

This part of the standards map assesses what exists for describing an organisation's prequalification and assurance.

No international data standard for contractor prequalification was found, and none was expected.

What exists in New Zealand is a regulator's position and template, an industry cross-recognition scheme, a number of commercial schemes, and a set of certifications and accreditations that buyers already accept.

Together they define the content OpenPrequal must be able to carry.

The positions used here are defined in `standards-map.md` section 3, and the method in its section 4.

## 2. WorkSafe New Zealand's position and template

**Position: Reference, as the alignment target for OpenPrequal evidence categories.**

WorkSafe New Zealand's position statement, *The work health and safety information needed before hiring contractors*, states that WorkSafe expects a hiring business to request health and safety information from a contractor before engagement, that a formal prequalification process is one way of doing so, and that prequalification is not compulsory.[^wsposition]

It requires the amount of detail sought to be proportionate to the size, complexity, and risk of the work.

It notes that prequalification may be done "either through a formally recognised provider or through a simple conversation".

Alongside it, WorkSafe published a form titled *Risk-based health and safety pre-qualification information*, described as a template that "is not a checklist" and is intended to help small businesses bring together examples of their practice.[^wstemplate]

The template covers twelve topics.

1. business information;
2. key personnel;
3. sub-contractors;
4. associations, memberships, and competent advice and assessments;
5. health and safety record and regulator interventions over the last five years;
6. policy and procedures;
7. hazard identification and risk assessment;
8. worker engagement, participation, representation, and communication;
9. information, training, and supervision;
10. coordination;
11. emergency procedures and planning;
12. checking, investigating, and improving health and safety.

The Minister for Workplace Relations and Safety announced both documents on 20 August 2026, citing "a lack of consistency and duplication within New Zealand's prequalification systems", one submitter who had completed 76 prequalifications in a year, and an expectation that the template would be useful across government procurement so that "businesses do not need to complete multiple forms to 'prequalify' for working with different agencies".[^beehive2026]

An earlier announcement of 28 July 2025 had directed WorkSafe to revise its prequalification guidance, "including developing free-to-use templates to improve national consistency", and asked for an Approved Code of Practice on overlapping duties.[^beehive2025]

The template is a PDF form.

It defines no data format and says nothing about digital exchange, and WorkSafe states that it "does not manage how this template is used or see any user details".

That is exactly the point at which OpenPrequal can contribute.

OpenPrequal's evidence categories should map one-to-one onto the twelve topics, so that a supplier whose records are organised for OpenPrequal can answer the template, and a buyer who uses the template can receive the answer as verifiable records.

The topics are those of the July 2026 form, and the mapping is revised if the form is.

That is an alignment, not a dependency, and `standards-map.md` section 7.10 explains the difference.

## 3. An industry cross-recognition scheme

**Position: Reference, as an existing recognition arrangement OpenPrequal must be able to carry.**

Tōtika is a health and safety prequalification cross-recognition scheme governed by the board of trustees of Construction Health and Safety New Zealand, an industry-led charitable trust.[^totikarules][^chasnz]

Its published scheme rules describe a common standard for prequalification assessment, a register of assessed suppliers, cross-recognition of external audit effort, and a common supplier classification.

Several features are directly relevant to how OpenPrequal records should be modelled.

- suppliers are classified into a sole-trader category and three further categories by headcount, contract value, and whether their primary activity is on a high-risk or very-high-risk list;
- assessments are conducted by independently audited member schemes, which may be commercial or non-commercial, against a published core criteria and assessment standard;[^totikacore]
- a supplier's listing carries a status of performing or developing and a percentage score, and expires after one year, or two years for the smaller categories;
- external certifications are cross-recognised as an alternative to assessment where they are an ISO or New Zealand standard, or a scheme endorsed by a New Zealand regulator;
- uploaded certificates are checked for validity directly with the certifying body, and expired certificates cause the listing to lapse;
- buyers retain the right to use suppliers who are not listed;
- personal information not needed for assessment is to be removed from evidence before it is submitted.

Each of these has an OpenAssurance counterpart.

A member scheme's assessment is an Assessment record issued by that scheme, with category, status, score, and validity as claims.

The scheme's acceptance of a certification standard for a category is an Endorsement with a scope.

A buyer's requirement that suppliers hold a listing at a given category is a Requirement record.

The register is a Host and Holder of records that other parties issued, and holding them does not make it their issuer.

The manual check of an uploaded certificate against the certifying body is the authenticity and currency question that a signed record with a status list answers automatically.

The instruction to remove unneeded personal information is the minimum-disclosure principle applied to organisation evidence.

Two things should be said plainly.

OpenPrequal does not propose to replace this or any other scheme, and the Charter's non-goals exclude it from doing so.

Its proposal is that the records such a scheme produces, and the evidence its suppliers hold, should be portable and independently verifiable, so that a listing on one register can be presented to a buyer who uses another, and so that a certificate need not be re-verified by hand at every register that receives it.

## 4. Common questionnaire content

Prequalification questionnaires in commercial use in New Zealand were reviewed as background, and are not named here in keeping with the neutrality rule in `CONTRIBUTING.md`.

Their content overlaps heavily with the WorkSafe template and the cross-recognition scheme's core criteria.

The information categories that recur across all of them are:

- organisation details, size, and category;
- insurance, evidenced by certificates of currency;
- health and safety policy and procedures, or an external certification in their place;
- leadership and commitment;
- hazard and risk identification and controls, including a risk register and high-risk work;
- training, competency, and supervision, including a training register;
- incident and near-miss reporting, recording, and investigation;
- emergency management;
- worker engagement, participation, and communication;
- health monitoring and wellbeing;
- inspections and checking;
- subcontractor management;
- plant and equipment;
- hazardous substances;
- health and safety performance history and regulator interventions;
- declarations.

Three modelling conventions also recur.

- assessment results are expressed as a percentage score and a tier;
- validity periods are tiered by score or by category, from six months to two years;
- sharing of a result with more than one client is offered within a scheme's own platform.

The last convention is the structural problem the Charter describes, and it is stated here without attribution because every scheme reviewed shares it.

## 5. Certifications and accreditations buyers already accept

**Position: Reference.**

Several certification and accreditation outcomes are already accepted by buyers and by the cross-recognition scheme as evidence of a health and safety system.

- ISO 45001 certification, where the certifier is accredited by a member of the International Accreditation Forum;
- NZS 7901 certification of safety management systems for public safety in the electricity and gas industries;[^nzs7901]
- a SafePlus onsite assessment, the joint programme of WorkSafe, ACC, and the Ministry of Business, Innovation and Employment;[^safeplus]
- accreditation under the ACC Accredited Employers Programme;
- a Maritime Operator Safety System audit under Maritime New Zealand.

Each is an Assessment record whose issuer is the certifier, assessor, or regulator, and whose currency is defined by its own audit cycle.

Accreditation of the certifier, by JAS-ANZ or another accreditation body, is an Endorsement of the issuer that a relying organisation may require.

OpenPrequal needs to be able to carry these as records with their original issuer visible.

It does not need to define any of them.

## 6. Insurance

**Position: define, as a small record type.**

No New Zealand open data standard for a certificate of currency was identified.

Insurers and brokers issue certificates as documents, and buyers verify them by inspection or by contacting the insurer.

An insurance record in OpenPrequal is an ordinary credential issued by the insurer or broker about the insured organisation, carrying policy type, insured party, limit, period, and a hash-linked copy of the certificate through `relatedResource`.

Whether insurers will issue such records is a question for Phase 1 engagement.

Until they do, a supplier's hosted service may hold the certificate as Evidence with the insurer identified as the source, which is weaker but honest about who asserted what.

## 7. Declarations

A declaration is a signed statement by the supplier about itself, such as a statement that it has no undisclosed regulator interventions.

It is an Attestation whose issuer and subject are the same organisation.

The data model represents that without difficulty.

What the organisation's signature does not show is who inside the organisation made the statement, whether they held the role they claim, and whether they approved these exact words.

**Position: Reference the Companies Register; define the evidence structure.**

The Companies Register publishes, for every company role, the type of role, its status as current or ceased, the person's full legal name, and the appointment and cessation dates.[^coroles]

The data is available through search, bulk data, and APIs, most of them free of charge.[^coapis]

That is enough for anyone to check, without asking permission, that a person of a given name was a director of a given company on a given date, including a date in the past.

It is a name match and no more, because addresses and dates of birth are restricted.

The government wallet documentation lists proof of role in a public register, and delegated authority, among the credential types it expects to hold, which would be the stronger form of the same evidence.[^wallettech]

The exchange model uses the register check as the floor for a declarant's authority, keeps the person's approval of the exact statement as separate evidence, reports both apart from the signature, and records the choice as decision D10 in `decisions.md`.

## 8. What OpenPrequal has to define

`standards-map.md` section 7 collects the gaps.

For organisations, the genuinely new content is a small vocabulary that:

- names the evidence categories, aligned to the WorkSafe template topics;
- separates supplier evidence from an assessor's assessment of it, as the profile already requires;
- expresses an assessment result with category, status, score, and validity in a scheme-neutral way, and a determination and finding for each requirement assessed;
- expresses a buyer requirement as a statement of what is expected, with non-exclusive examples of evidence, keeping what a system checks to objective criteria such as accepted assessments, certifications, endorsements, thresholds, and currency;
- carries a corrective action request and its closure as records the supplier can hold and present, and a recommendation as a note that fails nothing and does not travel;
- lets a supplier present an assessor's current conclusion to another buyer without the history behind it, with any outstanding corrective action stated inside the record the assessor signed;
- lets a buyer ask with a small signed request that pins the exact version of the requirements it refers to, and lets the supplier map what it presents to the requirements it is offered against.

The last of these borrows its terms from established audit practice.

Guidance on auditing management systems records findings of conformity and nonconformity and notes opportunities for improvement, the occupational health and safety management standard requires a nonconformity to be answered with corrective action, and the requirements for certification bodies distinguish major from minor nonconformities.[^iso19011][^iso45001][^iso17021]

Those are standards for how audits are conducted and not data formats, so OpenPrequal defines the record and takes the words from them.

The cross-recognition scheme in section 3 already requires a member scheme to tell a supplier that falls short how to improve, and nothing today lets the supplier carry that finding, or its resolution, to the next buyer.[^totikarules]

None of this replaces any scheme's methodology, scoring, or criteria, which remain the scheme's own.

## 9. Sources

Every status and date in this part was checked against the source listed in September 2026.

References to external organisations, schemes, and government publications are provided as evidence of what exists. No such reference implies consultation, participation, support, or endorsement.

[^wsposition]: WorkSafe New Zealand, "The work health and safety information needed before hiring contractors", WorkSafe position, June 2026, page last updated 20 August 2026. https://www.worksafe.govt.nz/laws-and-regulations/operational-policy-framework/worksafe-positions/work-health-safety-info-needed-before-hiring-contractors/ and https://www.worksafe.govt.nz/dmsdocument/72833-the-work-health-and-safety-information-needed-before-hiring-contractors/latest/

[^wstemplate]: WorkSafe New Zealand, "Risk-based health and safety pre-qualification information", form, 2026. https://www.worksafe.govt.nz/dmsdocument/73194-risk-based-health-and-safety-pre-qualification-information-template/latest/

[^beehive2026]: New Zealand Government, "New template to simplify prequalification process", 20 August 2026. https://www.beehive.govt.nz/release/new-template-simplify-prequalification-process

[^beehive2025]: New Zealand Government, "Clearer rules and prequalification guidance to support construction", 28 July 2025. https://www.beehive.govt.nz/release/clearer-rules-and-prequalification-guidance-support-construction

[^totikarules]: Tōtika, "Scheme Rules", version 3.3.9, 2 December 2024. https://www.totika.org/resources/totika-scheme-rules-v3.3.9.pdf

[^chasnz]: Construction Health and Safety New Zealand, "About". https://www.chasnz.org/about

[^totikacore]: Tōtika, "Core Criteria and Assessment Standard", version 3.1.4, 10 December 2024. https://www.totika.org/resources/totika-core-criteria-and-assessment-standard-v3.1.4.pdf

[^nzs7901]: Standards New Zealand, NZS 7901:2014, "Electricity and gas industries — Safety management systems for public safety". https://www.standards.govt.nz/shop/nzs-79012014/

[^safeplus]: WorkSafe New Zealand, "About SafePlus", a joint programme of WorkSafe New Zealand, ACC, and the Ministry of Business, Innovation and Employment. https://www.worksafe.govt.nz/managing-health-and-safety/businesses/safeplus/about-safeplus/

[^coroles]: New Zealand Companies Office, "Roles", available data. https://www.companiesoffice.govt.nz/data-services/available-data/roles/

[^coapis]: New Zealand Companies Office, "Using our data through APIs". https://www.companiesoffice.govt.nz/data-services/ways-to-get-our-data/using-our-data-through-apis/

[^wallettech]: Government Digital Delivery Agency, "Govt.nz app wallet technical guide". https://github.com/NZ-Digital-Public-Infrastructure/govt-nz-app-wallet

[^iso19011]: ISO 19011:2026, "Guidelines for auditing management systems", which replaced the 2018 edition. https://www.iso.org/standard/19011

[^iso45001]: ISO 45001:2018, "Occupational health and safety management systems — Requirements with guidance for use", confirmed 2024, with a revision in draft. https://www.iso.org/standard/63787.html

[^iso17021]: ISO/IEC 17021-1:2015, "Conformity assessment — Requirements for bodies providing audit and certification of management systems — Part 1: Requirements". https://www.iso.org/standard/61651.html
