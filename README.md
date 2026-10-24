# Olne plugins

Public client packages for **SC-Knowledge** and **Idiot Player**. No invitation to a private repository is needed.
The MCP services run remotely: you install instructions and connection metadata, not a server or a game database.

- [SC-Knowledge: overview and setup](https://olne.no/lab/sc-knowledge/)
- [Star Citizen Data Explorer](https://olne.no/sc/explorer/)
- [Play Idiot](https://olne.no/lab/idiot/)

## Claude Code

Run inside Claude Code:

```text
/plugin marketplace add olne-no/plugins
/plugin install sc-knowledge@olne
```

For the card game, install `idiot-player@olne` instead. Start a new session after installation.
The packages include both the skill and a remote HTTP MCP connection. No API key is required by these MCP services.

## Codex and ChatGPT desktop

Add `https://github.com/olne-no/plugins` as a marketplace source in the supported desktop plugin UI.
Use branch `main`, the repository root, and no sparse path. Select **Olne**, then install SC-Knowledge or Idiot Player.
In Codex CLI, add the marketplace with:

```text
codex plugin marketplace add olne-no/plugins
```

Then open `/plugins`, select Olne and install the plugin. Start a new session.
These root packages declare MCP directly and are **desktop/local-client packages**; importing them does not make them available on ChatGPT web or mobile.

## ChatGPT web and mobile

Create a personal connection in ChatGPT: **Plugins → Add custom MCP server**. Enter a name and the corresponding URL below,
choose **No authentication**, create it as a plugin and install it. Setup availability depends on your account and workspace policy.
You can then use the connection on supported surfaces for that account.

| Service | MCP URL |
|---|---|
| SC-Knowledge | `https://lab.olne.no/sc-knowledge/mcp` |
| Idiot Player | `https://lab.olne.no/idiot/mcp` |

This installs the MCP connection, not the repository's bundled skill.
[SC-Knowledge skill guidance](plugins/sc-knowledge/skills/sc-knowledge/SKILL.md) and
[Idiot guidance](plugins/idiot-player/skills/idiot/SKILL.md) are available to read or download separately.
Do not assume that uploading a file to a conversation installs a persistent skill.

### Workspace administrators: skill packages

The separate `openai/` catalog contains skill-only packages for workspace GitHub import.
Use this repository URL, branch `main`, and path `openai` in **Admin → Plugins → Import marketplace**.
Users connect the remote MCP separately, using the setup above, then enable the relevant skill.
These packages contain no registered app IDs and do not depend on the author's account or workspace.
They do not create a connection or grant access to account features. Workspace import requires administrator access;
external-account import and use have not been verified. Do not import the root desktop catalog for web/mobile use.

## Claude web, desktop and mobile

Use **Customize → Connectors → Add custom connector** (menu labels can vary). Enter a name and the MCP URL,
and select **No sign in**. In a managed organization, an owner may need to add the connector first.
Claude Code's marketplace installation does not create this separate account connection or install a cloud skill.

## What to try

For SC-Knowledge, ask: “Using SC-Knowledge, compare the latest three numbered LIVE patch cycles. Show the snapshot and source dates.”
Or ask about a ship, equipment, crafting or mining signature. Ask the AI to distinguish snapshot evidence from newer web information.
For Idiot, ask the AI to read the rules and help you join or start a game.

## Data, privacy and limits

SC-Knowledge serves versioned Star Citizen data, not guaranteed live game state. Data coverage and source dates can differ by topic.
The service receives the arguments your AI sends to its tools. Routine telemetry records operational metadata and aggregate gap signals.
If you explicitly ask to submit an answer issue, the supplied question, answer and comment can be sent to the service's process log.
Avoid including personal or confidential information. Anonymous feedback is unverified and does not change the source data.
The service is a small hobby project with rate limits; if busy, wait before retrying.

## Downloads and updates

`downloads/` contains versioned plugin ZIPs and standalone skill ZIPs. `distribution.json` lists file sizes and SHA-256 hashes.
ZIPs are convenience downloads; follow the installation route for your client. A remote server update and a client skill update are separate releases.
Use your client's marketplace update controls to receive new packages. This repository contains no hooks or installation scripts.
The files here are generated from reviewed client sources; development, server code and infrastructure remain private.

## Official installation references

- [OpenAI packaging and local marketplaces](https://developers.openai.com/plugins/build/plugins)
- [ChatGPT custom MCP setup](https://developers.openai.com/plugins/quickstart)
- [Workspace import, desktop-only packages and app permissions](https://learn.chatgpt.com/docs/enterprise/plugin-management)
- [Claude Code marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude custom connectors](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp)

SC-Knowledge is a community hobby project, not an official Cloud Imperium Games, OpenAI or Anthropic product.
