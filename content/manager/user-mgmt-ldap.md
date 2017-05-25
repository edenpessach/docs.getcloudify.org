---
layout: bt_wiki
title: LDAP and Managing Users
category: Manager
draft: false
weight: 890
---
 Click here for additional information about [managing users]({{< relref "cli/users.md" >}}) and here for information about [managing user groups]({{< relref "cli/user-groups.md" >}}).

## Managing Users and User Groups
Users and groups can only be managed by users with an `admin` role. Each Cloudify Manager has a default `super-admin` user that cannot be deleted. This user is the default `admin` for all tenants in the Cloudify Manager instance. You can add other users to the tenant.  

Use the user-related commands that are listed later in this topic to add a new user or user group to a tenant. You can add users individually or as part of a group. You can add them manually, or via your organization's LDAP/AD setup.  
  * To add a user or user group via LDAP/AD, connect to the LDAP/AD service.
  * To add a single user or user group manually, specify the name of the user or group as part of the command.  
  * Specify a password and role for users that you add manually.  
    Users who are added from LDAP/AD retain their LDAP/AD password. You might still want to assign them a role.

If you are connected to an LDAP/AD service, the names of user groups must match those defined in the service.   

#### Tenant-Related User Management Commands

There are a number of actions related to user access to tenants that an **`admin`** user can perform. 
To run these tenant-specific commands, use `cfy tenant`.

- `add-user` enables you to add an individual user to a tenant
- `add-user-group` enables you to add a group of users to a tenant
- `create` enables you to create a tenant
- `delete` enables you to delete a tenant
- `get` enables you to view information about the tenant, including its users
- `list` provides a list of all tenants in this instance of Cloudify Manager  
  By default, when you generate the list of tenants, only the number of linked resources is displayed. You can retrieve full details with the use of a `--get-data` flag.
- `remove-user` enables you to remove a specific user from a group
- `remove-user-group` enables you to remove a user group from a tenant

## Connecting Cloudify Manager to LDAP

To connect Cloudify Manager with LDAP/AD, you must know the the URL of the service and have sufficient credentials to perform searches and so on. 

You configure Cloudify with the LDAP configuration during the bootstrap process, in the `manager-input` section. You can also use the API to configure an LDAP connection after Cloudify Manager is installed, using the `cfy ldap set` command, as long as the manager is _clean_, meaning that no tenants, groups, users or resources exist in it.

### How Cloudify Manager Works with the LDAP/AD Service

When a user logs in to Cloudify Manager, their credentials are passed to the LDAP/AD service for authentication. By default, all users in the LDAP/AD service are authenticated to Cloudify Manager, however only users who have specific permissions for a tenant can access it. 

When a user logs into Cloudify Manager, the service authenticates the user and returns a list of any groups to which the user belongs. 

In Cloudify Manager, if you have added a group to a tenant, using the process that complies with the requirements for defining a group specified in LDAP/AD, all users in that LDAP group can access the tenant (unless an individual user is specifically suspended from the tenant.) The For more information about specifying LDAP/AD-compliant user-group names, see *Adding Users* on the [Tenant Management]({{< relref "manager_webui/tenant-management-page.md" >}}) page.

LDAP passwords are not saved in Cloudify Manager.

The following graphic indicates how Cloudify Manager interacts with an LDAP/AD service. 

![User/LDAP relationship]({{< img "manager/multi-tenancy-ldap-relationship.png" >}})



