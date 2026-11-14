# Approving agents in the Microsoft 365 admin center

## Microsoft 365 admin center

1. In Microsoft Edge, navigate to **https://admin.microsoft.com**.
1. In the navigation pane, expand **Agents**, and click **All agents**.
1. In All agents, click the tab **Requests**.

    *Note:* The tab Requests lists the agents that were submitted for approval. If the agent is not listed, click **Refresh**.

1. On the tab Requests, click the name of the agent **\<agent name\>** to open its details pane.
1. In the details pane of **\<agent name\>**, review the tabs **Details**, **Data & tools**, **Security**, and **Permissions**.
1. In the details pane of **\<agent name\>**, click the tab **Requests**, and click **Publish to store**.
1. In Publish agent to selected users, under **Select users or groups who can install the agent**, select **Specific users/groups**.
1. Click the search box below **Specific users/groups**, type **\<users or groups\>**, and click the user or the group in the results.
1. Under **Select users or groups who will have the agent pre-installed (optional)**, select **None**, and click **Next**.
1. In Review Security policy, keep the template **Default policy template for agents**, and click **Next**.
1. In Review permissions, review the permissions of the agent, and click **Next**.

    *Note:* If the agent requires permissions, click **Grant admin consent** first.

1. In Review and finish, click **Publish**.

    Verify that the message You published \<agent name\> is shown. Publishing can take about 30 seconds.

1. Click **Done**.

    Verify that **\<agent name\>** is no longer listed on the tab **Requests**.

*Note:* Only users with the role AI Administrator or Global Administrator can approve agent requests. To reject a request, on the tab Requests, click the *More options* icon (the three dots) next to the agent name, and click **Reject submission**.

## References

* [Agent Requests in Microsoft 365 Admin Center](https://learn.microsoft.com/en-us/microsoft-agent-365/admin/agent-requests)
* [Governance and Lifecycle actions for agents available in Microsoft 365 admin center](https://learn.microsoft.com/en-us/microsoft-agent-365/admin/agent-actions)
