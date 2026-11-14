# Checking the MFA registration of users

## Microsoft Entra admin center

1. In Microsoft Edge, navigate to **https://entra.microsoft.com**.
1. In the Microsoft Entra admin center, in the navigation pane, expand **Entra ID**, and click **Authentication methods**.
1. In Authentication methods, under **Monitoring**, click **User registration details**.
1. In User registration details, click the search box **Name or UPN starts with**, type **\<display name\>**, and press Enter.

    Verify that the user **\<display name\>** is listed.

1. In the list, check the column **Multifactor authentication capable**.

    Verify that the column shows **Capable** or **Not Capable** for the user.

1. Scroll to the right, and note the value in the column **Methods Registered** for the user.

    *Note:* The column **Methods Registered** is empty if the user has not registered an authentication method.

*Note:* The report is not updated in real time. Changes can take up to 36 hours to appear.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes:'AuditLog.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variable.

    ````powershell
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    ````

1. Show the MFA registration details of the user.

    ````powershell
    Get-MgReportAuthenticationMethodUserRegistrationDetail -Filter:"userPrincipalName eq '$userPrincipalName'" |
        Select-Object -Property UserDisplayName, IsMfaCapable, IsMfaRegistered, MethodsRegistered
    ````

    Verify that **IsMfaCapable** shows **True** or **False** for the user.

1. Note the value of **MethodsRegistered** for the user.
1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

## References

* [Authentication Methods Activity](https://learn.microsoft.com/en-us/entra/identity/authentication/howto-authentication-methods-activity)
