---
title: 'Transport agents: Exchange 2013 Help'
TOCTitle: Transport agents
ms:assetid: e7389d63-3172-40d5-bf53-0d7cd7e78340
ms:mtpsurl: https://technet.microsoft.com/library/Bb125012(v=EXCHG.150)
ms:contentKeyID: 48385663
ms.reviewer: 
ms.topic: article
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
description: Learn about the transport agents in Exchange 2013.
---

# Transport agents

_**Applies to:** Exchange Server 2013_

Transport agents let you install custom software that is created by Microsoft, by third-party vendors, or by your organization, on an Exchange server. This software can then process email messages that pass through the transport pipeline. In Microsoft Exchange Server 2013, the transport pipeline is made of the following processes:

- The Front End Transport service on Client Access servers

- The Transport service on Mailbox servers

- The Mailbox Transport service on Mailbox servers

- The Transport service on Edge Transport servers

For more information about the transport pipeline, see [Mail flow](mail-flow-exchange-2013-help.md)

Like the previous version of Exchange, Exchange 2013 transport provides extensibility through the Microsoft Exchange Server 2013 Transport Agents SDK. The Exchange 2013 version of the SDK is based on the Microsoft .NET Framework version 4.0 and allows third parties to implement the following predefined classes:

- **SmtpReceiveAgent**

- **RoutingAgent**

- **DeliveryAgent**

When complied against libraries in the SDK, the resulting assemblies are registered with Exchange 2013, which loads the agents and invokes their event handlers during specific stages of the SMTP sessions or message processing. These stages, or events, are part of the agent definitions. The agent registration information is stored in an XML configuration file.

The following list explains the requirements for using transport agents in Exchange 2013.

- The Transport service on Mailbox servers and Edge Transport servers fully supports all the predefined classes in the SDK, and therefore any third-party transport agents written for the Hub Transport or Edge Transport server roles in Microsoft Exchange Server 2010 should work in the Transport service in Exchange 2013.

- The Front End Transport service only supports the **SmtpReceiveAgent** class in the SDK, and third-party agents can't operate on the **OnEndOfData** SMTP event.

- The Mailbox Transport service doesn't support the SDK at all, so you can't use any third-party agents in the Mailbox Transport service.

Support for legacy transport agents based on versions of the .NET Framework prior to version 4.0 isn't enabled by default, but you can enable it. For instructions, see [Enable support for legacy transport agents](enable-support-for-legacy-transport-agents-exchange-2013-help.md).

## Updates to transport agent management

Due to the updates to the Exchange 2013 transport pipeline, the transport agent cmdlets need to distinguish between the Transport service and the Front End Transport service, especially if the Client Access server and the Mailbox server are installed on the same computer. For more information, see [Manage transport agents](manage-transport-agents-exchange-2013-help.md).

Transport Agent management cmdlets manipulate a configuration file located at `%ExchangeInstallPath%TransportRoles\Shared`. For the Transport service on Mailbox servers and Edge Transport servers, the file is `agents.config`. For the Front End Transport service on Client Access servers, the file is `fetagents.config`. Both files use the same format as in Exchange 2010. For more information about managing transport agents, see [Manage transport agents](manage-transport-agents-exchange-2013-help.md).

## Transport agents and SMTP events

Transport agents use SMTP events. These events are triggered as messages move through the transport pipeline. SMTP events give transport agents access to messages at specific points during the SMTP conversation and during routing of messages through the organization.

Note that there are new SMTP Receive events in Exchange 2013. SMTP Receive exists in the Front End Transport service on Client Access servers, the Transport service on Mailbox servers and Edge Transport servers and the Mailbox Transport Delivery service on Mailbox servers. The categorizer exists only in the Transport service on Mailbox servers and Edge Transport servers. For more information about transport services and the categorizer, see [Mail routing](mail-routing-exchange-2013-help.md).

The following tables list the SMTP events that provide access to messages in the transport pipeline.

### SMTP Receive events

|Sequence|SMTP event|Description|
|:---:|---|---|
|1|**OnConnectEvent**|This event is triggered by the initial connection from a remote SMTP host.|
|2|**OnHeloCommand**|This event is triggered when the `HELO` command is issued by the remote SMTP host.|
|3|**OnEhloCommand**|This event is triggered when the `EHLO` command is issued by the remote SMTP host.|
|4|**OnStartTlsCommand**|This event is triggered when the `STARTTLS` command is issued by the remote SMTP host.|
|5|**OnAuthCommand**|This event is triggered when the `AUTH` command is issued by the remote SMTP host.|
|6|**OnProcessAuthentication**|This event is triggered when authentication with the remote SMTP host is being processed.|
|7|**OnEndOfAuthentication**|This event is triggered when the remote SMTP host has completed authentication.|
|8|**OnXSessionParamsCommand**|This event is triggered when the `XSESSIONPARAMS` command is issued by the remote SMTP host.|
|9|**OnMailCommand**|This event is triggered when the `MAIL FROM` command is issued by the remote SMTP host.|
|10|**OnRcptToCommand**|This event is triggered when the `RCPT TO` command is issued by the remote SMTP host.|
|11|**OnDataCommand**|This event is triggered when the `DATA` (text) or `BDAT` (binary data) command is issued by the remote SMTP host.|
|12|**OnEndOfHeaders**|This event is triggered when the remote SMTP host has completed submitting the email message headers. This is indicated by a blank line (`<CRLF>`) that separates the message headers and the message body.|
|13|**OnProxyInboundMessage**|This event is triggered when an inbound SMTP session is relayed or _proxied_ by the Front End Transport service on a Client Access server to the Transport service on a Mailbox server.|
|14|**OnEndOfData**|This event is triggered when the remote SMTP host issues an end of data command. For text sessions started by the `DATA` command, the end of data indicator is `<CRLF>.<CRLF>`. For binary sessions started by the `BDAT` command, the end of data indicator is `BDAT LAST`.|
|\*\*|**OnHelpCommand**|This event is triggered if the `HELP` command is issued by the remote SMTP host.|
|\*\*|**OnNoopCommand**|This event is triggered if the `NOOP` command is issued by the remote SMTP host.|
|\*\*|**OnReject**|This event is triggered if the receiving SMTP host issues a temporary or permanent delivery status notification (DSN) code to the sending SMTP host.|
|\*\*|**OnRsetCommand**|This event is triggered if the `RSET` command is issued by the sending SMTP host.|
|15|**OnDisconnectEvent**|This event is triggered by the disconnection of the SMTP conversation by either the receiving or sending SMTP host. Typically, this happens when the `QUIT` command is issued by the remote SMTP host.|

\*\* These events can occur at any time after **OnConnectEvent** but before **OnDisconnectEvent**.

### Categorizer events

|Sequence|SMTP event|Description|
|:---:|---|---|
|1|**OnSubmittedMessage**|This event is triggered when a message arrives in the Submission queue in the Transport service on the receiving Mailbox server or Edge Transport server.|
|2|**OnResolvedMessage**|This event is triggered after all the recipients have been resolved, but before the next hop has been determined for each recipient. The **OnResolvedMessage** routing event enables subsequent events to override the default routing behavior by using the per-recipient **SetRoutingOverride** method.|
|3|**OnRoutedMessage**|This event is triggered after messages have been categorized, distribution lists have been expanded, and recipients have been resolved.|
|4|**OnCategorizedMessage**|This event is triggered when the categorizer completes processing the message.|

## Priority of transport agents

There are two factors that determine the order that transport agents act on messages in the transport pipeline:

1. The SMTP event where the transport agent is registered, and when that SMTP event encounters messages.

2. The priority value that's assigned to the transport agent if there are multiple agents registered to the same SMTP event. The highest priority is 1. A higher integer value indicates a lower agent priority.

For example, suppose you configured the following transport agents:

- Transport Agent A with a priority of 1 and Transport Agent C with a priority of 2 are registered to the **OnEndOfHeaders** SMTP event.

- Transport Agent B with a priority of 4 is registered to the **OnMailCommand** SMTP event.

Transport Agent B is applied to messages first because the **OnMailCommand** event encounters messages before the **OnEndOfHeaders** event. When messages reach the **OnEndOfHeaders** event, Transport Agent A is applied before Transport Agent C because Transport Agent A has a higher priority (lower integer value) than Transport Agent C.

## Built-in transport agents

Exchange 2013 includes many built-in transport agents that provide features such as anti-spam, transport rules and journaling. Most of the built-in transport agents on Exchange 2013 Mailbox servers and Client Access servers are invisible and unmanageable by the transport agent management cmdlets. Virtually all of the built-in transport agents that are visible and manageable are in the Transport service on Mailbox servers and on Edge Transport servers.

The more interesting built-in transport agents on Mailbox servers are described in the following table. Note that this table doesn't include many of the invisible and unmanageable transport agents.

### Interesting built-in transport agents on Mailbox servers

|Agent name|Manageable?|Priority|SMTP or categorizer events|
|---|:---:|:---:|---|
|Transport Rule Agent|Yes|1|**OnResolvedMessage**|
|Malware Agent|Yes|2|**OnSubmittedMessage**|
|Text Messaging Routing Agent|Yes|3|**OnSubmittedMessage**|
|Text Messaging Delivery Agent|Yes|4|n/a|
|Journal Agent|No|Not configurable|**OnRoutedMessage**|
|Journal Report Decryption Agent|No|Not configurable|**OnCategorizedMessage**|
|RMS Decryption Agent|No|Not configurable|**OnSubmittedMessage**|
|RMS Encryption Agent|No|Not configurable|**OnSubmittedMessage** <br> **OnRoutedMessage**|
|RMS Protocol Decryption Agent|No|Not configurable|**OnEndOfData**|

On Edge Transport servers, most of the built-in transport agents are visible and manageable by the transport agent management cmdlets or by other feature-specific cmdlets.

The more interesting built-in transport agents on Edge Transport servers are described in the following table. Note that this table doesn't include invisible or unmanageable transport agents.

### Interesting built-in transport agents on Edge Transport servers

|Agent name|Manageable?|Priority|SMTP or categorizer events|
|---|:---:|:---:|---|
|Connection Filtering Agent|Yes|1|**OnConnectEvent** <br> **OnMailCommand** <br> **OnRcptComand** <br> **OnEndOfHeaders**|
|Address Rewriting Inbound Agent|Yes|2|**OnRcptComand** <br> **OnEndOfHeaders**|
|Edge Rule Agent|Yes|3|**OnEndOfData**|
|Content Filter Agent<sup>*</sup>|Yes|4|**OnEndOfData**|
|Sender ID Agent<sup>*</sup>|Yes|5|**OnEndOfHeaders**|
|Sender Filter Agent<sup>*</sup>|Yes|6|**OnMailCommand** <br> **OnEndOfHeaders**|
|Recipient Filter Agent|Yes|7|**OnRcptCommand**|
|Protocol Analysis Agent<sup>*</sup>|Yes|8|**OnConnectEvent** <br> **OnEndOfHeaders** <br> **OnEndOfData** <br> **OnReject** <br> **OnRsetCommand** <br> **OnDisconnectEvent**|
|Attachment Filtering Agent|Yes|9|**OnEndOfData**|
|Address Rewriting Outbound Agent|Yes|10|**OnSubmittedMessage** <br> **OnRoutedMessage**|

<sup>\*</sup> You can also install and configure these anti-spam agents on Mailbox servers. For more information, see [Enable anti-spam functionality on Mailbox servers](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

## Troubleshoot transport agents

To help you troubleshoot issues with transport agents, you can use the following features:

- **Get-TransportPipeline**: This cmdlet shows the SMTP events and the corresponding transport agents that encounter messages on the Exchange server. For more information, see [View transport agents in the transport pipeline](view-transport-agents-in-the-transport-pipeline-exchange-2013-help.md).

- **Pipeline Tracing**: Pipeline tracing creates an exact snapshot of a message before and after it encounters each transport agent. This allows you to find a transport agent that's causing unexpected results. For more information, see [Pipeline tracing](pipeline-tracing-exchange-2013-help.md).
