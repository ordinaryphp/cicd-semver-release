# cicd-semver-release

Automatically create a release on pull request completion.

## Usage

```yaml
on:
  pull_request: # only supports pull_request event
    branches:
      - main
    types:
      - labeled # recommended for pre merge validation
      - unlabeled # recommended for pre merge validation
      - opened # recommended for pre merge validation
      - closed # required
      - reopened # recommended for pre merge validation
      - synchronize # recommended for pre merge validation
permissions:
  contents: write
jobs:
  job1:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@main
      - uses: ordinaryphp/cicd-semver-release@main
```

## Inputs

<!-- start inputs -->

| **<b>Input</b>**                                  | **<b>Description</b>**                                                                   | **<b>Default</b>**                   | **<b>Required</b>** |
| ------------------------------------------------- | ---------------------------------------------------------------------------------------- | ------------------------------------ | ------------------- |
| <b><code>prefix</code></b>                        | Prefix to add to semver                                                                  | <code>v</code>                       | **false**           |
| <b><code>suffix</code></b>                        | Suffix to add to semver                                                                  |                                      | **false**           |
| <b><code>strict_semver_last</code></b>            | When detecting last semver, requires the semver to have the configured prefix and suffix |                                      | **false**           |
| <b><code>create_release</code></b>                |                                                                                          | <code>true</code>                    | **false**           |
| <b><code>create_if_pr_complete</code></b>         | Disable to allow release creation when trigger is not a completed pull request           | <code>true</code>                    | **false**           |
| <b><code>enhancement_label</code></b>             | Label that indicates changes includes enhancements or new features                       | <code>enhancement</code>             | **false**           |
| <b><code>bug_label</code></b>                     | Label that indicates changes includes bug fixes                                          | <code>bug</code>                     | **false**           |
| <b><code>backward_compatible_label</code></b>     | Label that indicates changes are backward compatible                                     | <code>backward-compatible</code>     | **false**           |
| <b><code>not_backward_compatible_label</code></b> | Label that indicates changes are not backward compatible                                 | <code>not-backward-compatible</code> | **false**           |

<!-- end inputs -->

## Outputs

<!-- start outputs -->

| **<b>Output</b>**                        | **<b>Description</b>**        |
| ---------------------------------------- | ----------------------------- |
| <b><code>tag_last</code></b>             | Last semver tag detected      |
| <b><code>semver_last</code></b>          | Last semver detected          |
| <b><code>tag_next</code></b>             | Next semver tag to be created |
| <b><code>semver_next</code></b>          | Next semver to be created     |
| <b><code>change_compatibility</code></b> | Change compatibility          |
| <b><code>change_type</code></b>          | Change type                   |

<!-- end outputs -->
