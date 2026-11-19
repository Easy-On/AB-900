# Viewing the Microsoft 365 Copilot license report

## Microsoft 365 admin center

1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. In the navigation pane, expand **Billing**, and click **Licenses**.
1. In Licenses, click **Microsoft 365 Copilot (add-on)**.
1. In Microsoft 365 Copilot (add-on), under **Licenses**, note the number of assigned licenses, for example **5/5 assigned**, and the number of purchased licenses in the row **Subscription**, for example **5 purchased**.

    Verify that the list of users lists the users that you licensed in this lab.

    *Note:* The number of available licenses is the difference between the purchased and the assigned licenses. The color bar shows **Assigned** and **Available**.

*Note:* The Copilot readiness report also shows the numbers of assigned and available Copilot licenses. To open it, in the navigation pane, expand **Reports**, click **Usage**, and click **Microsoft Copilot**, **Copilot**.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes 'Organization.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Show the numbers of the Microsoft 365 Copilot licenses.

    ````powershell
    Get-MgSubscribedSku -All |
        Where-Object { $_.SkuPartNumber -eq 'Microsoft_365_Copilot' } |
        Select-Object -Property SkuPartNumber,
            @{ Name = 'Purchased'; Expression = { $_.PrepaidUnits.Enabled } },
            @{ Name = 'Assigned'; Expression = { $_.ConsumedUnits } },
            @{ Name = 'Available'; Expression = { $_.PrepaidUnits.Enabled - $_.ConsumedUnits } }
    ````

    Verify that the number of **Assigned** licenses matches the users that you licensed in this lab.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

### Microsoft Entra PowerShell

1. Open a terminal.
1. Connect to Microsoft Entra.

    ````powershell
    Connect-Entra -Scopes 'Organization.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Show the numbers of the Microsoft 365 Copilot licenses.

    ````powershell
    Get-EntraSubscribedSku |
        Where-Object { $_.SkuPartNumber -eq 'Microsoft_365_Copilot' } |
        Select-Object -Property SkuPartNumber,
            @{ Name = 'Purchased'; Expression = { $_.PrepaidUnits.Enabled } },
            @{ Name = 'Assigned'; Expression = { $_.ConsumedUnits } },
            @{ Name = 'Available'; Expression = { $_.PrepaidUnits.Enabled - $_.ConsumedUnits } }
    ````

    Verify that the number of **Assigned** licenses matches the users that you licensed in this lab.

1. Disconnect from Microsoft Entra.

    ````powershell
    Disconnect-Entra
    ````

## References

* [Assign or unassign licenses for users in the Microsoft 365 admin center](https://learn.microsoft.com/en-us/microsoft-365/admin/manage/assign-licenses-to-users)
* [Microsoft Copilot Readiness Report](https://learn.microsoft.com/en-us/microsoft-365/admin/activity-reports/microsoft-365-copilot-readiness)
