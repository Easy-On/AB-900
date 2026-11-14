# Publishing a sensitivity label

## Microsoft Purview portal

1. In Microsoft Edge, navigate to **https://purview.microsoft.com**.
1. In the Microsoft Purview portal, in the navigation pane on the left, click **Solutions**, and in the list of solutions click **Information Protection**.
1. In Information Protection, in the navigation pane, under **Policies**, click **Label publishing policies**.
1. In Label policies, click **Publish label**.
1. In Create policy, on the page Choose sensitivity labels to publish, click **Choose sensitivity labels to publish**.
1. In the panel Sensitivity labels to publish, select the check box next to **\<label name\>**, and click **Add**.
1. In Choose sensitivity labels to publish, click **Next**.
1. In Assign admin units, keep **Full directory**, and click **Next**.
1. In Publish to users and groups, keep the default setting for all users and groups, and click **Next**.
1. In Policy settings, keep the default settings, and click **Next**.
1. In Default settings for documents, keep the default label **None**, and click **Next**.
1. In Default settings for emails, keep the default settings, and click **Next**.
1. In Default settings for meetings, keep the default settings, and click **Next**.
1. In Default settings for Fabric and Power BI content, keep the default label **None**, and click **Next**.
1. In Name your policy, under **Name**, type **\<policy name\>**, and click **Next**.
1. In Review and finish, click **Submit**.
1. In New policy created, click **Done**.

    Verify that **\<policy name\>** is listed in **Label policies**. The column **Policy sync status** can show Sync in progress for some time.

*Note:* A published label can take up to 24 hours to appear in applications.

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
    $policyName = '' # Between the quotes insert the name of the label policy
    ````

1. Publish the label to all users.

    ````powershell
    New-LabelPolicy `
        -Name:$policyName `
        -Labels:$labelName `
        -ExchangeLocation:'All'
    ````

1. Check the label policy.

    ````powershell
    Get-LabelPolicy -Identity:$policyName | Select-Object -Property Name, Labels
    ````

    Verify that **\<policy name\>** is shown with the label **\<label name\>**.

1. Disconnect from Security & Compliance PowerShell.

    ````powershell
    Disconnect-ExchangeOnline -Confirm:$false
    ````

## References

* [Create and publish sensitivity labels: Publish sensitivity labels by creating a label policy](https://learn.microsoft.com/en-us/purview/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy)
