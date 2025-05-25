# merka.cloud
Integrated Cloud-Agnostic Cloud


## Ab-Initio (Installation/Setup)

The best way to get started currently is by using [NixOS](https://nixos.org/)

On Windows - make sure WSL2 is enabled and follow the instructions here: https://github.com/nix-community/NixOS-WSL 

On MacOS - Recommendation is to use OrbStack to add Virtual Machine with NixOS on it: https://docs.orbstack.dev/machines/distros

1. Place setup/wsl/configuration.nix file provided into your /etc/nixos/configuration.nix directory

2. Rebuild the NixOS with new configuration: <code>sudo nixos-rebuild switch</code>


## Setting up additional nodes

Merka supports large variety of nodes and endpoints, and all bring something unique to expand the ecosystem sometimes beyond your expectations.

