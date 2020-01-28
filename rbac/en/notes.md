Fine-grained Role-Based Access Control (RBAC)
Five standard roles are provided out of the box and any number of custom roles can be defined on a per-tenant basis.

Access to environments can be granted on a per-user basis based on specific role.

Scope!  Need to refer to that a bunch of times

Tags!

A user can exist with no environments

A user must exist within an organization, System is the built-in organization.

Can a plugin add permissions or create roles?

Just to environment roles

Is there a use-case for a guest account in System with an additional role of Operator?



Look at the permissions and see what you can't shuffle together in terms of ideas for roles.  For example, billing admin.  Could there be a network only admin easily possible?

Why is it  that for the stef-test account, which has a primary role of guest in the System org, can't create accounts even though the name of the permission is Environments: Create and scoped to the Aptum org.  How come the guest account needs the Environments:Own All permission is necessary for getting this to work,


What if a single email address needs to be added as a user to multiple organizations?  

Can someone with a primary role as user inside an organization be restricted to particular service connections?

So a User can see all service connections and can create environments, but can't see any existing environments until they're added.

Interesting note:  if you give a custom role zero privileges and scope global, they will be able to see every organization, but they won't see any environments inside the organization.
