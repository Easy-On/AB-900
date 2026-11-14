# Blocking the sign-in of a user in the Microsoft 365 admin center

## Microsoft 365 admin center

1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. In the navigation pane, expand **Users**, and click **Active users**.
1. In Active users, click the name **\<display name\>** to open the user panel.
1. In the user panel of **\<display name\>**, click **Block sign-in**.
1. In Block sign-in, select **Block this user from signing in**, and click **Save changes**.

    Verify that a message confirms that the user is now blocked from signing in.

1. In Block sign-in, click the *Back* icon (the arrow in the upper-left corner of the pane).

    Verify that the user panel shows **Sign-in blocked** below the name of the user, and that the button **Unblock sign-in** is available.

*Note:* Blocking an account immediately stops new sign-ins. If the user is already signed in, the user is signed out of all Microsoft services within 60 minutes.

*Note:* To allow the user to sign in again, open the user panel, click **Unblock sign-in**, deactivate **Block this user from signing in**, and click **Save changes**. A message confirms that the user is unblocked. It can take up to 15 minutes until the user can sign in again. Click the *Back* icon to return to the user panel, and verify that **Sign-in blocked** is no longer shown below the name of the user and that the button **Block sign-in** is available again.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes:'User.ReadWrite.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables.

    ````powershell
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    $accountEnabled = $false # Keep $false to block the sign-in. Change the value to $true to allow the sign-in again
    ````

1. Block the sign-in of the user.

    ````powershell
    Update-MgUser `
        -UserId:$userPrincipalName `
        -AccountEnabled:$accountEnabled
    ````

1. Check the sign-in status of the user.

    ````powershell
    Get-MgUser -UserId:$userPrincipalName -Property:'DisplayName', 'AccountEnabled' |
        Select-Object -Property DisplayName, AccountEnabled
    ````

    Verify that **AccountEnabled** shows **False** for a blocked user and **True** for a user who is allowed to sign in.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

### Microsoft Entra PowerShell

1. Open a terminal.
1. Connect to Microsoft Entra.

    ````powershell
    Connect-Entra -Scopes:'User.ReadWrite.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables.

    ````powershell
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    $accountEnabled = $false # Keep $false to block the sign-in. Change the value to $true to allow the sign-in again
    ````

1. Block the sign-in of the user.

    ````powershell
    Set-EntraUser `
        -UserId:$userPrincipalName `
        -AccountEnabled:$accountEnabled
    ````

1. Check the sign-in status of the user.

    ````powershell
    Get-EntraUser -UserId:$userPrincipalName |
        Select-Object -Property DisplayName, AccountEnabled
    ````

    Verify that **AccountEnabled** shows **False** for a blocked user and **True** for a user who is allowed to sign in.

1. Disconnect from Microsoft Entra.

    ````powershell
    Disconnect-Entra
    ````

## References

* [Step 1 - Prevent user sign-in and block access to Microsoft 365](https://learn.microsoft.com/en-us/microsoft-365/admin/add-users/remove-former-employee-step-1)
* [Block Microsoft 365 user accounts with PowerShell](https://learn.microsoft.com/en-us/microsoft-365/enterprise/block-user-accounts-with-microsoft-365-powershell)
