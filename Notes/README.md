
# Ansible for Beginners: A Quick Guide

## What is Ansible?
Ansible is an open-source automation tool that helps in automating tasks like configuration management, application deployment, and task execution across multiple servers. It uses simple YAML files (called playbooks) to define tasks.

### Key Concepts:
- **Playbook**: A YAML file that defines the tasks to be executed.
- **Inventory**: A list of managed nodes.
- **Modules**: Pre-built tasks that Ansible executes on the target system.
- **Task**: A unit of work that Ansible performs on the remote system.
- **Play**: A mapping of hosts to tasks that are executed in sequence.
- **Handler**: A special type of task that is triggered by notifications from other tasks.

---

## Ansible Installation:
### On Ubuntu/Debian:
```bash
sudo apt update
sudo apt install ansible
```

### On RedHat/CentOS:
```bash
sudo yum install ansible
```

---

## Ansible Playbook Basics
Playbooks are written in YAML format and consist of plays. Each play maps hosts to tasks that will be executed.

```yaml
---
- name: Install nginx on web servers
  hosts: webservers
  become: yes
  tasks:
    - name: Ensure nginx is installed
      apt:
        name: nginx
        state: present
```

---

## Common Ansible Playbook Examples in DevOps

### 1. Installing a Package on a Remote Host
This playbook installs the `nginx` package on a remote server.

```yaml
---
- name: Install Nginx
  hosts: all
  become: yes
  tasks:
    - name: Install nginx package
      apt:
        name: nginx
        state: present
```

### 2. Starting a Service
This playbook ensures that the `nginx` service is running.

```yaml
---
- name: Start nginx service
  hosts: all
  become: yes
  tasks:
    - name: Ensure nginx is started
      service:
        name: nginx
        state: started
        enabled: yes
```

### 3. Copying Files to Remote Servers
This playbook copies a file from the local machine to the remote server.

```yaml
---
- name: Copy a configuration file to remote server
  hosts: all
  become: yes
  tasks:
    - name: Copy nginx config file
      copy:
        src: /path/to/local/nginx.conf
        dest: /etc/nginx/nginx.conf
        mode: '0644'
```

### 4. Restarting a Service Based on Changes
This playbook restarts the `nginx` service only if the configuration file is changed.

```yaml
---
- name: Restart nginx if configuration changes
  hosts: all
  become: yes
  tasks:
    - name: Copy nginx config file
      copy:
        src: /path/to/local/nginx.conf
        dest: /etc/nginx/nginx.conf
        mode: '0644'
      notify:
        - Restart nginx

  handlers:
    - name: Restart nginx
      service:
        name: nginx
        state: restarted
```

### 5. Running a Shell Command on Remote Hosts
This playbook runs a custom shell command on remote servers.

```yaml
---
- name: Run a shell command on remote server
  hosts: all
  become: yes
  tasks:
    - name: Check the disk usage
      shell: df -h
      register: result

    - name: Display the result
      debug:
        var: result.stdout
```

---

## Common Ansible Commands
- **Check the syntax of a playbook**:
  ```bash
  ansible-playbook --syntax-check playbook.yml
  ```

- **Run a playbook**:
  ```bash
  ansible-playbook playbook.yml
  ```

- **Ping all hosts in inventory**:
  ```bash
  ansible all -m ping
  ```

- **List all hosts**:
  ```bash
  ansible all --list-hosts
  ```

---

## Conclusion
Ansible simplifies the process of automating server configurations, deployments, and more. By mastering playbooks and modules, you can automate various aspects of DevOps operations, reducing manual work and improving consistency.
