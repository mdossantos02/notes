
# 🛠️ Ansible Cheat Sheet

## 📦 Installation
```bash
# On Ubuntu/Debian
sudo apt update && sudo apt install ansible -y

# On macOS
brew install ansible

# On RHEL/CentOS
sudo yum install epel-release -y
sudo yum install ansible -y
```

## 📁 Directory Structure (Example)
```
my-ansible-project/
├── inventory          # Inventory file
├── playbook.yml       # Main playbook
├── roles/             # Roles (organized tasks)
│   └── webserver/
│       ├── tasks/
│       └── templates/
└── group_vars/
```

## 📘 Basic Inventory File (`inventory`)
```ini
[web]
web1.example.com
web2.example.com

[db]
db1.example.com ansible_user=admin ansible_port=2222
```

## ▶️ First Playbook Example (`playbook.yml`)
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

## 🚀 Running a Playbook
```bash
ansible-playbook -i inventory playbook.yml
```

## 🧪 Ad-hoc Commands
```bash
# Ping all hosts
ansible all -i inventory -m ping

# Run a command on all web servers
ansible web -i inventory -a "uptime"

# Install a package
ansible all -i inventory -b -m apt -a "name=git state=present"
```

## 🛠️ Common Modules

| Module      | Purpose                            | Example                                          |
|-------------|------------------------------------|--------------------------------------------------|
| `apt`       | Manage packages (Debian)           | `apt: name=nginx state=present`                 |
| `yum`       | Manage packages (RHEL)             | `yum: name=httpd state=absent`                  |
| `copy`      | Copy file to remote                 | `copy: src=hello.txt dest=/tmp/hello.txt`       |
| `template`  | Jinja2 templates                    | `template: src=app.conf.j2 dest=/etc/app.conf`  |
| `service`   | Manage services                     | `service: name=apache2 state=restarted`         |
| `user`      | Manage users                        | `user: name=john state=present groups=sudo`     |
| `file`      | Set file properties                 | `file: path=/tmp/test state=touch`              |
| `lineinfile`| Ensure line in file                 | `lineinfile: path=/etc/hosts line="127.0.0.1 localhost"` |

## 🔐 Variables
```yaml
vars:
  username: mark
tasks:
  - name: Add user
    user:
      name: "{{ username }}"
```

## 📄 Templates with Jinja2 (`template.j2`)
```
Hello {{ username }}!
Your hostname is {{ ansible_hostname }}
```

## 📚 Facts Gathering
```yaml
tasks:
  - name: Show hostname
    debug:
      var: ansible_hostname
```

## 🧱 Role Usage in Playbook
```yaml
- hosts: all
  roles:
    - webserver
```

## 🔄 Loops
```yaml
- name: Install packages
  apt:
    name: "{{ item }}"
    state: present
  loop:
    - git
    - curl
    - htop
```

## 🔍 Conditionals
```yaml
- name: Only run when OS is Ubuntu
  apt:
    name: apache2
    state: present
  when: ansible_distribution == 'Ubuntu'
```
