# Assigning an admin role to a user

## Microsoft 365 admin center

1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. In the navigation pane, expand **Users**, and click **Active users**.
1. In Active users, click the name **\<display name\>** to open the user panel.
1. In the user panel of **\<display name\>**, on the tab Account, under **Roles**, click **Manage roles**.
1. In Manage admin roles, select **Admin center access**.
1. Select the check box next to **\<role name\>**, for example **Helpdesk Administrator**. If you do not see the role, scroll down in the list of roles.
1. In Manage admin roles, click **Save changes**.

    Verify that the message Admin roles updated is shown.

1. Click the *Back* icon (the arrow in the upper-left corner of the pane).

    Verify that **\<role name\>** is listed under **Roles** on the tab **Account** of the user panel.

*Note:* Assign the role with the fewest permissions that the user needs. Use Global Administrator only for emergency scenarios.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes 'RoleManagement.ReadWrite.Directory', 'User.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables.

    ````powershell
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    $roleName = '' # Between the quotes insert the name of the role, for example Helpdesk Administrator
    ````

1. Assign the role to the user.

    ````powershell
    $user = Get-MgUser -UserId $userPrincipalName
    $roleDefinition = Get-MgRoleManagementDirectoryRoleDefinition -Filter "displayName eq '$roleName'"

    New-MgRoleManagementDirectoryRoleAssignment `
        -PrincipalId $user.Id `
        -RoleDefinitionId $roleDefinition.Id `
        -DirectoryScopeId '/'
    ````

1. Check the roles of the user.

    ````powershell
    Get-MgRoleManagementDirectoryRoleAssignment `
        -Filter "principalId eq '$($user.Id)'" `
        -ExpandProperty 'roleDefinition' |
        ForEach-Object { $_.RoleDefinition.DisplayName }
    ````

    Verify that **\<role name\>** is listed.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

### Microsoft Entra PowerShell

1. Open a terminal.
1. Connect to Microsoft Entra.

    ````powershell
    Connect-Entra -Scopes 'RoleManagement.ReadWrite.Directory', 'User.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables.

    ````powershell
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    $roleName = '' # Between the quotes insert the name of the role, for example Helpdesk Administrator
    ````

1. Assign the role to the user.

    ````powershell
    $user = Get-EntraUser -UserId $userPrincipalName
    $roleDefinition = Get-EntraDirectoryRoleDefinition -Filter "displayName eq '$roleName'"

    New-EntraDirectoryRoleAssignment `
        -PrincipalId $user.Id `
        -RoleDefinitionId $roleDefinition.Id `
        -DirectoryScopeId '/'
    ````

1. Check the roles of the user.

    ````powershell
    Get-EntraDirectoryRoleAssignment -Filter "principalId eq '$($user.Id)' and roleDefinitionId eq '$($roleDefinition.Id)'"
    ````

    Verify that an assignment of the role **\<role name\>** is returned.

1. Disconnect from Microsoft Entra.

    ````powershell
    Disconnect-Entra
    ````

## References

* [Assign admin roles in the Microsoft 365 admin center](https://learn.microsoft.com/en-us/microsoft-365/admin/add-users/assign-admin-roles)
