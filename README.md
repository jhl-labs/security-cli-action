# security-cli-action

GitHub Action for running `security-cli` in CI and publishing scan findings as workflow annotations.

```yaml
- uses: jhl-labs/security-cli-action@main
  env:
    SE_ACTIONS_API_KEY: ${{ secrets.SE_ACTIONS_API_KEY }}
  with:
    profile: ci
    target: .
```

The action installs the latest public `security-cli` binary from `jhl-labs/dist` through:

```bash
curl -fsSL https://jhl-labs.github.io/security-cli/install.sh | bash
```

It then runs `security-cli diagnose`, reads generated SARIF reports, and emits GitHub Actions
annotations for GitOps Console.

## Usage metrics

By default, this action reports usage metrics to SE Actions Space after `security-cli` finishes.
The metrics step is non-critical: if tracking fails, the scan result is not changed.

Required caller secret:

```yaml
env:
  SE_ACTIONS_API_KEY: ${{ secrets.SE_ACTIONS_API_KEY }}
```

Optional inputs:

```yaml
with:
  usage-tracking: "true"
  usage-action-slug: security-cli-action
  se-actions-base-url: https://actions.euno.work
```

The metrics payload is sent through:

```bash
https://actions.euno.work/api/scripts/track-usage.sh
```

`status` is derived from the `security-cli` exit code, and `duration` is measured around the
`security-cli` execution step.
