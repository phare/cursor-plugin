# Phare plugin for Cursor

Check and manage your [Phare](https://phare.io) uptime monitors, incidents, maintenance windows and status pages from Cursor.

The plugin adds:

- The [Phare MCP server](https://docs.phare.io/integrations/mcp) at `https://mcp.phare.io/mcp`.
- A `phare` skill telling the agent how to use it: call `whoami` first, pick the right project, and ask before deleting anything or publishing to a status page.

## Install

Install **Phare** from the [Cursor Marketplace](https://cursor.com/marketplace).

To try it from this repository instead, clone it into your local plugins folder and run **Developer: Reload Window**:

```bash
git clone https://github.com/phare/cursor-plugin ~/.cursor/plugins/local/phare
```

## Connect your account

Open **Customize** > **MCPs** in the sidebar and log in to Phare next to the Phare server. Phare shows the application, your email address, organization and role: click **Approve** to connect it.

No API key is needed. You need a Phare account with a verified email address and access to at least one project.

## Usage

Ask in plain words, for example:

- "Which monitors are down in my Production project?"
- "What was the uptime of the API monitor last month?"
- "Open an incident on the status page for the slow checkout, and post an update saying we are investigating."
- "Schedule a maintenance window on Sunday from 2:00 to 4:00 for the database monitors."
- "Create an HTTP monitor for https://example.com checking every minute."

If you have several projects, name the project in your request.

## Permissions

The plugin acts as you, with the permissions of your [role](https://docs.phare.io/user-management#roles):

- It only sees the tools your role can use, and only the projects you can access.
- It can't manage API keys, invitations, members, roles, single sign-on, the organization settings or billing.

The full list of tools is in the [MCP server documentation](https://docs.phare.io/integrations/mcp#tools).

To disconnect Cursor, remove it from the connected applications in your [user settings](https://app.phare.io/user/settings#connected-applications).

## Support

Contact [support@phare.io](mailto:support@phare.io) or open an issue on this repository.

## License

[MIT](LICENSE)
