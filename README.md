# OSW Ansible

Summary of Ansible Playbooks for Open Semantic World (OSW) components.

<!-- vscode-markdown-toc -->
<!-- markdownlint-disable-next-line MD036 -->
**Table of Contents**

- [OSW Ansible](#osw-ansible)
  - [Prerequisites](#prerequisites)
  - [Configuration](#configuration)
  - [Usage](#usage)
  - [Testing](#testing)

## Prerequisites

- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

    <details>
    <summary>Ansible Galaxy Modules</summary>

    To install the required Ansible Galaxy Modules after Ansible installation, run the following commands:

    ```bash
    ansible-galaxy install geerlingguy.docker geerlingguy.pip kwoodson.yedit
    ```

    ```bash
    ansible-galaxy collection install community.docker
    ```

    </details>

## Configuration

[Ansible Host and Group Variables](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#group-variables)

## Usage

<!-- Run the following command to install the base OSW components: -->

```bash
ansible-playbook -i "<VM_PUBLIC_IP>" base.playb.yml -e "vm_user=<VM_USER_NAME>"
```

## Testing

Check inventory:

```bash
ansible-inventory -i inventory.yml --list
```

Ping virtual machine:

```bash
ansible virtualmachines -m ping -i inventory.yml -u ubuntu
```

Run playbook:

```bash
ansible-playbook -i inventory.yml playbooks/install.yml
```
