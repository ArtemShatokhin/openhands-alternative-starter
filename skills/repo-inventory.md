# repo-inventory: a skill for the open-source Kortix AI Operating System

Kortix is the open-source AI Operating System. This skill is part of a Kortix
project, where skills are Markdown files that live beside the agents and memory
in one git repo.

## When to use it

Before any migration run, and whenever a new repository joins the team. It
produces the plain-fact inventory the migration agent plans from.

## Procedure

For each repository the team points you at:

1. List the entry points: CI workflows, cron jobs, webhook handlers, and any
   script that runs unattended.
2. For each entry point, write down the trigger, the steps it runs, the systems
   it reads, the systems it writes, and who owns the result.
3. Mark each step as code work, business-tool work, or reporting.
4. Note the secrets each entry point uses, by name only. Never copy a secret
   value into the inventory.
5. Write the result to `memory/repo-inventory.md` in the project repo, so the
   next session reads it instead of re-deriving it.

## Output

A Markdown table, one row per entry point:

| Repo | Trigger | Steps | Reads | Writes | Owner |
| --- | --- | --- | --- | --- | --- |

Keep one job per row. A row that needs more than one line of steps is two jobs.
