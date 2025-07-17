# JSON Version Check Action

A very simple GitHub Action to check if a specified key in a user-defined JSON file has changed between commits.

## Inputs

| Name      | Description           | Required | Default      |
| --------- | --------------------- | -------- | ------------ |
| file-path | Path to the JSON file | false    | package.json |
| key       | JSON key to compare   | false    | version      |

## Outputs

| Name    | Description                                         |
| ------- | --------------------------------------------------- |
| changed | `true` if the key' value changed, `false` otherwise |

## Example Usage

```
name: Check JSON Version
on:
    push:
        branches:
            - main
jobs:
    check-json-version:
        runs-on: ubuntu-latest
        steps:
            - uses: actions/checkout@v4
              with:
                  fetch-depth: 2
            - id: json_version_check
              uses: Lucas-PG/json-version-check@v1
              with:
                  file-path: package.json # Optional, defaults to package.json
                  key: version # Optional, defaults to version

            - if: steps.json_version_check.outputs.changed == 'true'
              run: echo "Version changed, proceeding with deployment..."
```
