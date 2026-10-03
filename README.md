# Tareno for Gemini CLI

A Gemini CLI extension bundling Tareno's remote MCP server, social operations skill, context and `/tareno:plan` command. Inspect accounts and posts, analyze performance, manage media and drafts, and request approval-backed scheduling and publishing.

## Install

```sh
gemini extensions install https://github.com/TarenoAI/tareno-gemini-extension
gemini
```

In Gemini CLI, run `/mcp auth tareno` and sign in to Tareno. No API key is bundled. A Tareno account with MCP access is required. Then run `/mcp` to confirm tool discovery and ask “List my connected Tareno accounts.”

## Examples

- `/tareno:plan Plan next week's Instagram content from last month's analytics.`
- “Compare platform performance this month.”
- “Create three drafts for the selected account.”

Publishing and scheduling return a Tareno approval link. Follow that link and check the action status before treating the action as complete.

## Release status

The package uses the documented Gemini CLI format. Full OAuth and tool execution must be verified against the production server before claiming end-to-end compatibility. Google's gallery discovers repositories tagged `gemini-cli-extension` daily; a public repository is not proof of gallery inclusion.

MCP: https://tareno.co/api/mcp  
Documentation: https://tareno.co/docs/mcp  
Support: support@tareno.co
