---
title: "Agent Sandbox Development"
category: concepts
date: 2026-06-08
updated: 2026-06-08
tags: [sandbox, dev-ops, hermes, container, isolation]
source: "SIYU — Discord #my-knowledge-base"
---

# Agent Sandbox Development

## Overview

Sandbox development means having an AI Agent execute code inside an isolated container environment rather than directly on the host machine. This approach is especially important in AI-agent-assisted development, since agent actions are not fully predictable — the sandbox provides a safety boundary.

## Benefits of Sandboxes

1. **Dependency isolation**: Packages from `pip install` or `npm install` don't pollute the host server. Each project's dependencies are completely independent.

2. **Safety boundary**: No matter what code the Agent runs, it cannot damage the system. Even problematic commands are confined to the container.

3. **Clean environment**: Switching projects gives you a completely clean environment, with no "old version conflicts from last time." Every session starts fresh.

## Code Persistence

Default containers are **stateless** — all files disappear on exit. To do meaningful development in a sandbox, you need to solve code persistence:

### Approach A: Mount project directory (recommended)

Mount a host directory into the container so file changes inside the container are written directly to the actual directory:

```bash
hermes -p <profile> config set terminal.cwd /home/ubuntu/projects/<project>
```

After mounting, file changes inside the container reflect in real time on the actual directory, and `git push` works exactly as it does locally. This is the recommended approach — it gives you both sandbox safety isolation and local-development persistence.

### Approach B: Pure sandbox + push promptly

Don't mount any directory. Write code in the container, then immediately `commit` + `push` — don't wait for the container to be destroyed. The downside: if you forget to push or the network drops, code is lost.

## Summary

Developing in a sandbox is better than working directly on the host. Approach A (mounting a directory) is recommended: writing code, testing, and git push all work as smoothly as local development, while protecting the server from accidental damage.

## Related

- [[../frameworks/hello-agents-framework]] — Agent framework design philosophy
