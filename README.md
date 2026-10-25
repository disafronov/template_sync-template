# template_sync-template

GitHub repository template for synchronizers that propagate selected paths
from a versioned source template to configured target repositories.
`include.list` defines managed paths and `delete.list` defines explicit
removals. Synchronization uses the latest `vMAJOR.MINOR.PATCH` release tag
of the source template, rather than its default branch.

When a target is itself a GitHub template, the synchronization commit uses a
release-triggering Conventional Commit prefix so changes can propagate through
successive template levels. Ordinary repository targets receive a non-release
commit.

## Files

- `template.repo` - Template repository (one line, format: `owner/repo`)
- `repos.list` - Target repositories to sync (one per line, format: `owner/repo`)
- `include.list` - Files to sync from template (rsync include patterns)
- `delete.list` - Files to delete from target repos (optional, one per line)

The workflow pushes changes directly to each target's default branch.
`delete.list` is an explicit removal mechanism, not an instruction to mirror
all deletions from the source template.

## Security

The `delete.list` processing includes safety checks:
- Prevents absolute paths (`/`)
- Prevents path traversal (`../`)
- Validates paths stay within repository boundaries

## Usage

1. Configure the files above
2. Set up `REPO_UPDATE_TOKEN` secret with appropriate permissions
3. The workflow runs daily at 2 AM UTC or manually via `workflow_dispatch`
