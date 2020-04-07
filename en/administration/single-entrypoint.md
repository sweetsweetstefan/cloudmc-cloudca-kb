---
title: "Presenting CloudMC Services and URLs: Single vs Multiple entry-point"
slug: single-entrypoint
---


When planning a deployment of CloudMC, it is important to decide how the CloudMC Web user interface and API will be presented to end-users.  Will there be a single URL for all organizations, or will each organization be accessed via a custom URL unique to that organization?  CloudMC provides the cloud operator with both of these options.
- Single entry-point: The portal is exposed via a common domain name. The login page is accessed using the same URL for all organizations.  This is the default behaviour
- Multi entry-point: Each organization receives a unique domain name.  The login page is accessed via a URL with that name


## Login entrypoint models
### Single entry-point
CloudMC can be configured to provide logins for end-users via a single common URL.  The URL is simply the value of the *public.host* property with no sub-domain.  This URL is the same for all organizations in the system.  All end-users see the same login page with the system branding.

Under this model, it is recommended that the following system properties be configured accordingly:
- **Login via email address** should be enabled
- **Login via username** should be disabled

The above two properties control whether end-users can log in with a username, an email address, or both.  Though it is not required that usernames be disabled and email addresses required, in practice it is easier for end-users to identify themselves with their email address, which is normally a unique attribute and is unlikely to be forgotten.

With single entry-point enabled, user accounts are created within each organization, but each account must have an email address (or username, if login via username is enabled) that is unique across all organizations in the system.

### Multi entry-point
CloudMC can be configured to provide logins for end-users via a URL that is unique for each organization.  When multi entry-point login is configured, each organization will be associated with an organization code.  The organization code is used as the subdomain for the URL, and the value of the *public.host* system property is appended to form the complete domain name for the URL.

Under this model, users are created within each organization, and are completely isolated from other organizations.  This means that both Organization A and Organization B could have users named UserA.  There is no ambiguity for authentication since the URL tells CloudMC which organization is being accessed.

Because organizations have unique URLs, each login page can be customized with a logo for branding.

### Comparison
| Feature | Single entry-point | Multi entry-point |
| --- | --- | --- |
| Common URL for all organizations | Yes | No |
| Each organization is accessed via a unique URL | No | Yes |
| Custom logo on login page | No | Yes |
| LDAP authentication | Yes | Yes |
| URL based on the customer code | No | Yes |
| Role-based access control | Yes | Yes |
| Trials can introduce lengthy and arbitrary domain names | No | Yes |
| Duplicate email addresses (or usernames) allowed across organizations | No | Yes |


## How to implement
### Properties to set
The login model is controlled by a CloudMC system property, under *System* -> *Properties*.  This requires the Operator role, or the *Configuration properties: Manage* permission assigned with a scope of **All Organizations**.

To enable single entry-point (enabled by default):
- **single_entrypoint_enabled** = true

To enable multi entry-point:
- **single_entrypoint_enabled** = false

When single entry-point is enabled, it is recommended to have the following two properties set accordingly:
- **login_via_email_enabled** = true
- **login_via_username_enabled** = false

![system properties](/assets/entrypoint-properties-en.png)

### Changing login model
CloudMC allows you to switch between login models at any time.  However, conflicting emails or usernames will have to be manually resolved prior to enabling single entry-point.

**Important:** CloudMC does not check for conflicts when switching between login models, therefore any existing conflicts will produce unexpected results when such a user attempts to log in.
