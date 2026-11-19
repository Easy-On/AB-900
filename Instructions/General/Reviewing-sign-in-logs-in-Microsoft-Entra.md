# Reviewing sign-in logs in Microsoft Entra

## Microsoft Entra admin center

1. In Microsoft Edge, navigate to **https://entra.microsoft.com**.
1. In the Microsoft Entra admin center, in the navigation pane, expand **Entra ID**, expand **Monitoring & health**, and click **Sign-in logs**.
1. In Sign-in events, click **Add filter**.
1. In Add filter, in the drop-down list **Filter**, keep **User principal name**.
1. Under **Value**, type **\<user name\>**, and click **Apply**.
1. In Sign-in events, in the list, click the date of a row with the **Status** **Failure** to open its activity details.
1. In Activity Details: Sign-ins, on the tab Basic info, note the **Date** and the **Failure reason**. Scroll down to note the **Application**.

    Verify that the activity details show the failure reason of the sign-in.

1. In Sign-in events, close the activity details by clicking the **X** icon.

*Note:* The filter **User principal name** expects the user principal name of the user, for example **user@\<your tenant\>.onmicrosoft.com**.

*Note:* The sign-in events of the last 24 hours are shown by default. To show older events, click **Date range: Last 24 hours**, select a longer period, and click **Apply**.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes 'AuditLog.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variable.

    ````powershell
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    ````

1. Show the failed sign-ins of the user.

    ````powershell
    Get-MgAuditLogSignIn `
        -Filter "userPrincipalName eq '$userPrincipalName'" `
        -Top 50 |
        Where-Object { $_.Status.ErrorCode -ne 0 } |
        Select-Object -Property CreatedDateTime, AppDisplayName, @{ Name = 'FailureReason'; Expression = { $_.Status.FailureReason } }
    ````

    Verify that the output shows the **CreatedDateTime**, the **AppDisplayName**, and the **FailureReason** of each failed sign-in.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

### Microsoft Entra PowerShell

1. Open a terminal.
1. Connect to Microsoft Entra.

    ````powershell
    Connect-Entra -Scopes 'AuditLog.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variable.

    ````powershell
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    ````

1. Show the failed sign-ins of the user.

    ````powershell
    Get-EntraAuditSignInLog `
        -Filter "userPrincipalName eq '$userPrincipalName'" `
        -Top 50 |
        Where-Object { $_.Status.ErrorCode -ne 0 } |
        Select-Object -Property CreatedDateTime, AppDisplayName, @{ Name = 'FailureReason'; Expression = { $_.Status.FailureReason } }
    ````

    Verify that the output shows the **CreatedDateTime**, the **AppDisplayName**, and the **FailureReason** of each failed sign-in.

1. Disconnect from Microsoft Entra.

    ````powershell
    Disconnect-Entra
    ````

## References

* [Customize and filter activity logs in Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-customize-filter-logs)
* [Learn about the sign-in log activity details](https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-sign-in-log-activity-details)
