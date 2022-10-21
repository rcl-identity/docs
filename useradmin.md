---
title: User Admins
description: Getting started with the RCL Digital Identity Application.
has_children: false
nav_order: 3
---

# User Admins
**V7.0.0**

> This section only applies to organizations issuing [Verified Digital IDs](./index.md#verified-digital-identity). You can ignore this section if your are issuing [Self Asserted Digital IDs](/index.md#self-asserted-digital-identity)

A User Admin is a user account that has been assigned access to the [Identity Proofing Application]() to perform the identity verification process. In this section, we will learn how to create a *User* and add the user to the **UserAdmins** *Security Group*.

# Create a UserAdmins Group

The Azure AD B2C tenant does not allow the creation of ``Security Groups``. You will need to create the group in the underlying Azure AD tenant.

- Open the AAD B2C tenant and click the ``Home`` link

![image](/images/useradmin/group-add.png)

- You are now in the underlying AAD tenant. Select the the ``Azure Active Directory`` icon

![image](/images/useradmin/group-add2.png)

- In the AAD tenant, select the ``Groups`` page

![image](/images/useradmin/group-add3.png)

- In the ``Groups`` page, click on the ``New group`` link

![image](/images/useradmin/group-add4.png)

- Create a ``Security Group`` named **UserAdmins**

![image](/images/useradmin/group-add5.png)

- Click the ``Create`` button when you are done

![image](/images/useradmin/group-add6.png)

# Create a User

In this section, we will create a user who will have access to the [Identity Proofing Application]().

- Open the AAD B2C tenant and click the ``users`` link

![image](/images/useradmin/user-add.png)

- In the ``User`` page, click the ``New user`` link

![image](/images/useradmin/user-add2.png)

- Select ``Azure AD B2C`` user

![image](/images/useradmin/user-add3.png)

- Add a user, assign an email (username) and password to the user. You will need to provide the password to the user to login.

![image](/images/useradmin/user-add4.png)

- Click the ``Create`` button when you are done

![image](/images/useradmin/user-add5.png)

# Add the User to the UserAdmins Group

- Select the user and click on the ``Groups`` page

![image](/images/useradmin/user-group-add.png)

- Click the ``Add membership`` link, then, choose the ``UserAdmins`` group

![image](/images/useradmin/user-group-add2.png)

- Click the ``Select`` button when you are done


![image](/images/useradmin/user-group-add3.png)

The user is now added to the UserAdmins group and can access the [Identity Proofing Application]() to verify the physical identity of persons signing up for a Digital ID.

**The user should be part of the [Identity Approver](aadb2c.md#customize-the-sign-up-page) organization, user or department.**


