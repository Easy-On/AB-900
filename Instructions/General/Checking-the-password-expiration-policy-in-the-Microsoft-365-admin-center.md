# Checking the password expiration policy in the Microsoft 365 admin center

## Microsoft 365 admin center

1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. In the Microsoft 365 admin center, in the navigation pane, expand **Settings**, and click **Org settings**.

    *Note:* If **Settings** is not visible, click **Show all** in the navigation pane.

1. In Org settings, click the tab **Security & privacy**.
1. On the tab Security & privacy, click **Password expiration policy**.
1. In Password expiration policy, note whether the check box **Set passwords to never expire (recommended)** is activated.

    *Important:* Do not change the setting. Close the panel without saving.

1. Close the panel by clicking the **X** icon in the upper-right corner.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes:'Domain.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Show the password validity period of the domains.

    ````powershell
    Get-MgDomain |
        Select-Object -Property Id, PasswordValidityPeriodInDays
    ````

    Verify that the value **2147483647** means that passwords never expire.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

## References

* [Set the password expiration policy for your organization](https://learn.microsoft.com/en-us/microsoft-365/admin/misc/password-policy-recommendations)
