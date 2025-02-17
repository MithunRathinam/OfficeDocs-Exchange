---
title: 'Exchange Online: World Wide Web Publishing Service is disabled or missing'
TOCTitle: The World Wide Web Publishing Service is disabled or missing_W3SVCDisabledOrNotInstalled
ms:assetid: 2d26d778-ddf1-4225-b5e2-f6b49d819c94
ms:mtpsurl: https://technet.microsoft.com/library/ms.exch.setupreadiness.w3svcdisabledornotinstalled(v=EXCHG.150)
ms:contentKeyID: 46628847
ms.reviewer: 
ms.topic: article
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
description: Explanation for The World Wide Web Publishing Service is disabled or missing error.
---

# The World Wide Web Publishing Service is disabled or missing\_W3SVCDisabledOrNotInstalled

_**Applies to:** Exchange Server 2013_

The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).

Microsoft® Exchange Server 2007 setup cannot continue because its attempt to install the Mailbox Server or Client Access role found that the World Wide Web Publishing Service is either disabled or not installed on this computer.

Exchange 2007 setup requires the computer that you are installing Microsoft Exchange to have the World Wide Web Publishing Service installed and set to something other than disabled.

To resolve this issue, verify that the World Wide Web Publishing service is installed and not disabled on the local computer, and then rerun Microsoft Exchange setup.

## To verify that the World Wide Web Publishing Service is installed and not disabled

1. Right-click **My Computer** on the desktop, and then click **Manage**.

2. Expand the **Services and Applications** node, and then click the **Services** node.

3. In the right pane, locate the **World Wide Web Publishing Service**.

    If the **World Wide Web Publishing Service** is not displayed in the list of services installed, follow the steps in the procedure below to install it.

4. If the **World Wide Web Publishing Service** is displayed but has a status other than **Started**, continue with the steps below to start it.

5. Right-click **World Wide Web Publishing Service**, and then click **Properties**.

6. Verify the **Startup Type** is **Automatic** and the **Service status** is set to **Started**.

7. Click **Apply**, and then click **OK**.

## To install the World Wide Web Publishing Service

1. On the **Start** menu, select **Settings**, **Control Panel**, and then click **Add or Remove Programs**

2. Click **Add/Remove Windows Components**.

3. In the **Components** list, select the **Application Server** check box, and then click **Details**.

4. Select **Internet Information Services Manager**, and then click **Details**.

5. Select **World Wide Web Service**, and then select the check box.

6. Click **OK** two times to return to the **Components** list, and then click **Next**.

7. Click **Finish** when the IIS service is installed.
