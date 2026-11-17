# Adding a member to a Microsoft 365 group

## Microsoft 365 admin center

1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. In the navigation pane, expand **Teams & groups**, and click **Active teams & groups**.
1. In Active teams and groups, click the name **\<group name\>** to open the group panel.
1. In the group panel of **\<group name\>**, click the tab **Membership**.
1. On the tab Membership, click **Members**, and click **Add members**.
1. In the panel Add members, click the search box, type **\<member name\>**, and press Enter.
1. Select the check box next to **\<member name\>**, and click **Add**.

    Verify that **\<member name\>** is listed under **Members**.

*Note:* The membership is applied to the SharePoint site of the group after a few minutes. If you cannot edit the site right away, wait a few minutes, and refresh the page.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes:'GroupMember.ReadWrite.All', 'User.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables.

    ````powershell
    $groupName = '' # Between the quotes insert the name of the group
    $memberUserPrincipalName = '' # Between the quotes insert the user principal name of the new member
    ````

1. Add the member to the group.

    ````powershell
    $group = Get-MgGroup -Filter:"displayName eq '$groupName'"
    $member = Get-MgUser -UserId:$memberUserPrincipalName

    New-MgGroupMemberByRef `
        -GroupId:$group.Id `
        -BodyParameter:@{ '@odata.id' = "https://graph.microsoft.com/v1.0/directoryObjects/$($member.Id)" }
    ````

1. Check the members of the group.

    ````powershell
    Get-MgGroupMember -GroupId:$group.Id | ForEach-Object { $_.AdditionalProperties.userPrincipalName }
    ````

    Verify that the user principal name of the new member is listed.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

### Microsoft Entra PowerShell

1. Open a terminal.
1. Connect to Microsoft Entra.

    ````powershell
    Connect-Entra -Scopes:'GroupMember.ReadWrite.All', 'User.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables.

    ````powershell
    $groupName = '' # Between the quotes insert the name of the group
    $memberUserPrincipalName = '' # Between the quotes insert the user principal name of the new member
    ````

1. Add the member to the group.

    ````powershell
    $group = Get-EntraGroup -Filter:"displayName eq '$groupName'"
    $member = Get-EntraUser -UserId:$memberUserPrincipalName

    Add-EntraGroupMember `
        -GroupId:$group.Id `
        -MemberId:$member.Id
    ````

1. Check the members of the group.

    ````powershell
    Get-EntraGroupMember -GroupId:$group.Id | Select-Object -Property DisplayName, UserPrincipalName
    ````

    Verify that the new member is listed.

1. Disconnect from Microsoft Entra.

    ````powershell
    Disconnect-Entra
    ````

## References

* [Add or remove members from Microsoft 365 groups using the admin center](https://learn.microsoft.com/en-us/microsoft-365/admin/create-groups/add-or-remove-members-from-groups)
