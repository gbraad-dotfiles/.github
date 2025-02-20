Gerard Braad's dotfiles using `git`, `stow`, and `zsh`
======================================================

!["Prompt"](https://raw.githubusercontent.com/gbraad/assets/gh-pages/icons/prompt-icon-64.png)

These are my dotfiles that I use for dall my workstation and developement environments on a daily basis. I share it because I got frustrated about moving a tarball around (and being scared of losing it). This eventually happened when my notebook got stolen... so, this is not an ideal solution for you. Treat it as, "what you see is what it is"...

These dotfiles are based around a few helpers that deal with setting up development containers, network functions and connectivity to my homelab services

  - `dotfiles`  
    handles installation and update of my dotfiles
  - `devenv`  
    deals with [development environments](https://github.com/gbraad-devenv/)
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

## Containers and Virtual Machines

  * Open in [GitHub Codespaces](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=60443888&skip_quickstart=true)
  * `devenv dotfed env`, `dev dotfed [sys|shell]` for Fedora 41
  * `devenv dotdeb env`, `dev dotdeb [sys|shell]` for Debian Bookworm
  * Bootable Container (bootc) [disk images](https://github.com/gbraad-dotfiles/upstream/releases/latest)
    * `machine dotfiles [download|create|start|console]`

## Developer Environments

  * [CentOS](https://github.com/gbraad-devenv/centos), [golang](https://github.com/gbraad-devenv/centos-golang)
  * [Debian](https://github.com/gbraad-devenv/debian)
  * [Fedora](https://github.com/gbraad-devenv/fedora), [golang](https://github.com/gbraad-devenv/fedora-golang)
  * [UBI9](https://github.com/gbraad-devenv/UBI9), [golang](https://github.com/gbraad-devenv/ubi9-golang)
