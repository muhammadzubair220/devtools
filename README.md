# muhammadzubair220.devtools

[![Ansible Galaxy](https://img.shields.io/badge/Ansible%20Galaxy-muhammadzubair220.devtools-blue)](https://galaxy.ansible.com/ui/standalone/roles/muhammadzubair220/devtools/)
[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)

An Ansible role that installs **Ansible**, **Terraform**, and **Docker** on multiple Linux distributions in a single run.

---

## Supported Platforms

| Distribution   | Version             |
|----------------|---------------------|
| Ubuntu         | 20.04, 22.04, 24.04 |
| Debian         | 11, 12              |
| Pop!_OS        | 22.04               |
| Linux Mint     | 21.x                |
| Rocky Linux    | 8, 9                |

---

## Requirements

- Ansible >= 2.15
- `become: true` on the managed node
- Internet access to reach package repositories

---

## Installation

```bash
ansible-galaxy role install muhammadzubair220.devtools
```

---

## Role Variables

### Tool selection

| Variable | Default | Description |
|----------|---------|-------------|
| `devtools_install_ansible` | `true` | Install Ansible |
| `devtools_install_terraform` | `true` | Install Terraform |
| `devtools_install_docker` | `true` | Install Docker |

### Ansible

| Variable | Default | Description |
|----------|---------|-------------|
| `devtools_ansible_install_method` | `pip` | `pip` or `package` |
| `devtools_ansible_version` | `latest` | Version string or `latest` |

### Terraform

| Variable | Default | Description |
|----------|---------|-------------|
| `devtools_terraform_version` | `latest` | Version string or `latest` |

### Docker

| Variable | Default | Description |
|----------|---------|-------------|
| `devtools_docker_compose_plugin` | `true` | Install Docker Compose plugin |
| `devtools_docker_users` | `[]` | Users to add to `docker` group |

---

## Example Playbook

### Install all three tools (default)

```yaml
---
- name: Install DevTools
  hosts: all
  become: true
  roles:
    - role: muhammadzubair220.devtools
```

### Install only Docker, add ubuntu user to docker group

```yaml
---
- name: Install Docker only
  hosts: all
  become: true
  roles:
    - role: muhammadzubair220.devtools
      vars:
        devtools_install_ansible: false
        devtools_install_terraform: false
        devtools_install_docker: true
        devtools_docker_users:
          - ubuntu
```

### Install specific versions

```yaml
---
- name: Install pinned versions
  hosts: all
  become: true
  roles:
    - role: muhammadzubair220.devtools
      vars:
        devtools_ansible_version: "2.17.0"
        devtools_terraform_version: "1.8.0"
```

---

## Tags

Run only specific tools using tags:

```bash
# Install only Docker
ansible-playbook site.yml --tags docker

# Install only Terraform
ansible-playbook site.yml --tags terraform

# Install only Ansible
ansible-playbook site.yml --tags ansible
```

---

## License

GPL-2.0-or-later

---

## Author

**Muhammad Zubair**
- GitHub: [@muhammadzubair220](https://github.com/muhammadzubair220)
- Ansible Galaxy: [muhammadzubair220.devtools](https://galaxy.ansible.com/ui/standalone/roles/muhammadzubair220/devtools/)
