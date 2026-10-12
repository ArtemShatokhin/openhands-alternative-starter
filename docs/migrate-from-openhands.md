# Migrate from OpenHands to the open-source Kortix

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers. This runbook moves the jobs you run in OpenHands into a Kortix project, step by step. It is written for a team that still wants coding agents and now needs the same agents to run work across the company.

## What OpenHands is good at

OpenHands is an open-source coding-agent harness, and its [repository](https://github.com/OpenHands/OpenHands) calls it "the self-hosted developer control center for coding agents and automations" (checked October 2026). Keep using it for the job it does well:

- It drives the coding agents you already use. Agent Canvas runs the OpenHands agent plus Claude Code, Codex, Gemini, Pi, and OpenCode, and you switch between local, remote, and cloud backends from one frontend.
- Self-hosting is first class. Run it on a laptop, in Docker, on a VM, or inside your own infrastructure. The repository documents each route, and its quickstart warns that the default install runs the agent server directly on your machine with access to your filesystem.
- Model choice stays yours. OpenHands works with any LLM, including open-weight models you host yourself, and its own [site](https://www.openhands.dev/) lists Kimi, DeepSeek, and Qwen among them (checked October 2026).
- Execution can be isolated. Each new conversation can run in its own Docker-isolated runtime with its own agent server.
- Automations reach developer tools. Agents run on a schedule or a webhook, and the project connects Slack, GitHub, Linear, and Notion.

## Where a coding-agent harness stops

OpenHands is built around code, and its agents read repositories, run terminals and tests, and open pull requests. That focus sets the boundary for a company-wide workforce.

- The job is software. Agent Canvas is a development control center, so it does not run an outbound campaign or close the books.
- Memory is per conversation. Conversations and their files persist, but no single repository holds the company's agents, skills, memory, and connector rules as versioned files a team reads and diffs.
- Execution starts on a host. The documented quickstart runs the agent server directly on your machine; the Docker and VM backends isolate it.
- Review lands on code. OpenHands opens pull requests on engineering changes, and it does not put agent work from every department behind one reviewed change request.

## The migration, in five steps

### 1. Inventory what your OpenHands automations do

List every job before you move anything. For each OpenHands automation, record its trigger (a schedule or a webhook), the tools it reaches (Slack, GitHub, Linear, Notion), and the output it produces. The `skills/repo-inventory.md` skill in this repository runs that inventory and writes the result to `memory/`. The list becomes the list of Kortix agents.

### 2. Model the same jobs as agents and skills

An agent is `agents/<name>.md` plus an `agents.<name>` block in `kortix.yaml`, where the `.md` file holds the behavior and the manifest holds the governance. Map each OpenHands job to one agent, and put the repeatable procedure in a skill. The `agents/openhands-migration.md` agent in this repository does the mapping for you and proposes it as a change request.

| Kortix | OpenHands |
| --- | --- |
| A project is a git repo with `kortix.yaml` | Agent Canvas is the frontend, with per-conversation state |
| A session is one agent sandbox on its own branch | A conversation runs one agent on a backend |
| Triggers are cron and webhook | Automations run on a schedule or a webhook |
| Connectors reach 3,000+ apps in a click, plus MCP | Integrations center on Slack, GitHub, Linear, and Notion |
| Work lands as a change request a person approves | Work lands as a pull request on code |

### 3. Wire connectors

Kortix connects 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP. Map each OpenHands integration to its Kortix connector. Connector credentials are brokered server-side and never enter the machine, so a job that used a stored token in OpenHands uses a brokered connector here.

### 4. Set allow, ask, or block

Set each tool call to Allow, Ask or Block, down to the arguments it was given. Approval gates you set are off until you set them. Put Ask on the step that matters, such as sending a message or writing to a system of record, so the call holds until a person approves it and the agent resumes.

### 5. Land work through change requests

A session runs on its own isolated machine and branch. The agent commits and opens a change request against the default branch, and a person with the `project.gitops.merge` permission reads the diff and merges. Merge is default-deny for agents.

## What stays open

You do not have to move everything at once. OpenHands keeps the coding loop, and Kortix takes the jobs that reach past it, so both can run side by side. The Kortix repo is yours outright, on Kortix Cloud, in your VPC, or on your own on-prem network, and self-host is free. For the questions a team asks before it moves, read the [FAQ](faq.md).
