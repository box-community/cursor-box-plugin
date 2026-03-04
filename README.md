# Box Plugin for Cursor

Search, read, and manage your Box content directly from Cursor — plus tap into
Box AI for Q&A, summarization, and metadata extraction without leaving your
editor.

This plugin connects Cursor to the
[Box MCP server](https://developer.box.com/guides/box-mcp/remote/),
giving the AI agent access to your files, folders, hubs, and Box AI tools.

## Prerequisites

You'll need a Box account with access to the
Box MCP server. Your Box admin may need to
enable the MCP server integration in the
[Admin Console](https://developer.box.com/guides/authorization/).

## Setup

### 1. Create a Box OAuth 2.0 app

Head to the Box Developer Console
and [create a new Custom App with OAuth 2.0 authentication](https://developer.box.com/guides/authentication/oauth2/oauth2-setup/).

Once created, grab your **Client ID** and **Client Secret** from the app's
Configuration tab.

### 2. Set your environment variables

The plugin reads credentials from two environment variables:

```sh
export BOX_CLIENT_ID="your_client_id"
export BOX_CLIENT_SECRET="your_client_secret"
```

Add these to your shell profile (`.zshrc`, `.bashrc`, etc.) or use whatever
secrets management your team prefers. Don't hardcode them anywhere.

### 3. Install the plugin

Install the Box plugin from the Cursor Marketplace, or add this repository
directly in Cursor's plugin settings.

That's it — the MCP server connection, skill, and rules are all configured
automatically.

## What's included

| File | What it does |
|---|---|
| `mcp.json` | Connects Cursor to the remote Box MCP server at `https://mcp.box.com` |
| `skills/box/SKILL.md` | Teaches the AI agent best practices for Box — search patterns, file write safety, metadata extraction workflows, and Box AI usage |
| `rules/box.mdc` | Enforces safety guardrails — confirmation prompts for destructive actions, hub modifications, and content display preferences |

## What you can do

Once installed, you can ask the Cursor agent to work with your Box content
naturally. A few examples:

- **Search** — "Find all Q4 reports in the Finance folder"
- **Read files** — "Show me what's in the project brief"
- **Upload** — "Upload this CSV to the Reports folder in Box"
- **Box AI Q&A** — "Summarize the key risks in this contract"
- **Metadata extraction** — "Extract invoice numbers and totals from these PDFs"
- **Hubs** — "List my hubs" or "Add this file to the Product Launch hub"
- **Collaboration** — "Show me the comments on this file" or "What tasks are assigned to me?"
- **Doc Gen** — "Generate an NDA from the template using this data"

The agent has access to 30+ Box MCP tools covering file operations, folder
management, search, collaboration, hubs, Box AI, and document generation. See
the [full tool list](https://developer.box.com/guides/box-mcp/remote/) for
details.

## Safety guardrails

The plugin comes with built-in guardrails so the agent doesn't do anything
surprising:

- **Destructive actions** (overwrite, delete, bulk changes) prompt you for
  confirmation the first time, then let you choose whether to keep confirming
  or auto-approve for the session.
- **Hub creation and modifications** always ask before proceeding, since hubs
  can be visible across your organization.
- **AI operations stay in Box** — when you need Q&A, summarization, or
  extraction, the agent uses Box AI rather than downloading files and
  processing them externally.
- **Content display** — the first time file content would be shown in chat, the
  agent asks whether you prefer a link to Box or the content pasted directly,
  then remembers your choice.

## Links

- [Box MCP Server docs](https://developer.box.com/guides/box-mcp/remote/)
- [Box OAuth 2.0 setup](https://developer.box.com/guides/authentication/oauth2/oauth2-setup/)
- [Box Developer Console](https://app.box.com/developers/console)
- [Box Developer Community](https://community.box.com/box-platform-5)

## License

MIT
