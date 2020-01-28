# Use cases: Basic
The following are use cases to illustrate the flexibility of CloudMC roles with real-world examples.  Unless otherwise indicated, the examples assume an account that has a primary role of *Guest*, no additional roles,  *Viewer* access on at least one environment in the organization, and that the account is created in the organization intended to be accessed.  These are examples only, individual needs will vary.

The diagram below depicts two hypothetical organizations with environments and a sub-organization.  Note that Organization A has two tags, **billable** and **managed**, and Sub-organization C has one tag, **billable**.

![use cases diagram](use_cases-en.png)

| Scenario | Role configuration | Notes from example |
| --- | --- | --- |
| Access to dashboards, view lists of resources | Primary role *Guest*, "Viewer" access on the assigned environments in the organization | Applied to a user in environment2, this would grant read-only access to only environment2 |
| Approve, deny, and purge trial organizations (Trials Administrator) | Additional custom role with the *Trials:Manage* permission.  Role must use *All organizations* for scope. |
| Create and delete users only (User Manager) | Additional custom role with the *Users:Manage* permission, scoped for the desired organizations |
| Create, edit, and delete knowledge base articles | Additional custom role with the *Content:Manage* permission.  Role must use *All organizations* for scope |
| Select logos and colour schemes (Branding manager) | Additional custom role with the permission *Branding:Manage*, scoped to the desired organizations |
