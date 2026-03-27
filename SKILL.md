---
name: ai-daily-update
description: Generates a highly formatted daily update email analyzing recent communications. Configuration-driven and delivery-agnostic. Use when asked to "Run AI Daily Update".
---

# AI Daily Update

This skill generates a highly structured daily briefing based on the user's communications. It is designed to be delivery-agnostic and configuration-driven.

## Execution Flow

When triggered, follow this exact sequence:

### 1. Load Configuration
Read `config.yaml` (and `.env` if needed) to determine:
- `sources`: Which platforms to read from (Gmail, Calendar, Slack, Beeper).
- `delivery.method`: How to send the final briefing.
- `rules`: Custom user instructions for categorizing items.

### 2. Gather Context
Use the available MCP tools to gather data over the past 24 hours based on the configured sources. 

### 3. Agnostic Synthesis (The Core)
Synthesize the gathered data into a strictly structured JSON object. Apply the user's custom `rules` from `config.yaml` to categorize items into:
- `action_items`: Urgent tasks or pending drafts.
- `fyis`: Completed items or general news.
- `tracking`: Ongoing items waiting on others.
- `schedule`: Tomorrow's meetings and prep notes.

*Important:* You must generate the data as a raw JSON structure in memory first. Do not generate HTML or Markdown directly from the prompt.

### 4. Delivery via Adapters
Based on the `delivery.method` in `config.yaml`:

**If `method` == "gmail":**
Take the synthesized JSON data and inject it into the precise HTML structure found in `assets/template.html`. Ensure the HTML is perfectly preserved (100% width tables, pill spans, etc.). Then, send the email using the `mcp_google-workspace_gmail.send` tool with `isHtml: true` to the `delivery.recipient`.

**If `method` == "slack":**
Save your synthesized JSON to a temporary file (e.g., `/tmp/daily_update.json`). Then, execute the `adapters/slack_adapter.py` script using the `run_shell_command` tool, passing the temp file as an argument:
`python3 adapters/slack_adapter.py /tmp/daily_update.json`

**If `method` == "stdout":**
Simply print the synthesized JSON or a clean markdown representation to the console for the user to read directly.