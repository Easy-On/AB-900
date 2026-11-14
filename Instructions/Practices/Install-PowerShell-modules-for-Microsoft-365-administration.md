# Practice: Install PowerShell modules for Microsoft 365 administration

## Task

Install the following PowerShell modules for your user on **LON-CL1**, so that you can administer Microsoft 365 with PowerShell in the labs and practices of this course:

* **Microsoft.Graph**
* **Microsoft.Entra**
* **ExchangeOnlineManagement**

Check that the modules are installed. Then connect to Microsoft Graph as **admin@\<your tenant\>.onmicrosoft.com**, check the connection, and disconnect again.

## Instructions

Perform this task in a terminal, on **LON-CL1**.

1. Open a terminal.

    *Note:* PowerShell 7 is recommended. Windows PowerShell 5.1 also works.

1. Allow the execution of locally created scripts and signed remote scripts for your user.

    ````powershell
    Set-ExecutionPolicy `
        -ExecutionPolicy:'RemoteSigned' `
        -Scope:'CurrentUser' `
        -Force
    ````

1. Install the module **Microsoft.Graph**.

    ````powershell
    Install-Module `
        -Name:'Microsoft.Graph' `
        -Repository:'PSGallery' `
        -Scope:'CurrentUser' `
        -Force
    ````

    *Note:* In Windows PowerShell 5.1, the message NuGet provider is required to continue appears. Type **Y**, and press Enter. The installation can take several minutes.

1. Install the module **Microsoft.Entra**.

    ````powershell
    Install-Module `
        -Name:'Microsoft.Entra' `
        -Repository:'PSGallery' `
        -Scope:'CurrentUser' `
        -AllowClobber `
        -Force
    ````

1. Install the module **ExchangeOnlineManagement**.

    ````powershell
    Install-Module `
        -Name:'ExchangeOnlineManagement' `
        -Repository:'PSGallery' `
        -Scope:'CurrentUser' `
        -AllowClobber `
        -Force
    ````

1. Check that the modules are installed.

    ````powershell
    Get-InstalledModule -Name:'Microsoft.Graph', 'Microsoft.Entra', 'ExchangeOnlineManagement' |
        Select-Object -Property Name, Version
    ````

    Verify that **Microsoft.Graph**, **Microsoft.Entra**, and **ExchangeOnlineManagement** are listed with a version.

1. Connect to Microsoft Graph.

    ````powershell
    Connect-MgGraph -Scopes:'User.Read'
    ````

1. In the sign-in window Let's get you signed in, select **Work or school account**, and click **Continue**. Sign in as **admin@\<your tenant\>.onmicrosoft.com**, and accept the requested permissions if prompted. If the message Sign in to all apps and websites on this device? appears, click **No, this app only**.

    *Note:* If the sign-in window does not appear, it can be hidden behind other windows. Look for it on the taskbar.

    Verify that the terminal shows the message Welcome to Microsoft Graph!

1. Check the connection.

    ````powershell
    Get-MgContext | Select-Object -Property Account, TenantId
    ````

    Verify that the column **Account** shows **admin@\<your tenant\>.onmicrosoft.com**.

1. Disconnect from Microsoft Graph.

    ````powershell
    Disconnect-MgGraph
    ````
