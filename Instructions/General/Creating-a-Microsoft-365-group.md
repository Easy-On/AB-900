# Creating a Microsoft 365 group

## Microsoft 365 admin center

1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. In the navigation pane, expand **Teams & groups**, and click **Active teams & groups**.
1. In Active teams and groups, click **Add a Microsoft 365 group**.
1. In Set up the basics, under **Name**, type **\<group name\>**.
1. Under **Description**, type **\<group description\>**.
1. Click **Next**.
1. In Assign owners, click **Assign owners**.
1. In the panel Assign owners, click the search box, type **\<owner name\>**, and press Enter.
1. Select the check box next to **\<owner name\>**, and click **Add**.
1. In Assign owners, click **Next**.
1. In Add members, click **Add members**.
1. In the panel Add members, click the search box, type **\<member name\>**, and press Enter.
1. Select the check box next to **\<member name\>**.

    *Note:* To add several members, search for the next member, and select the check box next to that member. The selections are kept. The button shows the number of selected members, for example **Add (2)**.

1. Click **Add**.
1. In Add members, click **Next**.
1. In Edit settings, under **Group email address**, type **\<group email address\>**, keep the default privacy setting, and click **Next**.
1. In Review and finish adding group, click **Create group**.

    Verify that the message \<group name\> group created is shown.

1. Click **Close**.

    Verify that **\<group name\>** is listed under **Active teams and groups**.

*Note:* If the new group is not listed, refresh the page.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes 'Group.ReadWrite.All', 'User.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables for the group.

    ````powershell
    $groupName = '' # Between the quotes insert the name of the group
    $groupDescription = '' # Between the quotes insert the description of the group
    $groupEmailAlias = '' # Between the quotes insert the part of the email address before the @ sign
    $ownerUserPrincipalName = '' # Between the quotes insert the user principal name of the owner
    $memberUserPrincipalNames = @('') # Between the quotes insert the user principal name of a member. Add further members as comma-separated values
    ````

1. Create the group.

    ````powershell
    $group = New-MgGroup `
        -DisplayName $groupName `
        -Description $groupDescription `
        -MailNickname $groupEmailAlias `
        -MailEnabled $true `
        -SecurityEnabled $false `
        -GroupTypes @('Unified')
    ````

1. Add the owner to the group.

    ````powershell
    $owner = Get-MgUser -UserId $ownerUserPrincipalName

    New-MgGroupOwnerByRef `
        -GroupId $group.Id `
        -BodyParameter @{ '@odata.id' = "https://graph.microsoft.com/v1.0/directoryObjects/$($owner.Id)" }
    ````

1. Add the members to the group.

    ````powershell
    foreach ($memberUserPrincipalName in $memberUserPrincipalNames) {
        $member = Get-MgUser -UserId $memberUserPrincipalName

        New-MgGroupMemberByRef `
            -GroupId $group.Id `
            -BodyParameter @{ '@odata.id' = "https://graph.microsoft.com/v1.0/directoryObjects/$($member.Id)" }
    }
    ````

1. Check the group.

    ````powershell
    Get-MgGroup -GroupId $group.Id | Select-Object -Property DisplayName, Mail

    Get-MgGroupMember -GroupId $group.Id | ForEach-Object { $_.AdditionalProperties.displayName }
    ````

    Verify that **\<group name\>** is shown with the email address **\<group email address\>**, and that the members are listed.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

### Microsoft Entra PowerShell

1. Open a terminal.
1. Connect to Microsoft Entra.

    ````powershell
    Connect-Entra -Scopes 'Group.ReadWrite.All', 'User.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables for the group.

    ````powershell
    $groupName = '' # Between the quotes insert the name of the group
    $groupDescription = '' # Between the quotes insert the description of the group
    $groupEmailAlias = '' # Between the quotes insert the part of the email address before the @ sign
    $ownerUserPrincipalName = '' # Between the quotes insert the user principal name of the owner
    $memberUserPrincipalNames = @('') # Between the quotes insert the user principal name of a member. Add further members as comma-separated values
    ````

1. Create the group.

    ````powershell
    $group = New-EntraGroup `
        -DisplayName $groupName `
        -Description $groupDescription `
        -MailNickName $groupEmailAlias `
        -MailEnabled $true `
        -SecurityEnabled $false `
        -GroupTypes @('Unified')
    ````

1. Add the owner to the group.

    ````powershell
    $owner = Get-EntraUser -UserId $ownerUserPrincipalName

    Add-EntraGroupOwner `
        -GroupId $group.Id `
        -OwnerId $owner.Id
    ````

1. Add the members to the group.

    ````powershell
    foreach ($memberUserPrincipalName in $memberUserPrincipalNames) {
        $member = Get-EntraUser -UserId $memberUserPrincipalName

        Add-EntraGroupMember `
            -GroupId $group.Id `
            -MemberId $member.Id
    }
    ````

1. Check the group.

    ````powershell
    Get-EntraGroup -GroupId $group.Id | Select-Object -Property DisplayName, Mail

    Get-EntraGroupMember -GroupId $group.Id | Select-Object -Property DisplayName
    ````

    Verify that **\<group name\>** is shown with the email address **\<group email address\>**, and that the members are listed.

1. Disconnect from Microsoft Entra.

    ````powershell
    Disconnect-Entra
    ````

## References

* [Create a group in the admin center](https://learn.microsoft.com/en-us/microsoft-365/admin/create-groups/create-groups)
