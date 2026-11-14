# Creating a user in the Microsoft 365 admin center

## Microsoft 365 admin center

1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. In the navigation pane, expand **Users**, and click **Active users**.
1. In Active users, click **Add a user**.
1. In Set up the basics, under **First name**, type **\<first name\>**.
1. Under **Last name**, type **\<last name\>**.
1. Click under **Display name**, and check that **\<display name\>** is shown.

    *Note:* The field **Display name** is filled in automatically from the first name and the last name as soon as you click it. If another text is shown, delete the text in the field, and type **\<display name\>**. Do not type before the automatic entry appears, because the text would be added twice.
1. Under **Username**, type **\<user name\>**. Keep the domain **\<your tenant\>.onmicrosoft.com**.
1. Deactivate **Automatically create a password**, and under **Password**, type **\<temporary password\>**.
1. Deactivate **Require this user to change their password when they first sign in**, and click **Next**.
1. In Assign product licenses, keep the location of the user, or select another location, and select **\<license name\>**.

    *Note:* If the user does not need a license, or if your tenant has no licenses available, scroll down, and select **Create user without product license**.

1. Click **Next**.
1. In Optional settings, keep the default settings, and click **Next**.
1. In Review and finish, click **Finish adding**.

    Verify that the **Username** and the **Display name** are correct.

1. In the confirmation page, click **Close**.

    Verify that **\<display name\>** is listed under **Active users**.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes:'User.ReadWrite.All', 'Organization.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables for the user.

    ````powershell
    $firstName = '' # Between the quotes insert the first name
    $lastName = '' # Between the quotes insert the last name
    $displayName = '' # Between the quotes insert the display name
    $userPrincipalName = '' # Between the quotes insert the user principal name, for example user@<your tenant>.onmicrosoft.com
    $temporaryPassword = '' # Between the quotes insert a temporary password
    $usageLocation = '' # Between the quotes insert the two-letter country code of the user, for example AT
    $licenseName = '' # Between the quotes insert the SKU part number of the license, for example ENTERPRISEPACK. To list the SKU part numbers, execute Get-MgSubscribedSku
    ````

1. Create the user.

    ````powershell
    $mailNickname = $userPrincipalName.Split('@')[0]

    $passwordProfile = @{
        Password                      = $temporaryPassword
        ForceChangePasswordNextSignIn = $false
    }

    New-MgUser `
        -DisplayName:$displayName `
        -GivenName:$firstName `
        -Surname:$lastName `
        -UserPrincipalName:$userPrincipalName `
        -MailNickname:$mailNickname `
        -UsageLocation:$usageLocation `
        -PasswordProfile:$passwordProfile `
        -AccountEnabled:$true
    ````

    Verify that the output shows the **DisplayName** and the **Id** of the user.

1. Assign the license to the user.

    ````powershell
    $sku = Get-MgSubscribedSku -All | Where-Object { $_.SkuPartNumber -eq $licenseName }

    Set-MgUserLicense `
        -UserId:$userPrincipalName `
        -AddLicenses:@(@{ SkuId = $sku.SkuId }) `
        -RemoveLicenses:@()
    ````

1. Check the license of the user.

    ````powershell
    Get-MgUserLicenseDetail -UserId:$userPrincipalName | Select-Object -Property SkuPartNumber
    ````

    Verify that **\<license name\>** is listed.

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
1. Define the variables for the user.

    ````powershell
    $firstName = '' # Between the quotes insert the first name
    $lastName = '' # Between the quotes insert the last name
    $displayName = '' # Between the quotes insert the display name
    $userPrincipalName = '' # Between the quotes insert the user principal name, for example user@<your tenant>.onmicrosoft.com
    $temporaryPassword = '' # Between the quotes insert a temporary password
    $usageLocation = '' # Between the quotes insert the two-letter country code of the user, for example AT
    $licenseName = '' # Between the quotes insert the SKU part number of the license, for example ENTERPRISEPACK. To list the SKU part numbers, execute Get-EntraSubscribedSku
    ````

1. Create the user.

    ````powershell
    $mailNickname = $userPrincipalName.Split('@')[0]

    $passwordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
    $passwordProfile.Password = $temporaryPassword
    $passwordProfile.ForceChangePasswordNextLogin = $false

    New-EntraUser `
        -DisplayName:$displayName `
        -GivenName:$firstName `
        -Surname:$lastName `
        -UserPrincipalName:$userPrincipalName `
        -MailNickName:$mailNickname `
        -UsageLocation:$usageLocation `
        -PasswordProfile:$passwordProfile `
        -AccountEnabled:$true
    ````

    Verify that the output shows the **DisplayName** and the **Id** of the user.

1. Assign the license to the user.

    ````powershell
    $license = New-Object -TypeName Microsoft.Open.AzureAD.Model.AssignedLicense
    $license.SkuId = (Get-EntraSubscribedSku | Where-Object { $_.SkuPartNumber -eq $licenseName }).SkuId

    $licenses = New-Object -TypeName Microsoft.Open.AzureAD.Model.AssignedLicenses
    $licenses.AddLicenses = $license
    $licenses.RemoveLicenses = @()

    Set-EntraUserLicense `
        -UserId:$userPrincipalName `
        -AssignedLicenses:$licenses
    ````

1. Check the license of the user.

    ````powershell
    Get-EntraUserLicenseDetail -UserId:$userPrincipalName | Select-Object -Property SkuPartNumber
    ````

    Verify that **\<license name\>** is listed.

1. Disconnect from Microsoft Entra.

    ````powershell
    Disconnect-Entra
    ````

## References

* [Add users and assign licenses in Microsoft 365](https://learn.microsoft.com/en-us/microsoft-365/admin/add-users/add-users)
