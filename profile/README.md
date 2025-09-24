Gerard Braad's dotfiles using `git`, `stow`, and `zsh`
======================================================

!["Prompt"](https://raw.githubusercontent.com/gbraad/assets/gh-pages/icons/prompt-icon-64.png)

These are my dotfiles that I use for all my workstation and developement environments on a daily basis. I share it because I got frustrated about moving a tarball around (and being scared of losing it). This eventually happened when my notebook got stolen. It is 'very personal' (my way of working), so, this is not an ideal solution for you. Treat it as, "what you see is what it is"...

These dotfiles are based around a few helpers that deal with setting up development containers, network functions and connectivity to my homelab services

  - `dotfiles`  
    handles installation and update of my dotfiles
  - `devenv`, `devbox`  
    deals with running [instant development environments](https://github.com/gbraad-devenv/) as containers with [Podman](https://podman.io)
  - `machine`  
    create VMs using packer and bootc image-based deployments of devenv, [homelab](https://github.com/gbraad-homelab), [apps](https://github.com/gbraad-apps) and others, utilizing [`macadam`](https://github.com/crc-org/macadam/) and [`machinefile`](https://github.com/gbraad-redhat/machinefile)
  - `proxy`  
    sets environment to use a proxy to access services
  - `davfs`  
    connects to remote WebDAV endspoints for file sharing
  - `tailscale`  
    aliases and commands for use with my tailnet
  - `secrets`  
    simple encrypt and decrypt for tokens and TOTP
  - `app`  
    installing and running according to [application definitions](https://github.com/gbraad-dotfiles/applications/) as Actionfiles
  - `action` / `run`  
    automation framework using Actionfiles, a markdown-based file for script execution
  - `screen`  
    smart(er) handling of local and remote screen session with tmux
  - ...


> [!NOTE]
> Do not use this directly, but take parts and learn from it.

---

## Related side-projects

### [Actionfile](https://dotfiles.gbraad.nl/actionfile)

A Markdown-based configuration file that describes a set of actions, scripts, or tasks for use in automation workflows


### [Machinefile](https://dotfiles.gbraad.nl/machinefile)

A simple executor that allows you to run `Dockerfile`/`Containerfile` commands directly on a local or remote host

---

## One-line install
```bash
curl -fsSL https://dotfiles.gbraad.nl/install.sh | sh
```

> [!NOTE]
> This [`script`](https://github.com/gbraad-dotfiles/gbraad-dotfiles.github.io/blob/main/install.sh) uses the stable [`downstream`](https://github.com/gbraad/dotfiles-stable) to install.

---

## Extensions for VS Code

### [Dotfiles checker](https://github.com/gbraad-vscode/dotfiles-checker/) - [Marketplace](https://marketplace.visualstudio.com/items?itemName=gbraad.dotfiles-checker), [Open VSX Registry](https://open-vsx.org/extension/gbraad/dotfiles-checker)

An extension that checks for and install my personal dotfiles


### [Dotfiles tools](https://github.com/gbraad-vscode/dotfiles-tools/) - [Marketplace](https://marketplace.visualstudio.com/items?itemName=gbraad.dotfiles-tools), [Open VSX Registry](https://open-vsx.org/extension/gbraad/dotfiles-tools)

An extension that automates `devenv.zsh` and `machine.zsh`.


### Dot environment (`.dotfiles` without install)

`settings.json`
```json
{
    "terminal.integrated.defaultProfile.linux": "dot",
    "terminal.integrated.profiles.linux": {
        "dot": {
            // absolute path is necessary (no variables)
            "path": "/home/.../.dotfiles/bash/.local/bin/dot"
        },
        "dotscreen": {
            "path": "/home/.../.dotfiles/bash/.local/bin/dotscreen"
        }
    }
}
```

`tasks.json`
```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "dot",
            "type": "shell",
            "problemMatcher": [],
            "command": "~/.dotfiles/bash/.local/bin/dot"
            //"command": "zsh"    // when dot is used as default terminal
        },
        {
            "label": "dotscreen",
            "type": "shell",
            "problemMatcher": [],
            "command": "~/.dotfiles/bash/.local/bin/dotscreen"
            //"command": "screen"
        }
    ]
}
```

> [!NOTE]
> Tasks are run in the `default` termina. If this is set to `dot`, any function that has been defined, can be run directly.

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

These are container images with the dotfiles and dependencies installed, able to run as a system container.

  * `devenv dotfedora env`, `dev dotfedora [system|shell|exec]` for Fedora
  * `devenv dotdebian env`, `dev dotdebian [system|shell|exec]` for Debian
  * ... `dotalma` for AlmaLinux
  * ... `dotcentos` for CentOS Stream
  * ... `dotubi9` for RHEL UBI9
  * ... `dotubuntu` for Ubuntu
  * ... `dotalpine` for Alpine
  

## Image-based Virtual Machines

The `machine.zsh`-helper assists in the process to set up and run image-based virtual machines.
This is called a Bootable Container (bootc). Disk images are stored as OCI artifacts.

```zsh
$ machine dotfiles [download|create|start|console]
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

## Instant Developer Environments

  * [Fedora](https://github.com/gbraad-devenv/fedora), with [golang](https://github.com/gbraad-devenv/fedora-golang)
  * [Debian](https://github.com/gbraad-devenv/debian), with [golang](https://github.com/gbraad-devenv/debian-golang)
  * [AlmaLinux](https://github.com/gbraad-devenv/almalinux), with [golang](https://github.com/gbraad-devenv/almalinux-golang)
  * [CentOS](https://github.com/gbraad-devenv/centos), with [golang](https://github.com/gbraad-devenv/centos-golang)
  * [UBI9](https://github.com/gbraad-devenv/UBI9), with [golang](https://github.com/gbraad-devenv/ubi9-golang)
  * [Ubuntu](https://github.com/gbraad-devenv/ubuntu), with [golang](https://github.com/gbraad-devenv/ubuntu-golang)


---

## Usage in Jupyter [notebooks](https://github.com/gbraad-dotfiles/notebooks)

```python
%load_ext dotfiles
```

```zsh
%%dotscript
country
```

    > The Netherlands

```
%%dotscript
proxy ndisguise
country
```

    > Germany

```zsh
out=%dotini dotfiles file
%code out ini
```

```zsh
out=%dot ps ax
%code out
```

```zsh
%apps list services
%apps pinger service install
%apps pinger service status
```


> [!NOTE]
> To use the extension, `stow ipython` needs to be run. More information can be found in the dedicated
> [gbraad-dotfiles/notebooks](https://github.com/gbraad-dotfiles/notebooks) repository with examples.

---

## GitHub Actions 

### GitHub Action: [`install-action`](https://github.com/gbraad-dotfiles/install-action/)

```yaml
      - name: Install dotfiles action
        uses: gbraad-dotfiles/install-action@main
```


### GitHub Action: [`dotfiles-action`](https://github.com/gbraad-dotfiles/dotfiles-action/)

```yaml
      - name: Run dotfiles command
        uses: gbraad-dotfiles/dotfiles-action@main
        with:
          action: update
```


### GitHub Action: [`devenv-action`](https://github.com/gbraad-dotfiles/devenv-action/)

```yaml
      - name: Run devenv command
        uses: gbraad-dotfiles/devenv-action@main
        with:
          prefix: dotfedora
          command: exec  #  [create/system/noinit|start|apps|...]
          args: cat /etc/os-release
```


### GitHub Action: [`devbox-action`](https://github.com/gbraad-dotfiles/devbox-action/)

```yaml
      - name: Run devbox command
        uses: gbraad-dotfiles/devbox-action@main
        with:
          prefix: fedora
          command: exec  #  [create|start|apps|...]
          args: cat /etc/os-release
```


### GitHub Action: [`machine-action`](https://github.com/gbraad-dotfiles/machine-action/)

```yaml
      - name: Run machine command
        uses: gbraad-dotfiles/machine-action@main
        with:
          prefix: dotfedora
          command: download   #  [create|start|stop|...]
```


### GitHub Action: [`app-action`](https://github.com/gbraad-dotfiles/app-action/)

```yaml
      - name: Run app install
        uses: gbraad-dotfiles/app-action@main
        with:
          appname: vivaldi
          action: install
```


### GitHub Action: [`dot-action`](https://github.com/gbraad-dotfiles/dot-action/)

```yaml
      - name: Requiremnent for dot
        run: |
          sudo apt update
          sudo apt install -y zsh

      - name: Run dot command - devenv dotfedora exec cat /etc/os-release
        uses: gbraad-dotfiles/dot-action@main
        with:
          run: |
            devenv dotfedora exec cat /etc/os-release
```

> [!NOTE]
> This runs the specified commands without the need to 'install' the dotfiles.
> It is required for the runner to have `zsh` installed.


---

## Ansible

### Ansible role: [`gbraad.dotfiles`](https://github.com/gbraad-dotfiles/ansible-role-dotfiles/) and [playbooks](https://github.com/gbraad-dotfiles/playbooks)

```yaml
    - name: Install dotfiles
      hosts: localhost
      roles:
        - role: gbraad.dotfiles
          vars:
            user: gbraad
```

### Ansible role: [`gbraad.dotfiles-devenv`](https://github.com/gbraad-dotfiles/ansible-role-dotfiles-devenv/)

```yaml
    - name: Run devenv command
      hosts: localhost
      roles:
        - role: gbraad.dotfiles-devenv
          vars:
            prefix: gofedora
            command: start
```

### Ansible role: [`gbraad.dotfiles-apps`](https://github.com/gbraad-dotfiles/ansible-role-dotfiles-apps/)

```yaml
    - name: Run app installs
      hosts: localhost
      roles:
        - role: gbraad.dotfiles-apps
          vars:
            appname: vivaldi
            action: install
```

### Example/test: [⚙️](https://github.com/gbraad-dotfiles/ansible-dotfiles-example/actions)
 [![ansible-dotfiles-test](https://github.com/gbraad-dotfiles/ansible-dotfiles-example/actions/workflows/build-process.yml/badge.svg)](https://github.com/gbraad-dotfiles/ansible-dotfiles-example/actions/workflows/build-process.yml)

---

## Build status of dotfiles Containers [⚙️](https://github.com/gbraad-dotfiles/upstream/actions) [🛠️](https://app.blacksmith.sh) [🛠️](https://app.warpbuild.com)

### Fedora
 [![build container - fedora](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-fedora.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-fedora.yml)  
 [![Build and Push Fedora bootc diskimage](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-diskimage-fedora-bootc.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-diskimage-fedora-bootc.yml)

### CentOS
 [![build container - centos](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-centos.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-centos.yml)  
 [![Build and Push CentOS bootc diskimage](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-diskimage-centos-bootc.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-diskimage-centos-bootc.yml)

### AlmaLinux
 [![build container - almalinux](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-almalinux.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-almalinux.yml)  
 [![Build and Push AlmaLinux bootc diskimage](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-diskimage-almalinux-bootc.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-diskimage-almalinux-bootc.yml)

### Others
 [![build container - UBI9](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-ubi9.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-ubi9.yml)  
 [![build container - Alpine](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-alpine.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-alpine.yml)  
 [![build container - debian](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-debian.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-debian.yml)  
 [![build container - ubuntu](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-ubuntu.yml/badge.svg)](https://github.com/gbraad-dotfiles/upstream/actions/workflows/build-container-ubuntu.yml)


---

## Other build status


### Container Registry Cleanup
 [![Container Registry Cleanup](https://github.com/gbraad-dotfiles/.github/actions/workflows/cleanup.yml/badge.svg)](https://github.com/gbraad-dotfiles/.github/actions/workflows/cleanup.yml)

### Application defintions
 [![Application installs](https://github.com/gbraad-dotfiles/applications/actions/workflows/build-process.yml/badge.svg)](https://github.com/gbraad-dotfiles/applications/actions/workflows/build-process.yml)

---

## Downstream

  - [`dotfiles-stable`](https://github.com/gbraad/dotfiles-stable) - used in [`one-line install`](https://github.com/gbraad-dotfiles#one-line-install)
  - [`gbraad-devenv`](https://github.com/gbraad-devenv/dotfiles)
  - [`gbraad-redhat/dotfiles`](https://github.com/gbraad-redhat/dotfiles)

---

## Presentations
  - [`.dotfiles` - Where `${HOME}` is best](https://docs.gbraad.nl/dotfiles-presentation/)


---

Runners kindly provided by [Blacksmith](https://docs.blacksmith.sh/introduction/why-blacksmith) and [WarpBuild](https://docs.warpbuild.com).
