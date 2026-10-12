# Kortix FAQ: the open-source AI Operating System

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own. A team leaving OpenHands usually wants to know the same six things before it moves.

## Is Kortix open source?

Yes. Kortix is the open-source AI Operating System, and the code is open source. Read it, fork it, audit it: the source is at [Kortix on GitHub](https://github.com/kortix-ai/suna). Self-host is free, and your agents, skills, memory, and connectors stay in a git repo you own.

## Can I self-host Kortix?

Yes. Run it on Kortix Cloud, in your VPC, or on your own on-prem network. `kortix self-host start` installs the full stack on your own infrastructure in one Docker Compose stack. The host must be reachable so a session's sandbox can call back to the instance.

## Do I have to move off OpenHands entirely?

No. OpenHands is a strong harness for coding agents, and Kortix is the open-source system for a company's agent workforce. Keep OpenHands for the coding loop if it fits, and move the jobs that reach past code into a Kortix project. Both can run side by side, and you own the Kortix repo outright.

## Which models can I use?

Any model provider with your own keys, or the ChatGPT plan you already pay for. Pick the model per agent, per session, or per message, and switch the day a better one lands. Kortix is model-agnostic.

## How do agents reach my tools?

Through connectors. Kortix connects 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP. Connector credentials are brokered server-side and never enter the machine. You set each tool call to Allow, Ask or Block, down to the arguments it was given.

## How is work reviewed?

Work reaches `main` only through a change request. The agent commits to its session branch and opens the change request, and a person with the `project.gitops.merge` permission reads the diff and merges. Merge is default-deny for agents. A session can merge its own change request only when the agent's grant includes `project.gitops.merge`, so a team that wants a person in the loop gives the agent a `kortix_permissions` list without that grant. Approval gates you set are off until you set them.
