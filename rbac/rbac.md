# Role-based access controls

Access control in CloudMC is achieved through a flexible, multi-tenant model that provides a simplified way to manage permissions across a hierarchy of organizations and environments.  Role-based access control (RBAC) features built into CloudMC allow fine-grained control over the permissions which are granted to users.

## Definitions
- Permission: An authorization to execute a particular task.  CloudMC has system permissions which govern the CloudMC console, and environment permissions which govern a service's virtual resources.

- Role: A defined collection of permissions inside an organization.  CloudMC comes with five system roles which cannot be modified: Operator, Reseller, Administrator, User, Guest.  Custom roles can be created.

- Scope: The organization or organizations to which a role is applied.

- Organization: A logical unit to which users and service connections can be assigned.  A base installation of CloudMC comes with the System organization.

- User:  A user account is how an individual connects to the CloudMC portal.  A user is always assigned a primary role in a single organization. A user can be assigned additional roles, which can be scoped to one or more organizations.

- Environment:  A logical unit within an organization, used to isolate and group resources securely. (Is environment relevant to RBAC?  Are Viewer/Editor/Owner documented elsewhere?  There may be some confusion for users here because when adding a user to an environment, the word "role" is used, but these are different roles.)

![user access control chart](roles_chart.png)
## Using roles to enforce user access
The function of a role is to provide a simple and standard set of permissions to users within an organization.  Roles can also provide access to a user in a different organization.  The five roles included with CloudMC are applicable to a broad range of use cases.  

Roles have a scope, which can be any of the following:
- All organizations
- Top-level organizations only
- A specific organization but not its sub-organizations
- A specific organization and its sub-organizations
- Only the sub-organizations of a specific organization
- All organizations with a specific tag

## Explanation of the system roles
![permissions chart](permissions.png)

Summary of each role:
- Guest: A read-only role.  Can view resources in scoped organizations.
- User: Can create and environments in scoped environments.
- Administrator: Can manage scoped organizations.  Cannot view sub-organizations nor create new organizations. Can create environments, users, roles, and access usage data in scoped organizations.
- Reseller: Can manage branding and pricing in scoped organizations and sub-organizations.
- Operator: Can create organizations, manage service connections, quotas, commitments, and full access to all other system resources.

Each system role has a default scope:
- Guest: Only the organization in which the user exists
- User: Only the organization in which the user exists
- Administrator: Only the organization in which the user exists  
- Reseller: The organization in which the user exists and all of its sub-organizations
- Operator: All organizations

Primary role must be one of the five standard roles, it can never be a custom role.

## Use cases
- Administrator, single organization
- Administrator of one organization, read-only for another organization
- Network administrator, no instances
- Administrator of customers, tag the customer orgs so that admins with that role automatically get correct permissions
- Billing administrator
