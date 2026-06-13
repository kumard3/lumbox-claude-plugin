# Lumbox plugin for Claude Code

Email for AI agents: self-provision inboxes, receive email, wait for parsed OTP codes,
send and reply. Bundles the 87-tool Lumbox MCP server (browser automation, credential
vault, TOTP 2FA).

## Install

```
/plugin marketplace add kumard3/lumbox-claude-plugin
/plugin install lumbox@lumbox
```

## Zero-human setup

The agent provisions itself — no console, no dashboard:

```bash
npx lumbox signup --source claude-code
```

That returns an API key (saved to `~/.lumbox/config.json`). Export it as `LUMBOX_API_KEY`
and the bundled MCP server is live.

Free tier: 3 inboxes, 5,000 inbound + 100 outbound emails/month. Paid from $9/mo.

## What you get

- `npx lumbox inbox create` — a real email address for your agent
- `npx lumbox wait-otp` — blocks until a verification email arrives, prints the parsed code
- `npx lumbox send` — outbound email
- MCP: 87 tools covering email, browser sessions, credential vault, TOTP 2FA, webhooks, custom domains

Docs: https://docs.lumbox.co • https://lumbox.co
