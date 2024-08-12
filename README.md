# tailscale-just-in-time-github-action

[![status: experimental](https://img.shields.io/badge/status-experimental-blue)](https://tailscale.com/kb/1167/release-stages/#experimental)

## Setup

Requires the following environment variables:

```shell
TAILSCALE_OAUTH_CLIENT_ID
TAILSCALE_OAUTH_CLIENT_SECRET
```

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
