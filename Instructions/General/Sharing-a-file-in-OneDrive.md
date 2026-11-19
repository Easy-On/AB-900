# Sharing a file in OneDrive

## OneDrive

1. In Microsoft Edge, navigate to **https://www.office.com**.
1. In Microsoft 365 Copilot, click the *App launcher* icon (the waffle icon) next to **Copilot**, and click **OneDrive**.

    *Note:* OneDrive opens in a new browser tab. If a message about Copilot in OneDrive appears, click **Not now**.
1. In OneDrive, in the navigation pane, click **My files**.
1. In My files, find the file **\<file name\>** and select the check box next to it.
1. In the toolbar, click **Share**.
1. In the dialog Share, click the field **Add a name, group, or email**, wait two seconds, and type **\<user name\>**.
1. In the list of results, click the user **\<user name\>**.
1. To the right of the field, click the *Permissions* icon (the pencil icon), and select **\<permission\>**, for example **Can edit** or **Can view**.
1. Click **Send**.

    Verify that the message You've invited \<user name\> to view or edit the file is shown.

1. In the details pane, under **Has access**, click **Manage access**.

    Verify that the user is listed on the tab **People** with the permission **\<permission\>**.

## PowerShell

### Microsoft Graph PowerShell

1. Open a terminal.
1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes 'Files.ReadWrite.All'
    ````

1. In the sign-in window, sign in with your administrator account, and accept the requested permissions if prompted.
1. Define the variables.

    ````powershell
    $fileName = '' # Between the quotes insert the name of the file in the root folder of your OneDrive, including the extension, for example Contoso Strategy.docx
    $userPrincipalName = '' # Between the quotes insert the user principal name of the user
    $role = '' # Between the quotes insert read for the permission Can view, or write for the permission Can edit
    ````

1. Find the file.

    ````powershell
    $item = Invoke-MgGraphRequest `
        -Method 'GET' `
        -Uri "v1.0/me/drive/root:/$([uri]::EscapeDataString($fileName))"
    ````

1. Share the file with the user.

    ````powershell
    $body = @{
        recipients     = @( @{ email = $userPrincipalName } )
        roles          = @( $role )
        requireSignIn  = $true
        sendInvitation = $true
    }

    Invoke-MgGraphRequest `
        -Method 'POST' `
        -Uri "v1.0/me/drive/items/$($item.id)/invite" `
        -Body ($body | ConvertTo-Json -Depth 5) `
        -ContentType 'application/json'
    ````

1. Show the access to the file.

    ````powershell
    (Invoke-MgGraphRequest -Method 'GET' -Uri "v1.0/me/drive/items/$($item.id)/permissions").value |
        ForEach-Object { [pscustomobject]@{ User = $_.grantedToV2.user.displayName; Roles = $_.roles -join ', ' } }
    ````

    Verify that the user is listed with the role **\<role\>**.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````

## References

* [Share files and folders in Microsoft OneDrive](https://support.microsoft.com/en-us/office/share-onedrive-files-and-folders-9fcc2f7d-de0c-4cec-93b0-a82024800c07)
