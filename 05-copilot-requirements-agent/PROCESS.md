# Process: As-Is and To-Be

A BPMN-style view of how stakeholder input becomes a Jira backlog item, before and after the agent. The **approval step** is marked in yellow on the To-Be diagram.

## As-Is: manual

![As-Is process](Imagesprocess-as-is.png)

The BA reads the input, writes the stories by hand, chases stakeholders about gaps and conflicts, then enters the stories in Jira. Gaps are found late, and the quality of the stories depends on how much time the BA has.

## To-Be: agent drafts, BA approves

![To-Be process](Imagesprocess-to-be.png)

1. The agent splits the input into one draft story per requirement.
2. It marks missing detail as `[TO CONFIRM]` and raises conflicts as questions. It does not invent numbers, systems or rules.
3. The BA reviews and edits the draft.
4. **Approval step:** the BA approves or rejects each story. Nothing reaches Jira without this decision.
5. Approve: the flow creates the Jira issue and logs `Approved` with the Jira key. Reject: the flow logs `Rejected` and the story goes back to the BA.

## Design choice

The agent only drafts. The BA makes every decision, and every decision leaves a record in the audit log.
