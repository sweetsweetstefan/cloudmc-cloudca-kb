# Administrator guide:  Presenting CloudMC Services and URLs

When planning a deployment of CloudMC, it is important to decide how the CloudMC Web user interface and API will be presented to end-users.  Will there be a single URL for all organizations, or will each organization be accessed via a custom URL unique to that organization?  CloudMC provides the cloud operator with both of these options.
- Single-entrypoint: All services are exposed via a single common domain name, and the login page is accessed via a common URL with that domain name.  This is the default behaviour
- Multi-entrypoint: Each organization receives a unique domain name, and the login page is accessed via a URL with that unique domain name


## Login entrypoint models
### Single-entrypoint
CloudMC can be configured to provide logins for end-users via a single common URL.  The URL is simply the value of the *public.host* property with no sub-domain.  This URL is the same for all organizations in the system.  All end-users see the same login page with the system branding.

Under this model, it is recommended that the following system properties be configured accordingly:
- **Login via email address** should be enabled
- **Login via username** should be disabled

The above two properties control whether end-users can log in with a username, an email address, or both.  Though it is not required that usernames be disabled and email addresses required, in practice it is easier for end-users to identify themselves with their email address, normally a unique attribute.

With single-entrypoint enabled, accounts must be local.  Organizations cannot have LDAP login configured, because the organization of the end-user is not identified until the user is authenticated.  User accounts are created within each organization, but each account must have an email address that is unique across all organizations in the system (or username if login by username is enabled).

### Multi-entrypoint
CloudMC can be configured to provide logins for end-users via a URL that is unique for each organization.  When multi-entrypoint login is configured, each organization will be associated with an organization code.  The organization code is used as the subdomain for the URL, and the value of the *public.host* property is appended to form the complete domain name for the URL.

Under this model, users are created within each organization, and are completely isolated from other organizations.  This means that both Organization A and Organization B could have users named UserA.  There is no ambiguity for authentication because CloudMC knows which organization to look for when attempting to login, based on the URL that the end-user has accessed.

Because each organization has a unique URL, the login page can be customized with a logo for branding for each organization.

### Pros and cons
| Feature | Single-entrypoint | Multi-entrypoint |
| --- | --- | --- |
| URL to access CloudMC | Common URL for all organizations | Each organization is accessed via a unique URL |
| Custom logo on login page | No | Yes |
| LDAP authentication | No | Yes |
| URL based on the customer name | No | Yes |

- Multi-entrypoint allows arbitrary domain names of long length, which can get messy

- Trials don't allow you to control what the organization code is

- Login by name requires end-users to remember a username, login by email is usually a bit easier to remember.

- In multi-entrypoint,


## How to implement
### Properties to set
single_entrypoint_enabled
login_via_email_enabled
login_via_username_enabled

### Changing login model
