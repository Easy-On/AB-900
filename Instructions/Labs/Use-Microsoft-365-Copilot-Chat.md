# Lab: Use Microsoft 365 Copilot Chat

## Setup

1. On **LON-CL1**, sign in to Microsoft 365 as **admin@\<your tenant\>.onmicrosoft.com**.

Your account must have a Microsoft 365 Copilot license. If it does not, ask your instructor to assign one before you start.

## Introduction

Contoso wants its employees to use Microsoft 365 Copilot Chat to work faster with their documents. As an administrator, you test how Copilot Chat answers questions about a document in OneDrive and how a follow-up prompt refines the answer. You then start a new conversation to see how a new chat differs from a continued one. You also let Copilot draft an email, use a file as a source, compare the response modes, ask a predefined agent for help with administration, and manage your chat history.

## Exercises

1. [Ask Copilot Chat about a document](#exercise-1-ask-copilot-chat-about-a-document)
1. [Refine an answer and start a new chat](#exercise-2-refine-an-answer-and-start-a-new-chat)
1. [Draft an email](#exercise-3-draft-an-email)
1. [Use a file as a source](#exercise-4-use-a-file-as-a-source)
1. [Compare the response modes](#exercise-5-compare-the-response-modes)
1. [Manage the chat history](#exercise-6-manage-the-chat-history)
1. [Use a predefined agent](#exercise-7-use-a-predefined-agent)
1. [Compare an agent with Copilot Chat](#exercise-8-compare-an-agent-with-copilot-chat)

## Exercise 1: Ask Copilot Chat about a document

1. On **LON-CL1**, start a chat in Microsoft 365 Copilot Chat, and ask Copilot to summarize the document **Contoso Marketing Plan** in OneDrive.

    [Starting a chat with Microsoft 365 Copilot Chat](/Instructions/General/Starting-a-chat-with-Microsoft-365-Copilot-Chat.md)

    Verify that Copilot shows a summary of the document.

## Exercise 2: Refine an answer and start a new chat

1. On **LON-CL1**, in the same chat, ask Copilot to rewrite the summary as three bullet points.

    Verify that Copilot shows the summary as three bullet points.

1. On **LON-CL1**, start a new chat, and ask Copilot the question **What is Contoso Marketing Plan about?**

    [Starting a chat with Microsoft 365 Copilot Chat](/Instructions/General/Starting-a-chat-with-Microsoft-365-Copilot-Chat.md)

    Verify that the new chat does not show the earlier conversation.

## Exercise 3: Draft an email

1. On **LON-CL1**, in a new chat, ask Copilot to write a short, friendly email to the sales team that announces the new document **Contoso Marketing Plan**.

    [Drafting an email with Microsoft 365 Copilot Chat](/Instructions/General/Drafting-an-email-with-Microsoft-365-Copilot-Chat.md)

    Verify that Copilot shows an email draft that mentions **Contoso Marketing Plan**.

    *Important:* Do not send the email.

1. In the same chat, ask Copilot to make the email more formal and shorter.

    [Drafting an email with Microsoft 365 Copilot Chat](/Instructions/General/Drafting-an-email-with-Microsoft-365-Copilot-Chat.md)

    Verify that the new draft is more formal and shorter than the first draft.

## Exercise 4: Use a file as a source

1. On **LON-CL1**, start a new chat, attach the file **Contoso Marketing Plan** from OneDrive, and send the prompt **Make suggestions for Contoso Marketing Plan.docx**.

    [Attaching a file to a chat in Microsoft 365 Copilot Chat](/Instructions/General/Attaching-a-file-to-a-chat-in-Microsoft-365-Copilot-Chat.md)

    Verify that Copilot shows a list of suggested improvements for **Contoso Marketing Plan**.

1. Ask Copilot the question **Which of the suggestions is the most important for the sales team, and why?**

    [Starting a chat with Microsoft 365 Copilot Chat](/Instructions/General/Starting-a-chat-with-Microsoft-365-Copilot-Chat.md)

    Verify that Copilot names one suggestion and gives a reason.

## Exercise 5: Compare the response modes

1. On **LON-CL1**, start a new chat, select the mode **Quick response**, and ask Copilot **Explain what a sensitivity label is in two sentences.** Note how long the answer takes.

    [Choosing the response mode in Microsoft 365 Copilot Chat](/Instructions/General/Choosing-the-response-mode-in-Microsoft-365-Copilot-Chat.md)

    Verify that Copilot answers in two sentences.

1. In the same chat, select the mode **Think deeper**, and ask the same question. Note how long the answer takes.

    [Choosing the response mode in Microsoft 365 Copilot Chat](/Instructions/General/Choosing-the-response-mode-in-Microsoft-365-Copilot-Chat.md)

    Verify that Copilot answers in two sentences and that the drop-down list shows **Think deeper**.

    *Note:* For short questions, both modes give similar answers. **Think deeper** is useful for complex questions.

## Exercise 6: Manage the chat history

1. On **LON-CL1**, start a new chat, and ask Copilot **What is a sensitivity label?** Then rename the chat to **Contoso Marketing Plan Review**.

    [Renaming a chat in Microsoft 365 Copilot Chat](/Instructions/General/Renaming-a-chat-in-Microsoft-365-Copilot-Chat.md)

    Verify that the list under **Chats** shows **Contoso Marketing Plan Review**.

1. Delete the chat **Contoso Marketing Plan Review**.

    [Deleting a chat in Microsoft 365 Copilot Chat](/Instructions/General/Deleting-a-chat-in-Microsoft-365-Copilot-Chat.md)

    Verify that the chat is no longer listed under **Chats**.

## Exercise 7: Use a predefined agent

1. On **LON-CL1**, start a new chat with the agent **Microsoft 365 Admin**, and ask the question **Which users have a Microsoft 365 Copilot license?**

    [Starting a chat with a predefined agent in Microsoft 365 Copilot Chat](/Instructions/General/Starting-a-chat-with-a-predefined-agent-in-Microsoft-365-Copilot-Chat.md)

    Verify that the answer is shown under the name **Microsoft 365 Admin** and describes the steps in the Microsoft 365 admin center, for example **Billing**, **Licenses**.

1. In the same chat, ask the agent **How do I reset the password of a user?**

    [Starting a chat with a predefined agent in Microsoft 365 Copilot Chat](/Instructions/General/Starting-a-chat-with-a-predefined-agent-in-Microsoft-365-Copilot-Chat.md)

    Verify that the answer describes how to reset a password in the Microsoft 365 admin center.

## Exercise 8: Compare an agent with Copilot Chat

1. On **LON-CL1**, start a new chat without an agent, and ask the question **How do I assign a license to a user?**

    [Starting a chat with Microsoft 365 Copilot Chat](/Instructions/General/Starting-a-chat-with-Microsoft-365-Copilot-Chat.md)

    Verify that Copilot answers the question. Note the length and the structure of the answer.

1. Start a new chat with the agent **Microsoft 365 Admin**, and ask the same question.

    [Starting a chat with a predefined agent in Microsoft 365 Copilot Chat](/Instructions/General/Starting-a-chat-with-a-predefined-agent-in-Microsoft-365-Copilot-Chat.md)

    Verify that the agent answers the question. Compare the answer with the answer of the chat without an agent, and note the differences.

    *Note:* An agent is specialized in a topic and its tools. Copilot Chat without an agent answers more generally.
