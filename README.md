# Auto Merge

Enable or disable PR auto-merge.

## What it does

- `enable` - Waits for checks to pass, then merges
- `disable` - Cancels auto-merge
- `now` - Merges immediately (skip checks)

## Labels

| Label | Mode | Behavior |
|-------|------|----------|
| `auto-merge` | enable | Waits for checks, then merges |
| `auto-merge-now` | now | Merges immediately |

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

  auto-merge-now:
    runs-on: ubuntu-latest
    if: contains(github.event.pull_request.labels.*.name, 'auto-merge-now')
    steps:
      - uses: libnudget/auto-merge@v1
        with:
          mode: now
```

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| mode | enable, disable, or now | enable |
| repo | Repository | current |
| branch | Target branch | main |

## License

MIT