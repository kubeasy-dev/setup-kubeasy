# setup-kubeasy

GitHub Action to install the [kubeasy CLI](https://github.com/kubeasy-dev/kubeasy-cli) and set up a Kind cluster with infrastructure (Kyverno + local-path-provisioner) for Kubeasy challenges.

## Usage

```yaml
- uses: kubeasy-dev/setup-kubeasy@v1
  with:
    api-key: ${{ secrets.KUBEASY_API_KEY }}
```

### Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `version` | No | `latest` | Version of kubeasy CLI to install (e.g. `v2.5.2`) |
| `api-key` | Yes | | Kubeasy API key for authentication |

### Outputs

| Output | Description |
|--------|-------------|
| `version` | Installed kubeasy CLI version |

## What it does

1. Installs the kubeasy CLI (latest or pinned version)
2. Sets the `KUBEASY_API_KEY` environment variable
3. Runs `kubeasy setup` to create a Kind cluster and install infrastructure

## Example

```yaml
name: Test Challenge
on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: kubeasy-dev/setup-kubeasy@v1
        with:
          api-key: ${{ secrets.KUBEASY_API_KEY }}

      - name: Start challenge
        run: kubeasy challenge start pod-evicted

      - name: Submit solution
        run: kubeasy challenge submit pod-evicted
```

## License

See [LICENSE](./LICENSE) file for details.
