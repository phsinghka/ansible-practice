# Project 4: File Management

## Overview
This project demonstrates managing files and directories on remote servers using Ansible. The tasks include creating directories, copying files, generating files from templates, deleting files, and setting file permissions.

## How to Run
1. Ensure Ansible is installed and configured on your machine.
2. Clone this repository and navigate to the `project4-file-management` directory.
3. Update the `inventory` file to include your remote hosts.
4. Run the playbook using the command:

## Components
- `playbook.yml`: Ansible playbook containing all tasks.
- `templates/example.j2`: Jinja2 template for generating files.
- `files/example.txt`: Example file to be copied to remote hosts.
- `inventory`: Lists the hosts the playbook will run against.

