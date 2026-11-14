# Assigning a Microsoft 365 Copilot license

## Microsoft 365 admin center

1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. In the navigation pane, expand **Users**, and click **Active users**.
1. In Active users, click the search box, type **\<user name\>**, and press Enter.
1. Click the name **\<user name\>** to open the user panel.
1. In the user panel of **\<user name\>**, click the tab **Licenses and apps**.
1. On the tab Licenses and apps, under **Select location**, keep the location, or select the location of the user.
1. Under **Licenses**, if the user has no Microsoft 365 license yet, activate the check box next to **\<Microsoft 365 license name\>**, for example **Microsoft 365 E5 (no Teams)**.
1. Activate the check box next to **Microsoft 365 Copilot (add-on)**.

    *Note:* A message below **Microsoft 365 Copilot (add-on)** offers to send a welcome email for Copilot to the user. Keep the check box activated, or deactivate it if the user must not receive the email.

1. Click **Save changes**.

    Verify that the message Your changes have been saved is shown, and that the check box next to **Microsoft 365 Copilot (add-on)** is activated.

1. Close the user panel by clicking the **X** icon in the upper-right corner of the pane.

*Note:* Users need a Microsoft 365 license before you can assign a Copilot license to them. If the number of available licenses is 0, remove the license from another user first: [Removing a license from a user in the Microsoft 365 admin center](/Instructions/General/Removing-a-license-from-a-user-in-the-Microsoft-365-admin-center.md). Copilot can take up to 24 hours to appear in some apps.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes:'User.ReadWrite.All', 'Organization.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variable.

    ````powershell
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    ````

1. Assign the license to the user.

    ````powershell
    $sku = Get-MgSubscribedSku -All | Where-Object { $_.SkuPartNumber -eq 'Microsoft_365_Copilot' }

    Set-MgUserLicense `
        -UserId:$userPrincipalName `
        -AddLicenses:@(@{ SkuId = $sku.SkuId }) `
        -RemoveLicenses:@()
    ````

1. Check the licenses of the user.

    ````powershell
    Get-MgUserLicenseDetail -UserId:$userPrincipalName | Select-Object -Property SkuPartNumber
    ````

    Verify that **Microsoft_365_Copilot** is listed.

    *Note:* The change can take up to 30 seconds to appear in the output. Execute the command again after a short time if the output shows the previous state.

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
1. Define the variable.

    ````powershell
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    ````

1. Assign the license to the user.

    ````powershell
    $license = New-Object -TypeName Microsoft.Open.AzureAD.Model.AssignedLicense
    $license.SkuId = (Get-EntraSubscribedSku | Where-Object { $_.SkuPartNumber -eq 'Microsoft_365_Copilot' }).SkuId

    $licenses = New-Object -TypeName Microsoft.Open.AzureAD.Model.AssignedLicenses
    $licenses.AddLicenses = $license
    $licenses.RemoveLicenses = @()

    Set-EntraUserLicense `
        -UserId:$userPrincipalName `
        -AssignedLicenses:$licenses
    ````

1. Check the licenses of the user.

    ````powershell
    Get-EntraUserLicenseDetail -UserId:$userPrincipalName | Select-Object -Property SkuPartNumber
    ````

    Verify that **Microsoft_365_Copilot** is listed.

    *Note:* The change can take up to 30 seconds to appear in the output. Execute the command again after a short time if the output shows the previous state.

1. Disconnect from Microsoft Entra.

    ````powershell
    Disconnect-Entra
    ````

## References

* [Assign or unassign licenses for users in the Microsoft 365 admin center](https://learn.microsoft.com/en-us/microsoft-365/admin/manage/assign-licenses-to-users)
* [Microsoft Copilot adoption and onboarding guide for IT admins](https://learn.microsoft.com/en-us/copilot/adopt/enablement-resources)
