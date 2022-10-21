---
title: Create AAD B2C
description: Creating an Azure AD B2C for the RCL Digital Identity Application.
has_children: false
nav_order: 3
---

# Create AAD B2C
**V7.0.0**

In this section, we will create an Azure Active Directory B2C tenant for the RCL Digital Identity platform.

# Create an Azure AD B2C tenant

- In the Azure Portal, create an Azure Active Directory B2C tenant

![image](/images/aadb2c/aadb2c-create.png)

- Create a new tenant

![image](/images/aadb2c/aadb2c-create2.png)

- Select the B2C tenant type

![image](/images/aadb2c/aadb2c-create3.png)

- Configure the tenant

![image](/images/aadb2c/aadb2c-create4.png)

- Review and create the tenant

![image](/images/aadb2c/aadb2c-create5.png)

# Register a web application

Before an applications can interact with Azure AD B2C, it must be registered in the B2C tenant.

- Open Azure AD B2C tenant, click the ``New registration`` link to register a new app

![image](/images/aadb2c/app-registration.png)

- Set the name of the app 

![image](/images/aadb2c/app-registration2.png)


- In the ``Redirect URI``, select **Web** and set the URI to **https://jwt.ms** . We will use this URI for testing purposes.

![image](/images/aadb2c/app-registration3.png)

- Click the ``Register`` button when you are done.

- In the newly registered application, copy the following for configuration purposes :

    - Application (client) ID
    - Directory (tenant) ID

![image](/images/aadb2c/app-registration4.png)

- In the application, navigate to the ``Certificates & secrets`` page

- Add a new client secret

![image](/images/aadb2c/app-registration5.png)

- Copy the value for the secret for configuration purposes

    - Client Secret

![image](/images/aadb2c/app-registration6.png)

# Access the Microsoft Graph

The Microsoft Graph API provides programmatic access to manage AAD B2C *Users*. We will configure the web application we created previously to access the Microsoft Graph.

- Open the AAD B2C tenant and then open the web application

![image](/images/aadb2c/ms-graph.png)

- Open the ``API permissions`` page and click on the ``Add a permission`` link

- Select the ``Microsoft Graph`` API

![image](/images/aadb2c/ms-graph2.png)

- Select ``Application permissions``

![image](/images/aadb2c/ms-graph3.png)

- Then, select the ``Directory.ReadWrite.All`` permission from the ``Directory`` API. Click the ``Add permissions`` button when you are done

![image](/images/aadb2c/ms-graph4.png)

- Click the ``Grant admin consent`` link 

![image](/images/aadb2c/ms-graph5.png)

- The web application can now access the Microsoft Graph

![image](/images/aadb2c/ms-graph6.png)

# Adding Custom Attributes for Verified Identity

> Custom Attributes are only required for [Verified Digital IDs](./index.md#verified-digital-identity). If you are issuing [Self Asserted Digital IDs](./index.md#self-asserted-digital-identity), you can ignore this section.

Azure AD B2C does not contain a *Built-in* attributes for **Date of Birth** and **Identity Approver**. 

The *Identity Approver* attribute can be used by the organization to manage the approval of a Digital ID among several different departments, organizations or approvers. We will add these as approvers in our custom attribute.

- Open the AAD B2C tenant

- In the ``User attributes`` page, click the ``Add`` link 

![image](/images/aadb2c/attribute-add.png)

- Add the **Date of Birth** custom attribute 

![image](/images/aadb2c/attribute-add2.png)

- Add the **Identity Approver** custom attribute

![image](/images/aadb2c/attribute-add4.png)

- Click the ``Create`` button when you are done

![image](/images/aadb2c/attribute-add3.png)

# Create a Sign-In/Sign-Up User flow

The sign up/ sign in workflow will allow the user to sign up for a Digital ID.

> You should create separate user flows for Self Asserted and Verified Digital IDs. Both will have different user claims.

- In the B2C tenant, open the ``User flows`` page

- Click the ``New user flow`` link to create a user flow

![image](/images/aadb2c/userflow-add.png)

- Select the ``Sign up and sign in`` user flow and select the ``Recommended`` version

![image](/images/aadb2c/userflow-add2.png)

- Add a name for the user flow 

    - For a Self Asserted Digital ID, you can use the name : ``susi-sa``
    - For a Verified Digital ID, you can use the name : ``susi``

![image](/images/aadb2c/userflow-add3.png)

- Select the ``Email signup`` identity provider and set the Multi-Factor Authentication (MFA) as follows:

![image](/images/aadb2c/userflow-add4.png)

- In the ``User attributes and token claims``, click the ``Show more`` link to add the user attributes

- Add the following user attributes and claims :

    - City
    - Country/Region
    - Display Name
    - Email Address
    - Email Addresses
    - Given Name
    - Postal Code
    - State/Province
    - Street Address
    - Surname
    - User's Object ID

- *Additional Claims for the Verified Digital ID*

    - Date of Birth
    - Identity Approver

![image](/images/aadb2c/userflow-add5.png)

- Click the ``Create`` when you are done

![image](/images/aadb2c/userflow-add6.png)

# Customize the Sign Up page

- Open the user flow

- In the ``Page layouts`` page, select the ``Local account sign up page``

![image](/images/aadb2c/signup-layout.png)

- Format the sign-up page user attributes and their labels as follows or to your preferences:

![image](/images/aadb2c/signup-layout2.png)

- If you are issuing Verified Digital IDs, add each of the available Identity Approver(s) as a dropdown select assigning a *text* and *value* for the attribute. We will use the **Value** property as the *Identity Approver Identifier* reference in the RCL Identity Platform APIs and applications.

![image](/images/aadb2c/signup-layout6.png)

- Click the ``Save`` icon when you are done

# Configure Password Properties

- Open the user flow

- In the ``Properties`` page, configure the password properties as follows

![image](/images/aadb2c/password-configure.png)

- Click the ``Save`` icon when you are done

# Test the User Flow

- To test the user flow, click the ``Run user flow`` icon


- Select the **Application** and **Reply URL** we registered in the previous section

![image](/images/aadb2c/signup-layout3.png)

- Click the ``Run user flow`` button to test the sign-up page

- In the ``Sign in`` page, click the **Sign up now** link

![image](/images/aadb2c/signup-layout4.png)

- You can now test the ``Sign up`` page

![image](/images/aadb2c/signup-layout5.png)



