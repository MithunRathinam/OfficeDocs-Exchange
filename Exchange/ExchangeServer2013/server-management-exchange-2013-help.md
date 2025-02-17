---
title: 'Server Management: Exchange 2013 Help'
TOCTitle: Server Management
ms:assetid: 30cbc4de-adb3-42e8-922f-7661095bdb8c
ms:mtpsurl: https://technet.microsoft.com/library/Dd876866(v=EXCHG.150)
ms:contentKeyID: 49289215
ms.reviewer: 
ms.topic: article
description: About the Server Management management role group in Microsoft Exchange
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Server Management

_**Applies to:** Exchange Server 2013_

The Server Management management role group is one of several built-in role groups that make up the Role Based Access Control (RBAC) permissions model in Microsoft Exchange Server 2013. Role groups are assigned one or more management roles that contain the permissions required to perform a given set of tasks. The members of a role group are granted access to the management roles assigned to the role group. For more information about role groups, see [Understanding management role groups](understanding-management-role-groups-exchange-2013-help.md).

Administrators who are members of this role group can configure server-specific configuration of transport client access, and mailbox features such as database copies, certificates, transport queues and Send connectors, virtual directories, and client access protocols.

This role group is similar to the Exchange Server Administrators role in Microsoft Exchange Server 2007. It grants access to manage the configuration of physical servers. However, unlike the Exchange Server Administrators role in Exchange 2007, which provided access only to a local server running Exchange 2007, the Server Management role group enables access to view and configure all Exchange Server 2010 servers in the organization.

If you want to allow administrators to manage only specific servers in your organization, you can change the management scopes that are applied to this role group. Alternatively, you can create a role group, based on the Server Management role group, and customize the management scopes on the new role group. For more information, see the "Role Group Customization" section later in this topic.

For more information about RBAC, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

## Role group membership

If you want to add or remove members to or from this role group, see [Manage role group members](manage-role-group-members-exchange-2013-help.md).

By default, only members of the Organization Management role group can add or remove members from this role group. For more information about how to add additional role group delegates, see the "Add or remove a role group delegate" section in [Manage role groups](manage-role-groups-exchange-2013-help.md).

You can use the following command to view a list of users or universal security groups (USGs) that are members of this role group.

```powershell
Get-RoleGroupMember "Server Management"
```

For more information about the members of a role group, see [View the members of a role group](manage-role-group-members-exchange-2013-help.md) in [Manage role group members](manage-role-group-members-exchange-2013-help.md).

## Role group customization

This role group is assigned management roles by default. The roles that are included are listed in the "Management Roles Assigned to this Role Group" section. You can add or remove role assignments to or from this role group to match the needs of your organization.

The role groups provided with Exchange 2013 are designed to match more granular tasks. By assigning roles to a role group, you enable the members of that role group to perform the tasks associated with the role. For example, the Journaling role enables the management of the Journaling agent and journaling rules. For more information about how roles are assigned to role groups, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

The roles assigned to this role group are given default management scopes. Management scopes determine what Exchange objects can be viewed or modified by the members of a role group. You can change the scopes associated with assignments between roles and role groups. For example, you might want to do this if you only want members of a role group to be able to change recipients that are under a specific organizational unit or in a specific location. For more information about management scopes, see [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md).

For more information about how to customize this role group, see the following topics:

- [Manage role groups](manage-role-groups-exchange-2013-help.md)
- [Manage role group members](manage-role-group-members-exchange-2013-help.md)

If you want to create a role group and assign some of the roles that are assigned to this role group to the new role group, see the "Create a role group" section in [Manage role groups](manage-role-groups-exchange-2013-help.md).

## Management roles assigned to this role group

The following table lists all the management roles that are assigned to this role group and the following attributes of each role assignment:

- **Regular assignment**: Enables members of the role group to access the management role entries made available by the associated management role.
- **Delegating assignment**: Gives members of the role group the ability to assign the specified role to other role groups, role assignment policies, users, or USGs.
- **Recipient read scope**: Determines what recipient objects members of the role group are allowed to read from Active Directory.
- **Recipient write scope**: Determines what recipient objects members of the role group are allowed to modify in Active Directory.
- **Configuration read scope**: Determines what configuration and server objects members of the role group are allowed to read from Active Directory.
- **Configuration write scope**: Determines what organizational and server objects members of the role group are allowed to modify in Active Directory.

For more information about role assignments and management scopes, see the following topics:

- [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md)
- [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md)

|Management role|Regular assignment|Delegating assignment|Recipient read scope|Recipient write scope|Configuration read scope|Configuration write scope|
|---|:---:|:---:|---|---|---|---|
|[Database Copies role](database-copies-role-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Databases role](databases-role-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Exchange Connectors role](exchange-connectors-role-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Exchange Server Certificates role](exchange-server-certificates-role-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Exchange Servers role](exchange-servers-role-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Exchange Virtual Directories role](exchange-virtual-directories-role-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Monitoring role](monitoring-role-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[POP3 and IMAP4 Protocols role](pop3-and-imap4-protocols-role-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Receive Connectors role](receive-connectors-role-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Transport Queues role](transport-queues-role-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
