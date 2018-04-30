## How do I add a dependency to Istio?

1. Make sure you have the latest `dep` tool by running `go get -u github.com/golang/dep/cmd/dep`.
2. Add the new import to your code.
3. Run `dep ensure` from the command line.
4. Create a PR
    - Use separate commits for `Gopkg.lock`/`vendor` changes and the actual business logic. This makes easier for the reviewers to skip the vendor noise when reviewing your PR.

## Why does my PR fail the CI vendor lint check?

It could be that you're using a different version of the `dep` tool. The CI linter always grabs the latest version. You should update to the latest `dep` version and follow the process described above.

## How can I replicate the CI vendor lint check locally?

Commit any changes to your local branch and then run `make depend.diff`

This will generate a diff file under `${ISTIO_OUT}/dep.diff`. This target, will re-run `dep ensure` and verify that there are no changes from your current branch HEAD. This file should be empty, since you just committed your local changes. The CI linter fails when this file is non-empty.

## Historical FAQ

We tried vendor as a submodule and while it has a lot of benefits it also proved too much complexity ([#4746](https://github.com/istio/istio/issues/4746)) so we switched to fully checked-in vendor.

Please ask/see @nmittler @rshriram @geeknoid for any question or issue with vendor

[Historical vendor experiment FAQ](https://github.com/istio/vendor-istio/blob/master/README.md)