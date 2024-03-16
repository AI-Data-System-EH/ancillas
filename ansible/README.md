# Ansible

Managing remote servers with [Ansible](https://www.ansible.com/).

<br/>

---

<br/>

## Before You Start

- [Ansible Documentation](https://docs.ansible.com/ansible/latest/index.html)
- [Ansible Best Practices](https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html)
- [Ansible Galaxy](https://galaxy.ansible.com/)

<br/>

_When running ansible commands,_<br/>
_Make sure that your current working directory is `ansible`._

> ansible will look for the `ansible.cfg` file in the current working directory.

```bash
$ cd <repository-root>/ansible

# using git repository root
$ cd $(git rev-parse --show-toplevel)/ansible
```

## Installation

See the [Prerequisites](#prerequisites) section for installation.

<br/>

---

<br/>

## Table of Contents

- [Before You Start](#before-you-start)
- [Installation](#installation)
- [Configured Roles and Playbooks](#configured-roles-and-playbooks)
  - [Overview](#overview)
  - [Role: `apt`](#role-apt)
  - [Role: `poetry`](#role-poetry)
  - [Role: `oh-my-zsh`](#role-oh-my-zsh)
  - [Role: `docker`](#role-docker)
  - [Role: `python`](#role-python)
  - [Role: `nvm`](#role-nvm)
  - [Role: `tailscale`](#role-tailscale)
- [Prerequisites](#prerequisites)
- [Usage](#usage)

<br/>

---

<br/>

## Configured Roles and Playbooks

### Overview

| Role                           | Description                               | Playbook(s) | Status             |
| ------------------------------ | ----------------------------------------- | ----------- | ------------------ |
| [`apt`](#role-apt)             | APT package management.                   | `update`    | :white_check_mark: |
| [`poetry`](#role-poetry)       | Python package management with Poetry.    | `poetry`    | :construction:     |
| [`oh-my-zsh`](#role-oh-my-zsh) | Zsh configuration with Oh My Zsh.         | `oh-my-zsh` | :construction:     |
| [`docker`](#role-docker)       | Docker installation and configuration.    | `docker`    | :thinking:         |
| [`python`](#role-python)       | Python installation and configuration.    | `python`    | :thinking:         |
| [`nvm`](#role-nvm)             | Node Version Manager installation.        | `nvm`       | :thinking:         |
| [`tailscale`](#role-tailscale) | Tailscale installation and configuration. | `tailscale` | :thinking:         |

### Role: `apt`

Runs APT package management tasks and updates the system.

> Included in playbook: [`update.yaml`](playbook/update.yaml)
>
> Tasks: [`tasks/main.yaml`](roles/apt/tasks/main.yaml)
>
> Variables: [`defaults/main.yaml`](roles/apt/defaults/main.yaml)

| Task Tag         | Sub-task Tag      | Description                    | Variables |
| ---------------- | ----------------- | ------------------------------ | --------- |
| `system-inspect` | `ansible-inspect` | Inspect the system.            |           |
| `system-update`  |                   | Update the system.             |           |
|                  | `apt-upgrade`     | Upgrade the APT packages.      |           |
|                  | `dist-upgrade`    | Upgrade the distribution.      | `bool`    |
|                  | `apt-clean`       | Clean up the APT cache.        |           |
| `system-reboot`  |                   | Reboot the system if required. | `bool`    |
|                  | `reboot-required` | Check if reboot is required.   | `path`    |
|                  | `reboot`          | Reboot the system.             |           |

### Role: `poetry`

Runs Python package management tasks with Poetry.

> Included in playbook: [`poetry.yaml`](playbook/poetry.yaml)
>
> Tasks: [`tasks/main.yaml`](roles/poetry/tasks/main.yaml)
>
> Variables: [`defaults/main.yaml`](roles/poetry/defaults/main.yaml)

| Task Tag         | Sub-task Tag | Description     | Variables |
| ---------------- | ------------ | --------------- | --------- |
| `poetry-install` |              | Install Poetry. |           |

### Role: `oh-my-zsh`

Runs Zsh configuration tasks with Oh My Zsh.

> Included in playbook: [`oh-my-zsh.yaml`](playbook/oh-my-zsh.yaml)
>
> Tasks: [`tasks/main.yaml`](roles/oh-my-zsh/tasks/main.yaml)
>
> Variables: [`defaults/main.yaml`](roles/oh-my-zsh/defaults/main.yaml)

| Task Tag    | Sub-task Tag | Description | Variables |
| ----------- | ------------ | ----------- | --------- |
| `oh-my-zsh` |              |             |           |

### Role: `docker`

Runs Docker installation and configuration tasks.

> Included in playbook: [`docker.yaml`](playbook/docker.yaml)
>
> Tasks: [`tasks/main.yaml`](roles/docker/tasks/main.yml)
>
> Variables: [`defaults/main.yaml`](roles/docker/defaults/main.yaml)

| Task Tag         | Sub-task Tag | Description | Variables |
| ---------------- | ------------ | ----------- | --------- |
| `docker-install` |              |             |           |

### Role: `python`

Runs Python installation and configuration tasks.

> Included in playbook: [`python.yaml`](playbook/python.yaml)
>
> Tasks: [`tasks/main.yaml`](roles/python/tasks/main.yml)
>
> Variables: [`defaults/main.yaml`](roles/python/defaults/main.yaml)

| Task Tag         | Sub-task Tag | Description | Variables |
| ---------------- | ------------ | ----------- | --------- |
| `python-install` |              |             |           |

### Role: `nvm`

Runs Node Version Manager installation tasks.

> Included in playbook: [`nvm.yaml`](playbook/nvm.yaml)
>
> Tasks: [`tasks/main.yaml`](roles/nvm/tasks/main.yml)
>
> Variables: [`defaults/main.yaml`](roles/nvm/defaults/main.yaml)

| Task Tag      | Sub-task Tag | Description | Variables |
| ------------- | ------------ | ----------- | --------- |
| `nvm-install` |              |             |           |

### Role: `tailscale`

Runs Tailscale installation and configuration tasks.

> Included in playbook: [`tailscale.yaml`](playbook/tailscale.yaml)
>
> Tasks: [`tasks/main.yaml`](roles/tailscale/tasks/main.yml)
>
> Variables: [`defaults/main.yaml`](roles/tailscale/defaults/main.yaml)

| Task Tag            | Sub-task Tag | Description | Variables |
| ------------------- | ------------ | ----------- | --------- |
| `tailscale-install` |              |             |           |

<br/>

---

<br/>

## Prerequisites

- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) installed on your local machine.

  `pipx`

  ```bash
  $ pipx install --include-deps ansible
  ```

  `Homebrew`

  ```bash
  $ brew install ansible
  ```

  `APT`

  ```bash
  $ sudo apt update
  $ sudo apt install ansible
  ```

- [Python](https://www.python.org/downloads/) installed on both local machine and remote servers.

  - Recommended to use the **default Python** that comes with OS. (remote servers)

    > :information_source: **Issue**
    >
    > You may need to install `python3-apt` package on your remote servers.

## Usage

1. Clone this repository.

   > :information_source: **Note**
   >
   > `git clone` will create a new directory with the repository name in the <u>_current working directory_</u>.

   ```bash
   $ git clone "https://github.com/AI-Data-system-EH/ancillas.git"
   ```

2. Change directory to the `ansible` in cloned repository.

   ```bash
   $ cd $(git rev-parse --show-toplevel)/ansible
   ```

3. Create the inventory file for your remote servers.

   - Edit this file: [inventory/hosts.yaml](inventory/hosts.yaml)

     > :information_source: **Note**
     >
     > ansible will look for the `/etc/ansible/hosts` file by default.
     >
     > In `ansible.cfg`, the `inventory` option can be set to the path of the inventory file.
     >
     > ```ini
     > [defaults]
     > inventory = inventory/hosts.yaml
     > ```

     - If not exists, create the `inventory` directory and the `hosts.yaml` file.

       ```bash
       $ mkdir -p inventory
       $ touch inventory/hosts.yaml
       ```

   - If sensitive data is required, use `ansible-vault` to encrypt the file.

     > :warning: **Important**
     >
     > _Do not add the `secret` or `encrypted` files to the repository._
     >
     > _Add the secret files to `.gitignore`._

     - (<u>Case1</u>) Encrypt the whole `host` file.

       ```bash
       # encrypt an existing unencrypted file
       $ ansible-vault encrypt inventory/hosts.yaml
       ```

     - (<u>Case2</u>) Create `secret` files separately.

       1. Create `host_vars` directory to store variables for each host.

          ```bash
          $ mkdir -p inventory/host_vars
          ```

       2. Create a `secret` file for each host.

          ```bash
          # (case b-1) respective file for each host
          $ ansible-vault create inventory/host_vars/your_hostname.yaml

          # (case b-2) respective folder for each host and include files
          $ ansible-vault create inventory/host_vars/your_hostname/secret.yaml
          ```

   - To input the password interactively, add `--ask-vault-pass` or `-J` option to the `ansible-playbook` command.

     ```bash
     $ ansible-playbook --ask-vault-pass -i inventory path/to/playbook.yaml
     ```

     - Or, add the `vault_password_file` option to the `ansible.cfg` file.

       > :warning: **Important**
       >
       > <i>It should be <u>not-encrypted plaintext file</u> and <span style="color:red"><u>**should not be added to the repository.**</u></span></i>

       ```bash
       $ echo "your-vault-password" > path/to/vault-password-file
       # Do not encrypt the vault-password-file.
       ```

       ```ini
       [defaults]
       vault_password_file = path/to/vault-password-file
       ```

4. Run the playbook.

   ```bash
   # (Case1) to run with the default host file (configured in `ansible.cfg`)
   $ ansible-playbook playbook/play.yaml

   # (Case2) to run with a specific host file
   $ ansible-playbook -i inventory/hosts.yaml path/to/playbook.yaml

   # (Case3) to run with all host files in the `inventory` directory
   $ ansible-playbook -i inventory path/to/playbook.yaml
   ```

   - (Option) `--check` to perform a dry-run.

     ```bash
     $ ansible-playbook playbook/play.yaml --check
     ```

   - (Option) `--limit` to run on specific hosts or groups.

     ```bash
     $ ansible-playbook playbook/play.yaml --limit "host1,host2,group1"
     ```

   - (Option) `--tags` to run specific tasks.

     ```bash
     $ ansible-playbook playbook/play.yaml --tags "tag1,tag2"
     ```

     - If you want to run `all` tasks including `never` tasks, use the `never` tag.

       > :information_source: **Note**
       >
       > <i>`never` tag is skipped by default to prevent accidental execution.</i>

       ```bash
       $ ansible-playbook playbook/play.yaml --tags "all,never"
       ```

     - To list all tags in the playbook, use the `--list-tags` option.

       ```bash
       $ ansible-playbook playbook/play.yaml --list-tags
       ```

     - To skip specific tasks, use the `--skip-tags` option.

       ```bash
       $ ansible-playbook playbook/play.yaml --skip-tags "tag1,tag2"
       ```
