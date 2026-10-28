# Agentic BA Portfolio

AI agents that do business analysis work: turning requirements into Jira backlogs, summarising sprints, and tracking delivery. Built by Moses Quaye, Business Analyst, using n8n, Microsoft Copilot Studio, Power Automate, Power BI, and the Jira REST API. Every project is built against a real Jira project.

## Projects

| # | Project | Stack | What it does |
|---|---------|-------|--------------|
| 1 | [Requirements-to-Backlog Agent](01-requirements-to-backlog-agent) | n8n, GPT-4.1, Jira | Takes meeting notes or stakeholder transcripts, drafts user stories with acceptance criteria, flags gaps and contradictions, and creates Epics in Jira. |
| 2 | [Automated Requirements Intake Agent](02-requirements-intake-agent) | Copilot Studio, Power Automate, Jira POST API | Captures a requirement through conversation and creates the Jira issue once the stakeholder confirms the summary. |
| 3 | [Sprint Review Summariser](03-sprint-review-summariser) | Copilot Studio, Jira GET API | Pulls sprint data from Jira and writes a stakeholder-ready sprint review summary. |
| 4 | [BA Dashboard](04-ba-dashboard) | Power BI, Jira GET API | Jira delivery metrics published to Power BI Service. |
| 5 | Requirements Tracker (in progress) | Power Apps | Requirements tracking app that extends the intake agent. |

## About me

Business Analyst with 10+ years of experience across banking, insurance, healthcare, and transport. Microsoft PL-300 certified, preparing for AB-620 (AI Agent Builder).

LinkedIn: linkedin.com/in/moses-quaye-813a37228
