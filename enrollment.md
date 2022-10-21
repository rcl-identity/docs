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