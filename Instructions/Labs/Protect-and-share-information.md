# Lab: Protect and share information

## Setup

You must have completed the practice [Install PowerShell modules for Microsoft 365 administration](../Practices/Install-PowerShell-modules-for-Microsoft-365-administration.md).

## Introduction

Contoso handles confidential documents. As the administrator, you create a sensitivity label for confidential documents and publish it to all users. You then apply the label to a document that you store in OneDrive, share the document with a colleague, check the access as the colleague, and finally remove the access again.

## Exercises

1. [Create and publish a sensitivity label](#exercise-1-create-and-publish-a-sensitivity-label)
1. [Create a document and apply the label](#exercise-2-create-a-document-and-apply-the-label)
1. [Share the document](#exercise-3-share-the-document)
1. [Remove access to the document](#exercise-4-remove-access-to-the-document)

## Exercise 1: Create and publish a sensitivity label

1. On **LON-CL1**, create a sensitivity label with the following values:

    * **Name:** Contoso Confidential
    * **Description for users:** Use for internal documents that must not leave the company
    * **Scope:** Files & other data assets
    * **Encryption:** Do not encrypt files or emails

    [Creating a sensitivity label](../General/Creating-a-sensitivity-label.md)

    Verify that **Contoso Confidential** is listed on the page Labels.

1. On **LON-CL1**, publish the label **Contoso Confidential** with a label policy named **Contoso Confidential Policy** to all users.

    [Publishing a sensitivity label](../General/Publishing-a-sensitivity-label.md)

    Verify that **Contoso Confidential Policy** is listed on the page Policies.

## Exercise 2: Create a document and apply the label

1. On **LON-CL1**, in OneDrive, create a Word document named **Contoso Strategy**.

    [Creating a file in OneDrive](../General/Creating-a-file-in-OneDrive.md)

1. On **LON-CL1**, in OneDrive, apply the label **Contoso Confidential** to the document **Contoso Strategy**.

    [Applying a sensitivity label to a file](../General/Applying-a-sensitivity-label-to-a-file.md)

    Verify that **Contoso Strategy** shows the label **Contoso Confidential**.

## Exercise 3: Share the document

1. On **LON-CL1**, share the document **Contoso Strategy** with **Amber Rodriguez** with the permission **Can view**.

    [Sharing a file in OneDrive](../General/Sharing-a-file-in-OneDrive.md)

    Verify that **Amber Rodriguez** is listed under the access of **Contoso Strategy**.

1. On **LON-CL1**, in an InPrivate window, sign in to **https://www.office.com** as **AmberR@\<your tenant\>.onmicrosoft.com** with the password from the field **User password** of the lab environment.

1. On **LON-CL1**, as **Amber Rodriguez**, open the document **Contoso Strategy** that was shared with you.

    [Opening a file shared with you in OneDrive](../General/Opening-a-file-shared-with-you-in-OneDrive.md)

    Verify that the document opens in the mode Viewing, that you cannot edit it, and that it shows the label **Contoso Confidential**.

1. On **LON-CL1**, close the InPrivate window to sign out **Amber Rodriguez**.

## Exercise 4: Remove access to the document

1. On **LON-CL1**, remove the access of **Amber Rodriguez** to the document **Contoso Strategy**.

    [Removing access to a file in OneDrive](../General/Removing-access-to-a-file-in-OneDrive.md)

    Verify that **Amber Rodriguez** is no longer listed under the access of **Contoso Strategy**.

1. On **LON-CL1**, in an InPrivate window, sign in to **https://www.office.com** as **AmberR@\<your tenant\>.onmicrosoft.com**, and try to open the document **Contoso Strategy**.

    [Opening a file shared with you in OneDrive](../General/Opening-a-file-shared-with-you-in-OneDrive.md)

    Verify that **Contoso Strategy** is no longer listed under **With you**, or that a message states that you need permission to access the document.

1. On **LON-CL1**, close the InPrivate window to sign out **Amber Rodriguez**.
