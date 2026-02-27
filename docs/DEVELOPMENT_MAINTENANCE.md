# Upgrading the Renovate Package

In most cases renovate will be ran against this repository and flagging new images that are available in Iron Bank for use in upgrading the chart. The image availability is the dependency for upgrading the chart.

When new images are identified as available for this chart - we will want to look to the [upstream chart](https://github.com/renovatebot/helm-charts) and identify the tag release for the chart that contains the image versions we want to upgrade to.

This package uses the passthrough pattern, so overrides needed for the upstream renovate chart will be under the `upstream:` key in [values.yaml](../chart/values.yaml#L37)

## Testing new Renovate Version

Identify a repository with a valid `renovate.json` to execute renovate against. Search for a repo with an active renovate MR that has not been merged yet, and save this information to be used in later steps.

It is best to test renovate with Gitlab enabled, so you can observe Renovate working and making changes against a repository.

1. Deploy Bigbang with Gitlab enabled using [renovate-dev-override.yaml](./renovate-dev-override.yaml) (you will edit this file again later). Refer to the [quick-start guide](https://repo1.dso.mil/big-bang/bigbang/-/blob/master/docs/installation/environments/quick-start.md) for instructions. Be sure to reference the [Gitlab Development and Maintenance guide](https://repo1.dso.mil/big-bang/product/packages/gitlab/-/blob/main/docs/DEVELOPMENT_MAINTENANCE.md) for instructions on deploying gitlab

1. After Gitlab is deployed, you will want to run the [renovate-dev.sh](https://repo1.dso.mil/big-bang/pipeline-templates/renovate-runner/-/blob/main/dev/renovate-dev.sh) script from the [renovate-runner](https://repo1.dso.mil/big-bang/pipeline-templates/renovate-runner) repository. This script will configure gitlab to run renovate, create necessary PAT tokens, and emulate the repository structure similar to Repo1. For further instructions, refer to the [Testing and Development](https://repo1.dso.mil/big-bang/pipeline-templates/renovate-runner/-/blob/main/dev/TESTING_DEVELOPMENT.md) guide. Select the following options when prompted:
  
- "Do you want to import packages for testing?" -> Yes
- "Do you want to import all packages?" -> Just some
- Select your chosen package(s) using by moving the cursor next to the package and pressing tab, then hit enter.
- "Do you want to delete all existing renovate/ironbank branches?" -> Yes
- "Do you want to revert all packages to previous renovate tag?" -> No (sometimes this reverts to extremely old versions if Yes is chosen)
- "Do you want to trigger the renovate runner pipeline?" -> No

The script output will also include a line that says `Renovate Bot Token created successfully:`. You will need to copy this PAT token and update [renovate-dev-override.yaml](./renovate-dev-override.yaml#L32) and set this as the value for `token:` in the `config:` section. Be sure to update your credentials for registry1 in subsequent lines so Renovate is able to query the repository for updated images.

1. Run your `helm upgrade` command again to apply the new changes.

1. Once the deployment is successful, trigger a cronjob to run Renovate

```bash
kubectl create job --from=cronjob/renovate-upstream renovate-upstream-manual -n renovate
```

Once the job is successful, log in to Gitlab and search for the newly created MRs. Additionally, you can view the pod logs for the created pod in the `renovate` namespace to see what activity was performed.

## Targeting a fork (old method)

For testing purposes, it may be preferable to target a fork of a repository to avoid opening MRs and issues against the original repository. To do this, you first need to request the ability to create personal projects on repo1. Consult the anchors and government leads to request this access.

Once granted, select a repo that you would like to test that already has a valid `renovate.json` file. Click the "fork" button in the top right of the repo UI and fork it into your personal namespace. Note the address, it should look something like `https://repo1.dso.mil/user.name/project_name`.

On the fork's page, click the "Settings" tab and select "Access Tokens" from the left hand menu.Click the "New Access Token" button and select the "api" scope. Choose a reasonable expiration date and click "Generate token".

With this adresss, we can now configure the renovate chart to target this fork:

```yaml
config: |
  {
    "repositories": ["user.name/project_name"],
    "platform": 'gitlab',
    "endpoint": 'https://repo1.dso.mil/api/v4',
    "token": "<the token you generated>",
    "autodiscover": false,
    "hostRules": [{
      "hostType": "docker",
      "matchHost": "registry1.dso.mil",
      "username": "<registry1 user>",
      "password": "<registry1 secret key>"
    }]
  }
```

## Files That Require Integration Testing

Currently, this package does not undergo any sort of integration testing. There is an [open issue in Renovate](https://repo1.dso.mil/big-bang/product/maintained/renovate/-/issues/57) to assess the need for expanding test coverage. This section should be updated as that ticket progresses.
