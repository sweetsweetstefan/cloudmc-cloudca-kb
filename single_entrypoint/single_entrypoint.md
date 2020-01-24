# Administrator guide:  Login entrypoint

When presenting CloudMC services to end-users, two separate models of login are available to the cloud operator:
- Each organization receives a unique domain name, the login page is accessed via a URL with that unique domain name, and end-users log in with a username defined in the organization
- All services are exposed via a single common domain name, the login page is access via a common URL with that domain name, and end-users log in with an email address that is unique across all organizations in the system


## Login models
### Multi-entrypoint
CloudMC can be configured to provide logins for end-users via a URL that is unique for each organization.  When multi-entrypoint login is configured, each organization will be associated with an organization code.  This code is used as the subdomain for the URL, and the value of the *public.host* property is appended to form the complete domain name for the URL.

Under this model, users are created within each organization, and are completely isolated from other organizations.  This means that both Organization A and Organization B could have users named UserA.  There is no ambiguity at login because CloudMC does user-lookup based on the URL that was used to access the login page.


### Single-entrypoint
CloudMC can be configured to provide logins for end-users via a single common URL, and is simply the value of the *public.host* property with no sub-domain.  This URL is the same for all organizations.

Under this model, users are still created within each organization, but are identified via email address rather than by a username.

Organizations cannot have LDAP login configured because this is incompatible with systems where email-based login is enabled.

### Pros and cons

## When to use

## How to implement
### Properties to set
### Changing login model
