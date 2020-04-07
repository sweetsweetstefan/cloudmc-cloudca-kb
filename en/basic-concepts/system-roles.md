---
title: "Using system roles to enforce access control"
slug: system-roles
---


The **system role(s)** assigned to a user determines the features available to him/her. A role is a set of permissions within the system. For example, the  Users create permission is part of the Organization Admin role, but is not part of the End-User role. As a result, only a user with the Organization Admin role can create new users within his organization.

To check your current **System role(s)**, do the following:

1. In the username menu (in the menu bar), select **Preferences**:

![Preferences menu](/assets/preferences-en.jpg)

2. Look for the **System roles** value:

![Preference edit page](/assets/preferences-edit-en.jpeg)

By default, cloud.ca provides two basic system roles ( Organization Admin and End-User). If you require a more granular security model, you can create more roles, using any combination of permissions. You can then select multiple roles for any given user, wher" the result is the union of all permissions of the different roles.

To prevent role escalation, a user who has the Users update permission can only assign roles that he possesses himself.
