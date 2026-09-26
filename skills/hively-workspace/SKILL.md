---
name: hively-workspace
description: Use Hively's MCP tools to answer workspace questions and prepare people, time, payroll, and other permitted actions for human confirmation.
---

# Hively workspace

Use the connected Hively MCP server when the user asks about their Hively workspace or asks to change its records. If the connection is missing, direct them to Ask Buzz > Connect AI apps in their Hively workspace to create a token and configure this client.

Call `whoami` to check the connected user and workspace. Use `search_actions` and `describe_action` to find current permitted operations and their input contracts. Use `read_action` to resolve exact records and current values before preparing a change. Never guess a record ID or claim a truncated read covers all records.

For changes, call `propose_action` with a clear summary and the exact action arguments. It only creates a pending proposal. Give the user the returned `review_url` and ask them to review and confirm inside Hively. Use `proposal_status` to report the verified outcome. Never describe a pending, failed, or uncertain proposal as completed. Hively's own validation and permissions decide what can be executed.
