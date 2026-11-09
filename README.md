<img src="https://static.easyscribe.guide/Brand%20Assets/easy_scribe_logo.png" alt="Easy Scribe logo" width="72" height="72">

# Easy Scribe MCP server

[![Easy Scribe MCP connector](https://glama.ai/mcp/connectors/guide.easyscribe/easy-scribe/badges/score.svg)](https://glama.ai/mcp/connectors/guide.easyscribe/easy-scribe)

Turn a screen recording into a step-by-step guide, SOP or user doc with screenshots, from Claude, ChatGPT, Cursor, VS Code or Claude Code.

[Easy Scribe](https://www.easyscribe.guide) reads what happens on screen and any narration, then writes numbered steps with a screenshot at each one. Recordings without audio work too. This server lets your AI assistant do that for you: hand it a recording, and it gets back the finished document.

```text
https://mcp.easyscribe.guide/mcp
```

Remote server, Streamable HTTP. You sign in with your Easy Scribe account (OAuth), so there is nothing to install and no API key to copy. Works on the Free plan.

## What you can ask

- "Use Easy Scribe to turn `~/Movies/refund-walkthrough.mp4` into an SOP called How to issue a refund."
- "Make a user guide in Spanish from this recording: https://files.example.com/onboarding.mp4"
- "Get my latest Easy Scribe document as Markdown and summarise the steps."

Naming Easy Scribe and the recording in your message helps the assistant pick it. In Claude and ChatGPT an upload box appears in the chat: choose the video there, and it creates the document for you.

Processing takes a few minutes. Every document also lands in your Easy Scribe library, where you can edit it and export to PDF, Word or Markdown.

## Connect

### Claude

1. Open **Settings**, then **Connectors**, then **Add custom connector**.
2. Name it `Easy Scribe` and paste `https://mcp.easyscribe.guide/mcp`.
3. Select **Connect**, sign in to Easy Scribe, then **Allow**.

To start it from a chat, select **+**, then **Easy Scribe**, then **Turn a recording into a document**.

### ChatGPT

1. Open **Settings**, then **Apps & Connectors**, and create a connector. Some plans need **Developer mode** under **Advanced settings** first.
2. Paste `https://mcp.easyscribe.guide/mcp`, choose **OAuth**, sign in, then **Allow**.

To use it in a chat, type `@Easy Scribe` before your request, or select **+** and choose Easy Scribe.

### Claude Code

```bash
claude mcp add --transport http easy-scribe https://mcp.easyscribe.guide/mcp
```

Then run `/mcp` and choose **Authenticate** next to `easy-scribe`.

### Cursor

`~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "easy-scribe": {
      "url": "https://mcp.easyscribe.guide/mcp"
    }
  }
}
```

### VS Code

`.vscode/mcp.json`:

```json
{
  "servers": {
    "easy-scribe": {
      "type": "http",
      "url": "https://mcp.easyscribe.guide/mcp"
    }
  }
}
```

## Tools

| Tool | Read-only | What it does |
| --- | --- | --- |
| `create_document` | No | Creates a document from a direct video link (.mp4, .webm, .mov) or an uploaded file |
| `create_upload_url` | No | Starts an upload for a video on your computer, with an upload box in Claude and ChatGPT |
| `get_document` | Yes | Status, and the finished document with screenshot links |
| `list_documents` | Yes | Your recent documents, filtered by title or status |
| `list_templates` | Yes | Formats: General, SOP, User guide, Acceptance criteria, Tutorial, Onboarding guide, Release notes, Troubleshooting guide |
| `list_workspaces` | Yes | Workspaces you belong to |
| `share_document` | No | Creates a share link for a document you own |

No tool deletes or overwrites anything.

There is also one prompt, `document-a-recording`, for apps that list prompts.

Loom, YouTube and Vimeo links open a web page, not a video file. Download the video first and give the assistant the file.

## Before you sign in

Directories and agents can call `initialize`, `tools/list` and `prompts/list` without a token to see what the server does. Every tool call needs you to sign in, and one without a token gets `401` with a `WWW-Authenticate` header that points to the OAuth metadata.

## Plans

Free plan, and Pro at $9.99 a month with a 14-day free trial. PII redaction needs Pro. See [pricing](https://www.easyscribe.guide/pricing).

## Links

- [Setup guide](https://docs.easyscribe.guide/docs/ai-assistants/connect-easy-scribe-mcp)
- [Official MCP Registry entry](https://registry.modelcontextprotocol.io/v0/servers?search=guide.easyscribe): `guide.easyscribe/easy-scribe`
- [Privacy policy](https://www.easyscribe.guide/privacy-policy) · [Terms](https://www.easyscribe.guide/terms-of-service)
- Support: hello@easyscribe.guide

To disconnect an assistant, open **Settings → AI assistants** in Easy Scribe and select **Disconnect**.

This repository holds the listing and setup instructions. The server itself is hosted by Easy Scribe.
