---
title: 'Client protocol management: Exchange 2013 Help'
TOCTitle: Client protocol management
ms:assetid: 89ba6d24-d1d3-46d5-a0ae-61f0d4c6df21
ms:mtpsurl: https://technet.microsoft.com/library/JJ657727(v=EXCHG.150)
ms:contentKeyID: 49300565
ms.topic: article
description: Client protocol management for Exchange 2013 Help.
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Client protocol management

_**Applies to:** Exchange Server 2013_

Management of the client protocols of Exchange ActiveSync, Outlook Web App, POP3, IMAP4, the Autodiscover service, Exchange Web Services, and the Availability service occurs in three different areas: the Exchange admin center (EAC), the Exchange Management Shell, and Internet Information Services (IIS) Manager. The settings that are managed in each location vary per client protocol.

## Managing Outlook Web App settings

Most of the settings that affect which Outlook Web App features are available to users can be set on the Outlook Web App virtual directory or can be configured in an Outlook Web App mailbox policy. By using Outlook Web App mailbox policies, you can define the features available to individual users. Mailbox policy settings override virtual directory settings. For more information on managing Outlook Web App, see [Outlook Web App](outlook-web-app-exchange-2013-help.md).

## Managing Exchange ActiveSync settings

In Exchange 2010, all client access protocols were implemented and managed on a single server role, the Client Access server role. Management of the protocols was performed on a single instance of IIS, there was a single virtual directory object in Active Directory for each client protocol, and a single set of cmdlets were used to configure the virtual directory.

In Exchange 2013, the client protocol management for Exchange ActiveSync is split between the Client Access server and the Mailbox server. Because of this architecture change, you can run different virtual directory management tasks on both the Client Access server and the Mailbox server. If these two servers aren't installed on the same physical computer, the parameters that you use with the virtual directory cmdlets will change based on the server role on which you are running them.

For more information about the architecture changes in Exchange 2013, see [What's new in Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).

There are two types of settings that can be applied to the Exchange ActiveSync virtual directory:

- Settings applicable to the mailbox session

- Settings applicable to the server and the virtual directory

The settings that are applicable to the mailbox session are user session settings. When a user connects to a Client Access server, the connection is proxied to the Mailbox server that contains the user's mailbox. A unique identifier of the virtual directory is included with the proxied request. The Mailbox server then retrieves the virtual directory settings from Active Directory and applies them to the session. The virtual directory settings are cached on the Mailbox server to improve performance.

If the connection is proxied to a different Active Directory site, the virtual directory settings will be loaded from the Client Access server in the same site as the Mailbox server, not from the Client Access server where the connection originated.

The following tables indicate which virtual directory settings can be managed on which servers. If you try to manage a particular setting on a server for which it isn't applicable, you will receive an error message indicating that the property you are trying to set is read-only for the server that you are operating on.

**Exchange ActiveSync virtual directory settings on Client Access servers**:

|Setting|Server|
|---|---|
|BadItemReportingEnabled|Client Access|
|BasicAuthEnabled|Client Access|
|ClientCertAuth|Client Access|
|CompressionEnabled|Client Access|
|ExternalAuthenticationMethods|Client Access|
|ExternalURL|Client Access|
|InternalAuthenticationMethods|Client Access|
|InternalURL|Client Access|
|MobileClientCertificateAuthorityURL|Client Access|
|MobileClientCertificateProvisioningEnabled|Client Access|
|MobileClientCertTemplateName|Client Access|
|RemoteDocumentsActionForUnknownServers|Client Access|
|RemoteDocumentsAllowedServers|Client Access|
|RemoteDocumentsBlockedServers|Client Access|
|RemoteDocumentsInternalDomainSuffixList|Client Access|
|SendWatsonReport|Client Access|

**Exchange ActiveSync virtual directory settings on Client Access and Mailbox servers**:

|Setting|Server|
|---|---|
|ApplicationRoot|Client Access and Mailbox|
|AppPoolID|Client Access and Mailbox|
|MetabasePath|Client Access and Mailbox|
|Name|Client Access and Mailbox|
|Path|Client Access and Mailbox|
|ProxySubVdir|Client Access and Mailbox|
|VirtualDirectoryName|Client Access and Mailbox|
|WebsiteName|Client Access and Mailbox|

## Managing POP3 and IMAP4 settings

In Exchange 2013, the implementation of the POP3 and IMAP4 protocols has also been segmented between the Client Access and Mailbox server roles. Due to the new implementation, POP3 and IMAP4 connectivity are each managed by a service on the Client Access server, as well as by a service on the Mailbox server. The names of the services that run on the Client Access server are the same as the names that existed in Exchange 2010: Microsoft Exchange IMAP4 service and Microsoft Exchange POP3 service. The names of the two new services that run on the Mailbox server are the Microsoft Exchange IMAP4 Backend service and the Microsoft Exchange POP3 Backend service.

Consider the following as you manage POP3 and IMAP4 connectivity in your organization:

- If you are running the Client Access server role and the Mailbox server role on the same computer, any changes you make to POP3 or IMAP4 settings are automatically applied to the correct POP3 and IMAP4 services.

- If you are running the Client Access server role and the Mailbox server role on separate computers, you need to manage the settings on the computer that manages the setting you want to change.

Use the following tables indicate which POP/IMAP settings are each server role.

**POP3 and IMAP4 settings on Client Access server**:

|Setting|Server|
|---|---|
|AuthenticatedConnectionTimeout|Client Access|
|Banner|Client Access|
|ExternalConnectionSettings|Client Access|
|InternalConnectionSettings|Client Access|
|MaxCommandSize|Client Access|
|MaxConnectionFromSingleIP|Client Access|
|MaxConnections|Client Access|
|MaxConnectionsPerUser|Client Access|
|PreAuthenticatedConnectionTimeout|Client Access|
|UnencryptedOrTLSBindings|Client Access|

**POP3 and IMAP4 settings on Mailbox server**:

|Setting|Server|
|---|---|
|CalendarItemRetrivalOption|Mailbox|
|EnableExactRFC822Size|Mailbox|
|MessageRetrievalSortOrder|Mailbox|
|OWAServerURL|Mailbox|
|ProxyTargetPort|Mailbox|
|ShowHiddenFoldersEnabled|Mailbox|
|SuppressReadReceipt|Mailbox|

**POP3 and IMAP4 settings on Client Access and Mailbox servers**:

|Setting|Server|
|---|---|
|X509CertificateName|Client Access and Mailbox|
|EnforceCertificateErrors|Client Access and Mailbox|
|LogFileLocation|Client Access and Mailbox|
|LogFileRolloverSettings|Client Access and Mailbox|
|LoginType|Client Access and Mailbox|
|LogPerFileSizeQuota|Client Access and Mailbox|
|ProotocolLogEnabled|Client Access and Mailbox|
|Server|Client Access and Mailbox|
|X509CertificateName|Client Access and Mailbox|
