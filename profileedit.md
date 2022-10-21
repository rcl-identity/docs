---
title: Profile Editing
description: Profile Editing for the RCL Digital Identity Application.
has_children: false
nav_order: 10
---

# Profile Editing
**V7.0.0**

You can manage user profile editing by using a **User Flow** in the AAD B2C tenant.

> You should create separate user flows for Self Asserted and Verified Digital IDs. Both will have different user claims.

- In the B2C tenant, open the ``User flows`` page

- Click the ``New user flow`` link to create a user flow

![image](/images/aadb2c/userflow-add.png)

- Select the ``Profile editing`` user flow and select the ``Recommended`` version and click the ``Create`` button

![image](/images/profileedit/userflow-add.png)

- Add a name for the user flow and set the ``Local accounts`` to **Email sign in**

    - For a Self Asserted Digital ID, you can use the name : ``profile_edit_sa``
    - For a Verified Digital ID, you can use the name : ``profile_edit``

![image](/images/profileedit/userflow-add2.png)

- Select the ``Email signup`` identity provider and set the Multi-Factor Authentication (MFA) as follows:

![image](/images/aadb2c/userflow-add4.png)

- In the ``User attributes and token claims``, click the ``Show more`` link to add the user attributes

- Add the following user attributes and claims :

- *Claims for Self Asserted Digital Identity*

    - City
    - Country/Region
    - Display Name
    - Given Name
    - Postal Code
    - State/Province
    - Street Address
    - Surname

- *Claims for the Verified Digital ID*

    - City
    - Postal Code
    - State/Province
    - Street Address

![image](/images/profileedit/userflow-add3.png)

- Click the ``Create`` button when you are done

![image](/images/profileedit/userflow-add4.png)

You can now reference the user flow in your [Identity Self Assertion Application]() or [Identity Enrollment Application]() to allow users to edit their personal information data.