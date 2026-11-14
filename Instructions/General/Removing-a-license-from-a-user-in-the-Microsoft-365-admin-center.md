# Removing a license from a user in the Microsoft 365 admin center

## Microsoft 365 admin center

1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. In the navigation pane, expand **Users**, and click **Active users**.
1. In Active users, click the search box, type **\<display name\>**, and press Enter.
1. Click the name **\<display name\>** to open the user panel.
1. In the user panel of **\<display name\>**, click the tab **Licenses and apps**.
1. On the tab Licenses and apps, under **Licenses**, deactivate the check box next to **\<license name\>**.

    *Note:* Repeat this step for every license that you want to remove from the user.

1. Click **Save changes**.

    Verify that the message Your changes have been saved is shown, and that the check box next to **\<license name\>** is deactivated. Verify that the license shows one more available license than before.

1. Close the user panel by clicking the **X** icon in the upper-right corner of the pane.

*Note:* If you remove a Microsoft 365 license from a user, the user can lose access to the apps and the data of the license. Remove an add-on license, for example Microsoft 365 Copilot, before you remove the Microsoft 365 license that it depends on.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes:'User.ReadWrite.All', 'Organization.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables.

    ````powershell
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    $licenseName = '' # Between the quotes insert the SKU part number of the license, for example Microsoft_365_Copilot. To list the SKU part numbers, execute Get-MgSubscribedSku
    ````

1. Remove the license from the user.

    ````powershell
    $sku = Get-MgSubscribedSku -All | Where-Object { $_.SkuPartNumber -eq $licenseName }

    Set-MgUserLicense `
        -UserId:$userPrincipalName `
        -AddLicenses:@() `
        -RemoveLicenses:@($sku.SkuId)
    ````

1. Check the licenses of the user.

    ````powershell
    Get-MgUserLicenseDetail -UserId:$userPrincipalName | Select-Object -Property SkuPartNumber
    ````

    Verify that **\<license name\>** is no longer listed.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

### Microsoft Entra PowerShell

1. Open a terminal.
1. Connect to Microsoft Entra.

    ````powershell
    Connect-Entra -Scopes:'User.ReadWrite.All', 'Organization.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables.

    ````powershell
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    $licenseName = '' # Between the quotes insert the SKU part number of the license, for example Microsoft_365_Copilot. To list the SKU part numbers, execute Get-EntraSubscribedSku
    ````

1. Remove the license from the user.

    ````powershell
    $license = New-Object -TypeName Microsoft.Open.AzureAD.Model.AssignedLicense
    $license.SkuId = (Get-EntraSubscribedSku | Where-Object { $_.SkuPartNumber -eq $licenseName }).SkuId

    $licenses = New-Object -TypeName Microsoft.Open.AzureAD.Model.AssignedLicenses
    $licenses.AddLicenses = @()
    $licenses.RemoveLicenses = @($license.SkuId)

    Set-EntraUserLicense `
        -UserId:$userPrincipalName `
        -AssignedLicenses:$licenses
    ````

1. Check the licenses of the user.

    ````powershell
    Get-EntraUserLicenseDetail -UserId:$userPrincipalName | Select-Object -Property SkuPartNumber
    ````

    Verify that **\<license name\>** is no longer listed.

1. Disconnect from Microsoft Entra.

    ````powershell
    Disconnect-Entra
    ````

## References

* [Assign or unassign licenses for users in the Microsoft 365 admin center](https://learn.microsoft.com/en-us/microsoft-365/admin/manage/assign-licenses-to-users)
