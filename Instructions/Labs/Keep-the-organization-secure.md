# Lab: Keep the organization secure

## Setup

You must have completed the practice [Install PowerShell modules for Microsoft 365 administration](../Practices/Install-PowerShell-modules-for-Microsoft-365-administration.md).

You must have completed the lab [Manage users, groups, and admin roles](Manage-users-groups-and-admin-roles.md). The lab uses the user **Patti Fernandez** and the blocked sign-in attempt of this user.

1. On **LON-CL1**, sign in to the Microsoft Defender portal as **admin@\<your tenant\>.onmicrosoft.com**. Use an account with the role **Global Administrator** or **Security Administrator** in your tenant.

## Introduction

Contoso wants to improve its security. As the administrator, you review the Microsoft Secure Score and plan the most important recommended action. You then check whether the users have registered a second authentication method, and you investigate why a sign-in failed. Finally, you trace administrative changes in the audit logs and review the protection settings of the tenant: Conditional Access, security defaults, authentication methods, the password expiration policy, the administrator roles, the named locations, and your own sign-ins.

## Exercises

1. [Review Microsoft Secure Score](#exercise-1-review-microsoft-secure-score)
1. [Check the MFA registration of users](#exercise-2-check-the-mfa-registration-of-users)
1. [Investigate a failed sign-in](#exercise-3-investigate-a-failed-sign-in)
1. [Trace administrative changes in the audit logs](#exercise-4-trace-administrative-changes-in-the-audit-logs)
1. [Review Conditional Access and security defaults](#exercise-5-review-conditional-access-and-security-defaults)
1. [Review the authentication method policies](#exercise-6-review-the-authentication-method-policies)
1. [Review the password expiration policy](#exercise-7-review-the-password-expiration-policy)
1. [Review the Global Administrators](#exercise-8-review-the-global-administrators)
1. [Review the named locations](#exercise-9-review-the-named-locations)
1. [Review your own sign-ins](#exercise-10-review-your-own-sign-ins)

## Exercise 1: Review Microsoft Secure Score

1. On **LON-CL1**, find the recommended action with the highest score impact in Microsoft Secure Score that has the status **To address**. Review what you must do to implement it.

    [Reviewing recommended actions in Microsoft Secure Score](../General/Reviewing-recommended-actions-in-Microsoft-Secure-Score.md)

1. Set the status of this recommended action to **Planned**, with the action plan note **Review in the next security meeting**.

    [Changing the status of a recommended action in Microsoft Secure Score](../General/Changing-the-status-of-a-recommended-action-in-Microsoft-Secure-Score.md)

    Verify that the column **Status** shows **Planned** for the recommended action.

## Exercise 2: Check the MFA registration of users

1. On **LON-CL1**, check whether **Patti Fernandez** has registered an authentication method for multifactor authentication (MFA). Note the value in the column **Methods Registered**.

    [Checking the MFA registration of users](../General/Checking-the-MFA-registration-of-users.md)

    Verify that the column **Multifactor authentication capable** shows **Capable** or **Not Capable** for **Patti Fernandez**.

## Exercise 3: Investigate a failed sign-in

1. On **LON-CL1**, in the sign-in logs, find the failed sign-in of **PattiF@\<your tenant\>.onmicrosoft.com** from the time the sign-in was blocked in the lab [Manage users, groups, and admin roles](Manage-users-groups-and-admin-roles.md). Note the **Failure reason**.

    [Reviewing sign-in logs in Microsoft Entra](../General/Reviewing-sign-in-logs-in-Microsoft-Entra.md)

    Verify that the failure reason states that the account is disabled.

    *Note:* Without Microsoft Entra ID P1 or P2, sign-in logs keep entries for 7 days only. If the sign-in is no longer listed, block the sign-in of **Patti Fernandez** again, try to sign in as **PattiF@\<your tenant\>.onmicrosoft.com** in an InPrivate window, wait a few minutes, and then unblock the sign-in.

## Exercise 4: Trace administrative changes in the audit logs

Audit logs record who changed which object in your tenant. In the lab [Manage users, groups, and admin roles](Manage-users-groups-and-admin-roles.md), you changed users, a group, and a role. Find these changes.

1. On **LON-CL1**, in the audit logs, filter the entries to the category **UserManagement**, and find the entry **Add user** for **Patti Fernandez**.

    [Reviewing audit logs in Microsoft Entra](../General/Reviewing-audit-logs-in-Microsoft-Entra.md)

    Verify that the tab **Target(s)** of the entry shows the user principal name **PattiF@\<your tenant\>.onmicrosoft.com**.

1. Find the entry **Reset user password** that belongs to **Patti Fernandez**. Note who initiated the change.

    [Reviewing audit logs in Microsoft Entra](../General/Reviewing-audit-logs-in-Microsoft-Entra.md)

    Verify that the tab **Target(s)** shows **PattiF@\<your tenant\>.onmicrosoft.com**.

1. Find the entry **Disable account** that belongs to the blocked sign-in of **Patti Fernandez**. Note the date and time.

    [Reviewing audit logs in Microsoft Entra](../General/Reviewing-audit-logs-in-Microsoft-Entra.md)

    Verify that the date and time of the entry match the time when you blocked the sign-in in the lab [Manage users, groups, and admin roles](Manage-users-groups-and-admin-roles.md).

    *Note:* Without Microsoft Entra ID P1 or P2, audit logs keep entries for 7 days only.

## Exercise 5: Review Conditional Access and security defaults

1. On **LON-CL1**, check whether the tenant has Conditional Access policies. Note the number of policies.

    [Checking Conditional Access policies and security defaults](../General/Checking-Conditional-Access-policies-and-security-defaults.md)

    Verify that the page lists the policies, or shows the introduction What is Conditional Access? if the tenant has no policies.

1. Check whether security defaults are enabled in the tenant. Do not change the value.

    [Checking Conditional Access policies and security defaults](../General/Checking-Conditional-Access-policies-and-security-defaults.md)

    Verify that the message states that your organization is not protected by security defaults, and that the value **Disabled** is shown.

    *Note:* Security defaults and Conditional Access policies exclude each other. If you have Conditional Access policies, you cannot enable security defaults.

## Exercise 6: Review the authentication method policies

1. On **LON-CL1**, review which authentication methods the tenant allows. Note which of the methods **Microsoft Authenticator**, **SMS**, **Temporary Access Pass**, and **Email OTP** are enabled.

    [Reviewing the authentication method policies in Microsoft Entra](../General/Reviewing-the-authentication-method-policies-in-Microsoft-Entra.md)

    Verify that the page lists the authentication methods with the columns **Method**, **Target**, and **Enabled**.

1. Open the policy of the method **Microsoft Authenticator**, and note which users it targets. Do not change any value.

    [Reviewing the authentication method policies in Microsoft Entra](../General/Reviewing-the-authentication-method-policies-in-Microsoft-Entra.md)

    Verify that the policy shows whether the method is enabled and which users are targeted.

## Exercise 7: Review the password expiration policy

1. On **LON-CL1**, in the Microsoft 365 admin center, check whether passwords expire in your organization. Do not change the setting.

    [Checking the password expiration policy in the Microsoft 365 admin center](../General/Checking-the-password-expiration-policy-in-the-Microsoft-365-admin-center.md)

    Verify that the check box **Set passwords to never expire (recommended)** is activated.

## Exercise 8: Review the Global Administrators

1. On **LON-CL1**, review who has the role **Global Administrator**. Note the number of users.

    [Reviewing the members of an admin role in Microsoft Entra](../General/Reviewing-the-members-of-an-admin-role-in-Microsoft-Entra.md)

    Verify that the tab **Active assignments** lists **MOD Administrator** with the type **User**.

    *Note:* Microsoft recommends fewer than five Global Administrators and at least two, so that one account is always available.

1. Review who has the role **Global Reader**.

    [Reviewing the members of an admin role in Microsoft Entra](../General/Reviewing-the-members-of-an-admin-role-in-Microsoft-Entra.md)

    Verify that the list shows the assignments of the role, or no assignments.

## Exercise 9: Review the named locations

1. On **LON-CL1**, check whether the tenant has named locations. Note the number of named locations.

    [Reviewing the named locations in Microsoft Entra](../General/Reviewing-the-named-locations-in-Microsoft-Entra.md)

    Verify that the page lists the named locations, for example **Teams Workers** and **ME Services**, with the location type **IP ranges**.

## Exercise 10: Review your own sign-ins

1. On **LON-CL1**, in the sign-in logs, find the sign-ins of **admin@\<your tenant\>.onmicrosoft.com** from the last 24 hours. Note the **Application** of the most recent sign-in.

    [Reviewing sign-in logs in Microsoft Entra](../General/Reviewing-sign-in-logs-in-Microsoft-Entra.md)

    Verify that the list shows sign-ins of **admin@\<your tenant\>.onmicrosoft.com**.

1. Open the most recent sign-in, and note the **IP address** and the **Operating system** on the tabs **Location** and **Device info**.

    [Reviewing sign-in logs in Microsoft Entra](../General/Reviewing-sign-in-logs-in-Microsoft-Entra.md)

    Verify that the tab **Device info** shows the operating system of **LON-CL1**.
