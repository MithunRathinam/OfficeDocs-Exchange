---
title: 'Org Custom Apps role: Exchange 2013 Help'
TOCTitle: Org Custom Apps role
ms:assetid: ab2aac13-f783-43e6-a369-75cce1d4943f
ms:mtpsurl: https://technet.microsoft.com/library/JJ657482(v=EXCHG.150)
ms:contentKeyID: 49289371
ms.reviewer: 
manager: serdars
ms.topic: article
description: About the Org Custom Apps role in Microsoft Exchange
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Org Custom Apps role

_**Applies to:** Exchange Server 2013_

The Org Custom Apps management role enables administrators to view and modify their organization's apps, and to add custom apps from a file or URL.

## Default management role assignments

This role has role assignments to one or more role assignees. The following table indicates whether the role assignment is regular or delegating, and also indicates the management scopes applied to each assignment. The following list describes each column:

- **Regular assignment**: Regular role assignments enable the role assignee to access the permissions provided by the management role entries on this role.
- **Delegating assignment**: Delegating role assignments give the role assignee the ability to assign this role to role groups, users, or USGs.
- **Recipient read scope**: The recipient read scope determines what recipient objects the role assignee is allowed to read from Active Directory.
- **Recipient write scope**: The recipient write scope determines what recipient objects the role assignee is allowed to modify in Active Directory.
- **Configuration read scope**: The configuration read scope determines what configuration and server objects the role assignee is allowed to read from Active Directory.
- **Configuration write scope**: The configuration write scope determines what organizational and server objects the role assignee is allowed to modify in Active Directory.

### Default management role assignments for this role

|Role group|Regular assignment|Delegating assignment|Recipient read scope|Recipient write scope|Configuration read scope|Configuration write scope|
|---|:---:|:---:|---|---|---|---|
|[Organization Management](organization-management-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
