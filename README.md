# security-cli-action

GitHub Action for running `security-cli` in CI and publishing scan findings as workflow annotations.

```yaml
- uses: jhl-labs/security-cli-action@main
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
