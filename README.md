# OSW Ansible

Summary of Ansible Playbooks for Open Semantic World (OSW) components.

<!-- vscode-markdown-toc -->
<!-- markdownlint-disable-next-line MD036 -->
**Table of Contents**

- [OSW Ansible](#osw-ansible)
  - [Prerequisites](#prerequisites)
  - [Configuration](#configuration)
  - [Usage](#usage)
  - [Authors](#authors)

## Prerequisites

- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

    <details>
    <summary>Details</summary>

    To install the required Ansible Galaxy Modules after Ansible installation, run the following commands:

    ```bash
    ansible-galaxy install geerlingguy.docker geerlingguy.pip kwoodson.yedit
    ```

    ```bash
    ansible-galaxy collection install community.docker
    ```

    </details>

## Configuration

1. Clone this repository:

    ```bash
    git clone https://github.com/OpenSemanticWorld/osw-ansible.git
    ```

2. To configure the OSW deployment, copy the `inventory.yml.example` file to `inventory.yml` in root directory and edit the variables.

    ```bash
    cd osw-ansible; cp -f inventory.yml.example inventory.yml
    ```

    You need to have the following information for a successful OSW deployment:

    - Public IP address of your VM or server
    - Username with `sudo` permissions and `SSH` access to the VM
    - Domain pointing to the VMs or servers public IP address

    For advanced modifications see [Ansible Host and Group Variables](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#group-variables).

## Usage

After configuration, you can run the Ansible Playbooks to deploy the OSW components. Either run the full OSW deployment or single specific components. Ensure you have the right permissions to run the Ansible Playbooks, your VM user must be in the `sudo` group and your deployment machine need to have `SSH` access to the VM.

1. To run the full OSW deployment, run [playbooks/main.yml](playbooks/main.yml) by the following command:

    ```bash
    ansible-playbook -i inventory.yml playbooks/main.yml
    ```

    This will run the following playbooks in the ordered sequence:

    1. [playbooks/install.yml](playbooks/install.yml)
    2. [playbooks/caddy.yml](playbooks/caddy.yml)
    3. [playbooks/osw.yml](playbooks/osw.yml)

    A reverse proxy will be installed and configured with `Caddy.` All OSW components will be installed and configured with Docker Compose. Ensure you have no other proxy, e.g., `nginx` running on the desired host.

2. OPTIONAL: Customization

    If you want to create your own ansible playbooks for a OSW deployment, you optionally can run the playbooks as single components. For example, to use the `install.yml` playbook for basic dependency installations, run the following command:

    ```bash
    ansible-playbook -i inventory.yml playbooks/install.yml
    ```

    This will run the `install.yml` playbook only. Be aware of the dependencies of the playbooks. For example, the `osw.yml` playbook depends on the `install.yml` playbook. You need to set up the right dependencies by yourself if you run the playbooks separately or applying your own modifications to match your needs.

## Authors

- [Simon Stier](https://github.com/simontaurus)
- [Andreas Räder](https://github.com/raederan)
