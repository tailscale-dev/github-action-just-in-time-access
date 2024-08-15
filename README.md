# tailscale-just-in-time-github-action

[![status: experimental](https://img.shields.io/badge/status-experimental-blue)](https://tailscale.com/kb/1167/release-stages/#experimental)

A GitHub Action that demonstrates requesting and approving just-in-time access to devices on your tailnet. The action uses the [`workflow_dispatch` event](https://docs.github.com/en/actions/managing-workflow-runs-and-deployments/managing-workflow-runs/manually-running-a-workflow).

> :information_source: This experiment is in its early days and requires a feature flag be
> enabled on your account before you can make use of it. Please contact us if
> you'd like to test it - we're eager to hear your feedback.

## Setup

1. Copy [.github/workflows/tailscale-just-in-time.yaml.example](.github/workflows/tailscale-just-in-time.yaml.example) to your GitHub repo. Remove the `.example` suffix from the filename.
1. Customize the `inputs` in [.github/workflows/tailscale-just-in-time.yaml](.github/workflows/tailscale-just-in-time.yaml).
1. Commit your customized `tailscale-just-in-time.yaml` to your repo and push to GitHub.
1. [Create a **GitHub environment**](https://docs.github.com/en/actions/managing-workflow-runs-and-deployments/managing-deployments/managing-environments-for-deployment#creating-an-environment).
    1. Name the environment `tailscale-prod`, or a different value if you've changed it in the workflow file.
    1. Set [**Required reviewers**](https://docs.github.com/en/actions/managing-workflow-runs-and-deployments/managing-deployments/managing-environments-for-deployment#required-reviewers) to individuals or a team required to approve the request.
    1. [Create a Tailscale OAuth Client](https://tailscale.com/kb/1215/oauth-clients) and add the following **Environment secrets** to the GitHub environment:

        ```shell
        TAILSCALE_OAUTH_CLIENT_ID
        TAILSCALE_OAUTH_CLIENT_SECRET
        ```

1. [Manually run the workflow](https://docs.github.com/en/actions/managing-workflow-runs-and-deployments/managing-workflow-runs/manually-running-a-workflow).

## Local testing

Test locally using <https://github.com/nektos/act/>.

```shell
act workflow_dispatch \
    -s TAILSCALE_OAUTH_CLIENT_ID -s TAILSCALE_OAUTH_CLIENT_SECRET \
    --input source-device='cameron.tsjustworks.ts.net' \
    --input posture='custom:prodAcccess' \
    --input amount-of-time='12 hours' \
    --input reason='need to test something'
```
