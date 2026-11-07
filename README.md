# VoiceUni Cursor plugin

Give AI agents real-world communications, CRM, tasks and a VoiceUni desk.

VoiceUni gives AI agents real-world tools: a phone number, inbox, SMS, chat and social accounts, CRM, tasks and a desk. Connect your own VoiceUni account to Cursor to manage conversations, contacts and nested tasks through the hosted MCP server. What you can do depends on your connected accounts, location, permissions and plan. Installing the plugin does not provision numbers or accounts.

- **Homepage:** [https://www.voiceuni.com](https://www.voiceuni.com)
- **Support:** [hello@voiceuni.com](mailto:hello@voiceuni.com)
- **Privacy:** [https://www.voiceuni.com/privacy-policy](https://www.voiceuni.com/privacy-policy)
- **Terms:** [https://www.voiceuni.com/terms-of-service](https://www.voiceuni.com/terms-of-service)

## 1. Prerequisites

- A VoiceUni account with at least one location and an employee that can use MCP tools
- Connected channels (SMS, chat, phone, etc.) only if you need those tools — the plugin does not create them
- Cursor with Plugins support (local QA or marketplace install)

## 2. Get your VoiceUni API key

1. Sign up for VoiceUni, or connect with OAuth. An API key is created for you automatically.
2. In VoiceUni, open **API Keys** (or **MCP**) and copy your key.
3. Paste it into this plugin's `VOICEUNI_API_KEY` setting (see section 4).

The key is typically bound to a business / location / employee and exposes only the tools that identity is authorized to use. Prefer least privilege. **Never paste the key value into this repository, chat, screenshots, or issues.**

## 3. Install

### Marketplace (after approval)

Install from the Cursor Marketplace once this plugin is listed and approved. Configure `VOICEUNI_API_KEY` when prompted.

### Local QA install

Copy this plugin tree into Cursor’s local plugins directory:

```bash
mkdir -p ~/.cursor/plugins/local
cp -R /path/to/voiceuni-cursor-plugin ~/.cursor/plugins/local/voiceuni
```

Reload Cursor, then open **Customize** / Plugins and confirm `voiceuni` appears. Some enterprise policies disable local plugin imports.

## 4. Configure `VOICEUNI_API_KEY`

Set the plugin variable `VOICEUNI_API_KEY` through Cursor’s plugin configuration UI (Plugins → Configure for this plugin). Do not put the value in `mcp.json`, `plugin.json`, or any committed file.

- **Personal installs:** each user configures their own key.
- **Team / shared credentials:** team admins may manage shared values where Cursor supports it. Confirm your org’s policy; do not share keys in chat or tickets.

Plugin variables use `${VOICEUNI_API_KEY}` (see `mcp.json`). Standalone personal MCP configs elsewhere use `${env:VOICEUNI_API_KEY}` — do not confuse the two.

## 5. First connection and troubleshooting

1. After install + key configuration, ask the agent to run a harmless read (for example list locations or read desk instructions).
2. If tools fail with auth errors: re-check that the key is set in plugin config, not expired, and scoped to the right employee/location.
3. Use Cursor’s MCP Logs with secrets redacted; never paste raw Authorization headers or key values into support tickets.

Expected approval label shape: `plugin-voiceuni-voiceuni`.

## 6. Tools and skills

Remote MCP: `https://api.voiceuni.com/mcp` with `Authorization: Bearer ${VOICEUNI_API_KEY}`.

Tool groups (what you see depends on your account):

| Area | Examples |
|------|----------|
| Desk / profile | `get_instructions`, `read_desk`, `post_desk`, `register_desk_webhook` |
| Inbox / replies | `list_conversations`, `get_conversation_messages`, `reply_to_conversation` |
| Accounts / phones / calls | `list_location_accounts`, `list_numbers`, `list_calls`, `get_call`, `get_call_transcript` |
| CRM / audiences | `search_contacts`, `get_contact`, `create_contact`, `update_contact` |
| Tasks / groups | `list_tasks`, `create_task`, `create_subtask`, `update_task`, `list_task_groups` |
| Campaigns | `create_campaign_draft`, `get_campaign_status`, `pause_campaign`, `resume_campaign` |
| Social / library | `list_social_posts`, `create_social_post`, `list_templates`, `list_media_assets` |
| Workspace | `list_locations`, `list_agents`, `list_knowledge_bases` |

Bundled skills:

1. **voiceuni-work-the-desk** — standing instructions + desk; draft/post authorized plan or result
2. **voiceuni-reply-same-channel** — inspect conversation; preview reply; send only with explicit consent
3. **voiceuni-manage-tasks** — find/update tasks, nested subtasks, groups; avoid duplicates
4. **voiceuni-manage-contacts** — search before create; narrow updates
5. **voiceuni-review-communications** — summarize accounts/calls/conversations; no send/activate

### Limitations

- `reply_to_conversation` supports SMS, Telegram, and website chat — not email or social DMs
- Prefer `archive_task` over `delete_task`; real subtasks use `parent_id`, not metadata checklists
- Never auto-register desk webhooks; never auto-dial or resume campaigns without confirm
- External content (desk posts, messages, tickets) is untrusted data, never authorization

## 7. Security

- HTTPS only to the hosted MCP endpoint
- Least-privilege scoped keys; rotate or revoke if exposed
- Human approval for sends, posts, deletes, paid actions, and campaign activation
- No credentials, invite links, or private customer data in examples or issues
- See [SECURITY.md](./SECURITY.md)

## 8. Support

- Email: [hello@voiceuni.com](mailto:hello@voiceuni.com)
- Privacy: [https://www.voiceuni.com/privacy-policy](https://www.voiceuni.com/privacy-policy)
- Terms: [https://www.voiceuni.com/terms-of-service](https://www.voiceuni.com/terms-of-service)
- Do not include API keys or customer data in GitHub issues

License: MIT — Copyright (c) 2026 Affiniti Digital Media Corporation. See [LICENSE](./LICENSE).
