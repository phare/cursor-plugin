---
name: phare
description: Work with the user's Phare organization through the Phare MCP tools. Use when the user asks about their monitors, uptime or downtime, incidents, status pages, maintenance windows, alert rules or Phare projects.
---

# Phare

Phare checks websites and APIs from several regions, opens an incident when a monitor fails, alerts the team, and shows incidents and maintenance windows on public status pages.

## Start with whoami

Call `whoami` first. It returns the user's role, permissions and the projects they can access.

Everything except projects, users and integrations belongs to a project, so most tools need a `project_id`:

- If the user names a project, use its ID from `whoami`.
- If there is one project, use it.
- If there are several and the user didn't name one, read from all of them for questions like "which monitors are down", but ask which project to use before creating or changing anything.

The tools listed are the ones the user's role allows. If a tool is missing, tell the user their role doesn't allow it instead of looking for another way.

## Common tasks

**Monitor status.** `list_monitors` returns the status of each monitor: `online`, `offline`, `partial` (down in some regions), `paused`, or `fetching` (first check not done yet).

**Uptime.** `get_report` covers every monitor of a project, `get_monitor_report` a single monitor. Pass `from` and `to` as ISO 8601 dates in the past, at most one year apart. Without dates, the report covers the last 30 days. Durations are in seconds: convert them to minutes or hours for the user.

**Incidents.** Phare opens incidents on its own when a monitor fails. Use `create_incident` only for an outage the monitors didn't catch. A status page shows an incident once an update is published, so follow it with `create_incident_update`, using the `investigating`, `identified`, `monitoring` or `resolved` state. An update with the `resolved` state recovers the incident. `recover_incident` recovers it without posting an update.

**Maintenance windows.** `create_maintenance_window` takes `starts_at` and `ends_at` to the minute (seconds must be `00`). Include the timezone offset, and ask for the user's timezone when the request doesn't make it clear. `monitoring_mode` is `pause` (stop checking), `mute` (keep checking without incident alerts) or `normal` (only announce the maintenance).

**Status pages.** `get_status_page_current_status` gives what visitors see right now.

## Before changing data

- Ask for confirmation before any `delete_` tool. `delete_project` also deletes every monitor, incident, status page and alert rule of the project.
- Incident updates and maintenance windows appear on the linked public status pages right away. Show the user the text before publishing it, unless they gave the exact wording.

## Not available

The plugin can't manage API keys, invitations, members, roles, single sign-on, organization settings or billing. Point the user to the dashboard at https://app.phare.io for these.

The tools share a limit of 100 requests per minute across the organization: prefer one list call over many get calls.
