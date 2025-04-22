# Labeller

A simple Github Action allowing you to enforce labels on pull requests or add
labels to pull requests. Automatically create labels if they do not exist.

## Inputs

| Key               | Required | Description                                                                                              |
| ----------------- | -------- | -------------------------------------------------------------------------------------------------------- |
| `add_labels`      | False    | Comma separated list of labels to add to the pull request.                                               |
| `required_labels` | False    | Comma separated list of labels that are required. Multiple lists can be provided, separated by newlines. |

> [!IMPORTANT]  
> Note that any labels used in `add_labels` must exist in order for the action
> to succeed.

## Example usage

```yaml
name: Check labels

on:
  pull_request:
    types: [opened, reopened, labeled, unlabeled]

# Thsee permissions are required for the action to work
permissions:
  contents: read
  pull-requests: write
  repository-projects: read

jobs:
  verify-labels:
    name: Verify required labels
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Verify labels and add needs-review label
        uses: Brains-Beyond-Expectations/labeller@v1
        with:
          add_labels: needs-review
          required_labels: |
            feature,enhancement,fix,bugfix,bug,chore
            major,minor,patch
```
