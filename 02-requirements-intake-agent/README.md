# Automated Requirements Intake Agent

Built in Microsoft Copilot Studio. A stakeholder says, "I have a new requirement," and the agent asks five questions one at a time: the business problem, the team affected, what success looks like, the urgency, and any supporting links. It summarises the answers and, once the stakeholder confirms, triggers a Power Automate flow that creates a Story in a Jira project through the Jira REST API.

**Stack:** Microsoft Copilot Studio, Power Automate (HTTP action), Jira REST API (POST)

![Jira ticket created by the agent](jira-ticket.png)
