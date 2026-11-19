# Reviewing the members of an admin role in Microsoft Entra

## Microsoft Entra admin center

1. In Microsoft Edge, navigate to **https://entra.microsoft.com**.
1. In the Microsoft Entra admin center, in the navigation pane, expand **Entra ID**, and click **Roles & admins**.
1. In Roles and administrators, click the search box **Search by name or description**, wait two seconds, and type **\<role name\>**.

    Verify that the role **\<role name\>** is listed. The column **Assignments** shows the number of assignments.

1. Click **\<role name\>**.
1. In \<role name\> | Assignments, click the tab **Active assignments**.

    Verify that the list shows the users and service principals that have the role. The column **Type** shows **User** or **Service principal**.

1. Note the names of the users in the list.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes 'RoleManagement.Read.Directory','Directory.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variable.

    ````powershell
    $roleName = '' # Between the quotes insert the name of the role, for example Global Administrator
    ````

1. Show the members of the role.

    ````powershell
    $role = Get-MgDirectoryRole -Filter "displayName eq '$roleName'"

    Get-MgDirectoryRoleMember -DirectoryRoleId $role.Id |
        ForEach-Object { $_.AdditionalProperties.displayName }
    ````

    Verify that the output lists the members of the role **\<role name\>**.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

## References

* [Microsoft Entra built-in roles](https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/permissions-reference)