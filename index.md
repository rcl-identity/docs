---
title: Introduction
description: The RCL Digital Identity platform allows organizations to issue Digital Identities to persons.
has_children: false
nav_order: 1
---

# Introduction
**V7.0.0**

The **RCL Digital Identity** platform allows organizations and governments to issue Digital Identities to people. A Digital Identity is a unique representation of a person carrying out an online transaction. In this context, a person holding a Digital ID has their *Personal Identifiable Information* (PII) stored with an *Identity Provider* (IdP). This IdP will provide the functionality for the person to sign-in to various websites (relying parties) and transmit their PII as claims to the relying party. The relying party can then use these claims to make a determination about the user (eg. whether to grant a service or not). 

The Digital ID can be :

**Self Asserted** - independent physical identity verification of the person is not required

**Verified** - the physical identity of the person is verified by a process of *Identity Proofing*

# Self Asserted Digital Identity

In a **Self Asserted** Digital ID, the person will sign-up for a Digital ID and be immediately granted the ID once they have confirmed their email. The physical identity of the person is not independently verified. The process of granting the ID is fully automated and does not require human intervention.

## Identity Self Assertion

A person will apply to the *issuing organization* for a Digital Identity using an online [Identity Self Assertion Application](https://github.com/rcl-identity/RCL.Core.Identity.SelfAssertion) that the issuing organization hosts. The *applicant* will provide their personal identification data and will verify their email address during the sign up process. The process follows the [NIST SP 800-63](https://pages.nist.gov/800-63-3/) IAL1 Identity Assurance level. 

# Verified Digital Identity

In a **Verified** Digital ID, the *applicant* will *Enroll* for a Digital ID. The physical identity of the person must be verified by an *Identity Approver* in an *Identity Proofing* process. This process requires human intervention in granting the ID.

## Identity Enrollment

An *applicant* will apply to the issuing organization for a Digital ID using an online [Identity Enrollment Application](https://github.com/rcl-identity/RCL.Core.Identity.Enrollment) that the organization hosts. The applicant will provide their personal identification data and will verify their email address during the sign up process. The identification data will be verified by an independent *Identity Approver* remotely or in-person. The process follows the [NIST SP 800-63](https://pages.nist.gov/800-63-3/) **IAL2** Identity Assurance level for remote verification and **IAL 3** for in-person verification. 

## Identity Proofing

Once the applicant has completed the sign up process, they will submit photo IDs (eg: National IDs, Drivers Permits, Passports) to verify their personal identification. An Identity Approver will review the photo IDs and approve the Digital ID once the applicant's identity is physically verified. Approval of a Digital ID is carried out by the approver in the issuing organization using an online [Identity Proofing Application](https://github.com/rcl-identity/RCL.Core.Identity.Proofing.Portal) hosted by the organization.

# Digital ID

The person's Digital ID data will be managed in [Azure Active Directory B2C](https://learn.microsoft.com/en-us/azure/active-directory-b2c/overview) (AAD B2C) acting as an *Identity Provider (IdP)*. The issuing organization will subscribe for and control the AAD B2C tenant in their Azure subscription. The following  PII is  stored and issued by the IdP as ``User Claims``:

- Given Name
- Surname
- Display Name
- Street Address
- City
- State/Province
- Postal Code
- Country
- Email
- Object Id

*Additional claims for a Verified Digital ID*
 
 - Date of Birth
 - Identity Approver

The unique identifier for the person's Digital ID will be stored in the ``Object Id``.

# Single Sign-On
A person with a Digital Identity will utilize [Single Sign-On](https://learn.microsoft.com/en-us/azure/active-directory-b2c/custom-policy-reference-sso) provided by the AAD B2C IdP to sign in to multiple web sites using the same sign-in credentials.

Single Sign-On is accomplished using the [Open ID Connect](https://learn.microsoft.com/en-us/azure/active-directory-b2c/openid-connect) protocol. Using Open ID Connect, the Digital ID issuing organization can set up single sign-on on multiple regional and international websites it directly controls. 

It can also allow its partners and external organizations (*Relying Parties*) use its AAD B2C as an *External Identity Provider* (External IdP) to sign in its users to external websites.

# Authentication

The Digital ID issuing organization can set up single-factor authentication using username and password credentials. This follows [NIST SP 800-63](https://pages.nist.gov/800-63-3/) **AAL1** Authenticator Assurance level.

In addition, multi-factor authentication utilizing the time-based one-time password (TOTP) verification process is supported. This is done using an **Authenticator Application** (eg: Google Authenticator, Microsoft Authenticator on the user's mobile device). This follows [NIST SP 800-63](https://pages.nist.gov/800-63-3/) **AAL2** Authenticator Assurance level.


# Assertion and User Claims

The AAD B2C Identity Provider (IdP) will send the ``User Claims`` in [JWT](https://www.rfc-editor.org/rfc/rfc7519) **id tokens as** an *assertion* when a user signs in to a website (relying party). The IdP and relying party will use the **Open ID Connect** protocol to communicate with each other.

The IdP will sign the JWT with its private key. The relying party will verify that the *user claims* originated from the IdP by checking the JWT signature with the IdP's published public key. This follows [NIST SP 800-63](https://pages.nist.gov/800-63-3/) **FAL1** Federation Assurance level.  

Using these user claims, the relying parties to which the person signs in will have access to the *Personally Identifiable Information* (PII). The relying party will use the PII to make decisions about the user (eg. whether to grant a service).

# Standards Compliance

The RCL Identity platform are APIs built on Azure AD B2C and is compliant with the following standards :

- [NIST SP 800-63 Digital Identity Guidelines](https://pages.nist.gov/800-63-3/)

- [Open ID Connect](https://openid.net/developers/specs/) for single sign-on and authentication


- [OAuth2 Authorization Framework](https://datatracker.ietf.org/doc/html/rfc6749) for authorization


- [SAML](http://saml.xml.org/saml-specifications) for single sign-on and authentication

# Architecture and Applications

## Cloud Services

The organization issuing the Digital ID will subscribe for the applicable cloud services provided by the [Microsoft Azure Cloud](https://azure.microsoft.com/en-us/). The issuing organization will have sole and full control over its cloud services and resources. 

## Azure AD B2C

The issuing organization will create and administer an [Azure AD B2C](https://azure.microsoft.com/en-us/services/active-directory/external-identities/b2c/) tenant that will act as an *Identity Provider (IdP)* and will use it to store identity data for those people that they issue Digital IDs. The IdP will also provide single sign-on technology using OAuth2, SAML and OpenID Connect. The issuing organization will have sole and full control over its IdP.

![image](/images/intro/b2c.jpg)

## Identity Self Assertion Application

For a Self Asserted Digital Identity, the issuing organization will host the customizable open-source [Identity Self Assertion Application](https://github.com/rcl-identity/RCL.Core.Identity.SelfAssertion) as a Web App in its Azure subscription. It will have full control over this application.

![image](/images/intro/self-asserted.jpg)

## Identity Enrollment Application

For a Verified Digital Identity, the issuing organization will host the customizable open-source [Identity Enrollment Application](https://github.com/rcl-identity/RCL.Core.Identity.Enrollment) as a Web App in its Azure subscription. It will have full control over this application.

![image](/images/intro/verified.jpg)

## Identity Proofing

For a Verified Digital Identity, the issuing organization will host the customizable open-source [Identity Proofing Application](https://github.com/rcl-identity/RCL.Core.Identity.Proofing.Portal) as a Web App in its Azure subscription. It will have full control over this application.

![image](/images/intro/proofing.jpg)

## RCL Identity SaaS application

For a Verified Digital Identity, the issuing organization will subscribe to the [RCL Digital Identity](https://azuremarketplace.microsoft.com/en/marketplace/apps/rayconsulting.009?tab=Overview) Software as a Service (SaaS) application provided in the Azure Marketplace to access the RCL Identity Platform APIs to facilitate **Identity Proofing**. The issuing organization will have full control over this application.

![image](/images/intro/portal.jpg)
