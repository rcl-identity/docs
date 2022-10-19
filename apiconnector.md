---
title: API Connector
description: Creating an API Connector for the RCL Digital Identity Application.
has_children: false
nav_order: 3
---

# Introduction

After a person applies for a Digital ID using the Azure AD B2C sign-up page, their physical identity must be verified. The verification process may require the person to provide photo IDs to confirm their identity and date of birth. The purpose of the API Connector is to capture the user data on sign up and provide the data to the RCL Identity Proofing application to conduct the Identity Verification process.

# Identity Approver

## Add Identity Approvers in the Sign-up Page

An Identity Approver can be an organization, department or person assigned to perform the identity verification. An organization may have single or multiple Identity Approvers. Identity approvers are added when you [Customize the Sign-up Page](./aadb2c.md/#customize-the-sign-up-page).

- Add the available Identity Approver(s) as a dropdown select on the AD B2C Sign-up page

![image](/images/aadb2c/signup-layout6.png)

## Register Identity Approvers in the RCL Digital Identity Application

Each identity Approver must be registered in the RCL Digital Identity Application.

- Open the RCL Digital Identity Application

- Navigate to the Identity Approvers page and click on the ``Create New Identity Approver`` button

![image](/images/apiconnector/identityapprover-create.png)

- Add the Identity Approver

![image](/images/apiconnector/identityapprover-create2.png)

- The **Identitfier** should be the **Value** of the Identity Approver in the dropdown select box in the AD B2C Sign-up page (please refer to the image in the previous section).

![image](/images/apiconnector/identityapprover-create3.png)

# API Authentication

The API Connector uses **Basic Authentication**. For basic authentication a username and password is required. 

- The username is **ApiClient**

Follow these steps to set the password :

- Open the RCL Digital Identity Application

- Navigate to the **Subscription > API Client** page and click on the ``Register a Client Id`` button

![image](/images/apiconnector/identityapprover-create4.png)

- Add a value and click the ``Submit`` button

![image](/images/apiconnector/identityapprover-create5.png)

- Use this **Client Id** as the password.

![image](/images/apiconnector/identityapprover-create6.png)

# Get the Subscription ID

- Open the RCL Digital Identity Application

- Navigate to the **Subscription > Details** page 

![image](/images/apiconnector/subscription.png)

- Scroll down the page, and copy the Subscription Id

![image](/images/apiconnector/subscription2.png)

- You will use the subscription id to construct the URL end point for the API connector


# Adding the API Connector to AD B2C

- Open the AB B2C tenant and navigate to the ``API connectors`` page

- Click the ``New API connector`` to add the API Connector

![image](/images/apiconnector/apiconnector-add.png)

- Add the API Connector

![image](/images/apiconnector/apiconnector-add2.png)

    - The Endpoint URL is in the format : https://https://rclapi.azure-api.net/development/v1/did/userapproval/subscriptionid/{your-subscription-id}

    - Replace the {your-subscription-id} place holder with the **Subscription Id** you obtained in the previous section

    - Add the username and password for the basic authentication

![image](/images/apiconnector/apiconnector-add3.png)

- In the AD B2C tenant, navigate to the ``User flows`` page and select the user flow

![image](/images/apiconnector/test.png)

- In the user flow page, select the ``API connectors``

- Add the API connector ``Before creating the user``

![image](/images/apiconnector/apiconnector-add4.png)

- Click the ``Save`` icon when you are done

# Test the API Connector

- In the AD B2C tenant, navigate to the ``User flows`` page and select the user flow

![image](/images/apiconnector/test.png)

- Click the ``run user flow`` button

![image](/images/apiconnector/test2.png)

- In the ``Sign in`` page, click the **Sign up now** link

![image](/images/aadb2c/signup-layout4.png)

- Complete the Sign-up process

![image](/images/aadb2c/signup-layout5.png)

- After you complete the sign-up, the following message will be displayed 

![image](/images/apiconnector/test3.png)

- At this point the user data will be provided to the RCL Identity Proofing application of the Identity Approver to start the process for verification of the user's physical identity

# Next Steps

- [Identity Proofing]()

