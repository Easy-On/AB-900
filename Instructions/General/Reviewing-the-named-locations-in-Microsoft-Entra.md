# Reviewing the named locations in Microsoft Entra

## Microsoft Entra admin center

1. In Microsoft Edge, navigate to **https://entra.microsoft.com**.
1. In the Microsoft Entra admin center, in the navigation pane, expand **Entra ID**, and click **Conditional Access**.
1. In Conditional Access, under **Manage**, click **Named locations**.
1. In Named locations, on the tab All Named Locations, note the number of named locations.

    Verify that the list shows the named locations with the columns **Name**, **Location type**, **Trusted**, and **Conditional Access**, or the message 0 named locations found.

    *Note:* Named locations define countries, regions, or IP address ranges that Conditional Access policies can allow or block.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes:'Policy.Read.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Show the named locations.

    ````powershell
    Get-MgIdentityConditionalAccessNamedLocation |
        Select-Object -Property DisplayName, Id
    ````

    Verify that the output lists the named locations. If the tenant has no named locations, the output is empty.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

## References

* [Using the location condition in a Conditional Access policy](https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-assignment-network)