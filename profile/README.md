# Plugboard

**One assistant for the company. An agent from every team.**

People ask in one place. A supervisor reads each message, decides which agent acts, chains
them when a job needs two, and asks when something is unclear. Teams own their agents in
their own repositories here; GitHub is the governance. Agents reach shared systems only
through provider contracts and never hold a credential.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/plugboard-hq/plugboard/main/docs/images/overview-dark.svg">
  <img alt="Agents, one repository each, reviewed on GitHub and installed into Plugboard, which everyone asks in one place; identity and warehouse systems sit behind contracts." src="https://raw.githubusercontent.com/plugboard-hq/plugboard/main/docs/images/overview-light.svg" width="100%">
</picture>

## Repositories

| Repository | What it is |
|---|---|
| [plugboard](https://github.com/plugboard-hq/plugboard) | The host: supervisor, registry, providers, capabilities, console, the chat and its panes. Start here to run it. |
| [plugboard-sdk](https://github.com/plugboard-hq/plugboard-sdk) | The contract an agent is built against: the manifest, the frontend SDK, exact core signatures, and the Claude Code skill. |
| [plugboard-agent-starter](https://github.com/plugboard-hq/plugboard-agent-starter) | Start a new agent here: a working package agent with a pane, a skill-agent example, and how to make it yours. |
| [plugboard-genbi](https://github.com/plugboard-hq/plugboard-genbi) | Charts agent and a SQL workbench pane: chart, data and an editable query for any dataset that carries SQL. |
| [plugboard-weather](https://github.com/plugboard-hq/plugboard-weather) | The reference package agent: one tool over Open-Meteo, its own forecast pane. |
| [plugboard-inventory](https://github.com/plugboard-hq/plugboard-inventory) | The reference skill agent: one `SKILL.md` over the host's database tools. |

## Build an agent

Use [plugboard-agent-starter](https://github.com/plugboard-hq/plugboard-agent-starter) as a
template. A skill agent is a page of markdown over the host's capabilities; a package agent
is Python with its own tools and, if it needs one, its own pane. Both install into a host
with a line in its environment. The decisions behind the design are in the host's
[architecture decision records](https://github.com/plugboard-hq/plugboard/tree/main/docs/adr).
