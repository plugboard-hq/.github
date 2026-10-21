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

## How it all comes together

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/plugboard-hq/plugboard/main/docs/images/system-dark.svg">
  <img alt="Agent repositories on the left, the Plugboard host in the middle (chat, supervisor, registry, capabilities, providers, console, organisations), connected systems on the right; one turn numbered through them." src="https://raw.githubusercontent.com/plugboard-hq/plugboard/main/docs/images/system-light.svg" width="100%">
</picture>

Teams own the agent repositories. The platform team runs one host and configures the
connected systems once. The numbered turn is one question travelling through all three:
a person asks, the supervisor routes to a skill agent, its capability calls the warehouse
through a provider contract with the person's identity, the result is published, a second
agent draws it, and a contributed pane opens in the chat.

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

## The core repositories

Three repositories make the platform. Everything else here is an agent built on them.

### [plugboard](https://github.com/plugboard-hq/plugboard) — the host

The thing you run. A Django service and a React chat that together hold:

- **The supervisor.** Reads each message, picks the agent, chains agents when a job needs
  two, asks the person when something is unclear, and streams the whole turn to the screen
  as AG-UI events.
- **The registry.** Every installed agent's manifest: what it answers, which tools it has,
  which providers it needs, what it can put on screen. Agents arrive by package import or
  by a `SKILL.md`, named in the environment or installed from the console.
- **Providers and capabilities.** The connected systems (warehouse, identity directory,
  repositories) behind contracts, and the ready-made tools an agent takes instead of
  writing its own: `database_tools`, `ask_user`, and so on.
- **The chat and its panes.** The conversation, the trail of what each agent did, the
  right-hand work surface, the header badges, and the organisation switcher. Panes the host
  draws itself (tables, schema browser, people, repositories) and panes an agent brings.
- **The console.** Agents, providers, organisations and branding, for whoever runs the
  installation.

It has one built-in agent, Docs, as the example. Everything domain-specific lives
elsewhere.

### [plugboard-sdk](https://github.com/plugboard-hq/plugboard-sdk) — the contract

An agent lives in its own repository and is built by a team that does not touch the host.
This repository is the agreement between the two: the exact set of things an agent may
rely on, and nothing more.

- **The Python contract.** The manifest an agent registers, the capabilities it may take,
  the provider API it reaches systems through, the turn it runs in, the widgets it may put
  on screen. Written as exact signatures in the skill's reference so an agent built against
  it keeps working across host releases.
- **The frontend SDK, `@plugboard/sdk`.** What an agent's own screen is built with. The
  host runs one React and one SDK; an agent's pane is built against those as externals, so
  its bundle is a small ESM file the host loads by URL and mounts in place. The SDK is the
  pane chrome, the host's table and SQL views, the theme tokens, and the ways a pane acts
  on the conversation and the connected providers. No credentials, no host internals.
- **A Claude Code skill.** `plugboard-agent` knows the contract: it scaffolds a package or a
  skill agent, writes the manifest and tools to spec, installs it into a host and runs the
  example prompts through the supervisor.

The SDK's job, in one line: let an agent ship its own tools and its own UI without the
host knowing it exists until it is installed. The host serves the SDK from its own tree and
this repository is the published copy, so the two are always at the same version.

### [plugboard-agent-starter](https://github.com/plugboard-hq/plugboard-agent-starter) — the template

Where a new agent starts. A working package agent with one tool and one pane, a
skill-agent example, the Vite build that turns the pane into a bundle, and a README on
what an agent is and how to make the template yours. Use it as a GitHub template; the
first commit is already a plugged-in agent.

## Reference and demo agents

Each is a repository a team would own. They show the three shapes an agent takes.

| Repository | What it is |
|---|---|
| [plugboard-weather](https://github.com/plugboard-hq/plugboard-weather) | The reference package agent: one tool over Open-Meteo, its own forecast pane. The smallest complete example of an agent with a frontend. |
| [plugboard-inventory](https://github.com/plugboard-hq/plugboard-inventory) | The reference skill agent: one `SKILL.md` over the host's database tools. No Python, no build. |
| [plugboard-genbi](https://github.com/plugboard-hq/plugboard-genbi) | Charts agent and a SQL workbench pane: chart, data and an editable query for any dataset that carries SQL. An agent that replaces a host pane. |
| [plugboard-hotel](https://github.com/plugboard-hq/plugboard-hotel) | A customer-facing organisation on the same host: six guest agents for a hotel, a stay pane with email, PDF and calendar, and a checkout pane for anything that costs money. |

## Build an agent

Use [plugboard-agent-starter](https://github.com/plugboard-hq/plugboard-agent-starter) as a
template. A skill agent is a page of markdown over the host's capabilities; a package agent
is Python with its own tools and, if it needs one, its own pane. Both install into a host
with a line in its environment. The decisions behind the design are in the host's
[architecture decision records](https://github.com/plugboard-hq/plugboard/tree/main/docs/adr).
