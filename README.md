# actions-mise-upgrade

GitHub workflow to upgrade tools managed by [`mise`](https://mise.jdx.dev).

Uses the [`mise upgrade`](https://mise.jdx.dev/cli/upgrade.html) command to
check for the latest versions of each tool and update the `.mise.toml` with
the results.

## Inputs

There are currently no inputs to provide to this action.

## Usage

```yaml
name: Update mise tool versions
"on":
  schedule:
      - cron: 0 15 1 * * # First day of each month at 15:00 UTC
  workflow_dispatch: {}

permissions: {}

jobs:
  updatecli:
    runs-on: ubuntu-latest
    permissions:
      # required to write to the repo
      contents: write
      # required to open a pr with changes
      pull-requests: write
    steps:
      - name: upgrade mise tools
        uses: prefecthq/actions-mise-upgrade@main
```
