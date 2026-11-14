# Managing agents in the Microsoft 365 admin center

## Microsoft 365 admin center

1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. In the navigation pane, expand **Agents**, and click **All agents**.
1. In All agents, on the tab Registry, find the agent **\<agent name\>** in the list, and click the agent name to open its details pane.

    *Note:* If the agent is not listed, click the search box above the list, and type **\<agent name\>**.

1. In the details pane of **\<agent name\>**, on the tab Details, review the status below the agent name, and the **Publisher** and **Owner** in the section **Overview**.

    Verify that the details pane shows the status **Available** below the agent name. The value of **Owner** is empty if the agent was created with Agent Builder.

1. In the details pane of **\<agent name\>**, in the upper-right corner, click the *Block* icon (the circle with a diagonal line).
1. In the message box Block agent, activate **Block agent**, and click **Confirm**.

    Verify that the message Agent blocked is shown, and that the status below the agent name shows **Blocked**. Saving can take about 15 seconds.

1. In the details pane of **\<agent name\>**, in the upper-right corner, click **Unblock**.
1. In the message box Unblock agent, activate **Unblock agent**, and click **Confirm**.

    Verify that the message Agent unblocked is shown, and that the status below the agent name shows **Available**.

*Note:* Blocking an agent created with Agent Builder or Copilot Studio affects Copilot and other apps, such as Outlook and Teams. Blocking an agent created in SharePoint affects only its availability in Copilot Chat.

## References

* [Manage agents in the Microsoft 365 admin center](https://learn.microsoft.com/en-us/microsoft-agent-365/admin/manage-copilot-agents-integrated-apps)
* [Governance and Lifecycle actions for agents available in Microsoft 365 admin center: Block or unblock agents](https://learn.microsoft.com/en-us/microsoft-agent-365/admin/agent-actions#block-or-unblock-agents)
