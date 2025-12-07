---
title: Public WikiMesh
description: Publicly available wiki articles for WikiMesh
published: true
date: 2025-12-07T22:34:01.885Z
tags: overview, public
editor: markdown
dateCreated: 2025-10-15T01:18:02.471Z
---

# Public WikiMesh
Public WikiMesh is the open-knowledge side of the federated WikiMesh network — a shared space where contributors publish documentation, tutorials, and insights drawn from their own self-hosted projects.

This section exists to make knowledge freely available, foster collaboration, and help new contributors learn how to build, document, and federate their own systems.

## Purpose
### The public wiki serves three main goals:
#### Share practical knowledge
Articles here cover self-hosting practices, infrastructure design, automation, security, and more — written so that anyone can reproduce the concepts on their own hardware or cloud environment.
#### Promote transparency and reproducibility
Each public guide represents a working example from one or more contributors’ own deployments. By documenting what we build and how we build it, we strengthen the entire self-hosting community.
#### Act as a gateway for future contributors
This is the first stop for people discovering WikiMesh. It explains what the federation is, how it works, and how to join in by creating your own node.

## How Contributions Work
### WikiMesh isn’t a single centralized wiki.
Every participant runs an independent Wiki.js instance that syncs portions of its content through Git federation.

### Contributors:
* Maintain their own wiki under their preferred domain or local hostname.
* Publish selected articles or guides publicly under home/public/.
* Optionally federate those articles into shared upstream repositories for others to clone or merge.
* Keep full control over their private drafts, secrets, and environment-specific materials.

This model keeps ownership local while allowing the network as a whole to grow organically through shared knowledge.

## Joining the Federation
### To become part of WikiMesh:
While it is possible to get an account made for an exisitng node and contribute that way, it is preferred that those seeking to join and contribute
* **Set up your own Wiki.js instance** — self-host it on your homelab, VPS, or any environment you control.
* Adopt the WikiMesh folder structure (home/public/, home/private/, etc.) for consistency.
* Publish your own projects and documentation under your public section.
* Federate via Git — add a remote to the shared WikiMesh repository or sync selectively with other contributors.
* Engage and collaborate — share ideas, troubleshoot issues, and refine guides so others can benefit.

By joining, you contribute not just articles, but resilience: every node strengthens the mesh.

## Guiding Principles
* Knowledge should be portable — all articles are Markdown and Git-based.
* Federation over centralization — no single server owns the truth.
* Respect autonomy — each contributor’s wiki reflects their environment and expertise.
* Teach by example — documentation is stronger when it’s lived and tested.

## Community and Onboarding

If you’re exploring self-hosting or documenting your own stack, the Public WikiMesh is the best place to start.
Read existing guides, mirror the structure, and begin drafting your own content.

When you’re ready, you can register your wiki node with the federation. Currently accepting known applicants only. Should already know atleast one contributor. May change policy to allow automatic self service joins at some point in the future. 

## What next?
* Browse the [Self-Hosted Guides](/home/public/selfhosted)


> Every new node makes the mesh stronger. Start by documenting what you already know — and let others learn from your build.
