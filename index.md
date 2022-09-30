---
title: Introduction
description: The RCL Identity application allows organizations to issue Digital Identities to persons.
has_children: false
nav_order: 1
---

# Introduction
**V7.0.0**

The **RCL Identity** application allows organizations to issue Digital Identities to persons. The processes of issuing a Digital Identity include :

- Identity Enrollment
- Identity Proofing

The Organization will have full control of the applications and platform it uses to issue the Digital IDs. 

# Identity Enrollment
A person will apply to the organization for a Digital Identity using an online [Enrollment Application](https://github.com/rcladmin/RCL.Core/tree/master/src/RCL.Identity/RCL.Core.Identity.Enrollment) that the organization hosts. The applicant will provide their personal identification data and will verify their email address during the sign up process. The process follows the [NIST SP 800-63](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63a.pdf) IAL2 Identity Assurance level. 

# Identity Proofing
Once the applicant has completed the sign up process, they will submit photo IDs (eg: National IDs, Drivers Permits, Passports) to verify their personal identification. An approver will review the photos and approve the Digital ID when the applicant's identity is verified. Identity proofing is carried out by the approver in the issuing organization using an online [Identity Proofing](https://github.com/rcladmin/RCL.Core/tree/master/src/RCL.Identity/RCL.Core.Identity.Proofing.Portal) application hosted by the organization.

# Digital ID

The person's Digital ID data will be managed in the [Azure Active Directory B2C](https://learn.microsoft.com/en-us/azure/active-directory-b2c/overview) (AAD B2C) acting as an identity provider (IdP). The organization will subscribe for and control the AAD B2C directory in their Azure subscription. The following ``User Claims`` are stored and issued by the IdP :

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

The unique identifier for the person's Digital ID will be stored in the ``Object Id``.

# Single Sign-On
A person with a Digital Identity will utilize [Single Sign-On](https://learn.microsoft.com/en-us/azure/active-directory-b2c/custom-policy-reference-sso) provided by AAD B2C IdP to sign in to multiple web sites using the same sign-in credentials.

Single Sign-On is compliant with the [Open ID](https://learn.microsoft.com/en-us/azure/active-directory-b2c/openid-connect) specification. Using Open ID, the Digital ID issuing organization can set up single sign-on on multiple regional and international websites it directly controls. 

It can also allow its partners and external organizations (relying parties) to use its AD B2C as an eternal Identity Provider (external IdP) to sign in its users to external websites using the ``Client Credentials Grant`` described in the [OAuth2](https://www.rfc-editor.org/rfc/rfc6749) specification.

# Authentication

The Digital ID issuing organization can set up single-factor authentication using username and password credentials.

In addition, multi-factor authentication utilizing the time-based one-time password (TOTP) verification process is supported. This is done using an **Authenticator Application** (eg: Google Authenticator, Microsoft Authenticator). The follows [NIST SP 800-63](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63b.pdf) AAL2 Authenticator Assurance level.


# User Claims

The AAD B2C Identity Provider will send the ``User Claims`` identified above in the [JWT](https://www.rfc-editor.org/rfc/rfc7519) tokens when a user signs in to a website. Using these claims, the relying parties to which the person signs in will have access the Personally Identifiable Information (PII). The relying party will use the PII to make decisions about the user (eg. grant a service).

# Standards Compliance

The RCL Identity application is an API built on AAD B2C and is complaint with the following standards :

- [NIST SP 800-63 Digital Identity Guidelines](https://pages.nist.gov/800-63-3/)
- [OAuth2 Authorization Framework](https://datatracker.ietf.org/doc/html/rfc6749) for single sign-on

- [Open ID](https://openid.net/developers/specs/) for single sign-on
- [SAML](http://saml.xml.org/saml-specifications) for single sign-on

# Process Flow

![image](/images/identity-process.png)

# Architecture

## Cloud Services

The organization will subscribe for the applicable cloud services provided by the [Microsoft Azure Cloud](https://azure.microsoft.com/en-us/). The organization will have sole and full control over its cloud services and resources. 

## Azure AD B2C

The organization will create and administer an [Azure AD B2C](https://azure.microsoft.com/en-us/services/active-directory/external-identities/b2c/) directory that will act as an Identity Provider (IdP) and will use it to store identity data for those people that they issue Digital IDs. The IdP will also provide single sign-on technology using OAuth2, SAML and OpenID.

## Identity Enrollment
The organization will host the open-source [Identity Enrollment](https://github.com/rcladmin/RCL.Core/tree/master/src/RCL.Identity/RCL.Core.Identity.Enrollment) application as a Web App in its Azure subscription. It will have full control over this application.

## Identity Proofing

The organization will host the open-source [Identity Proofing](https://github.com/rcladmin/RCL.Core/tree/master/src/RCL.Identity/RCL.Core.Identity.Proofing.Portal) application as a Web App in its Azure subscription. It will have full control over this application.

## RCL Identity SaaS application

The organization will subscribe to the RCL Identity Software as a Service (SaaS) application provided in the Azure Marketplace to access the RCL Identity APIs to facilitate Identity Proofing. The organization will have full control over this application.
