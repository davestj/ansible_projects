# Global  Ansible Projects

## Overview

This project aims to automate various tasks across our infrastructure, providing a consistent and efficient way to manage configurations, deployments, and maintenance.

## Features

- **Infrastructure as Code (IaC)**: Define infrastructure in code using Ansible playbooks, roles, and inventories.
- **Modular Architecture**: Organize tasks into reusable roles for better maintainability and scalability.
- **Inventory Management**: Dynamically manage hosts and groups through inventory files or external inventory plugins.
- **Task Automation**: Automate repetitive tasks such as provisioning servers, configuring applications, and deploying updates.
- **Idempotent Operations**: Ensure consistent state across infrastructure by running tasks multiple times without side effects.
- **Security and Compliance**: Enforce security policies, compliance standards, and secrets management using Ansible Vault.
- **Artifact Generation**: Terraform tfvars management

## Getting Started

### Prerequisites

- Install [Ansible](https://www.ansible.com/) on the control node.
- Have SSH access to target hosts with proper authentication and permissions.
- Define inventory hosts and groups in the inventory file(s).

### Installation

No installation steps required for this project. Ansible is the only dependency, which should be installed on the control node.

### Usage

1. Clone this repository to your local machine:

   ```bash
   git clone git@github.com:davestj/ansible_projects.git
   ```

2. Navigate to the project directory:

   ```bash
   cd ansible_projects
   ```

3. Edit the inventory file(s) to define your infrastructure hosts and groups once you have ssh-copy-id:
   ```bash
   vim inventory/hosts.yml
   ```
   3.A You can also take this time to edit the ansible.cfg to fit your stack environment

4. Create or modify Ansible playbooks and roles to automate tasks according to your requirements.

5. Run Ansible playbooks to execute tasks across your infrastructure:

   ```bash
   ansible-playbook -i inventory/hosts.yml playbooks/WHATEVER_playbook.yml
   ```

6. Monitor playbook execution and review output for any errors or warnings.

### Directory Structure

- `inventory/`: Contains inventory files to define hosts and groups.
- `playbooks/`: Stores Ansible playbooks for executing tasks.
- `roles/`: Organizes tasks into reusable roles for better organization and maintenance.

## License

This project is licensed under the [MIT License](LICENSE).

