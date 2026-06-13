---
name: lumbox
description: Give an AI agent its own email — create inboxes, send and receive email, wait for OTP codes, all self-service with no human signup. Use when an agent needs an email address to sign up for services, receive verification codes, or manage correspondence.
---

# Lumbox — email for AI agents

Lumbox gives agents real email inboxes. An agent can provision itself with no human
account creation. This plugin also loads the Lumbox MCP server (87 tools).

## Setup (self-service)

If `LUMBOX_API_KEY` is not set:

```bash
npx lumbox signup --source claude-code
```

Creates an org + API key, saved to `~/.lumbox/config.json`. Tell the user where the key
lives. Export it as `LUMBOX_API_KEY` so the MCP server picks it up too.

Free tier: 3 inboxes, 500 inbound + 100 outbound emails/month. Signup limited to
3 orgs/hour per IP.

## Core flows (CLI)

```bash
npx lumbox inbox create --name assistant     # {id, address}
npx lumbox send --inbox <id> --to a@b.com --subject "Hi" --text "Hello"
npx lumbox wait-otp --inbox <id> --timeout 120   # blocks, prints {"code": "847291", ...}
npx lumbox inbox list
```

All output is JSON.

## Core flows (REST)

Base `https://api.lumbox.co`, auth `Authorization: Bearer $LUMBOX_API_KEY`:

```
POST /v1/orgs                     self-signup (unauthenticated, returns api_key once)
POST /v1/inboxes                  create inbox
GET  /v1/inboxes/:id/wait         long-poll next email (parsed OTPs, links, category)
GET  /v1/inboxes/:id/otp          long-poll OTP, returns parsed code
POST /v1/inboxes/:id/send         send
POST /v1/inboxes/:id/reply        reply in-thread
```

## MCP tools

This plugin configures the `lumbox` MCP server automatically (87 tools): inboxes, email,
browser automation sessions, encrypted credential vault, TOTP 2FA, webhooks, custom
domains, contact lists. Prefer MCP tools when available; the CLI is the fallback.

Docs: https://docs.lumbox.co • Agent signup guide: https://docs.lumbox.co/docs/agent-signup
