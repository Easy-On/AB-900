# Checking Conditional Access policies and security defaults

## Microsoft Entra admin center

1. In Microsoft Edge, navigate to **https://entra.microsoft.com**.
1. In the Microsoft Entra admin center, in the navigation pane, expand **Entra ID**, and click **Conditional Access**.
1. In Conditional Access, click **Policies**.

    Verify that the page lists the policies of the tenant, or shows the introduction What is Conditional Access? if the tenant has no policies.

1. In the Microsoft Entra admin center, in the navigation pane, click **Overview**.
1. On the tab Properties, scroll down to **Security defaults**.

    Verify that the message states whether your organization is protected by security defaults.

1. Click **Manage security defaults**.
1. In Security defaults, note the value of the drop-down list **Security defaults**, for example **Disabled**.

    *Important:* Do not change the value. Close the pane without saving.

1. Close the pane by clicking the **X** icon in the upper-right corner.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes 'Policy.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Show the Conditional Access policies.

    ````powershell
    Get-MgIdentityConditionalAccessPolicy |
        Select-Object -Property DisplayName, State
    ````

    Verify that the output lists the policies. If the tenant has no policies, the output is empty.

1. Show the state of the security defaults.

    ````powershell
    Get-MgPolicyIdentitySecurityDefaultEnforcementPolicy |
        Select-Object -Property DisplayName, IsEnabled
    ````

    Verify that **IsEnabled** shows **True** or **False**.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

## References

* [What is Conditional Access?](https://learn.microsoft.com/en-us/entra/identity/conditional-access/overview)
* [Security defaults in Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/fundamentals/security-defaults)
