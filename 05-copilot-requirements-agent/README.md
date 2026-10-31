# Requirements-to-Backlog Agent (Copilot Studio)

An agent that turns stakeholder input into draft user stories for a business analyst (BA), with a human approval step, an audit log and a measured evaluation. Built for a UK banking and insurance setting, using synthetic data only.

## What it does

1. The BA pastes stakeholder input into the agent.
2. The agent returns draft stories under four fixed headings: **Stories, Conflicts found, Questions for the BA, Assumptions to confirm**.
3. After the BA confirms a story, a flow asks for approval. On **Approve** it creates the Jira issue and writes an audit row. On **Reject** it writes an audit row and creates nothing.

See [PROCESS.md](PROCESS.md) for the As-Is and To-Be diagrams, with the approval step marked.

## Evaluation: three instruction versions on ten test cases

I wrote ten synthetic cases, each with a known trap: a conflict, a vague requirement, a missing detail, a solution written as a requirement, a non-functional requirement, and so on. I ran every case against three versions of the agent's instructions and scored each output by hand.

| Measure | v1 (basic) | v2 | v3 (current) |
|---|---|---|---|
| Requirements missed (of the requirements in the 10 inputs) | 0 | 3 | 0 |
| Invented requirements (total across 10 cases) | 32 | 0 | 0 |
| Gaps and conflicts caught (of 8 cases that contained one) | 2 | 8 | 7 |
| Cases with concrete acceptance criteria (of 10) | 10 | 3 | 3 |

What changed between versions:

- **v1** wrote confident stories and invented detail: thresholds, options, systems and rules that were not in the input.
- **v2** stopped inventing but over-corrected. In case 6 it dropped three requirements because a different one in the same input was unclear.
- **v3** fixed that with an explicit "split first, never defer one requirement because another is unclear" rule, and kept the no-invention rule. In case 7 it asked what the twelve dropdown options are, but not what need the dropdown meets, so that case scored Partial.

**The trade-off:** v2 and v3 only write concrete acceptance criteria when the input gives enough to base them on (3 of 10 cases). v1 wrote criteria for all ten, but 32 requirements were invented to do it. The agent now asks instead of guessing, which is the behaviour a BA wants, but it means more questions back to the stakeholder.

The full scoring sheet is in [evaluation/agent-comparison.xlsx](evaluation/agent-comparison.xlsx).

### How far to trust these numbers

- Each case was run **once** per version. Wording varies between runs, so a repeat could score slightly differently.
- **One person** scored the outputs, with no second scorer.
- Ten cases is a small set. This shows the direction of the change, not a benchmark.
- The model setting was not recorded for each run.

## Approval and audit flow

Built as a Copilot Studio agent flow with these steps:

1. **Trigger:** receives the requirement, affected team, success outcome, urgency and supporting links.
2. **Start and wait for an approval:** sends an Approve/Reject request to the BA.
3. **Condition:** if the outcome is `Approve`, call Jira and then log it; otherwise log the rejection.
4. **Audit log:** one row per decision in a Dataverse table (`R2B Audit Log`) with Title, Requirement, AffectedTeam, Decision and JiraKey.

### Test run (synthetic requirement)

I ran the flow once with a synthetic requirement and approved it.

| Check | Result |
|---|---|
| Approval request received | Yes ([approval card](Imagesapproval-card.png)) |
| Jira issue created after approval | Yes, MC-20 ([screenshot](Imagesjira-mc-20.png)) |
| Audit row written | Yes: Decision `Approved`, JiraKey `MC-20` ([screenshot](Imagesaudit-row.png)) |
| Reject branch | Built, **not yet tested** |

## Stack

Microsoft Copilot Studio, Power Automate (agent flow, Approvals), Dataverse, Jira Cloud (HTTP call), Excel (scoring sheet).

## Limitations

- **The agent is not yet wired to the flow as a tool.** The flow runs and was tested on its own, but the agent's tool picker did not list it, so the agent does not call it yet. This is the next step.
- **The Respond step waits for a human.** An agent caller times out after about two minutes, so for agent use the flow should reply "sent for approval" straight away and continue in the background. Not yet changed.
- The **Reject** branch has not been run.
- The approval card's Details field runs the lines together, because line breaks and labels were not added.
- Synthetic data only. No real customer or patient data.
- Jira credentials are held in the flow and are not included in this repository.
