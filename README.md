# fluxcd-playground
Explore GitOps with Flux CD. 

**_Note:_** This example works in collaboration with [fleet-infra repository](https://github.com/ks-yim/fleet-infra)

## Workflow with GitOps powered by Flux CD
1. DEV: push code changes to the app repository main branch
2. CI: test/build the commit
3. CI: build and push a docker container image tagged as ${APP_NAME}:${APP_VERSION}
4. CD: pull the latest image metadata from the app registry (Flux - image scanning)
5. CD: update the image tag in the app's `HelmRelease` manifest to the most recent version (Flux - cluster to Git reconciliation, Flux CD makes a commit to update the image tag)
6. CD: deploy helm release with the newest docker image to kubernetes cluster (Flux - Git to cluster reconciliation)

## Benefits
* **Pull-based deployment:**
  
  There used to be no clear boundary between CI and CD as many CI/CD pipelines have adopted a push-based deployment model.   
  Flux CD enables pull-based deployment by setting its kubernetes resources that watch Git repositories and reconcile any changes by incoming commits.
  
* **Deployments are VERSION CONTROLLED!**

  Now that you have a complete history of how your environment has changed over time, error recovery is as easy as issuing a revert PR! Flux CD, then, will take care of the whole recovery process!
  It will soon bring you back to the exactly same environment you used to have before the error.
