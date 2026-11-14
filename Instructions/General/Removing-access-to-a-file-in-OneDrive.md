# Removing access to a file in OneDrive

## OneDrive

1. In Microsoft Edge, navigate to **https://www.office.com**.
1. In Microsoft 365 Copilot, click the *App launcher* icon (the waffle icon) next to **Copilot**, and click **OneDrive**.

    *Note:* OneDrive opens in a new browser tab. If a message about Copilot in OneDrive appears, click **Not now**.
1. In OneDrive, in the navigation pane, click **My files**.
1. In My files, find the file **\<file name\>** and select the check box next to it.
1. In the upper-right corner of the command bar, click **Details**.
1. In the details pane, under **Has access**, click **Manage access**.
1. In the dialog Manage Access, on the tab People, click the permission next to the name **\<user name\>**, for example **Can view**.
1. Click **Direct Access**, select **No direct access**, and click **Apply**.
1. In the message box Want to remove \<user name\>'s direct access, click **Remove**.

    Verify that the tab People shows only the owner and the message This file has not been shared with anyone yet.

*Note:* If the user has access through a sharing link, remove or change the link on the tab Links in Manage access. If the access is inherited from a parent folder, remove the access on the parent folder.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes:'Files.ReadWrite.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables.

    ````powershell
    $fileName = '' # Between the quotes insert the name of the file in the root folder of your OneDrive, including the extension, for example Contoso Strategy.docx
    $userDisplayName = '' # Between the quotes insert the display name of the user, for example Amber Rodriguez
    ````

1. Find the file and the access of the user.

    ````powershell
    $item = Invoke-MgGraphRequest `
        -Method:'GET' `
        -Uri:"v1.0/me/drive/root:/$([uri]::EscapeDataString($fileName))"

    $permissionsUri = "v1.0/me/drive/items/$($item.id)/permissions"

    $permission = (Invoke-MgGraphRequest -Method:'GET' -Uri:$permissionsUri).value |
        Where-Object { $_.grantedToV2.user.displayName -eq $userDisplayName }
    ````

1. Remove the access of the user.

    ````powershell
    Invoke-MgGraphRequest `
        -Method:'DELETE' `
        -Uri:"$permissionsUri/$($permission.id)"
    ````

1. Show the access to the file.

    ````powershell
    (Invoke-MgGraphRequest -Method:'GET' -Uri:$permissionsUri).value |
        ForEach-Object { [pscustomobject]@{ User = $_.grantedToV2.user.displayName; Roles = $_.roles -join ', ' } }
    ````

    Verify that **\<user name\>** is no longer listed.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

## References

* [Manage sharing and permissions in OneDrive and SharePoint](https://support.microsoft.com/en-us/office/stop-sharing-onedrive-or-sharepoint-files-or-folders-or-change-permissions-0a36470f-d7fe-40a0-bd74-0ac6c1e13323)
