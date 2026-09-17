# OpenAssurance Standards Map: New Zealand Context

**Part of:** `standards-map.md`  
**Status:** Working draft, Phase 2  
**Last reviewed:** September 2026

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

## 8. Sources

Every status and date in this part was checked against the source listed in September 2026.

References to external organisations, schemes, and government publications are provided as evidence of what exists. No such reference implies consultation, participation, support, or endorsement.

[^ipp3a]: Privacy Amendment Act 2025, 2025 No 53, Part 1, inserting Information Privacy Principle 3A with effect from 1 May 2026. https://www.legislation.govt.nz/act/public/2025/0053/latest/whole.html

[^ipp13]: Office of the Privacy Commissioner, "Principle 13: Unique identifiers". https://www.privacy.org.nz/privacy-principles/13/

[^piatoolkit]: Office of the Privacy Commissioner, "Privacy Impact Assessments", toolkit revised 2024. https://www.privacy.org.nz/responsibilities/privacy-impact-assessments/

[^distfact]: Digital Identity Services Trust Framework Act 2023, 2023 No 13, sections 3, 8, 10, 15, 18 to 23, 34, 43, and 58. https://www.legislation.govt.nz/act/public/2023/0013/latest/whole.html

[^gdda]: Government Digital Delivery Agency, "Government Digital Delivery Agency established", 2026. https://www.digital.govt.nz/news/government-digital-delivery-agency-established

[^distfrules]: Digital Identity Services Trust Framework Rules 2024, version 2, 24 July 2025, rules 8 and 9, as mirrored on the government standards site; consolidated rules of 29 June 2026 published by the Government Digital Delivery Agency. https://standards.digital.govt.nz/nz/dia-distfr/2/en/ and https://www.publicservice.govt.nz/about-the-commission/government-digital-delivery-agency/trust-framework-for-digital-identity/about-digital-identity-services/trust-framework-legislation/trust-framework-rules

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
