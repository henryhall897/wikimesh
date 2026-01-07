---
title: Ansible User Bootstrap
description: How to Set up an Ansible user on a New Machine for SSH connection
published: true
date: 2026-01-07T18:04:33.824Z
tags: infrastructure, public, selfhosted, home, automation, ansible, tutorials, ansible-user
editor: markdown
dateCreated: 2026-01-06T17:28:56.851Z
---

# Bootstrapping a New Ansible User

## Purpose

Before Ansible can manage a host, it must be able to log in non-interactively using SSH and escalate privileges safely. This article documents the standard bootstrap procedure for creating the permanent ansible user on a new host and installing the controller’s SSH key (ansible-controller.pub). Once this process is complete, all future automation must use the ansible user.

## When This Is Required

You must bootstrap a host if any of the following are true:

* The host has never been managed by Ansible
* The ansible user does not exist
* SSH key authentication is not configured
* The host was reinstalled or reset
* This process is one-time per host.

## Assumptions

* You have console or SSH access using an existing user (e.g. dev, ubuntu, pi)
* SSH is reachable on the host
* You have the controller’s public key: `ansible-controller.pub`
* The host uses sudo for privilege escalation

## Target State (End Goal)

After bootstrapping, the host must satisfy all of the following:

* A user named ansible exists
* ansible has a home directory
* ansible can authenticate via SSH key
* The key installed matches ansible-controller.pub
* ansible can run sudo without a password
* Password-based SSH is no longer required for automation

## Manual Bootstrap (Reference Procedure)

This section documents the explicit system-level steps.
In practice, this is automated via an Ansible bootstrap role.

### 1. Create the ansible User

`sudo useradd -m -s /bin/bash ansible`

### 2. Set Password: 

`sudo usermod ansible -p <password>`

### 3. Unlock Account:

`sudo passwd -u ansible`

### 4. Verify

`id ansible`

### 5. Create the SSH Directory

```bash
sudo mkdir -p /home/ansible/.ssh
sudo chmod 700 /home/ansible/.ssh
sudo chown ansible:ansible /home/ansible/.ssh
```

### 6. Install the Controller SSH Key

Copy the contents of `ansible-controller.pub` into:

```bash
sudo tee /home/ansible/.ssh/authorized_keys <<EOF
<PASTE_KEY_HERE>
EOF
```

**Set permissions**:

```bash
sudo chmod 600 /home/ansible/.ssh/authorized_keys
sudo chown ansible:ansible /home/ansible/.ssh/authorized_keys
```

**Important**

`authorized_keys` must contain the full **public key**, not a **filename**.

### 7. Grant Passwordless Sudo

#### Create a sudoers file:

```bash
sudo tee /etc/sudoers.d/ansible <<EOF
ansible ALL=(ALL) NOPASSWD: ALL
EOF
```

#### Set correct permissions:

```bash
sudo chmod 440 /etc/sudoers.d/ansible
```

#### Validate:

```bash
sudo visudo -cf /etc/sudoers.d/ansible
```

### 8. Allow Ansible through Firewall (UFW)

```bash
sudo ufw allow in from <ANSIBLE_MACHINE_IP> to any port 22 proto tcp comment 'SSH from Ansible controller'
sudo ufw reload
```

### 9. Update /etc/ssh/sshd_config

```bash 
sudo nano /etc/ssh/sshd_config
```

Ensure values are set:

```bash
PubkeyAuthentication yes
AuthorizedKeysFile      .ssh/authorized_keys .ssh/authorized_keys2
PasswordAuthentication no
UsePAM no
ChallengeResponseAuthentication no
AllowUsers <your-account> ansible
```

## Post-Bootstrap

### Verify connectivity:

On Machine Expecting SSH connection, log SSH attempts for better debugging. 

```bash
sudo journalctl -u ssh -f
```

On Ansible Machine, run the ping.yaml playbook to test connection. 

```bash
ansible-playbook playbooks/ping.yaml -v 
```

All hosts should return:

```bash
TASK [Ansible ping] **************************************************************
ok: [computer1] => {"changed": false, "ping": "pong"}
ok: [computer2] => {"changed": false, "ping": "pong"}
ok: [computer3] => {"changed": false, "ping": "pong"}
ok: [computer4] => {"changed": false, "ping": "pong"}
ok: [computer5] => {"changed": false, "ping": "pong"}
```

## Security Notes

* The ansible user is intended only for **automation**
* **Human logins** should use **separate** accounts
* SSH keys must be rotated if the controller is compromised
* Password authentication can be disabled after bootstrap
* Firewall rules should restrict SSH to trusted subnets

## Common Failure Modes

* SSH Timeout
* SSH daemon not running
* Firewall blocking port `22`
* Host offline or unreachable
* Permission Denied (publickey)
* Incorrect key installed
* Wrong user
* Incorrect file permissions
* sudo Requires Password
* `/etc/sudoers.d/ansible` missing or misconfigured

Verification Checklist

Before marking a host as “managed”, confirm:

* ssh ansible@host.lan works
* sudo -n true succeeds
* ansible-playbook playbooks/ping.yaml returns pong
* Host resolves correctly via CoreDNS
* No temporary bootstrap overrides remain

## Summary

Bootstrapping establishes trust between the Ansible controller and a new host.

It is intentionally explicit, repeatable, and conservative.

Once complete:

* All automation uses the ansible user
* Inventory becomes authoritative
* Failures indicate real infrastructure issues

This process is foundational to the homelab automation model and must not be skipped or improvised.