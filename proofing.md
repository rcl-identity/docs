---
title: Identity Proofing
description: Identity Proofing for the RCL Digital Identity Application.
has_children: false
nav_order: 5
---

# Identity Proofing
**V7.0.0**

> This section only applies to organizations issuing [Verified Digital IDs](./index.md#verified-digital-identity). You can ignore this section if your are issuing [Self Asserted Digital IDs](/index.md#self-asserted-digital-identity)

An *Identity Approver* associated with an organization issuing a Digital ID will verify the physical identity of an application and use the Identity Proofing Application to approve the Digital ID.

# Installing the Application

The application is available on [GitHub](https://github.com/rcl-identity/RCL.Core.Identity.Proofing.Portal). 

- Click on the ``Deploy to Azure`` button on the GitHub page

![image](/images/proofing/install.png)

- Install the application as a Web App in your azure account

![image](/images/identityenrollment/install2.png)

**Alternatively, you can download the solution to Visual Studio and install the application from Visual Studio.**

# Customizing the Application

You can customize the application and install in your azure account.

- Download the application and open ith with Visual Studio

![image](/images/proofing/install2.png)

- Customize the application in Visual Studio

![image](/images/identityenrollment/install4.png)

- When you are done, publish the application to your Azure Web App

![image](/images/identityenrollment/install5.png)

# Configuring the Application

After you have installed the application as an Azure Web app, you must configure it.

- Open the Azure Web app

- Open the ``Configuration`` page

![image](/images/proofing/configure.png)

In the [Web App](./aadb2c.md#register-a-web-application) that was configured in the AAD B2C tenant, copy the values for the ``Application (client) ID, Directory (tenant) ID and Client Secret`` to the configuration :

    - AzureAd:ClientId
    - AzureAd:TenantId
    - AzureAd:ClientSecret

For the AAD B2C tenant

![image](/images/identityenrollment/configure2.png)

Use the name of the ``Azure AD B2C tenant`` for the configuration :

    - AzureAd:Domain

The value of the ``Instance`` should be in the format ``https://{tenant}.b2clogin.com/`` , eg . https://contoseco.b2clogin.com/

Set the instance in the configuration :

        - AzureAd:Instance

In the [User Flow](./aadb2c#create-a-sign-insign-up-user-flow) you created for the Sign In Sign Up page, get the name of the User Flow (eg. B2C_1_susi). Use as the value for the configuration :

        - AzureAd:SignUpSignInPolicyId

Use the value of ``/signin-oidc`` for the configuration :

        - AzureAd:CallbackPath

Use the value of ``/signout-callback-oidc`` for the configuration :

        - AzureAd:SignedOutCallbackPath

You will need to add the configuration settings to connect to the RCL APIs to perform the identity proofing.

Use the value of ``https://rclapi.azure-api.net/production`` for the configuration :

        - IdentityProofingApi:ApiEndpoint

Use the value of ``d02dc52b-fec2-47b7-9088-5a01e3a4dcae`` for the configuration :

        - IdentityProofingApi:Resource

Get your [Subscription ID](./apiconnector.md#get-the-subscription-id) from the RCL Digital Identification Application. Use the value for the configuration :

        - IdentityProofingApi:SubscriptionId

Get the identifier for the [Identity Approver](./apiconnector.md#identity-approver) that will be using this application. Use the value for the configuration :

        - IdentityProofingApi:IdentityApproverIdentifier

# Configure the AAD B2C App Registration

- Open the [AAD B2C Application](./aadb2c.md#register-a-web-application) your registered for the B2C tenant

- Open the ``Authentication`` page

![image](/images/identityenrollment/redirect-uri.png)

- In the Redirect URI add the uri for the Identity Enrollment Application in the format : ``https://{uri}/signin-oidc`` eg. https://rcl-demo-identity-proofing.azurewebsites.net/signin-oidc

![image](/images/proofing/redirect-uri.png)

- In the ``Implicit grant and hybrid flows`` section, select both  ``Access tokens`` and ``ID tokens``

![image](/images/identityenrollment/redirect-uri3.png)

- Click the ``Save`` button when you are done

When you are done with the configuration, open the web app to ensure it is up and running.

![image](/images/proofing/app.png)

# Functionality

## Add Identity Approvers

You can use the Identity Proofing Application to register [Identity Approvers](./apiconnector.md#register-identity-approvers-in-the-rcl-digital-identity-application) for an organization issuing Digital IDs.

## Approver Applicants for a Digital ID

When an applicant has provided evidence to prove their physical identity, the Identity Approver will review the evidence and approve the Digital ID. The approve a ``User Request`` for a Digital ID follow these steps :

- Open the Identity Proofing Application

- Open the `User Requests` page

![image](/images/proofing/user-request.png)

- Click the ``Approve`` link to approve a user request

![image](/images/proofing/user-request2.png)

- Click the ``Approve`` button to approve a user request

![image](/images/proofing/user-request3.png)

Once a user request is approved , it will be deleted for the user requests list.