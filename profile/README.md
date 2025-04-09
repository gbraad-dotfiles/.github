Gerard Braad's dotfiles using `git`, `stow`, and `zsh`
======================================================

!["Prompt"](https://raw.githubusercontent.com/gbraad/assets/gh-pages/icons/prompt-icon-64.png)

These are my dotfiles that I use for all my workstation and developement environments on a daily basis. I share it because I got frustrated about moving a tarball around (and being scared of losing it). This eventually happened when my notebook got stolen... so, this is not an ideal solution for you. Treat it as, "what you see is what it is"...

These dotfiles are based around a few helpers that deal with setting up development containers, network functions and connectivity to my homelab services

  - `dotfiles`  
    handles installation and update of my dotfiles
  - `devenv`  
    deals with [instant development environments](https://github.com/gbraad-devenv/)
  - `machine`  
    create VMs using bootc image-based deployments of devenv, [homelab](https://github.com/gbraad-homelab), [apps](https://github.com/gbraad-apps) and others
  - `proxy`  
    sets environment to use a proxy to access services
  - `davfs`  
    connects to remote WebDAV endspoints for file sharing
  - `tailscale`  
    aliases and commands for use with my tailnet
  - `secrets`  
    simple encrypt and decrypt for tokens and TOTP
  - ...


> [!NOTE]
> Do not use this directly, but take parts and learn from it.


---

## Extensions for VS Code

### [Dotfiles checker](https://github.com/gbraad-vscode/dotfiles-checker/) - [Marketplace](https://marketplace.visualstudio.com/items?itemName=gbraad.dotfiles-checker), [Open VSX Registry](https://open-vsx.org/extension/gbraad/dotfiles-checker)

An extension that checks for and install my personal dotfiles


### [Dotfiles tools](https://github.com/gbraad-vscode/dotfiles-tools/) - [Marketplace](https://marketplace.visualstudio.com/items?itemName=gbraad.dotfiles-tools), [Open VSX Registry](https://open-vsx.org/extension/gbraad/dotfiles-tools)

An extension that automates `devenv.zsh` and `machine.zsh`.


---

## Feature for devcontainers

Install my personal dotfiles as a feature during the devcontainer build process.

```json
    "features": {
        "ghcr.io/gbraad-dotfiles/devcontainer-features/dotfiles:latest": {}
    }
```

---

## Containers

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=60443888&skip_quickstart=true)

  * `devenv dotfedora env`, `dev dotfedora [sys|shell]` for Fedora 41
  * `devenv dotdebian env`, `dev dotdebian [sys|shell]` for Debian Bookworm
  * `dotalma`
  * `dotubuntu`
  * `dotcentos`
  * `dotubi9`
  * `dotalpine`
  

## Image-based Virtual Machines

The `machine.zsh`-helper aids in the process to set up and run image-based virtual machines.
This is called a Bootable Container (bootc) and here you find the [disk images](https://github.com/gbraad-dotfiles/upstream/releases/latest).

```zsh
$ machine dotfiles [download|create|start|console]`
```

### Manual process using `virt-install`

You can otherwise also run

```bash
$ wget https://github.com/gbraad-dotfiles/upstream/releases/download/250223/almalinux-disk.qcow2 \
     -O base.qcow2
$ sudo virt-install \
    --name base --os-variant fedora-eln \
    --cpu host --vcpus 4 --memory 4096 \
    --import --disk ./base.qcow2,format=qcow2
```

## Developer Environments

  * [AlmaLinux](https://github.com/gbraad-devenv/almalinux), with [golang](https://github.com/gbraad-devenv/almalinux-golang)
  * [CentOS](https://github.com/gbraad-devenv/centos), with [golang](https://github.com/gbraad-devenv/centos-golang)
  * [Debian](https://github.com/gbraad-devenv/debian), with [golang](https://github.com/gbraad-devenv/debian-golang)
  * [Fedora](https://github.com/gbraad-devenv/fedora), with [golang](https://github.com/gbraad-devenv/fedora-golang)
  * [UBI9](https://github.com/gbraad-devenv/UBI9), with [golang](https://github.com/gbraad-devenv/ubi9-golang)
  * [Ubuntu](https://github.com/gbraad-devenv/ubuntu), with [golang](https://github.com/gbraad-devenv/ubuntu-golang)


---

## Build status of dotfiles Containers [⚙️](https://github.com/gbraad-dotfiles/upstream/actions)

### AlmaLinux
[![build container - almalinux](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-almalinux.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-almalinux.yml)
[![build container - almalinux-bootc](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-almalinux-bootc.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-almalinux-bootc.yml)

### Fedora
[![build container - fedora](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-fedora.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-fedora.yml)
[![build container - fedora-bootc](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-fedora-bootc.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-fedora-bootc.yml)

### CentOS
[![build container - centos](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-centos.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-centos.yml)
[![build container - centos-bootc](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-centos-bootc.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-centos-bootc.yml)

### Others
[![build container - debian](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-debian.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-debian.yml)
[![build container - ubuntu](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-ubuntu.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-ubuntu.yml)
[![build container - UBI9](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-ubi9.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-ubi9.yml)
[![build container - Alpine](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-alpine.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-alpine.yml)


---

## Other build status

### Ansible role [`gbraad.dotfiles`](https://github.com/gbraad-dotfiles/ansible-role-dotfiles/) and example/test [⚙️](https://github.com/gbraad-dotfiles/ansible-dotfiles-example/actions)
[![ansible-dotfiles-test](https://github.com/gbraad-dotfiles/ansible-dotfiles-example/actions/workflows/build-process.yml/badge.svg)](https://github.com/gbraad-dotfiles/ansible-dotfiles-example/actions/workflows/build-process.yml)

### Container Registry Cleanup
[![Container Registry Cleanup](https://github.com/gbraad-dotfiles/.github/actions/workflows/cleanup.yml/badge.svg)](https://github.com/gbraad-dotfiles/.github/actions/workflows/cleanup.yml)


---

## Presentations
  - [`.dotfiles` - Where `${HOME}` is best](https://docs.gbraad.nl/dotfiles-presentation/)
