# Getting started with the open-source Kortix

Kortix is the open-source AI Operating System: agents, skills, memory and connectors live in a git repo you own, and every session runs on its own cloud computer ([Kortix docs](https://kortix.com/docs)). This guide installs the CLI, scaffolds a project, runs a session, and shows where a person reviews the work.

## Prerequisites

- The Kortix CLI. Install it with `curl -fsSL https://kortix.com/install | bash`.
- A model. Name any model provider with your own keys, or use the ChatGPT plan you already pay for.
- A git repository for the project. Kortix hosts the repo, or you connect your own.
- Docker, only if you self-host. Self-host is free and runs the full stack on your own infrastructure, and `kortix self-host start` brings up one Docker Compose stack.

## Create the project

`kortix init` turns a directory into a Kortix project. It creates `kortix.yaml` plus your agents, skills and runtime config.

```bash
kortix init
kortix ship   # pushes your repo and brings the project live
```

Prefer zero setup? Create a project at [kortix.com](https://kortix.com) and start a session there, with nothing to install.

## The repo layout

A project is a git repo with `kortix.yaml` at its root. Agents, skills, memory, tools, triggers and connectors are files in it.

| Path | What it holds |
| --- | --- |
| `agents/` | Who does the work. An agent is `agents/<name>.md`, and `kortix.yaml` holds its governance. |
| `skills/` | How the company does one job, in Markdown plus scripts. |
| `memory/` | What the company has learned so far, as plain files. |
| `kortix.yaml` | The Kortix layer: machine image, connectors, triggers, secret names and grants. |

Secret values never appear in the repo. Members and roles are live project state, not files.

## Run a session

A session runs one agent in its own sandbox. The sandbox clones the repo and works on a new branch, and the branch name is the session's id. Each session has its own isolated machine and branch.

```bash
kortix sessions new --prompt "Reproduce issue #327, fix it, and open a change request"
```

Start a session from the CLI, the web app, Slack, or Microsoft Teams. A trigger starts a session on a cron schedule or a signed webhook with nobody present. Slack and Microsoft Teams are live; email is experimental, per project.

## Review and merge

Work reaches `main` only through a change request. The agent commits, pushes the session branch, and opens the change request against the project's default branch. A person with the `project.gitops.merge` permission reviews the diff and merges. Merge is default-deny for agents.

```bash
kortix cr ls   # list the change requests an agent proposes
```

A session can merge its own change request only when the agent's `kortix_permissions` grant includes `project.gitops.merge`. To require a person, give the agent a `kortix_permissions` list without that grant.

## Where to read more

- [Migrate from OpenHands](migrate-from-openhands.md)
- [Kortix FAQ](faq.md)
- [Kortix docs](https://kortix.com/docs)
