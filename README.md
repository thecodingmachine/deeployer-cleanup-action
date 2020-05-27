# Deeployer cleanup action

This Github action can be used to delete a Kubernetes action.

It works similarly to the [thecodingmachine/deeployer](https://github.com/thecodingmachine/deeployer/#usage-in-github-actions) action 
except it will delete a whole Kubernetes namespace instead of deploying an application.

```deploy_workflow.yaml
name: Clean Kubernetes namespace

on:
  - delete

jobs:
  clean:
    runs-on: ubuntu-latest

    steps:
      - name: Delete namespace
        uses: thecodingmachine/deeployer@master
        env:
          KUBE_CONFIG_FILE: ${{ secrets.KUBE_CONFIG_FILE }}
        with:
          namespace: target-namespace
```

You will need to put the content of your Kubernetes configuration file in the `KUBE_CONFIG_FILE` secret on Github.

### Cleanup in a Google cloud Kubernetes cluster

If you are connecting to a Google Cloud cluster, instead of passing a `KUBE_CONFIG_FILE`, you will need to pass
this set of environment variables:

- `GCLOUD_SERVICE_KEY`
- `GCLOUD_PROJECT`
- `GCLOUD_ZONE`
- `GKE_CLUSTER`
