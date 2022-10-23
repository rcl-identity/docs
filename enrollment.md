---
title: Identity Enrollment
description: Identity Enrollment for the RCL Digital Identity Application.
has_children: false
nav_order: 4
---

# Identity Enrollment
**V7.0.0**

> This section only applies to organizations issuing [Verified Digital IDs](./index.md#verified-digital-identity). You can ignore this section if your are issuing [Self Asserted Digital IDs](/index.md#self-asserted-digital-identity)

An applicant for a Digital ID must use the [AAD B2C Sign-up](aadb2c.md#customize-the-sign-up-page) page to register. The organization may develop its own web application to accomplish this. There is also the option for the organization to use the open-source [Identity Enrollment Application]().

# Enrollment URL and Instructions

The organization must register the URL for their identity enrollment application, as well as, the instructions on how to obtain the Digital ID. The instructions can be a public web page or document available on the web. The enrollment URL and instructions are registered in the RCL Digital Identity application when creating an [Identity Approver](./apiconnector.md#identity-approver).

![image](/images/apiconnector/identityapprover-create2.png)

# Identity Enrollment Application

The Identity Enrollment Application is an open-source application that allows applicants to register for a Digital ID. The application is hosted as a Azure Web app by the organization issuing the Digital ID.

# Installing the Application

The application is available on [GitHub](https://github.com/rcl-identity/RCL.Core.Identity.Enrollment). 

- Click on the ``Deploy to Azure`` button on the GitHub page

![image](/images/identityenrollment/install.png)

- Install the application as a Web App in your azure account

![image](/images/identityenrollment/install2.png)

**Alternatively, you can download the solution to Visual Studio and install the application from Visual Studio.**

# Customizing the Application

You can customize the application and install in your azure account.

- Download the application and open ith with Visual Studio

![image](/images/identityenrollment/install3.png)

- Customize the application in Visual Studio

![image](/images/identityenrollment/install4.png)

- When you are done, publish the application to your Azure Web App

![image](/images/identityenrollment/install5.png)

# Configuring the Application

After you have installed the application as an Azure Web app, you must configure it.

- Open the Azure Web app

- Open the ``Configuration`` page

![image](/images/identityenrollment/configure.png)

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

Whe you are done with the configuration, open the web app to ensure it is up and running.

![image](/images/identityenrollment/configure3.png)

# Configure the AAD B2C App Registration

- Open the [AAD B2C Application](./aadb2c.md#register-a-web-application) your registered for the B2C tenant

- Open the ``Authentication`` page

![image](/images/identityenrollment/redirect-uri.png)

- In the Redirect URI add the uri for the Identity Enrollment Application in the format : ``https://{uri}/signin-oidc`` eg. https://rcl-demo-identity-enrollment.azurewebsites.net/signin-oidc

![image](/images/identityenrollment/redirect-uri2.png)

- In the ``Implicit grant and hybrid flows`` section, select both  ``Access tokens`` and ``ID tokens``

![image](/images/identityenrollment/redirect-uri3.png)

- Click the ``Save`` button when you are done

# Functionality

- Users can sign up for a Digital ID by clicking the ``Sign up now`` link at the bottom of the sign in page

![image](/images/aadb2c/signup-layout4.png)

- Users can manage their profile

![image](/images/identityenrollment/profile.png)


- Users can change their passwords

![image](/images/identityenrollment/password.png)


- Users can see the Security Groups that they belong to

![image](/images/identityenrollment/securitygroup.png)




