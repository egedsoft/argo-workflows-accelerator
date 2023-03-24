# Sample ML Pipeline using Argo Workflows

This is an accelerator that provides a template for deploying a simple analytics pipeline using Argo Workflows [Argo](https://argoproj.github.io/argo-workflows/).

* Install App Accelerator: (see https://docs.vmware.com/en/Tanzu-Application-Platform/1.0/tap/GUID-cert-mgr-contour-fcd-install-cert-mgr.html)
```
tanzu package available list accelerator.apps.tanzu.vmware.com --namespace tap-install
tanzu package install accelerator -p accelerator.apps.tanzu.vmware.com -v 1.0.1 -n tap-install -f resources/argo-workflows-accelerator.git.yaml
Verify that package is running: tanzu package installed get accelerator -n tap-install
Get the IP address for the App Accelerator API: kubectl get service -n accelerator-system
```

Publish Accelerators:
```
tanzu plugin install --local <path-to-tanzu-cli> all
tanzu acc create argo-pipelines-acc --git-repository https://github.com/agapebondservant/argo-workflows-accelerator.git --git-branch main
```

## Integrate with TAP

* Deploy the app (on TAP):
```
tanzu apps workload create argoworkflows-tap -f resources/tapworkloads/workload.yaml --yes
```

* Tail the logs of the main app:
```
tanzu apps workload tail argoworkflows-tap --since 64h
```

* Once deployment succeeds, get the URL for the main app:
```
tanzu apps workload get argoworkflows-tap     #should yield datahub.default.<your-domain>
```

* To delete the app:
```
tanzu apps workload delete argoworkflows-tap --yes
```

### (TODO: Pipeline documentation)