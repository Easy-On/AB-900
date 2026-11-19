# Reviewing the authentication method policies in Microsoft Entra

## Microsoft Entra admin center

1. In Microsoft Edge, navigate to **https://entra.microsoft.com**.
1. In the Microsoft Entra admin center, in the navigation pane, expand **Entra ID**, and click **Authentication methods**.
1. In Authentication methods, click **Policies**.

    Verify that the page lists the authentication methods with the columns **Method**, **Target**, and **Enabled**.

1. In the list, note the value in the column **Enabled** for the method **\<method name\>**, for example **Microsoft Authenticator**.
1. Click **\<method name\>**.
1. On the tab Enable and target, note whether the method is enabled and which users it targets.

    *Important:* Do not change any value. Close the page without saving.

1. Close the page by clicking the **X** icon in the upper-right corner.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes 'Policy.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Show the state of the authentication methods.

    ````powershell
    (Get-MgPolicyAuthenticationMethodPolicy).AuthenticationMethodConfigurations |
        Select-Object -Property Id, State
    ````

    Verify that the output lists the methods with the state **enabled** or **disabled**.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

## References

* [Manage authentication methods for Microsoft Entra multifactor authentication](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-methods-manage)
