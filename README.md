# auto-go-ansible

## 📋 Overview

An Ansible automation toolkit for quickly setting up a production-ready Ubuntu host with Docker, deployment users, and secure SSH access.

## 🛠 Features

- **System Setup** – Install common system tools, Docker Engine, and Docker Compose Plugin (`host_base.yml`)
- **Application Deployment** – Creates secure deployment user, generates Docker configs, and preserves environment files for CI/CD (`deployer.yml`)
- **User & SSH Configuration** – Add authorized keys, enable passwordless sudo for SSH users (`user_ssh.yml`)

## 🛠️ Prerequisites

### Core Tools

Ensure you have the following installed:

| Tool    | Installation Command (example)                                        | Verified Version |
| ------- | --------------------------------------------------------------------- | ---------------- |
| Ansible | `pipx install ansible` _(or)_ `python3 -m pip install --user ansible` | `2.18.8`         |

### Environment Configuration

Create a `.env` file in the project root:

```env
ANSIBLE_SSH_USER=user
ANSIBLE_SSH_KEY=~/.ssh/user_key
ANSIBLE_VAULT_PASSWORD=my_super_secret
```

> **Tip:** Use different `.env` files for dev/staging/prod and load them with:
>
> ```bash
> source .env.prod
> ```

## 🔒 Encrypting Secrets

Encrypt a value for Vault:

```bash
ansible-vault encrypt_string 'your_secret_value' \
  --name 'variable_name' \
  --vault-password-file=<(echo "$ANSIBLE_VAULT_PASSWORD")
```

## 🚀 Running Playbooks

Run a playbook with Vault:

```bash
ansible-playbook playbook.yml \
  --vault-password-file=<(echo "$ANSIBLE_VAULT_PASSWORD")
```

## 📂 Playbook Reference

| Playbook        | Purpose                                                    |
| --------------- | ---------------------------------------------------------- |
| `host_base.yml` | Install system tools, Docker Engine, Docker Compose Plugin |
| `deployer.yml`  | Create deployment user for CI/CD app deployments           |
| `user_ssh.yml`  | Configure SSH access and passwordless sudo                 |

## 📌 Notes

- Designed for **Ubuntu hosts**.
- Requires **SSH access** to the target system.
- Uses **Ansible Vault** for secret management — never commit plain text secrets.
