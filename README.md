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

## References

- https://github.com/jdx/mise/discussions/1823: this issue discusses workflows for plugin updates. Might be worth following along in case there ends up being a more 'official' way to do this.
- https://github.com/jdx/mise/discussions/4057: this discussion mentions the `mise upgrade --bump` command we're using here, along with some context.
- https://github.com/jdx/mise/discussions/4241: this discussion suggests adding a changelog to the `self-update` command, which is somewhat related and hopefully will carry over to the `upgrade` command for us to use in pull request descriptions.
