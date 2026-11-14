# Reviewing audit logs in Microsoft Entra

## Microsoft Entra admin center

1. In Microsoft Edge, navigate to **https://entra.microsoft.com**.
1. In the Microsoft Entra admin center, in the navigation pane, expand **Entra ID**, expand **Monitoring & health**, and click **Audit logs**.

    *Note:* You may have to scroll down in the navigation pane to find **Monitoring & health**.

1. In Audit Logs, on the tab Directory, note the filter **Date range: Last 24 hours**.
1. Click **Category : All**.
1. In the drop-down list **Value**, select **\<category\>**, for example **UserManagement**, and click **Apply**.

    *Note:* The list contains many categories. Click the drop-down list, and press the End key to jump to the end of the list.

    Verify that the list shows only entries of the category **\<category\>**.

1. In the list, find the entry with the activity **\<activity\>**, for example **Reset user password**, and click its date.
1. In Audit Log Details, on the tab Activity, review the **Date**, the **Activity Type**, the **Status**, and the person or application under **Initiated by (actor)**.
1. Click the tab **Target(s)**, and note the **User Principal Name** of the object that was changed.

    Verify that the tab shows the user **\<user name\>**.

1. Close the pane by clicking the **X** icon in the upper-right corner.

*Note:* Without Microsoft Entra ID P1 or P2, audit logs keep entries for 7 days only.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes:'AuditLog.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variable.

    ````powershell
    $activity = '' # Between the quotes insert the activity, for example Reset user password
    ````

1. Show the audit log entries of the activity.

    ````powershell
    Get-MgAuditLogDirectoryAudit -Filter:"activityDisplayName eq '$activity'" -Top:20 |
        Select-Object -Property ActivityDateTime, ActivityDisplayName, Result, @{ Name = 'Target'; Expression = { $_.TargetResources.UserPrincipalName } }
    ````

    Verify that the output lists the entries with the activity **\<activity\>** and the user that was changed.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

## References

* [Microsoft Entra audit logs](https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-audit-logs)
