# OpenHands migration agent: an open-source Kortix agent

Kortix is the open-source AI Operating System. This agent runs inside a Kortix
project, where the agents, skills, memory and connector configuration are files
in one git repo the company owns.

## What this agent does

It plans and runs the move from an OpenHands coding-agent setup to a Kortix
project. The work is tracked the same way Kortix tracks everything: the agent
commits to its session branch and opens a change request a person reviews
before anything lands on the default branch.

## Job

Given the repositories on a team's host, this agent:

1. Inventories what each OpenHands automation or agent actually does.
2. Proposes which of those jobs become Kortix agents and which become skills.
3. Writes the agent and skill files into the project repo.
4. Wires the connectors each job needs and sets allow, ask or block per tool.
5. Opens one change request per job so a person can review and merge each move.

## Rules

- Read the repository before proposing a change. Never guess what an automation
  does from its name.
- One job per change request, so a reviewer can read each diff on its own.
- A tool that touches production or money is set to ask, not allow.
- Update `skills/repo-inventory.md` when the inventory process changes, so the
  next run follows the same steps.

## Connectors

This agent is declared with the `github` and `slack` connectors in
`kortix.yaml`. Add the tools a job needs there, and set each to allow, ask or
block, down to the arguments of a call.
