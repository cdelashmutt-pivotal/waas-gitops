# Tanzu Platform for K8s EMEA GitOps Install

## Prerequisites

- Install the Carvel tools [kapp](https://carvel.dev/kapp/docs/latest/install/) and [ytt](https://carvel.dev/ytt/docs/latest/install/). If you choose the script install, all of them will be installed together.

## Each cluster

### Prerequisites

#### Install kapp-controller
```
kapp deploy -a kapp-controller -f https://github.com/carvel-dev/kapp-controller/releases/latest/download/release.yml
```
#### Install secretgen-controller
```
kapp deploy -a secret-gen-controller -f https://github.com/carvel-dev/secretgen-controller/releases/latest/download/release.yml
```

### Deploy cluster sync app
```
ytt -f sync-app --data-value git.url=$(git remote get-url origin) | kapp deploy -a sync -y -f -
```