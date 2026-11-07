# Security Policy

## Reporting a vulnerability

Email **hello@voiceuni.com** with a clear description of the issue, steps to reproduce if applicable, and impact. Do not open a public GitHub issue for security problems.

## Do not include in reports or issues

- API keys, tokens, or passwords
- Customer data, contact PII, call recordings, or message content
- Private invite links or webhook URLs

## Credential hygiene

- Store `VOICEUNI_API_KEY` only through Cursor’s plugin configuration UI (or your team’s approved secret store). Never commit it to this repo, paste it into chat, or put it in `.env` files that are tracked.
- If a key may have leaked: revoke or rotate it in your VoiceUni account immediately, then configure the new value in Cursor.
- Prefer scoped keys bound to the least privilege your workflow needs (location / employee / tools).

## Transport and approvals

- The MCP endpoint is served over HTTPS only: `https://api.voiceuni.com/mcp`.
- Cursor will prompt for tool approvals. Review each irreversible or externally visible action (sends, posts, deletes, paid actions, campaign activation) before confirming.
- This plugin never auto-registers desk webhooks and never auto-dials or resumes campaigns without an explicit confirm.

## Scope

This repository contains plugin manifests, skills, and documentation only. It does not ship VoiceUni server code or customer data.
