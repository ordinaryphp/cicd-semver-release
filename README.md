# cicd-semver-release

Automatically create a release on pull request completion.

## Version Bumping

Version bumps are determined by the detection of keywords found in commits within the scope of the pull request.
Keywords are case-insensitive and by default `#vmajor, #vminor, #vpatch` will respectively add a major, minor,
or patch bump. If multiple keywords are found, the most significant version type will take priority. There will only be
one version bump per pull request, so multiple of the same keyword will NOT trigger multiple version bumps.

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

**Note: Be sure to use `token` input to supply a personal or app token to allow push workflows to be triggered**

## Inputs

<!-- start inputs -->

| **<b>Input</b>**                       | **<b>Description</b>**                                                                                            | **<b>Default</b>**   | **<b>Required</b>** |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | -------------------- | ------------------- |
| <b><code>token</code></b>              | Custom app or personal access token to use for release creation. (Required if tag push should trigger a workflow) |                      | **false**           |
| <b><code>prefix</code></b>             | Prefix to add to semver                                                                                           | <code>v</code>       | **false**           |
| <b><code>suffix</code></b>             | Suffix to add to semver                                                                                           |                      | **false**           |
| <b><code>major_token</code></b>        | Token in commits to trigger a major version change                                                                | <code>#vmajor</code> | **false**           |
| <b><code>minor_token</code></b>        | Token in commits to trigger a minor version change                                                                | <code>#vminor</code> | **false**           |
| <b><code>patch_token</code></b>        | Token in commits to trigger a patch version change                                                                | <code>#vpatch</code> | **false**           |
| <b><code>default_bump</code></b>       | The default version bump when no tokens are found (major, minor, patch, none)                                     | <code>none</code>    | **false**           |
| <b><code>strict_semver_last</code></b> | When detecting last semver, requires the semver to have the configured prefix and suffix                          |                      | **false**           |
| <b><code>create_release</code></b>     | Use this to add additional conditions for or for not creating a release                                           | <code>true</code>    | **false**           |

<!-- end inputs -->

## Outputs

<!-- start outputs -->

| **<b>Output</b>**                 | **<b>Description</b>**        |
| --------------------------------- | ----------------------------- |
| <b><code>tag_latest</code></b>    | Latest semver tag detected    |
| <b><code>semver_latest</code></b> | Latest semver detected        |
| <b><code>tag_next</code></b>      | Next semver tag to be created |
| <b><code>semver_next</code></b>   | Next semver to be created     |
| <b><code>change_type</code></b>   | Change type                   |

<!-- end outputs -->
