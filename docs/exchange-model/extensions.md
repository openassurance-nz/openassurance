# OpenAssurance Minimum Exchange Model: Extensions

**Part of:** `exchange-model.md`  
**Status:** Working draft, not proposed for v0.1  
**Last reviewed:** September 2026

## 1. Purpose

The core of the minimum exchange model is in `exchange-model.md`.

This document holds the extensions that were drafted alongside it and are not proposed for v0.1.

They are kept so that the core does not foreclose them, and so that the thinking behind them is not lost.

Requirement words, working assumptions, and the split between system requirements and operator obligations are used as `exchange-model.md` section 2 defines them.

Nothing here is needed for the two reference exchanges in Phase 4.

Each extension reuses an existing mechanism before defining anything, and each is open to challenge through the process in `CONTRIBUTING.md`.

## 2. Endorsement

An endorsement record states that one party recognises another party, an achievement definition, or a particular record.

**Working assumption, decision D7.**

An endorsement record is an Open Badges 3.0 endorsement credential.

Its subject MUST carry a scope: what the endorsement covers, by record type, activity, category, or period.

An endorsement without a scope MUST be treated by a verifier as informational only.

## 3. Requirement

A requirement record states what a relying organisation expects for a role, activity, contract, or supplier category.

Its subject is the requirement itself.

It MUST carry:

- what the requirement applies to;
- the conditions, each naming the record type and claims that satisfy it;
- which conditions are mandatory and which are informational;
- any alternatives, where one of several conditions will do.

It MAY carry, for any condition, the issuers or endorsements the relying organisation accepts and the currency it needs.

A requirement record SHOULD be readable by a person, and is intended to be translatable into a DCQL query for use in an interactive exchange.

**Working assumption, decision D8.**

Terms that match the CTDL condition profile exactly are borrowed from it, and the rest are defined by OpenAssurance.

Publishing a requirement is optional, and a relying organisation MAY keep its requirements private.

## 4. Discovery

**Proposed.**

An organisation SHOULD publish a DNS TXT record at the name `_openassurance` under its domain, giving its issuer identifier, its New Zealand Business Number, and the address at which it receives presentations and requests.

```text
_openassurance.harbourbeverages.example.  TXT  "v=OA1; issuer=https://harbourbeverages.example/issuer; nzbn=(number); inbox=mailto:assurance@harbourbeverages.example"
```

The pattern is the one DKIM and similar mechanisms use, it is familiar to anyone who has set up email for a domain, and it needs no website.

It lets a sender who knows only an organisation's domain find where to send a presentation, and it gives the `aud` claim of a presentation a value.

The inbox MAY be an email address, because the floor in `exchange-model.md` section 11.1 is a file that can travel by any channel, or an HTTPS address that accepts such a file.

Keys stay in the controller document and are not published in DNS.

`examples.md` section 4 works through an example, with the controller document and the binding check.

The record format, the behaviour of an HTTPS inbox, and whether a well-known address should be offered as an alternative are open points in section 10.

## 5. Request and Response

The floor lets a holder send a presentation unprompted.

The other pattern is a relying organisation asking for one.

A request is a signed object sent to the inbox that the holder's discovery record gives.

It MUST carry:

- the requester's identifier, so that the holder can check the requester's issuer binding as `exchange-model.md` section 7.5 describes;
- who the request is about, by claims such as a name and the job or contract concerned;
- what is needed, as a reference to a requirement record or as a list of record types and claims;
- the purpose;
- the period for which the records are needed;
- the address to reply to, an expiry, and a nonce.

The holder decides.

It works out who the request concerns, decides whether it has a lawful basis and a proper purpose to disclose, selects the minimum records, and replies with a presentation that names the requester as recipient and carries the stated purpose, the nonce, and an expiry no later than the end of the period it has approved.

A holder MUST NOT confirm or deny that it holds records about a person to a requester whose signature or issuer binding it cannot verify.

A holder MAY decline any request without giving a reason.

```text
Requester                               Holder
   |  look up the holder's discovery record
   |  signed request: who is asking, about whom,
   |  what is needed, why, for how long, reply-to, nonce  ->
   |                                     check the requester's binding
   |                                     identify the subject, check basis,
   |                                     select the minimum
   |  <-  presentation: recipient, purpose, nonce, expiry
   verify, then apply own recognition and requirement
```

Where possible the request reuses the claims of the OpenID for Verifiable Presentations request object, which already carries a nonce, a query, and a response address.

That protocol assumes the person using the wallet is the subject, so a way to say whom a request is about is the one genuinely new element, and it is an open point in section 10.

## 6. Approval for a Period

An engagement lasts weeks or years, and a relying organisation needs the records to stay current for that long.

Most of that need is already met without any further mechanism.

- the expiry of the presentation is the end of the period the holder approved;
- every record in it carries its own validity period and, where `exchange-model.md` section 9.2 requires one, a status entry;
- the relying organisation can check status again whenever it chooses, and the issuer does not learn which record was checked.

An authorisation withdrawn when a worker leaves, or a licence that lapses, therefore shows at the relying organisation's next check, with nothing sent by anyone.

What status cannot deliver is a record that did not exist when the presentation was made, such as a renewed licence, a new attestation, or a replacement.

For that, a holder MAY record its approval as a standing grant: for a stated requester, subject, requirement, purpose, and period, it sends a fresh presentation to the requester's inbox when a relevant record is issued, renewed, or replaced.

That is publish and subscribe without a broker.

The subscription is the holder's own approval, held by the holder, and it ends when the period ends or when the holder withdraws it.

A holder MAY also send a change notice, which says only that something covered by a grant has changed and that the relying organisation should verify again.

A change notice MUST NOT carry personal information and MUST NOT say what changed.

A conforming system MUST NOT require a broker, a hub, or a shared message service, because that would make a third party a precondition for exchange.

A grant is a disclosure like any other, so it appears in the list a subject can ask for under `exchange-model.md` section 15.2, and the relying organisation's retention runs from the end of the period.

Existing event formats, in particular the IETF security event token with its push and poll delivery, should be evaluated for the change notice before anything new is defined.

## 7. Interactive Exchange

Where both parties run systems that support them, records SHOULD be issued using OpenID for Verifiable Credential Issuance 1.0 and presented using OpenID for Verifiable Presentations 1.0, with requests expressed in DCQL.

A system that supports interactive exchange MUST still support the floor.

The credential format identifier that those protocols use for a record secured under `exchange-model.md` section 8.1 is an open point in section 10.

## 8. Government-Issued Credentials

**An optional conformance class, decision D3.**

A relying organisation's requirement may name a government-issued credential such as a driver licence.

The government issues such credentials in the mdoc format, with a status mechanism of its own.

A verifier that claims this optional class MUST be able to accept a presentation of such a credential in that format, including its status mechanism, and MUST NOT require it to be re-issued as an OpenAssurance record.

No conforming system is required to claim that class, and it is expected to matter once government-issued credentials are in general use.

## 9. Stronger Evidence of Role and Approval

**Decision D10.**

`exchange-model.md` section 5.6 lets a record carry a named person's authority and approval, and leaves two methods to this document because their formats are not settled.

A signed approval is a signature made with a key bound to the person, over the same statement digest the core requires, carried inside the record beside the organisation's own signature.

It shows that the holder of that key approved the statement, and it is only as strong as the binding between the key and the person.

A credentialed approval adds a credential issued by someone other than the organisation, establishing the person's identity and their role.

The government wallet documentation lists proof of role in a public register, and delegated authority, among the credential types it expects to hold.

An accredited provider could issue such a credential by establishing a person's identity and checking the Companies Register, without OpenAssurance operating anything.

No such credential is known to be available yet, and nothing in the core depends on one.

When one exists, a verifier SHOULD accept it as authority evidence in place of a register check, and SHOULD report the role as independently verified.

A conforming system MUST NOT require either method, because a small supplier must be able to make a declaration with nothing more than the core.

## 10. Open Points

These are unresolved in the extensions, and none of them holds up the core.

- **The request object.** Section 5 reuses the claims of the OpenID request object where it can, and how a request says whom it is about, and how it is signed and delivered to an email inbox, are undecided;
- **Grants and change notices.** Section 6 describes a standing grant and a content-free change notice, and neither has a format, so existing event formats need evaluating first;
- **The discovery record.** Section 4 proposes a DNS record, and its format, the behaviour of an HTTPS inbox, and a well-known address as an alternative are undecided;
- **Format identifier in the interactive protocols.** How the OpenID format identifiers for W3C credentials apply to a record secured under `exchange-model.md` section 8.1 needs confirming by implementation;
- **An mdoc rendering.** `exchange-model.md` section 14 keeps it possible, and whether to define one is decision D3, which depends on answers from the Government Digital Delivery Agency.

## 11. Standards Referenced

Assessment, status, and sources for each of these are in `standards-map.md` and its parts, and the standards the core relies on are listed in `exchange-model.md` section 20.

- IETF BCP 222, RFC 8552, underscored naming of DNS attribute leaves, <https://www.rfc-editor.org/info/rfc8552>;
- IETF RFC 8417, Security Event Token, with RFC 8935 and RFC 8936 for push and poll delivery, <https://www.rfc-editor.org/info/rfc8417>;
- OpenID for Verifiable Credential Issuance 1.0, <https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0-final.html>;
- OpenID for Verifiable Presentations 1.0, <https://openid.net/specs/openid-4-verifiable-presentations-1_0-final.html>;
- Credential Engine CTDL, <https://credreg.net/ctdl/handbook>.
