# register-deployment-action

Public GitHub Action that registers a deployment in [DeploymentViewer](https://github.com/sysadminspl/DeploymentViewer) via `POST /api/deployments`.

## Usage

```yaml
- uses: sysadminspl/register-deployment-action@v1
  with:
    api_url: https://deployments.sysadmins.pl
    api_key: ${{ secrets.DEPLOYMENT_VIEWER_API_KEY }}
    application_name: my-service
    environment_name: production
    version: ${{ github.ref_name }}
    commit_hash: ${{ github.sha }}
```

Pin production workflows to a major tag (`@v1`) or an exact release (`@v1.0.0`).

## Inputs

| Input | Required | Description |
|-------|----------|-------------|
| `api_url` | yes | Base URL of DeploymentViewer (no trailing slash) |
| `api_key` | yes | Workspace API key (Bearer) |
| `application_name` | yes | Application name in the workspace |
| `environment_name` | yes | Environment name in the workspace |
| `version` | yes | Version / image tag shown in the UI |
| `commit_hash` | no | Defaults to `github.sha` |
| `deployer_identity` | no | Defaults to `actor via workflow` |
| `deployed_at` | no | ISO-8601 UTC; defaults to now |

## Prerequisites

1. In DeploymentViewer: application + environment exist and are linked.
2. Create a workspace API key; store it as a GitHub Actions secret (e.g. `DEPLOYMENT_VIEWER_API_KEY`).
