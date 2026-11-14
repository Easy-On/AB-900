# Lab: Manage users, groups, and admin roles

## Setup

You must have completed the practice [Install PowerShell modules for Microsoft 365 administration](/Instructions/Practices/Install-PowerShell-modules-for-Microsoft-365-administration.md).

## Introduction

Contoso is hiring three employees for its sales department. As the administrator, you create their user accounts. You then create a group for the sales team, reset the password of one employee, and give another employee the Helpdesk Administrator role so that the helpdesk can support the team.

## Exercises

1. [Create users](#exercise-1-create-users)
1. [Reset a password and block sign-in](#exercise-2-reset-a-password-and-block-sign-in)
1. [Create a group](#exercise-3-create-a-group)
1. [Assign an admin role](#exercise-4-assign-an-admin-role)

## Exercise 1: Create users

Create the following users. Use the values from the table. The users do not need a license for this lab, so select **Create user without product license** in the step Assign product licenses.

| First name | Last name | Display name | User name |
| ---------- | --------- | ------------ | --------- |
| Debra      | Berger    | Debra Berger | DebraB    |
| Irvin      | Sayers    | Irvin Sayers | IrvinS    |
| Patti      | Fernandez | Patti Fernandez | PattiF |

1. On **LON-CL1**, create the user **Debra Berger** from the table, without a license. Use a password of your choice, deactivate the requirement to change the password at the first sign-in, and note the password, because you need it in Exercise 4.

    [Creating a user in the Microsoft 365 admin center](/Instructions/General/Creating-a-user-in-the-Microsoft-365-admin-center.md)

1. Create the user **Irvin Sayers** from the table, without a license, and with the same password. The user does not have to change the password at the first sign-in.

    [Creating a user in the Microsoft 365 admin center](/Instructions/General/Creating-a-user-in-the-Microsoft-365-admin-center.md)

1. Create the user **Patti Fernandez** from the table, without a license, and with the same password. The user does not have to change the password at the first sign-in.

    [Creating a user in the Microsoft 365 admin center](/Instructions/General/Creating-a-user-in-the-Microsoft-365-admin-center.md)

    Verify that **Debra Berger**, **Irvin Sayers**, and **Patti Fernandez** are listed under **Active users**.

## Exercise 2: Reset a password and block sign-in

1. On **LON-CL1**, reset the password of **Patti Fernandez**. Let Microsoft 365 create the password automatically, deactivate the requirement to change the password at the first sign-in, and note the new password.

    [Resetting the password of a user in the Microsoft 365 admin center](/Instructions/General/Resetting-the-password-of-a-user-in-the-Microsoft-365-admin-center.md)

1. Block the sign-in of **Patti Fernandez**.

    [Blocking the sign-in of a user in the Microsoft 365 admin center](/Instructions/General/Blocking-the-sign-in-of-a-user-in-the-Microsoft-365-admin-center.md)

    Verify that the user panel of **Patti Fernandez** shows **Sign-in blocked** below the name.

1. In an InPrivate window, try to sign in to **https://www.office.com** as **PattiF@\<your tenant\>.onmicrosoft.com** with the new password from the first step.

    Verify that the sign-in fails with the message Your account has been locked. Contact your support person to unlock it, then try again.

    *Note:* The block can take a few minutes to take effect. If the sign-in succeeds, close the InPrivate window, wait a few minutes, and try again.

1. Close the InPrivate window.
1. Unblock the sign-in of **Patti Fernandez** again.

    [Blocking the sign-in of a user in the Microsoft 365 admin center](/Instructions/General/Blocking-the-sign-in-of-a-user-in-the-Microsoft-365-admin-center.md)

    Verify that the user panel of **Patti Fernandez** no longer shows **Sign-in blocked** and that the button **Block sign-in** is available again.

## Exercise 3: Create a group

1. On **LON-CL1**, create a Microsoft 365 group with the following values:

    * **Name:** Sales Team
    * **Description:** Members of the sales team at Contoso
    * **Email address:** SalesTeam
    * **Owner:** Debra Berger
    * **Members:** Irvin Sayers and Patti Fernandez

    [Creating a Microsoft 365 group](/Instructions/General/Creating-a-Microsoft-365-group.md)

    Verify that **Sales Team** is listed under **Active teams & groups**.

## Exercise 4: Assign an admin role

1. On **LON-CL1**, assign the role **Helpdesk Administrator** to **Irvin Sayers**.

    [Assigning an admin role to a user](/Instructions/General/Assigning-an-admin-role-to-a-user.md)

    Verify that **Helpdesk Administrator** is listed under **Roles** on the tab **Account** of the user panel of **Irvin Sayers**.

1. In an InPrivate window, sign in to **https://admin.microsoft.com** as **IrvinS@\<your tenant\>.onmicrosoft.com** with the password from Exercise 1.

    Verify that the **Microsoft 365 admin center** opens.

1. As **Irvin Sayers**, reset the password of **Debra Berger**. Let Microsoft 365 create the password automatically, and deactivate the requirement to change the password at the first sign-in.

    [Resetting the password of a user in the Microsoft 365 admin center](/Instructions/General/Resetting-the-password-of-a-user-in-the-Microsoft-365-admin-center.md)

    Verify that the message Password has been reset is shown. A Helpdesk Administrator can reset the passwords of users without admin roles.

1. As **Irvin Sayers**, try to reset the password of **admin@\<your tenant\>.onmicrosoft.com**.

    [Resetting the password of a user in the Microsoft 365 admin center](/Instructions/General/Resetting-the-password-of-a-user-in-the-Microsoft-365-admin-center.md)

    Verify that the message We could not reset the password for this user is shown. A Helpdesk Administrator cannot reset the password of a Global Administrator.

1. Close the InPrivate window to sign out **Irvin Sayers**.
