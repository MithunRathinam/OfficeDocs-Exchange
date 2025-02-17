---
title: 'Connectivity logging: Exchange 2013 Help'
TOCTitle: Connectivity logging
ms:assetid: c31fd710-4ae4-4d9a-8936-d056e7ca2748
ms:mtpsurl: https://technet.microsoft.com/library/Bb124500(v=EXCHG.150)
ms:contentKeyID: 49287004
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
ms.topic: article
description: Connectivity logging in Exchange Server
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Connectivity logging

_**Applies to:** Exchange Server 2013_

Connectivity logging records the outbound connection activity that's used to transmit messages from a transport service on the Exchange server. The purpose of the connectivity log isn't to track the transmission of individual email messages. Rather, the connectivity log tracks the connection activity from source to the destination, regardless of how many messages are transmitted. Connectivity logging is available in the Front End Transport service on Client Access servers, the Transport service on Mailbox servers, and the Mailbox Transport service on Mailbox servers. The following list describes the type of information recorded in the connectivity log:

- Source

- Destination

- DNS resolution information

- Detailed information about connection failures

- Number of messages and bytes transmitted

You use the **Set-TransportService**, **Set-FrontEndTransportService** and **Set-MailboxTransportService** cmdlets in the Exchange Management Shell to perform all connectivity log configuration tasks. The following options are available for the connectivity logs:

- Enable or disable connectivity logging. The default is enabled.

- Specify the location of the connectivity log files.

- Specify a maximum size for the individual connectivity log files. The default size is 10 megabytes (MB).

- Specify a maximum size for the directory that contains connectivity log files. The default size is 1000 MB.

- Specify a maximum age for the connectivity log files. The default age is 30 days.

By default, Exchange uses circular logging to limit the connectivity logs based on file size and file age to help control the hard disk space used by the connectivity log files.

## Structure of the connectivity log files

By default, the connectivity log files exist in the following locations:

- **Transport service**: %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\Connectivity

- **Front End Transport service**: %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\Connectivity

- **Mailbox Transport service**: %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\Connectivity

The naming convention for the connectivity log files is CONNECTLOG*yyymmdd-nnnn_.log. The placeholders represent the following information:

- The placeholder _yyyymmdd_ is the Coordinated Universal Time (UTC) date that the log file was created. The placeholder _yyyy_ = year, _mm_ = month, and _dd_ = day.

- The placeholder _nnnn_ is an instance number that starts at the value of 1 for each day.

Information is written to the log file until the file size reaches its maximum specified value, and a new log file that has an incremented instance number is opened. This process is repeated throughout the day. Circular logging deletes the oldest log files when the connectivity log directory reaches its maximum specified size, or when a log file reaches its maximum specified age.

The connectivity log files are text files that contain data in the comma-separated value file (CSV) format. Each connectivity log file has a header that contains the following information:

- **\#Software**: Name of the software that created the connectivity log file. Typically, the value is Microsoft Exchange Server.

- **\#Version**: Version number of the software that created the connectivity log file. Currently, the value is 15.0.0.0.

- **\#Log-Type**: Log type value, which is Transport Connectivity Log.

- **\#Date**: UTC date-time when the log file was created. The UTC date-time is represented in the ISO 8601 date-time format: _yyyy-mm-dd_T_hh:mm:ss.fff_Z, where _yyyy_ = year, _mm_ = month, _dd_ = day, T indicates the beginning of the time component, _hh_ = hour, _mm_ = minute, _ss_ = second, _fff_ = fractions of a second, and Z signifies Zulu, which is another way to denote UTC.

- **\#Fields**: Comma delimited field names used in the connectivity log files.

## Information written to the connectivity log

The connectivity log stores each outbound transport service connection event on a single line in the connectivity log. The information stored on each line is organized by fields. These fields are separated by commas. The following table describes the fields used to classify each outgoing connection event.

|Field name|Description|
|---|---|
|**date-time**|UTC date-time of the connection event. The UTC date-time is represented in the ISO 8601 date-time format: _yyyy-mm-dd_T_hh:mm:ss.fff_Z, where _yyyy_ = year, _mm_ = month, _dd_ = day, T indicates the beginning of the time component, _hh_ = hour, _mm_ = minute, _ss_ = second, _fff_ = fractions of a second, and Z signifies Zulu, which is another way to denote UTC.|
|**session**|GUID that's unique for each SMTP session but is the same for each event associated with that SMTP session. For MAPI sessions in the Mailbox Transport service, the session field is blank.|
|**source**|**SMTP** for SMTP connections, **MAPI** for Mailbox Transport service connections to the local mailbox database.|
|**destination**|Name of the destination.|
|**direction**|Single character that represents the start, middle, or end of the connection. The possible values for the direction field are as follows: <ul><li>**+**: Connect</li><li>**-**: Disconnect</li><li>**>**: Send</li></ul>|
|**description**|Text information associated with the connection event. The following values are examples of values for the description field: <ul><li>Number and size of messages that were transmitted</li><li>DNS MX resource record resolution information for destination domains</li><li>DNS resolution information for destination Mailbox servers</li><li>Connection establishment messages</li><li>Connection failure messages</li></ul>|

When transport service establishes a connection to a destination, the transport service may be prepared to send one message or several messages. The connection and message transmission processes generate multiple events written on multiple lines in the connectivity log. Simultaneous connections to different destinations create connectivity log entries related to different destinations that are interlaced. However, you can use the date-time, session, source, and direction fields to arrange the connectivity log entries for each separate connection from start to finish.
