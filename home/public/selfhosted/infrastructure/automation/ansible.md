---
title: Ansible Overview
description: An overview of Ansible and its purpose as an infrastructure piece 
published: true
date: 2025-12-08T12:46:15.451Z
tags: infrastructure, public, selfhosted, home, automation, ansible
editor: markdown
dateCreated: 2025-12-08T12:46:15.451Z
---

# Ansible Overview

Ansible is the central configuration management tool used throughout the homelab.
It acts as the source of truth for machine setup, system configuration, user management, and update policy.
This section explains what Ansible is, why it was chosen, and how it integrates into the automation strategy.

## What Is Ansible?
### Ansible is an agentless automation framework that uses:
* SSH for communication
* YAML for describing desired state
* Idempotent modules to ensure consistent outcomes
* Inventory files to define hosts and groups

Because it is agentless, no special software or daemon needs to be installed on target hosts—just Python and SSH.

## Why I Chose Ansible for the Homelab
### 1. Agentless and Lightweight
* No running agents, no services to maintain.
* If a machine has SSH + Python, Ansible can manage it.

### 2. Perfect for Hybrid Environments
### The homelab contains:
* Kubernetes nodes
* Game servers
* Utility servers
* Containers and orchestrators
* Ansible works across all of them without special requirements.

## 3. Idempotent Configuration
### Running the same playbook twice results in the same state—critical for:
* Reprovisioning nodes
* Handling drift
* Rebuilding machines

## 4. Human-readable YAML
### Configuration is declarative and easy to audit:
```yaml
- name: Install packages
  apt:
    name:
      - htop
      - curl
    state: present
```
## 5. Great Fit for GitOps-Style Workflows
### All configuration lives in git:
* Versioned history
* Rollbacks
* Code review
* Infrastructure-as-code
* Future CI/CD plans will execute Ansible automatically on change.

## How Ansible Fits Into the Homelab
### Ansible is responsible for:
#### Base System Provisioning
* Creating standardized users
* Installing baseline packages
* Ensuring correct time sync, locales, motd, security settings
* Managing SSH configuration

#### System Updates
* OS upgrades
* Automatic security patching
* Safe reboot logic

#### Network Configuration
* Managing WireGuard peers
* Standardizing firewall rules
* Applying network profiles across nodes

#### Cluster Node Setup
* Preparing machines for Kubernetes
* Installing container runtimes
* Ensuring consistent sysctl, limits, cgroups, etc.

#### App-Specific Needs
Used alongside orchestrators for:
* Updating modded servers
* Deploying lightweight services outside Kubernetes

## Ansible Documentation Structure

This overview acts as the gateway to more detailed sections:

### Setup & Installation
* Installing Ansible via pipx
* Preparing the controller machine
* SSH key management

### Inventory & Configuration
* hosts.yml structure
* Groups, variables, host_vars & group_vars
* Ansible configuration (ansible.cfg)

### User & Access Management
* Creating automation users
* Deploying SSH keys
* Sudo configuration

### Playbooks & Roles
* Writing playbooks
* Creating reusable roles
* Role directory structure

### Running Ansible
* common commands
* Ad-hoc tasks
* Playbook execution
* Dry runs and check mode

### Use Cases in the Homelab
* Update automation
* Baseline provisioning
* Firewall configuration
* WireGuard automation
* Kubernetes node setup

#### Quick Example: Ping a Host
```
ansible cluster1 -m ping
```

##### Output:
```
cluster1 | SUCCESS => { "ping": "pong" }
```

This validates SSH access, user configuration, and inventory correctness.
