# Lab: Manage Microsoft 365 Copilot agents

## Setup

You must have completed the lab [Manage users, groups, and admin roles](Manage-users-groups-and-admin-roles.md), because the group **Sales Team** is used in this lab.

1. On **LON-CL1**, open **Microsoft Edge**.
1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. Sign in as **admin@\<your tenant\>.onmicrosoft.com**. This account is a global administrator of your tenant.

    After signing in, you are in the **Microsoft 365 admin center**, on the home page.

Your account must have a Microsoft 365 Copilot license. If it does not, ask your instructor to assign one before you start. Your instructor provides the name of a SharePoint site, **\<site name\>**, that you can use for the SharePoint agent.

## Introduction

Contoso wants its employees to use agents that answer questions about the sales team's work. As the administrator, you create two agents, approve an agent request, test the agents with prompts, and manage the lifecycle of an agent. You block an agent and make it available again.

## Exercises

1. [Create a SharePoint agent](#exercise-1-create-a-sharepoint-agent)
1. [Create a Copilot Chat agent](#exercise-2-create-a-copilot-chat-agent)
1. [Approve an agent](#exercise-3-approve-an-agent)
1. [Test the agents](#exercise-4-test-the-agents)
1. [Block and unblock an agent](#exercise-5-block-and-unblock-an-agent)

## Exercise 1: Create a SharePoint agent

1. On **LON-CL1**, create a SharePoint agent for the site **\<site name\>** with the following values:

    * **Name:** Contoso Sales Assistant
    * **Instructions:** Answer questions about the documents of the sales team.

    [Creating a SharePoint agent](../General/Creating-a-SharePoint-agent.md)

    Verify that the agent **Contoso Sales Assistant** answers a test prompt with content from the site.

## Exercise 2: Create a Copilot Chat agent

1. On **LON-CL1**, create a Copilot Chat agent with the description **Help the sales team write short status updates**, and create it with the name **Contoso Sales Helper**.

    [Creating a Copilot Chat agent](../General/Creating-a-Copilot-Chat-agent.md)

    Verify that **Contoso Sales Helper** is listed under **Agents**.

## Exercise 3: Approve an agent

1. On **LON-CL1**, in Microsoft 365 Copilot, submit the agent **Contoso Sales Helper** to the org catalog, so that an administrator can approve it.

    [Submitting an agent to the org catalog in Microsoft 365 Copilot](../General/Submitting-an-agent-to-the-org-catalog-in-Microsoft-365-Copilot.md)

    Verify that the message shows the state Waiting for approval.

1. On **LON-CL1**, in the Microsoft 365 admin center, approve the agent request for **Contoso Sales Helper**, and publish the agent to the group **Sales Team**.

    [Approving agents in the Microsoft 365 admin center](../General/Approving-agents-in-the-Microsoft-365-admin-center.md)

    Verify that **Contoso Sales Helper** is no longer listed on the tab **Requests**.

## Exercise 4: Test the agents

1. On **LON-CL1**, in Microsoft 365 Copilot Chat, test the agent **Contoso Sales Helper** with the following prompts.

    | Prompt | Expected result |
    | ------ | --------------- |
    | **Write a short status update: we closed two deals with Fabrikam this week.** | A short status update that mentions Fabrikam and the two deals |
    | **Make the status update shorter and more formal.** | A shorter, more formal version of the previous status update |
    | **What is the capital of France?** | The agent answers or points out that it helps with status updates; note how the instructions of the agent influence the response |

    [Chatting with an agent](../General/Chatting-with-an-agent.md)

    Verify that each response matches the expected result.

1. On **LON-CL1**, in the site **\<site name\>**, test the agent **Contoso Sales Assistant** with the following prompts.

    | Prompt | Expected result |
    | ------ | --------------- |
    | **Which documents does the site contain?** | A list of documents from the site |
    | **Summarize the most recent document.** | A summary with a reference to a document from the site |
    | **What is the weather in Vienna today?** | The agent explains that it cannot retrieve the information |

    [Chatting with an agent](../General/Chatting-with-an-agent.md)

    Verify that the responses to the first two prompts contain references to documents from the site.

## Exercise 5: Block and unblock an agent

1. On **LON-CL1**, block the agent **Contoso Sales Helper**.

    [Managing agents in the Microsoft 365 admin center](../General/Managing-agents-in-the-Microsoft-365-admin-center.md)

    Verify that the status of **Contoso Sales Helper** shows **Blocked**.

1. On **LON-CL1**, unblock the agent **Contoso Sales Helper** again.

    [Managing agents in the Microsoft 365 admin center](../General/Managing-agents-in-the-Microsoft-365-admin-center.md)

    Verify that the status of **Contoso Sales Helper** shows **Available**.
