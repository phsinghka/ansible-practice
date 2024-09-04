# Ansible Web Server Deployment

## Project Overview
This project demonstrates how to deploy an Nginx web server using Ansible. The playbook installs Nginx, deploys a basic configuration, and serves a dynamic HTML page that displays the server's hostname. This project highlights the use of Ansible roles, templates, variables, and handlers.

### Features
- Installation and configuration of Nginx on a remote server.
- Dynamic HTML page generation using Ansible templates.
- Service management and automated restarts using handlers.
- Use of variables for flexibility and reusability.
- Fully idempotent playbook for consistent results on reruns.

## Project Structure
```
07-web-server-deployment/
│
├── ansible.cfg           # Ansible configuration file
├── hosts                 # Inventory file with target server information
├── playbook.yml          # Main Ansible playbook
└── roles/
    └── webserver/        # Ansible role for deploying the web server
        ├── tasks/
        │   └── main.yml              # Task file for installing and configuring Nginx
        ├── templates/
        │   └── nginx.conf.j2          # Nginx configuration template
        │   └── index.html.j2          # HTML template served by Nginx
        ├── vars/
        │   └── main.yml              # Variables used in the role
        ├── handlers/
        │   └── main.yml              # Handlers to restart Nginx on changes
```

## Prerequisites
- Ansible installed on your local machine.
- A remote server (e.g., AWS EC2 instance) with SSH access.
- Ansible configured to access the remote server (update the `hosts` file with the correct server information).

## How to Run the Playbook

1. **Clone this repository** to your local machine:
   ```bash
   git clone https://github.com/phsinghka/ansible-practice.git
   cd 07-web-server-deployment
   ```

2. **Update the Inventory (`hosts`) File:**
   Modify the `hosts` file to include your server's IP address and SSH user.

3. **Run the Ansible Playbook:**
   Execute the playbook to deploy the web server:
   ```bash
   ansible-playbook -i hosts playbook.yml
   ```

4. **Access the Web Server:**
   After the playbook finishes, you can access the web server by entering your server’s IP address in a web browser:
   ```
   http://<your_server_ip>
   ```

   The web page will display: "Welcome to Nginx on `<hostname>`", where `<hostname>` is dynamically rendered by Ansible.

## Things to Learn from This Project

### 1. **Ansible Roles:**
   - This project organizes tasks into roles, making the playbook more modular and reusable.
   - Roles help separate different components (e.g., installing packages, configuring services).

### 2. **Using Variables:**
   - Variables are defined in `vars/main.yml` and used throughout the role to configure the web server dynamically.
   - They provide flexibility for easily changing configurations, such as the port, document root, or index file.

### 3. **Jinja2 Templating:**
   - Jinja2 templates are used for the Nginx configuration file (`nginx.conf.j2`) and the HTML file (`index.html.j2`).
   - Templates enable dynamic content generation based on variables (e.g., displaying the hostname of the server).

### 4. **Handlers:**
   - Handlers are used to restart Nginx whenever a configuration change is detected, ensuring the web server is running with the latest settings.

### 5. **Idempotency:**
   - Ansible playbooks are idempotent, meaning they can be run multiple times without making unnecessary changes.
   - This ensures consistency and prevents configuration drift on subsequent runs.

### 6. **Service Management:**
   - The playbook ensures that the Nginx service is installed, started, and enabled to start automatically on system boot.

### 7. **File Deployment:**
   - The `template` module is used to deploy files with Jinja2 variables, allowing for dynamic content creation during playbook execution.

## Customization

You can easily customize this playbook by:
- Changing the variables in `vars/main.yml` to use a different document root, port, or server.
- Modifying the `nginx.conf.j2` template to customize the Nginx configuration for your needs.
- Expanding the playbook to include SSL setup, additional virtual hosts, or application deployments.

## Conclusion
This project provides a foundation for deploying web servers using Ansible. It demonstrates key DevOps skills such as automation, configuration management, and infrastructure as code. By mastering these concepts, you can extend this project to more complex environments and services.