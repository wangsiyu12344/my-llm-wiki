---
title: "HelloAgents Framework"
category: concepts
date: 2026-06-08
updated: 2026-06-08
tags: [agent-framework, open-source, education, tool-abstraction]
source: "Datawhale《Hello Agents》Chapter 7 — Building Your Agent Framework"
source_url: "https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter7/第七章%20构建你的Agent框架.md"
---

# HelloAgents Framework

## Overview

HelloAgents is a lightweight AI agent framework introduced in Datawhale's *Hello Agents* tutorial, designed to guide learners through building an agent framework from scratch. It is education-oriented rather than production-grade, with the core philosophy that "everything is a tool."

## Design Philosophy

1. **Lightweight + Education-Friendly**: Core code is organized by chapter with minimal dependencies (only essential libraries like the OpenAI SDK), maximizing readability. Learners can trace specific lines of code rather than getting lost in sprawling framework internals.

2. **Standards-Based API**: Fully compatible with the OpenAI API specification, making migration and integration straightforward. Any OpenAI-compatible service, including local models, can be plugged in.

3. **Progressive Learning Path**: The framework iterates through pip versions (e.g., `hello-agents==0.1.1`), with each version corresponding to a learning chapter, allowing learners to progress step by step.

4. **Unified Tool Abstraction**: Complex modules like Memory, RAG, and MCP are all abstracted as "tools." This reduces abstraction layers and returns to the core Agent logic: calling tools to accomplish tasks.

## Architecture

```
hello_agents/
├── core/          # Core framework layer (Agent base class, LLM interface, messaging, config)
├── agents/        # Agent implementation layer (Simple, ReAct, Reflection, PlanAndSolve)
└── tools/         # Tool system layer (base, registry, async executor, built-in tools)
```

The three-layer separation allows each layer to be extended independently: you can add a new LLM provider without touching agent logic, or add a new agent paradigm without modifying the tool system.

## Why Build Your Own?

Mainstream frameworks like LangChain have notable pain points:

- **Over-abstraction**: Too many concepts; even simple tasks require extensive prerequisite knowledge
- **API Instability**: Rapid version iteration with high maintenance costs
- **Black-box Logic**: Opaque core implementations make deep customization difficult
- **Dependency Complexity**: Large package sizes with frequent dependency conflicts

Building your own framework offers deep understanding of agent internals, full control over behavior, and systems design skills. This is especially valuable in vertical domains (finance, healthcare, education) where customization needs often exceed what general-purpose frameworks provide.

## Related

- [[agent-paradigms]] — Agent paradigms supported by HelloAgents
- [[agent-llm-abstraction]] — Multi-provider LLM abstraction layer design
