## Working with CircleCI

We use CircleCI as one of the systems for continuous integration. Any PR
will have to pass all CircleCI tests (in addition to Prow tests) before
being ready to merge. When you fork Istio repository, you will
automatically inherit the CircleCI testing environment as well, allowing
you to fully reproduce our testing infrastructure. If you have
already signed up for CircleCI, you can test your code changes in your fork
against the full suite of tests that we run for every PR.

### CircleCI set up

To use CircleCI, you must sign up for the free service and authorize
CircleCI to access your Github account. Follow the steps outlined here to
[setup CircleCI](https://circleci.com/docs/2.0/first-steps/).

### Re-run failing tests

Occasionally, a test on CircleCI may fail spuriously for reasons unrelated
to your PR - such as inability to start the minikube cluster. If you
suspect that the failure was a flake, you can rebuild the failing test
using the CircleCI user interface using the steps below:

1. Click on the failing test in the PR

[[images/circleci-failing-pr.png]]

2. Navigate one level up to the suite of tests associated with the PR

[[images/circleci-navigate-to-pr.png]]

3. Click rebuild for the failing tests.

[[images/circleci-rebuild-test.png]]

## Re-run entire workflow

If you wish to re-run the entire CircleCI workflow (all tests)

1. click on the workflow called "all"

[[images/circleci-locate-workflow.png]]

2. Click "rerun" to restart all tests.

[[images/circleci-rerun-entire-workflow.png]]

### SSH into container to debug

If you wish to investigate the contents of a pod or debug a failing test
within CircleCI, you can ssh into the container/VM running the test. Follow
the steps below:

1. Add your public keys to your Github profile by following the steps
   outlined
   [here](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/).

1. Click on the failing test in the PR

[[images/circleci-failing-pr.png]]

2. Click on "Rerun job with SSH"

[[images/circleci-rerun-job-with-ssh.png]]

3. CircleCI will restart the job with SSH enabled. The SSH details will be
   visible as the first step in the job.

[[images/circleci-ssh-details.png]]
   
4. SSH to the host denoted by CircleCI using your public key.

[[images/circleci-ssh-into-container.png]]

