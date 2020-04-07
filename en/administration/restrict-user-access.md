---
title: "Restrict user access"
slug: restrict-user-access
---


The role a user has determines the features available to that user. A role is a set of permissions within the system. For example, the *Users create* permission is part of the *Org. Admin* role, but is not part of the *End-User* role. As a result, only an Org admin can create new users.

To check your current role, do the following:

- In the username menu (in the menu bar), select **Preferences** and look for the **System roles** value.

By default, there are two pre-configured roles (Org. Admin and End-User). If you require a more granular security model, you can create more roles, using any combination of permissions. You can then select multiple roles for any given user, where the result is the union of all permissions of the different roles).

To avoid role escalation, a user who has the *Users update* permission can assign only roles that he possesses himself.
