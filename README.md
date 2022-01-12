# KEDA Helm Chart Dependency & CRDs
Reproduction for KEDA's Helm CRD issue when using dependencies, see [kedacore/charts #226](https://github.com/kedacore/charts/issues/226).

## Reproducing the issue

1. Check current CRDs, none should be there:
```shell
k get crd
```

2. Navigate to meta Helm chart folder
```shell
cd metachart
```

3. Update dependency of meta Helm chart
```shell
helm dependency update
```

4. Install Helm chart
```shell
helm install metachart .
```

5. KEDA should be installed with the new CRDs and our app
```shell
k get crd
```

However, step 5 will fail with error:
> Error: INSTALLATION FAILED: unable to build kubernetes objects from release manifest: unable to recognize "": no matches for kind "TriggerAuthentication" in version "keda.sh/v1alpha1"

## Notes

The `keda` chart in the repo is a copy of KEDA's official chart to play around with