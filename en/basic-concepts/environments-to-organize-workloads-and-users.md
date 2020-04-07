---
title: "Using Environments to organize users & workloads"
slug: environments-to-organize-workloads-and-users
---

## Environments overview
cloud.ca provides a powerful mechanism, **environments**, to segregate workloads/ressources and control who get access to those. A typical use case of this concept is to create distinct environments to isolate production workloads from development systems, or to establish project-specific [sandboxes](https://en.wikipedia.org/wiki/Sandbox_%28computer_security%29).

An environment belongs to an organization, is associated with a specific service (e.g.: Compute or Object Storage) and is comprised of a set of users who have visibility on a pool of shared resources (e.g.: instances, storage, etc). New cloud.ca organizations are provisioned with default environments, which are accessible to all their users. However, any user with the **Environment Create** permission (given by default to members of the Organization Admin role) can add additional environments and decide who should have access to it.

Although cloud.ca calculates service usage at the organization-level for billing purpose, the resources consumed by each environments are also tracked separately, which allows businesses to generate internal chargeback reports on a per-environment basis if they wish.

## Environment Roles
Furthermore, the environment membership is also coupled with an environment role, which controls what a user can do with the resources contained in this environment. Contrary to [System](system-roles.md) roles, the Environment roles are fixed and cannot (yet) be customized granularly.
