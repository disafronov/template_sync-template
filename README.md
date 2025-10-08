# template_sync-template

Automated synchronization of repositories from a template repository using GitHub Actions.

## Files

- `template.repo` - Template repository (one line, format: `owner/repo`)
- `repos.list` - Target repositories to sync (one per line, format: `owner/repo`)
- `include.list` - Files to sync from template (rsync include patterns)
- `delete.list` - Files to delete from target repos (optional, one per line)

## Security

The `delete.list` processing includes safety checks:
- Prevents absolute paths (`/`)
- Prevents path traversal (`../`)
- Validates paths stay within repository boundaries

## Usage

1. Configure the files above
2. Set up `REPO_UPDATE_TOKEN` secret with appropriate permissions
3. The workflow runs daily at 2 AM UTC or manually via `workflow_dispatch`
