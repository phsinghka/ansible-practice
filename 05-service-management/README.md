# Ansible Playbook for Web Service Management

This repository contains an Ansible playbook for managing the Nginx web service on remote servers. It includes tasks for installing, starting, stopping, and restarting Nginx, as well as updating its configuration with minimal downtime.

## Features

- **Install Nginx:** Installs Nginx on remote hosts.
- **Service Control:** Allows starting, stopping, and restarting of the Nginx service.
- **Configuration Management:** Updates the Nginx configuration and restarts the service if the configuration is changed.
- **Handlers:** Uses handlers to ensure that service restarts only occur when necessary.

## Requirements

- Ansible 2.9 or higher.
- Target servers must be running a Debian-based operating system.

## Getting Started

### Setup Inventory

Modify the `hosts` file in the root of this project to include your servers under the `[webservers]` group.


### Run the Playbook

To run the playbook, use the following command:

```bash
ansible-playbook -i hosts manage_web_service.yml
ansible-playbook -i hosts manage_web_service.yml -e "ansible_playbook_run=start"

