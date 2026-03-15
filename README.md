# @clawnitor/plugin

OpenClaw plugin for Clawnitor — agent monitoring, alerting, and kill switch.

## Installation

```bash
openclaw plugins install @clawnitor/plugin
```

## Configuration

Add to your `openclaw.json`:

```json
{
  "plugins": {
    "entries": {
      "clawnitor": {
        "config": {
          "apiKey": "clw_live_your_key_here"
        }
      }
    }
  }
}
```

### Options

| Option | Default | Description |
|--------|---------|-------------|
| `apiKey` | required | Your Clawnitor API key |
| `backendUrl` | `https://api.clawnitor.io` | Backend URL |
| `spendLimit` | `100` | Max spend per session ($) before auto-pause |
| `rateLimit` | `120` | Max tool calls per minute before auto-pause |
| `toolBlocklist` | `[]` | Tool names to always block |
| `redactionPatterns` | `[]` | Additional regex patterns for secret redaction |

## What it monitors

- Tool calls (before and after execution)
- LLM requests (input/output, token usage, cost)
- Messages (sending, sent, received)
- Session lifecycle (start, end, agent completion)
- Sub-agent spawning and completion

## Safety features

- **Kill switch** — blocks tool calls and messages when agent is paused (server or local)
- **Spend circuit breaker** — auto-pauses at configurable spend limit
- **Rate limiter** — auto-pauses at configurable tool call rate
- **Tool blocklist** — prevents specific tools from ever executing
- **Secret redaction** — strips API keys, passwords, tokens from logged data

## Privacy

Event data streams to the Clawnitor backend for monitoring. Sensitive data (API keys, passwords, tokens) is automatically redacted before transmission. Data sharing for aggregate pattern improvement is opt-in (default OFF).

Learn more at https://clawnitor.io
