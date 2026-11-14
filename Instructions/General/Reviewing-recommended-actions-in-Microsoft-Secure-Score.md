# Reviewing recommended actions in Microsoft Secure Score

## Microsoft Defender portal

1. In Microsoft Edge, navigate to **https://security.microsoft.com**.
1. In the Microsoft Defender portal, in the navigation pane, find and click **Secure score**. If you do not see **Secure score**, expand **Exposure management**, and click **Secure score**.
1. Click the tab **Recommended actions**.
1. On the tab Recommended actions, check the column **Score impact**.

    *Note:* The list is sorted by the column **Rank**, so the action with the highest score impact is at the top. To change the order, click the column header **Score impact**, and click **Sort ascending** or **Sort descending**.

1. Click the name of an action to open its details.
1. In the details pane of the recommended action, review the **Status** below the name of the action, the **Description**, and the **Points achieved** under **Details**.

    Verify that the details pane shows the status of the action.

1. In Recommended actions, close the details pane by clicking the **X** icon.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes:'SecurityEvents.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Show the recommended actions with the highest score impact.

    ````powershell
    Get-MgSecuritySecureScoreControlProfile -All |
        Sort-Object -Property MaxScore -Descending |
        Select-Object -First 3 -Property Title, MaxScore, ControlCategory, UserImpact, ImplementationCost
    ````

    Verify that the output shows three actions. **MaxScore** is the maximum number of points that you can gain with the action.

    *Note:* The output contains all actions of Microsoft Secure Score, also for products that you do not use, and actions with the same **MaxScore**. The order can differ from the column **Rank** in the Microsoft Defender portal.

1. Show the description and the remediation steps of the first action.

    ````powershell
    Get-MgSecuritySecureScoreControlProfile -All |
        Sort-Object -Property MaxScore -Descending |
        Select-Object -First 1 -Property Title, Remediation, RemediationImpact |
        Format-List
    ````

    Verify that the output shows the remediation steps of the action.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

## References

* [Microsoft Secure Score](https://learn.microsoft.com/en-us/defender-xdr/microsoft-secure-score)
* [Assess your security posture through Microsoft Secure Score](https://learn.microsoft.com/en-us/defender-xdr/microsoft-secure-score-improvement-actions)
