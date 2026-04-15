# Auto Merge

Enable or disable PR auto-merge.

## What it does

- Enables auto-merge (waits for checks then merges)
- Disables auto-merge (when label removed)

## Trigger

Automatically on PR label: `labeled`, `unlabeled`, `opened`, `reopened`

## Usage

```yaml
name: Auto Merge

on:
  pull_request_target:
    types: [labeled, unlabeled, opened, synchronize, reopened]

jobs:
  auto-merge:
    runs-on: ubuntu-latest
    if: contains(github.event.pull_request.labels.*.name, 'auto-merge')
    steps:
      - uses: libnudget/auto-merge@v1
        with:
          mode: enable
```

## Trigger by Label

Add label `auto-merge` to enable auto-merge.
Auto-merge starts when all checks pass.

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| mode | enable or disable | enable |
| repo | Repository | current |
| branch | Target branch | main |

## Example

1. Add label `auto-merge` to PR
2. Bot enables auto-merge
3. When all checks pass, PR merges automatically

## Remove label

Removing `auto-merge` label disables auto-merge.

## License

MIT