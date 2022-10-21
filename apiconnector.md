---
title: API Connector
description: Creating an API Connector for the RCL Digital Identity Application.
has_children: false
nav_order: 3
---

# API Connector
**V7.0.0**

> This section only applies to organizations issuing [Verified Digital IDs](./index.md#verified-digital-identity). You can ignore this section if your are issuing [Self Asserted Digital IDs](/index.md#self-asserted-digital-identity)

After a person applies for a Digital ID using the Azure AD B2C sign-up page, their physical identity must be verified. The verification process may require the person to provide photo IDs to confirm their identity and date of birth. The purpose of the API Connector is to capture the user data on sign-up and provide the data to the [Identity Proofing Application]() to conduct the identity verification process. The Digital ID is only issued when the person's physical identity is verified by an *Identity Approver*.

# Identity Approver

## Add Identity Approvers in the Sign-up Page

An **Identity Approver** can be an organization, department or person assigned to perform the identity verification. An organization may have single or multiple Identity Approvers. Identity approvers are added when you [Customize the Sign-up Page](./aadb2c.md/#customize-the-sign-up-page).

- Add the available Identity Approver(s) as a dropdown select on the AD B2C Sign-up page. Add each of the available Identity Approver(s) as a dropdown select assigning a *text* and *value* for the attribute. We will use the **Value** property as the *Identity Approver Identifier* reference in the RCL Identity Platform APIs and applications.

![image](/images/aadb2c/signup-layout6.png)

## Register Identity Approvers in the RCL Digital Identity Application

Each identity Approver must be registered in the [RCL Digital Identity SaaS Application]().

- Open the RCL Digital Identity Application

- Navigate to the Identity Approvers page and click on the ``Create New Identity Approver`` button

![image](/images/apiconnector/identityapprover-create.png)

- Add the Identity Approver

![image](/images/apiconnector/identityapprover-create2.png)

- The **Identitfier** should be the **Value** of the Identity Approver in the dropdown select box in the AD B2C Sign-up page (please refer to the image in the previous section).

- Click the ``Submit`` button when you are done

![image](/images/apiconnector/identityapprover-create3.png)

# API Authentication

The API Connector uses **Basic Authentication**. For basic authentication, a *username* and *password* are required. 

- The username is **ApiClient**

Follow these steps to set the password :

- Open the RCL Digital Identity Application

- Navigate to the **Subscription > API Client** page and click on the ``Register a Client Id`` button

![image](/images/apiconnector/identityapprover-create4.png)

- Copy the **Application(client) ID** for the [Web Application](./aadb2c.md#register-a-web-application) you registered previously

![image](/images/aadb2c/app-registration4.png)

- Add the **Application(client) ID** value and click the ``Submit`` button

![image](/images/apiconnector/identityapprover-create5.png)

- You will use the **Client Id** as the password for the ``Basic Authentication``.

![image](/images/apiconnector/identityapprover-create6.png)

# Get the Subscription Id

- Open the RCL Digital Identity Application

- Navigate to the **Subscription > Details** page 

![image](/images/apiconnector/subscription.png)

- Scroll down the page, and copy the Subscription Id

![image](/images/apiconnector/subscription2.png)

- You will use the subscription id to construct the **Endpoint URL** for the API connector


# Adding the API Connector to AAD B2C

- Open the AD B2C tenant and navigate to the ``API connectors`` page

- Click the ``New API connector`` link to add the API Connector

![image](/images/apiconnector/apiconnector-add.png)

- Add the API Connector

![image](/images/apiconnector/apiconnector-add2.png)

- The Endpoint URL is in the format : ``https://rclapi.azure-api.net/production/v1/did/userapproval/subscriptionid/{your-subscription-id}``

- Replace the {your-subscription-id} placeholder with the **Subscription Id** you obtained in the previous section

- Add the *username* and *password* for the ``Basic Authentication``

- Click the ``Save`` icon when you are done

![image](/images/apiconnector/apiconnector-add3.png)

- In the AAD B2C tenant, navigate to the ``User flows`` page and select the user flow

![image](/images/apiconnector/test.png)

- In the user flow page, click the ``API connectors`` link

- Add the API connector ``Before creating the user``

![image](/images/apiconnector/apiconnector-add4.png)

- Click the ``Save`` icon when you are done

# Test the API Connector

- In the AD B2C tenant, navigate to the ``User flows`` page and select the user flow

![image](/images/apiconnector/test.png)

- Click the ``Run user flow`` button

![image](/images/apiconnector/test2.png)

- In the ``Sign in`` page, click the **Sign up now** link

![image](/images/aadb2c/signup-layout4.png)

- Complete the Sign-up process

![image](/images/aadb2c/signup-layout5.png)

- After you complete the sign-up, the following message will be displayed 

![image](/images/apiconnector/test3.png)

- At this point, the user data will be provided to the [Identity Proofing Application]() for the Identity Approver to start the process for verification of the user's physical identity

# Next Steps

- [Identity Proofing]()

