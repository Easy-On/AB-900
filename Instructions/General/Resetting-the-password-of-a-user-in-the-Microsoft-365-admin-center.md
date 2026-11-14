# Resetting the password of a user in the Microsoft 365 admin center

## Microsoft 365 admin center

1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. In the navigation pane, expand **Users**, and click **Active users**.
1. In Active users, click the name **\<display name\>** to open the user panel.
1. In the user panel of **\<display name\>**, click **Reset password**.
1. In Reset password, keep **Automatically create a password** activated.
1. Deactivate **Require this user to change their password when they first sign in**, and click **Reset password**.

    Verify that the message Password has been reset is shown.

1. In the message Password has been reset, next to the password of **\<display name\>**, click **Show**, and note the new temporary password.

    *Note:* To set a password of your choice instead, deactivate **Automatically create a password** in the step before, and under **Password**, type **\<new temporary password\>**.

1. Click **Close**.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes:'User-PasswordProfile.ReadWrite.All', 'User.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables.

    ````powershell
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    $newTemporaryPassword = '' # Between the quotes insert the new temporary password
    ````

1. Reset the password of the user.

    ````powershell
    $passwordProfile = @{
        Password                      = $newTemporaryPassword
        ForceChangePasswordNextSignIn = $false
    }

    Update-MgUser `
        -UserId:$userPrincipalName `
        -PasswordProfile:$passwordProfile
    ````

1. Check the date of the last password change.

    ````powershell
    Get-MgUser -UserId:$userPrincipalName -Property:'DisplayName', 'LastPasswordChangeDateTime' |
        Select-Object -Property DisplayName, LastPasswordChangeDateTime
    ````

    Verify that **LastPasswordChangeDateTime** shows the current date and time (in UTC).

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

### Microsoft Entra PowerShell

1. Open a terminal.
1. Connect to Microsoft Entra.

    ````powershell
    Connect-Entra -Scopes:'User-PasswordProfile.ReadWrite.All', 'User.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables.

    ````powershell
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    $newTemporaryPassword = '' # Between the quotes insert the new temporary password
    ````

1. Reset the password of the user.

    ````powershell
    $securePassword = ConvertTo-SecureString -String:$newTemporaryPassword -AsPlainText -Force

    Set-EntraUserPassword `
        -UserId:$userPrincipalName `
        -Password:$securePassword `
        -ForceChangePasswordNextLogin:$false
    ````

1. Check the date of the last password change.

    ````powershell
    Get-EntraUser -UserId:$userPrincipalName -Property:'DisplayName', 'LastPasswordChangeDateTime' |
        Select-Object -Property DisplayName, LastPasswordChangeDateTime
    ````

    Verify that **LastPasswordChangeDateTime** shows the current date and time (in UTC).

1. Disconnect from Microsoft Entra.

    ````powershell
    Disconnect-Entra
    ````

## References

* [Reset passwords](https://learn.microsoft.com/en-us/microsoft-365/admin/add-users/reset-passwords)
