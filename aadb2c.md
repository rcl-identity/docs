---
title: Create AAD B2C
description: Creating and Azure AD B2C for the RCL Digital Identity Application.
has_children: false
nav_order: 3
---

# Introduction
**V7.0.0**

In this section, we will create an Azure Active Directory B2C tenant for the RCL Digital Identity application.

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

- In the application, navigate to the ``Certificates & secrets page

- Add a new client secret

![image](/images/aadb2c/app-registration5.png)

- Copy the value for the secret for configuration purposes

![image](/images/aadb2c/app-registration6.png)


# Adding a Custom Attribute

Azure AD B2C does not contain a Built-in attribute for **Date of Birth**. We will add this as a custom attribute.

- Open the B2C tenant

- In the ``User attributes`` page, click the ``Add`` link 

![image](/images/aadb2c/attribute-add.png)

- Add the **Date of Birth** custom attribute 

![image](/images/aadb2c/attribute-add2.png)

- Click the ``Create`` button when you are done

![image](/images/aadb2c/attribute-add3.png)

# Create a Sign-In/Sign-Up User flow

The sign up/ sign in workflow will allow the user to sign up for a Digital ID.

- In the B2C tenant, open the ``User flows`` page

- Click the ``New user flow`` link to create a user flow

![image](/images/aadb2c/userflow-add.png)

- Select the ``Sign up and sign in`` user flow and select the ``Recommended`` version

![image](/images/aadb2c/userflow-add2.png)

- Add a name for the user flow and select the ``Email signup`` identity provider

![image](/images/aadb2c/userflow-add3.png)

- Set the Multi-Factor Authentication (MFA) as follows:

![image](/images/aadb2c/userflow-add4.png)

- In the ``User attributes and token claims``, click the ``Show more`` link to add the user attributes

- Add the following user attributes and claims :

    - City
    - Country/Region
    - Date of Birth
    - Display Name
    - Email Address
    - Email Addresses
    - Given Name
    - Postal Code
    - State/Province
    - Street Address
    - Surname
    - User's Object ID

![image](/images/aadb2c/userflow-add5.png)

- Click the ``Create`` when you are done

![image](/images/aadb2c/userflow-add6.png)

# Customize the Sign Up page

- Open the user flow

- In the ``Page layouts`` page, select the ``Local account sign up page``

![image](/images/aadb2c/signup-layout.png)

- Format the sign-up page user attributes as follows :

![image](/images/aadb2c/signup-layout2.png)

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



