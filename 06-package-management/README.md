# Project 6: Package Management with Ansible

## Key Learnings

### 1. **Inventory Management**
Defining an inventory file for different OS families:

```yaml
all:
  hosts:
    webserver1:
      ansible_host: 192.168.1.10
      ansible_user: ubuntu
    dbserver1:
      ansible_host: 192.168.1.11
      ansible_user: centos

  children:
    debian_hosts:
      hosts:
        webserver1:
    redhat_hosts:
      hosts:
        dbserver1:
```

### 2. **Roles for Package Management**
Using roles to manage package installations and updates.

- **Install Task:**
  ```yaml
  - name: Install packages on Debian-based systems
    apt:
      name: "{{ default_packages.debian }}"
      state: present
      update_cache: true
    when: ansible_os_family == 'Debian'

  - name: Install packages on RedHat-based systems
    yum:
      name: "{{ default_packages.redhat }}"
      state: present
    when: ansible_os_family == 'RedHat'
  ```

### 3. **Using Conditionals**
Conditionally running tasks based on the OS family:

```yaml
- name: Install packages
  apt:
    name: "{{ packages }}"
  when: ansible_os_family == 'Debian'
```

### 4. **Updating and Removing Packages**
- **Update Task:**
  ```yaml
  - name: Update packages on Debian-based systems
    apt:
      upgrade: dist
    when: ansible_os_family == 'Debian'

  - name: Update packages on RedHat-based systems
    yum:
      name: "*"
      state: latest
    when: ansible_os_family == 'RedHat'
  ```

- **Remove Task:**
  ```yaml
  - name: Remove packages
    apt:
      name: "{{ remove_packages }}"
      state: absent
    when: ansible_os_family == 'Debian'
  ```

### 5. **Handlers for Service Restart**
Restarting services after package installations or updates:

```yaml
- name: Restart Apache on Debian-based systems
  service:
    name: apache2
    state: restarted
  when: ansible_os_family == 'Debian'

- name: Restart Apache on RedHat-based systems
  service:
    name: httpd
    state: restarted
  when: ansible_os_family == 'RedHat'
```