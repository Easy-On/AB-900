# Lab: Manage Microsoft 365 Copilot licenses and usage

## Setup

You must have completed the practice [Install PowerShell modules for Microsoft 365 administration](../Practices/Install-PowerShell-modules-for-Microsoft-365-administration.md).

1. On **LON-CL1**, sign in to the Microsoft 365 admin center as **admin@\<your tenant\>.onmicrosoft.com**. Use an account with the role **Global Administrator** in your tenant.

## Introduction

Contoso wants to roll out Microsoft 365 Copilot to its sales team. All Copilot licenses of the tenant are already assigned, so you first free two licenses. You then assign a Copilot license to two employees, check how the users use Copilot in the usage reports, and check the license report to see how many licenses are still available. Finally, you move a license by removing it and assigning it again, and you review the Copilot controls of the tenant.

## Exercises

1. [Free licenses](#exercise-1-free-licenses)
1. [Assign Copilot licenses](#exercise-2-assign-copilot-licenses)
1. [Review Copilot usage](#exercise-3-review-copilot-usage)
1. [Review the Copilot license report](#exercise-4-review-the-copilot-license-report)
1. [Check the licenses of a user](#exercise-5-check-the-licenses-of-a-user)
1. [Move a Copilot license](#exercise-6-move-a-copilot-license)
1. [Review the Copilot controls](#exercise-7-review-the-copilot-controls)

## Exercise 1: Free licenses

The tenant has no available **Microsoft 365 Copilot** licenses. Remove the Copilot license from two users who do not need it for this lab.

1. On **LON-CL1**, remove the license **Microsoft 365 Copilot (add-on)** from the user **Corey Gray**. Keep the license **Microsoft 365 E5 (no Teams)**.

    [Removing a license from a user in the Microsoft 365 admin center](../General/Removing-a-license-from-a-user-in-the-Microsoft-365-admin-center.md)

    Verify that the number of available licenses of **Microsoft 365 Copilot (add-on)** is 1.

1. Remove the license **Microsoft 365 Copilot (add-on)** from the user **Hadar Caspit**. Keep the license **Microsoft 365 E5 (no Teams)**.

    [Removing a license from a user in the Microsoft 365 admin center](../General/Removing-a-license-from-a-user-in-the-Microsoft-365-admin-center.md)

    Verify that the number of available licenses of **Microsoft 365 Copilot (add-on)** is 2.

## Exercise 2: Assign Copilot licenses

1. On **LON-CL1**, assign a Microsoft 365 Copilot license to **Billie Vester**. Deactivate the check box for the welcome email.

    [Assigning a Microsoft 365 Copilot license](../General/Assigning-a-Microsoft-365-Copilot-license.md)

    Verify that the number of available licenses of **Microsoft 365 Copilot (add-on)** is 1.

1. Assign a Microsoft 365 Copilot license to **Adil Eli**. Deactivate the check box for the welcome email.

    [Assigning a Microsoft 365 Copilot license](../General/Assigning-a-Microsoft-365-Copilot-license.md)

    Verify that the number of available licenses of **Microsoft 365 Copilot (add-on)** is 0.

## Exercise 3: Review Copilot usage

1. On **LON-CL1**, open the Microsoft 365 Copilot usage report, and note the numbers of enabled users and active users.

    [Viewing Microsoft 365 Copilot usage](../General/Viewing-Microsoft-365-Copilot-usage.md)

    Verify that the report shows a number of active users. The number can be zero, because usage data can take up to 72 hours to appear.

## Exercise 4: Review the Copilot license report

1. On **LON-CL1**, open the license report for Microsoft 365 Copilot, and note the number of purchased and assigned licenses.

    [Viewing the Microsoft 365 Copilot license report](../General/Viewing-the-Microsoft-365-Copilot-license-report.md)

    Verify that the number of assigned licenses is 5 of 5 and that the list includes **Billie Vester** and **Adil Eli**.

## Exercise 5: Check the licenses of a user

1. On **LON-CL1**, check which licenses **Billie Vester** has.

    [Checking the licenses of a user in the Microsoft 365 admin center](../General/Checking-the-licenses-of-a-user-in-the-Microsoft-365-admin-center.md)

    Verify that the licenses **Microsoft 365 E5 (no Teams)** and **Microsoft 365 Copilot (add-on)** are activated.

1. Check which licenses **Cora Thomas** has.

    [Checking the licenses of a user in the Microsoft 365 admin center](../General/Checking-the-licenses-of-a-user-in-the-Microsoft-365-admin-center.md)

    Verify that the license **Microsoft 365 E5 (no Teams)** is activated and that the license **Microsoft 365 Copilot (add-on)** is deactivated.

## Exercise 6: Move a Copilot license

1. On **LON-CL1**, remove the license **Microsoft 365 Copilot (add-on)** from **Billie Vester**. Keep the license **Microsoft 365 E5 (no Teams)**.

    [Removing a license from a user in the Microsoft 365 admin center](../General/Removing-a-license-from-a-user-in-the-Microsoft-365-admin-center.md)

    Verify that the number of available licenses of **Microsoft 365 Copilot (add-on)** is 1.

1. Assign the license **Microsoft 365 Copilot (add-on)** to **Cora Thomas**. Deactivate the check box for the welcome email.

    [Assigning a Microsoft 365 Copilot license](../General/Assigning-a-Microsoft-365-Copilot-license.md)

    Verify that the number of available licenses of **Microsoft 365 Copilot (add-on)** is 0.

## Exercise 7: Review the Copilot controls

1. On **LON-CL1**, review the tabs **Overview**, **Security**, and **Health** of the Copilot controls. Note which protections are running on the tab **Security**.

    [Reviewing the Copilot controls in the Microsoft 365 admin center](../General/Reviewing-the-Copilot-controls-in-the-Microsoft-365-admin-center.md)

    Verify that the tab **Security** lists at least one protection with the status **Protected by default**.