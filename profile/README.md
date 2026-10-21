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

## Who this is for

Organisations with several departments or domains that want one assistant over their
data and systems, built collaboratively and governed as code.

- **Several teams, one assistant.** Finance, operations, product, data: each owns the agent
  for its domain in its own repository, on its own schedule. People ask in one place and the
  supervisor routes to whichever team's agent fits. Agents never call each other, so one
  team's change cannot break another's.
- **Governance where your code already lives.** An agent reaches the assistant the way code
  reaches production: a repository the Plugboard GitHub App can read, a manifest it can
  inspect, a review, an install. Who may plug in what is a question of repository access,
  not of a new admin tool.
- **Data governance by construction.** Agents hold no credentials. Shared systems, the
  warehouse, the identity directory, the repositories, sit behind provider contracts the
  platform team configures once, with read-only access and the signed-in person's identity
  on every call. Swap a warehouse or an identity provider and no agent changes.
- **Not only engineers.** An agent can be a page of markdown over the host's capabilities,
  reviewed like any document; a package with its own tools and screen when the domain needs
  it. Both arrive the same way.
- **One host, many faces.** Organisations within the host have their own branding, their
  own installed agents and their own sign-in, so the same platform can be the data team's
  assistant and a customer-facing one.

It is not a chatbot builder, and it is not a BI tool. It is the board those plug into.

## Repositories

| Repository | What it is |
|---|---|
| [plugboard](https://github.com/plugboard-hq/plugboard) | The host: supervisor, registry, providers, capabilities, console, the chat and its panes. Start here to run it. |
| [plugboard-sdk](https://github.com/plugboard-hq/plugboard-sdk) | The contract an agent is built against: the manifest, the frontend SDK, exact core signatures, and the Claude Code skill. |
| [plugboard-agent-starter](https://github.com/plugboard-hq/plugboard-agent-starter) | Start a new agent here: a working package agent with a pane, a skill-agent example, and how to make it yours. |
| [plugboard-genbi](https://github.com/plugboard-hq/plugboard-genbi) | Charts agent and a SQL workbench pane: chart, data and an editable query for any dataset that carries SQL. |
| [plugboard-weather](https://github.com/plugboard-hq/plugboard-weather) | The reference package agent: one tool over Open-Meteo, its own forecast pane. |
| [plugboard-inventory](https://github.com/plugboard-hq/plugboard-inventory) | The reference skill agent: one `SKILL.md` over the host's database tools. |
| [plugboard-hotel](https://github.com/plugboard-hq/plugboard-hotel) | A customer-facing organisation on the same host: guest agents for a hotel, with a checkout pane for anything that costs money. |

## Build an agent

Use [plugboard-agent-starter](https://github.com/plugboard-hq/plugboard-agent-starter) as a
template. A skill agent is a page of markdown over the host's capabilities; a package agent
is Python with its own tools and, if it needs one, its own pane. Both install into a host
with a line in its environment. The decisions behind the design are in the host's
[architecture decision records](https://github.com/plugboard-hq/plugboard/tree/main/docs/adr).
