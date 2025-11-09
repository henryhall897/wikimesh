---
title: Self Hosted
description: Everything to Know About Self Hosting a homelab
published: true
date: 2025-11-09T02:31:00.863Z
tags: public, selfhosted
editor: markdown
dateCreated: 2025-11-05T04:13:34.901Z
---

# Self-Hosted
## Everything You Need to Know About Running Your Own Homelab

Self-hosting is about taking control of your digital environment — running your own services, managing your own infrastructure, maintaining your privacy, and learning by building.

This section of WikiMesh serves as a comprehensive introduction for anyone who wants to host, document, and share their own stack as part of the federated WikiMesh network.

## Why Self-Host?

Self-hosting isn’t just about privacy or independence — it’s about understanding the systems you rely on.
### By running your own stack, you gain:
* Full data ownership — no vendor lock-in or third-party analytics.
* Customizability — tailor services to your workflow and security standards.
* Educational value — every deployment teaches networking, storage, automation, and maintenance.
* Resilience — when you host it, you control uptime, backups, and recovery.

The Self-Hosted section of WikiMesh is a guidebook and community knowledge base for builders, tinkerers, and system owners who want to do it right.

## Key Building Blocks

Self-hosting isn’t one topic — it’s a system of systems.
The following high-level categories form the foundation of any serious homelab or self-hosted platform.

### Infrastructure

Your backbone — covering compute, networking, storage, and security.
#### Topics include:
* Hardware
* Operating Systems
* Kubernetes / K3s clusters
* Networking and VPNs (WireGuard, Tailscale, etc.)
* Reverse proxies and ingress (Traefik, Caddy)
* Storage systems, backups, and ZFS/NFS management
* Security, RBAC, and secrets management

#### [Learn More About Infrastructure](/home/public/selfhosted/infrastructure)

## Applications & Services

The “user-facing” layer — what your infrastructure supports.
### Guides here explain how to deploy, manage, and customize apps like:
* Firefly III (personal finance)
* Wiki.js (documentation and collaboration)
* Vaultwarden (password management)
* Jellyfin (media streaming)

Each app page covers both concept and implementation, helping you translate real-world needs into reproducible configurations.

## Automation & Operations

Where consistency and efficiency come in.
This section focuses on Ansible, CI/CD, and GitOps workflows for keeping your stack reproducible and maintainable.

## Runbooks & Maintenance

Step-by-step operational guides for the ongoing care of your systems — from certificate rotation to restoring backups.

## Observability & Monitoring

Because every homelab deserves good visibility.
Articles here cover Prometheus, Grafana, Loki, and alerting strategies.

## Connecting to WikiMesh

Once you’ve built your own stack and understand the layers that make it work, you’re ready to federate with the wider WikiMesh network.

### Federation means:
* Publishing your knowledge in Markdown.
* Hosting your own Wiki.js instance.
* Mirroring or syncing public content via Git with other nodes.
* Your self-hosted wiki becomes your node in the larger mesh — a durable, personally owned, and collaboratively enriched source of truth.

## Next Steps

* [Explore Infrastructure Foundations](/home/public/selfhosted/infrastructure)
* Learn to deploy Applications & Services
* Discover Automation & Runbooks
* Join the Public WikiMesh to share what you’ve built

> “Self-hosting isn’t about running servers — it’s about running knowledge.”

**Build your system. Document it. Share it. Strengthen the mesh.**