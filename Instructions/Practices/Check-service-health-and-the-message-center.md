# Practice: Check service health and the message center

## Setup

To use PowerShell, you must have completed the practice [Install PowerShell modules for Microsoft 365 administration](Install-PowerShell-modules-for-Microsoft-365-administration.md).

Use a global administrator account of your tenant.

## Task

Check whether Microsoft 365 services have problems, and read the announcements about upcoming changes:

* Show the current health status of the services of your tenant.
* Open one service and note whether it has active incidents or advisories.
* Show the message center and review one message, including its relevance, its tag, and its publication date.
* Sort the message center by the date when action is required, to find the messages that require action.

Do not change any setting.

## Instructions

### Microsoft 365 admin center

Perform this task in the **Microsoft 365 admin center**, in **Microsoft Edge**, on **LON-CL1**.

1. Open **Microsoft Edge**.
1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. Sign in as **admin@\<your tenant\>.onmicrosoft.com**.

    After signing in, you are in the **Microsoft 365 admin center**, on the home page.

1. In the Microsoft 365 admin center, in the navigation pane, expand **Health**, and click **Service health**.

    *Note:* If you do not see **Health**, click **Show all** in the navigation pane.

1. In Service health, on the tab Overview, review the status of each service.

    Verify that each service shows a status, for example **Healthy** or **2 advisories**. You may have to scroll down to the list Service status.

1. In the list Service status, in the column Status, click the link of **Exchange Online**, for example **2 advisories**, or the link of any other service that shows an incident or an advisory.

    Verify that the panel Health issues affecting Exchange Online shows the active issues of the service.

1. Close the panel by clicking the **X** icon in the upper-right corner of the panel.
1. In Service health, click the tab **Issue history**, and click the first issue in the list.
1. In the details pane of the issue, review the title at the top and the **Status**, the **Start time**, and the **User impact**.
1. Close the details pane by clicking the **X** icon in the upper-right corner of the pane.
1. In the navigation pane, under **Health**, click **Message center**.
1. In Message center, review the list of messages.

    Verify that each message shows a title, a service, and a date.

    *Note:* The list has no filter for messages that require action. The next steps show how to find them with the column **Act by**.

1. In the list, scroll to the right until the column **Act by** is visible.
1. In the column header of **Act by**, click **Act by**, and click **Sort**.

    Verify that the messages with a date in the column **Act by** are listed first. These messages require action by that date.

1. Click the first message in the list to open it.
1. In the details pane of the message, review the **Relevance**, the **Message ID**, the **Published** date, and the **Tag**.
1. Close the details pane by clicking the **X** icon in the upper-right corner of the pane.
1. In the Microsoft 365 admin center, click your account picture in the upper-right corner, and click **Sign out**.

### PowerShell

Perform this task in PowerShell, on **LON-CL1**.

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes 'ServiceHealth.Read.All', 'ServiceMessage.Read.All'
    ````

1. In the sign-in window, sign in as **admin@\<your tenant\>.onmicrosoft.com**, and accept the requested permissions if prompted.
1. Show the health status of the services.

    ````powershell
    Get-MgServiceAnnouncementHealthOverview |
        Select-Object -Property Service, Status
    ````

    Verify that the output shows each service with its status.

1. Show the active issues.

    ````powershell
    Get-MgServiceAnnouncementIssue `
        -Filter "isResolved eq false" `
        -All |
        Select-Object -Property Id, Service, Title, Classification, StartDateTime
    ````

    Verify that the output shows the active incidents and advisories, or that it is empty if no issue is active.

1. Show the latest messages of the message center.

    ````powershell
    Get-MgServiceAnnouncementMessage `
        -Top 10 `
        -Sort 'lastModifiedDateTime desc' |
        Select-Object -Property Id, Title, Category, Severity, ActionRequiredByDateTime
    ````

    Verify that the output shows the title, category, and severity of each message.

1. Show the messages that require action.

    ````powershell
    Get-MgServiceAnnouncementMessage -All |
        Where-Object { $_.ActionRequiredByDateTime } |
        Select-Object -Property Id, Title, ActionRequiredByDateTime
    ````

    Verify that the output shows only messages with a date in **ActionRequiredByDateTime**. If no message requires action, the output is empty.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````
