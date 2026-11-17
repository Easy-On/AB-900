# Lab: Manage Microsoft 365 Copilot licenses and usage

## Setup

You must have completed the practice [Install PowerShell modules for Microsoft 365 administration](../Practices/Install-PowerShell-modules-for-Microsoft-365-administration.md).

The tenant has no available **Microsoft 365 Copilot (add-on)** licenses. To free two licenses for this lab, remove the Copilot license from the users **Corey Gray** and **Hadar Caspit**, who do not need it.

1. On **LON-CL1**, open **Microsoft Edge**.
1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. Sign in as **admin@\<your tenant\>.onmicrosoft.com**. This account is a global administrator of your tenant.

    After signing in, you are in the **Microsoft 365 admin center**, on the home page.

1. In the Microsoft 365 admin center, in the navigation pane, expand **Users**, and click **Active users**.
1. In Active users, click the search box, type **Corey Gray**, and press **Enter**.
1. Click the name **Corey Gray**.
1. In the user panel of **Corey Gray**, click the tab **Licenses and apps**.
1. On the tab Licenses and apps, under **Licenses**, clear the check box **Microsoft 365 Copilot (add-on)**. Keep the check box **Microsoft 365 E5 (no Teams)** activated.
1. Click **Save changes**.

    Verify that the message Your changes have been saved is shown, and that the check box **Microsoft 365 Copilot (add-on)** is cleared.

1. Click the *Close* icon (the **X** icon) in the upper-right corner of the user panel.

Repeat from step 5 for the user **Hadar Caspit**.

## Introduction

Contoso wants to roll out Microsoft 365 Copilot to its sales team. You assign a Copilot license to two employees, check how the users use Copilot in the usage reports, and check the license report to see how many licenses are still available. Finally, you move a license by removing it and assigning it again, and you review the Copilot controls of the tenant.

## Exercises

1. [Assign Copilot licenses](#exercise-1-assign-copilot-licenses)
1. [Review Copilot usage](#exercise-2-review-copilot-usage)
1. [Review the Copilot license report](#exercise-3-review-the-copilot-license-report)
1. [Check the licenses of users](#exercise-4-check-the-licenses-of-users)
1. [Move a Copilot license](#exercise-5-move-a-copilot-license)
1. [Review the Copilot controls](#exercise-6-review-the-copilot-controls)

## Exercise 1: Assign Copilot licenses

1. On **LON-CL1**, assign a Microsoft 365 Copilot license to the users **Billie Vester** and **Adil Eli**. Deactivate the check box for the welcome email.

    [Assigning a Microsoft 365 Copilot license](../General/Assigning-a-Microsoft-365-Copilot-license.md)

    Verify that the number of available licenses of **Microsoft 365 Copilot (add-on)** is 0.

## Exercise 2: Review Copilot usage

1. On **LON-CL1**, open the Microsoft 365 Copilot usage report, and note the numbers of enabled users and active users.

    [Viewing Microsoft 365 Copilot usage](../General/Viewing-Microsoft-365-Copilot-usage.md)

    Verify that the report shows a number of active users. The number can be zero, because usage data can take up to 72 hours to appear.

## Exercise 3: Review the Copilot license report

1. On **LON-CL1**, open the license report for Microsoft 365 Copilot, and note the number of purchased and assigned licenses.

    [Viewing the Microsoft 365 Copilot license report](../General/Viewing-the-Microsoft-365-Copilot-license-report.md)

    Verify that the number of assigned licenses is 5 of 5 and that the list includes **Billie Vester** and **Adil Eli**.

## Exercise 4: Check the licenses of users

1. On **LON-CL1**, check which licenses the users **Billie Vester** and **Cora Thomas** have.

    [Checking the licenses of a user in the Microsoft 365 admin center](../General/Checking-the-licenses-of-a-user-in-the-Microsoft-365-admin-center.md)

    Verify that the licenses match the following table.

    | User          | Microsoft 365 E5 (no Teams) | Microsoft 365 Copilot (add-on) |
    | ------------- | --------------------------- | ------------------------------ |
    | Billie Vester | Activated                   | Activated                      |
    | Cora Thomas   | Activated                   | Deactivated                    |

## Exercise 5: Move a Copilot license

1. On **LON-CL1**, remove the license **Microsoft 365 Copilot (add-on)** from **Billie Vester**. Keep the license **Microsoft 365 E5 (no Teams)**.

    [Removing a license from a user in the Microsoft 365 admin center](../General/Removing-a-license-from-a-user-in-the-Microsoft-365-admin-center.md)

    Verify that the number of available licenses of **Microsoft 365 Copilot (add-on)** is 1.

1. On **LON-CL1**, assign the license **Microsoft 365 Copilot (add-on)** to **Cora Thomas**. Deactivate the check box for the welcome email.

    [Assigning a Microsoft 365 Copilot license](../General/Assigning-a-Microsoft-365-Copilot-license.md)

    Verify that the number of available licenses of **Microsoft 365 Copilot (add-on)** is 0.

## Exercise 6: Review the Copilot controls

1. On **LON-CL1**, review the tabs **Overview**, **Security**, and **Health** of the Copilot controls. Note which protections are running on the tab **Security**.

    [Reviewing the Copilot controls in the Microsoft 365 admin center](../General/Reviewing-the-Copilot-controls-in-the-Microsoft-365-admin-center.md)

    Verify that the tab **Security** lists at least one protection with the status **Protected by default**.
