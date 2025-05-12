# has-changes-since-last-success

Action to determine if there are changes in the provided paths since the last successful workflow run. Supports only `push` and `pull_request` events.

Inputs

- `github-token`: GitHub token to checkout repo with, defaults to `github.token`
- `paths`: Paths to check for changes in, can be specified as signle line `>-` or multiline `|`; `.github` is always included unless `no-dot-github` is set to `true`
- `no-dot-github`: Set to `true` if `.github` folder should not be automatically included and only specified `paths` should be checked
- `fetch-depth`: Fetch depth for checkint out the repo, default `20`

Outputs:

- `success-commit`: Last successfull commit SHA
- `has-changes`: Specifies if there were changes (`true`) since last successfull commit in the specified path. If no successfull commits are found (e.g. first run, or fetch-depth is not enough, or `gh run list` does not list all runs, etc.), will be set to `true`

Examples:

- https://github.com/kt-npm-modules/npm-typescript-template/blob/main/.github/workflows/ci.yml#L25

Additional considerations:

- Checks out the repo into `temp_dir=".last_success_check_$(date +%s%N)"` for checking.
