# Garmin China to Global sync

The `Sync Garmin CN to Garmin Global` workflow copies recent activities from
Garmin China to Garmin Global every six hours. It can also be run manually in
dry-run mode before uploads are enabled.

## Configure repository secrets

Open **Settings > Secrets and variables > Actions**, then add these repository
secrets:

- `GARMIN_USERNAME`: Garmin China email address
- `GARMIN_PASSWORD`: Garmin China password
- `GARMIN_GLOBAL_USERNAME`: Garmin Global email address
- `GARMIN_GLOBAL_PASSWORD`: Garmin Global password

Do not put credentials in source files, workflow inputs, issues, or Actions
logs.

## Test the workflow

1. Open **Actions > Sync Garmin CN to Garmin Global > Run workflow**.
2. Keep `limit` at `30`, enable `dry_run`, and start the run.
3. Review the log. If authentication and activity discovery succeed, run it
   again with `dry_run` disabled.

The scheduled job runs automatically after the workflow is present on the
default branch. It compares recent activities and skips duplicates.

## Security notes

- The workflow has read-only repository permission.
- Login tokens are stored only in the GitHub-hosted runner's temporary folder
  and are deleted at the end of every run.
- The sync client is pinned to an audited Git commit instead of following a
  moving branch.
- No session database or token is committed back to this repository.

If either Garmin account requires an interactive MFA challenge on every login,
scheduled unattended runs may fail. Complete the challenge in a manual run if
the client supports it, or use an account configuration that permits normal
session login.
