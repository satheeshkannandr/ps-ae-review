# CLAUDE.md — PeopleSoft App Engine Review Workspace

This folder is a workspace for reviewing PeopleSoft Application Engine (AE) programs.

## The review playbook is a Skill
The full playbook (metadata map, extraction queries, review checklist, output format) now lives
in the **`ps-ae-review`** skill at [.claude/skills/ps-ae-review/SKILL.md](.claude/skills/ps-ae-review/SKILL.md).
It auto-runs when you ask to review an App Engine (e.g. *"Review App Engine `AR_AGING` and
connect to TEST"*), and you can invoke it directly with `/ps-ae-review`. It's committed in the
repo, so colleagues who open this project get it automatically and can use it the same way.

## Environment (always-true project facts)
- **Database connection:** connect with the `mcp__sqlcl` tools — `mcp__sqlcl__connect`
  (connection_name = the `<DB_NAME>` named in the request), then `mcp__sqlcl__sql_run`. If no DB is
  named, **ask the user which database to connect to — never assume or default to one.** If already
  connected to the requested DB, don't reconnect; if connected to a *different* DB, confirm before
  switching.
- **Reference instance — `TEST`:** Oracle 19c, schema **`SYSADM`**, charset UTF8,
  `NLS_DATE_FORMAT = DD-MON-RR`, PeopleSoft **FSCM 9.2 / PeopleTools 8.58**. Other instances may
  differ (tools release, schema, NLS); the `connect` call returns the actual context — rely on that.
- Tables are owned by `SYSADM`; query them unqualified (the connection user has access).
