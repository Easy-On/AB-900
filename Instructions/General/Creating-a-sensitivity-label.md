# Creating a sensitivity label

## Microsoft Purview portal

1. In Microsoft Edge, navigate to **https://purview.microsoft.com**.

    *Note:* If the message Welcome to the new Microsoft Purview portal appears, click **Get started**. Close the tour messages that appear with the **X** icon. Do not click **Go to classic portal** or **Switch**.

1. In the Microsoft Purview portal, in the navigation pane on the left, click **Solutions**, and in the list of solutions click **Information Protection**.
1. In Information Protection, in the navigation pane, click **Sensitivity labels**.
1. In Sensitivity labels, click **Create**, **Label**.
1. In New sensitivity label, on the page Provide basic details for this label, under **Name**, type **\<label name\>**.
1. Under **Display name**, type **\<label name\>**.
1. Under **Description for users**, type **\<label description\>**.

    *Note:* If a text does not appear in a field, wait one or two seconds after you click the field, and type the text again. Check that the first character of each text is present.

1. Click **Next**.
1. In Define the scope for this label, keep **Files & other data assets** selected, and deactivate **Emails**, **Meetings**, and **Groups & sites**.
1. In the message box Impact to current settings, click **Confirm**.
1. In Define the scope for this label, click **Next**.
1. In Choose protection settings for the types of items you selected, keep **Control access**, **Apply content marking**, and **Protect Teams meetings and chats** deactivated, and click **Next**.

    *Note:* Do not activate **Control access**. This setting encrypts the files.

1. In Auto-labeling for files and emails, keep the setting deactivated, and click **Next**.
1. In Define protection settings for groups and sites, keep the default settings, and click **Next**.
1. In Review your settings and finish, click **Create label**.

    *Note:* Creating the label can take up to a few minutes. The page shows Submitting until the label is created.

1. In Your sensitivity label was created, select **Don't create a policy yet**, and click **Done**.

    Verify that **\<label name\>** is listed in **Sensitivity labels**.

*Note:* A label is not available to users until it is published in a label policy.

## PowerShell

### Security & Compliance PowerShell

1. Open a terminal.
1. Connect to Security & Compliance PowerShell.

    ````powershell
    Connect-IPPSSession
    ````

1. In the sign-in window, sign in with your administrator account.
1. Define the variables.

    ````powershell
    $labelName = '' # Between the quotes insert the name of the label
    $labelDescription = '' # Between the quotes insert the description of the label for users
    ````

1. Create the label.

    ````powershell
    New-Label `
        -Name:$labelName `
        -DisplayName:$labelName `
        -Tooltip:$labelDescription
    ````

1. Check the label.

    ````powershell
    Get-Label -Identity:$labelName | Select-Object -Property DisplayName, Tooltip
    ````

    Verify that **\<label name\>** is shown with the description **\<label description\>**.

1. Disconnect from Security & Compliance PowerShell.

    ````powershell
    Disconnect-ExchangeOnline -Confirm:$false
    ````

## References

* [Create and publish sensitivity labels: Create and configure sensitivity labels](https://learn.microsoft.com/en-us/purview/create-sensitivity-labels#create-and-configure-sensitivity-labels)
