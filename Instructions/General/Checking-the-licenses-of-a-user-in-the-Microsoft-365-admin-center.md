# Checking the licenses of a user in the Microsoft 365 admin center

## Microsoft 365 admin center

1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. In the Microsoft 365 admin center, in the navigation pane, expand **Users**, and click **Active users**.
1. In Active users, in the search box, type **\<display name\>**, and press Enter.
1. Click **\<display name\>**.
1. In the user panel, click the tab **Licenses and apps**.

    Verify that the check boxes of the licenses **\<license name\>** under **Licenses** are activated.

1. Close the user panel by clicking the **X** icon in the upper-right corner.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes:'User.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variable.

    ````powershell
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    ````

1. Show the licenses of the user.

    ````powershell
    Get-MgUserLicenseDetail -UserId:$userPrincipalName |
        Select-Object -Property SkuPartNumber
    ````

    Verify that the output lists the licenses **\<license name\>**.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

## References

* [Assign Microsoft 365 licenses to users](https://learn.microsoft.com/en-us/microsoft-365/admin/manage/assign-licenses-to-users)
