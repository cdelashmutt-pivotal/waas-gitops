# Tanzu Platform for K8s EMEA GitOps Install

## Prerequisites

- Install the Carvel tools [kapp](https://carvel.dev/kapp/docs/latest/install/) and [ytt](https://carvel.dev/ytt/docs/latest/install/). If you choose the script install, all of them will be installed together.
- Download the contents of this repo, and `git init` to create a new repository.
- `git add -A && git commit -m "Initial commit"` 
- Push your repo to a server that can be accessed by your cluster

## For each cluster you want to manage via the repo
### Create cluster config directory
- `cd clusters`
- `mkdir $(k get configmap -n vmware-system-tmc stack-config -o jsonpath='{.data.cluster_name}')`
- Add your manifests to the directory
- Add, Commit and push your manifests to the server

### Deploy cluster sync app
```
ytt -f sync-app --data-value git.url=$(git remote get-url origin) | kapp deploy -a sync -y -f -
```