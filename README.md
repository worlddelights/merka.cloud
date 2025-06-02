# merka.cloud

Integrated Hyperscaler-Agnostic Cloud

Visit [Merka.Cloud](https://merka.cloud) to learn more.

## Ab-Initio (Installation/Setup)

The best way to get started currently is by using [NixOS](https://nixos.org/)

On Windows - make sure WSL2 is enabled and follow the instructions here: https://github.com/nix-community/NixOS-WSL 

On MacOS - Recommendation is to use OrbStack to add Virtual Machine with NixOS on it: https://docs.orbstack.dev/machines/distros

1. Place setup/wsl/configuration.nix file provided into your /etc/nixos/configuration.nix directory
1. Rebuild the NixOS with new configuration: <code>sudo nixos-rebuild switch</code>
1. Kubernetes K3s configuration file can be found at /etc/rancher/k3s/k3s.yaml , and should be placed on your client machine/host under ~/.kube/config to gain access to newly created cluster


## Setting up additional nodes

Merka supports large variety of nodes and endpoints, and all bring something unique to expand the ecosystem sometimes beyond your expectations.

## Experimental Steps

1. Enable persistent storage on your K3s cluster using 
1. Install Portainer using Helm on your K3s cluster: https://github.com/portainer/k8s/blob/master/charts/portainer/README.md
1. Install Rancher using Helm on your K3s cluster:
1. Connect Neon DB helm chart repo: helm repo add neondatabase https://neondatabase.github.io/helm-charts
1. Install Neon DB various charts: helm search repo neondatabase


### CloudNativePG

1. We will need to install CloudNativePG operator first, using helm: 
helm repo add cnpg https://cloudnative-pg.github.io/charts
helm upgrade --install cnpg \
  --namespace cnpg-system \
  --create-namespace \
  cnpg/cloudnative-pg

1. Next lets create dedicated Namespace for CloudNativePG databases and make it default by running: kubectl create namespace cnpg && kubectl config set-context --current --namespace=cnpg
1. Finally deploy /setup/cloudnative-pg/cloudnative-pg.yaml to your K3s cluster using: kubectl apply -f cloudnative-pg.yaml


### Portainer

helm upgrade --install --create-namespace -n portainer portainer portainer/portainer \
    --set tls.force=false \
    --set image.tag=sts

helm ls --all-namespaces

### NeonDB

1. Install another Nix WSL or VM, based on setup/neon-db/configuration.nix file
1. Login to NeonDB VM and execute the following:

#### Note: The path to the neon sources can not contain a space.

git clone --recursive https://github.com/neondatabase/neon.git
cd neon

# The preferred and default is to make a debug build. This will create a demonstrably slower build than a release build.
# For a release build, use "BUILD_TYPE=release make -j`nproc` -s"
# Remove -s for the verbose build log

make -j`nproc` -s