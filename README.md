# Hively MCP plugin

This package connects Claude Code, Cursor, and Codex to each person's own Hively workspace. It provides the same Hively skill to all three clients. The MCP server runs at `https://YOUR-WORKSPACE.hivelyhr.com/mcp` and reads or proposes only actions permitted to the connected Hively user. Proposed changes are confirmed in Hively.

## Connect

1. Sign in to your Hively workspace and open **Ask Buzz > Connect AI apps**.
2. Create a connection token. Copy it when shown; it expires after 90 days and can be revoked there.
3. Configure the client below with your workspace URL and token. Never commit a token to a repository.

### Claude Code

Add this repository as a marketplace, then install the plugin:

```text
/plugin marketplace add HivelyHR/hively-mcp-plugin
/plugin install hively@hively
```

Its configuration prompt asks for the workspace URL and stores the token as a sensitive setting. Start a new Claude Code session and run `/mcp` to check the connection. For local testing, use `claude --plugin-dir /path/to/hively-mcp-plugin`.

### Cursor

Import `https://github.com/HivelyHR/hively-mcp-plugin` in Customize > Plugins. Configure `HIVELY_WORKSPACE_URL` and `HIVELY_MCP_TOKEN` when prompted. Verify Hively appears in the MCP tools list.

### Codex

Install the `hively` plugin from your Codex marketplace, or add this folder as a local plugin. Codex's portable plugin format does not allow a per-user workspace URL or bearer token in the bundled MCP config, so add this connection to `~/.codex/config.toml`:

```toml
[mcp_servers.hively]
url = "https://YOUR-WORKSPACE.hivelyhr.com/mcp"
bearer_token_env_var = "HIVELY_MCP_TOKEN"
```

Set `HIVELY_MCP_TOKEN` in the environment that launches Codex. Run `codex mcp list` to check the connection.

## Tools

`whoami`, `search_actions`, `describe_action`, `read_action`, `propose_action`, and `proposal_status`. A proposed write remains pending until the person confirms it in Hively. Read and write permissions are enforced by the application's existing assistant action service.

## Privacy and support

The connected assistant can request the Hively data the signed-in person is permitted to access, including employee information. Hively does not send data to the assistant until it calls a tool. Connection tokens belong to one Hively user, expire after 90 days, and can be revoked in Hively. Changes require a separate confirmation inside Hively.

[Privacy policy](https://hivelyhr.com/privacy-policy) · [Terms of service](https://hivelyhr.com/terms-of-service) · [Support](https://hivelyhr.com/contact-us)
