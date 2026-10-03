---
name: tareno-social-ops
description: Use Tareno to inspect social accounts and posts, analyze performance metrics, derive content strategy, manage media, create or update drafts, and request approval-backed scheduling, publishing, rescheduling, or deletion.
---

# Tareno Social Operations

Use the bundled Tareno MCP tools for account-specific social media work. Treat Tareno as the source of truth for connected accounts, platform rules, post state, analytics, and approval status.

## Connection

- Connect to the bundled remote MCP endpoint using Tareno OAuth when prompted.
- If tools are unavailable, authenticate the Tareno MCP connection in the client's settings and retry.
- Never request, echo, log, or place credentials in prompts, URLs, files, or tool arguments.

## Resolve context first

1. Call `list_workspaces` when workspace context matters and the user has not selected one.
2. Call `list_accounts` before account-scoped work unless the current task already contains fresh Tareno account IDs.
3. If more than one account matches an ambiguous platform or name, ask the user which account to use.
4. Before drafting, scheduling, or publishing for an account, call `get_platform_schema`.
5. Call `get_platform_options` when Pinterest boards or TikTok creator information is required.

## Analytics-first workflow

When the user asks about performance, recommendations, or what to post next:

1. Use `get_analytics_overview` for the requested period, defaulting to `month` only when the user gives no period.
2. Use `get_platform_analytics` for relevant platform or account drill-downs.
3. Use `get_content_strategy` for analytics-backed recommendations and repurposing opportunities.
4. Separate observed metrics from recommendations. Do not invent missing values or imply causation that the returned data does not establish.
5. Make each recommendation traceable to a returned metric, trend, or content pattern.

## Draft, schedule, and publish

- Prefer `create_drafts` when the user is exploring copy, targets, or timing. Draft creation does not publish externally.
- Use `update_draft` only for an existing editable draft.
- Use `schedule_posts`, `publish_posts`, `reschedule_post`, or `update_scheduled_post` only when the user has clearly requested that consequence and supplied enough target, content, and timing detail.
- Use explicit ISO 8601 timestamps with a UTC offset and an IANA timezone for scheduled work.
- Give each consequential request a new stable `idempotencyKey`. Never reuse a key for a different operation or payload.
- Scheduling, publishing, scheduled edits, and deletions return an approval action. Report `approval_required`, summarize the exact impact, and provide the returned Tareno approval URL. Do not claim completion before `get_action_status` reports success.
- Use `delete_post` only for a draft or scheduled post and only after the user clearly asks to delete it.

## Media

- Use `list_media` before asking the user to re-upload an asset that may already exist.
- `upload_media_from_url` accepts only public HTTPS image or video URLs. Do not try local paths, private network URLs, embedded credentials, or non-HTTPS sources.

## Output

Lead with the result or decision. For analytics, include the period, key metrics, and evidence-linked recommendations. For pending actions, include targets, timing, approval status, and the approval link. For batch results, distinguish full success, partial success, and failure per item.
