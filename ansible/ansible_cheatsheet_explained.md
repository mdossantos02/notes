
# 🛠️ Ansible Cheat Sheet Explained

This document explains each section of the Ansible cheat sheet in detail, helping you understand not just the syntax, but what it actually does.

---

## 📦 Installation

Installs Ansible using the system's package manager:

- **Ubuntu/Debian**:
  ```bash
  sudo apt update && sudo apt install ansible -y
  ```
- **macOS**:
  ```bash
  brew install ansible
  ```
- **RHEL/CentOS**:
  ```bash
  sudo yum install epel-release -y
  sudo yum install ansible -y
  ```

---

## 📁 Directory Structure

A sample layout of a typical Ansible project for organizing playbooks, inventory, and roles.

```
my-ansible-project/
├── inventory          # Hosts to manage
├── playbook.yml       # Main automation logic
├── roles/             # Modular task collections
└── group_vars/        # Group-specific variables
```

---

## 📘 Inventory File

Defines groups of hosts and specific connection parameters:

```ini
[web]
web1.example.com
web2.example.com

[db]
db1.example.com ansible_user=admin ansible_port=2222
```

---

## ▶️ Playbook Example

A YAML script that defines automation tasks for a group of hosts:

```yaml
- name: Install Apache Web Server
  hosts: web
  become: yes
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present
```

- `become: yes` runs the tasks as sudo.
- `tasks` lists what Ansible should do.

---

## 🚀 Running a Playbook

Executes the defined tasks in your playbook:

```bash
ansible-playbook -i inventory playbook.yml
```

---

## 🧪 Ad-hoc Commands

Quick, one-off commands to run tasks on remote machines:

- Ping all hosts:
  ```bash
  ansible all -i inventory -m ping
  ```
- Install a package:
  ```bash
  ansible all -i inventory -b -m apt -a "name=git state=present"
  ```

---

## 🛠️ Common Modules

| Module        | Purpose                          |
|---------------|----------------------------------|
| `apt`, `yum`  | Install/remove packages          |
| `copy`        | Copy files to remote machines    |
| `template`    | Generate files from Jinja2       |
| `service`     | Start/stop/restart services      |
| `user`        | Manage users                     |
| `file`        | Handle file/directory attributes |
| `lineinfile`  | Ensure specific lines exist      |

---

## 🔐 Variables

Define dynamic values to reuse across tasks:
```yaml
vars:
  username: mark
```

---

## 📄 Templates

Jinja2 templating to generate config files:
```jinja
Hello {{ username }}
```

---

## 📚 Facts Gathering

Gathers useful system info automatically:
```yaml
debug:
  var: ansible_hostname
```

---

## 🧱 Roles

Reusable sets of tasks for better organization:
```yaml
roles:
  - webserver
```

---

## 🔄 Loops

Repeat a task for multiple values:
```yaml
loop:
  - git
  - curl
```

---

## 🔍 Conditionals

Run tasks only when certain conditions are met:
```yaml
when: ansible_distribution == 'Ubuntu'
```

---

This document should give you both a reference and the understanding needed to use Ansible effectively.
