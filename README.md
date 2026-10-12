# OpenHands alternative: the open-source Kortix AI Operating System

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers. This repository is a working Kortix starter for a team that has outgrown a coding-agent control center and wants the same jobs to run across the company.

## The problem this repository addresses

OpenHands is a coding-agent control center. [Its repository](https://github.com/OpenHands/OpenHands) calls it "the self-hosted developer control center for coding agents and automations" (checked October 2026). It runs coding agents locally, in Docker, on a VM, or in your cloud, and it does that job well.

The boundary appears when the work is not code. OpenHands agents read repositories, run tests, and open pull requests. Conversations and their files persist, but no single repository holds the company's agents, skills, memory, and connector rules as versioned files a team reads and reviews. A team that wants the same agents to run an outbound campaign, a weekly report, or a support queue keeps those jobs somewhere outside the code repository.

## What this repository gives you

The starter is runnable, and the project is the files themselves:

- A working `kortix.yaml` that declares the sandbox image, the connectors, the triggers, and the secret names a session may use.
- An example agent, `agents/openhands-migration.md`, that plans and runs the move.
- A skill, `skills/repo-inventory.md`, that inventories what your OpenHands automations do before you port them.

Agents and skills are Markdown, memory is files, and `kortix.yaml` is the layer that boots a session. You can grep the whole company, diff any change, and roll it back.

## File map

| Path | What it holds |
| --- | --- |
| `kortix.yaml` | Project manifest: sandbox image, connectors, triggers, secret names and grants |
| `agents/openhands-migration.md` | The example agent that runs the migration |
| `skills/repo-inventory.md` | A skill that inventories your OpenHands automations |
| `docs/getting-started.md` | Install, init, run a session, review a change request |
| `docs/migrate-from-openhands.md` | The step-by-step move from OpenHands |
| `docs/faq.md` | Questions readers ask before they move |

## Quickstart

Three commands install the CLI, scaffold a project, and bring it live. They come from the [Kortix on GitHub](https://github.com/kortix-ai/suna) README.

```bash
# 1: Install the CLI
curl -fsSL https://kortix.com/install | bash
# 2: Scaffold a project (creates kortix.yaml plus your agents, skills and runtime config)
kortix init
# 3: Ship it (pushes your repo and brings it live)
kortix ship
```

After that:

```bash
kortix sessions new --prompt "Summarize this week's commits and open a change request"
kortix cr ls   # review what an agent proposes, then merge to keep it
kortix chat    # talk to a session's agent from your terminal
```

Read [docs/getting-started.md](docs/getting-started.md) for the prerequisites, the repo layout, and the review gate.

## Kortix vs OpenHands

Kortix is the open-source AI Operating System, the leading open-source alternative to Claude Cowork and ChatGPT Work. OpenHands is a specialist harness for coding agents. The deciding question is the job: if you need agents that read and change code in your repositories, OpenHands is the specialist. If you need to own and govern the agents, skills, memory, and connectors that run across a company, run Kortix.

| | Kortix | OpenHands |
| --- | --- | --- |
| Open source | Yes | Yes, MIT-licensed |
| What it runs | A company-wide agent workforce | Coding agents and developer automations |
| Where configuration lives | Files in a git repo you own | Agent Canvas settings and per-conversation state |
| Where agents run | An isolated cloud computer per session | Your machine, Docker, or a VM |
| How work lands | A change request a person approves | Pull requests on code |

The full side-by-side is in [Kortix vs OpenHands](https://kortix.com/blog/kortix-vs-openhands) on the Kortix blog. For everything else, start at [the Kortix docs](https://kortix.com/docs).
