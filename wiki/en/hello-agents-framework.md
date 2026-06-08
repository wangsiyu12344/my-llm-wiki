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

HelloAgents is a lightweight AI Agent framework introduced in Datawhale's *Hello Agents* tutorial that guides readers through building an agent framework from scratch. It is not a production-grade heavy framework, but rather an **education-oriented** one, with the core philosophy that "Everything is a Tool."

## Design Philosophy

1. **Lightweight + Education-Friendly**: Core code is organized by chapter, with minimal dependencies (only essential libraries like the OpenAI SDK), and high readability. Learners can trace specific lines of code rather than getting lost in tens of thousands of lines of framework code.

2. **Standards-Based API**: Fully compatible with the OpenAI API specification, making migration and integration low-cost. Any OpenAI-compatible service (including local models) can be plugged in.

3. **Progressive Learning Path**: The framework iterates through pip versions (e.g., `hello-agents==0.1.1`), with each version corresponding to a learning chapter, allowing learners to go deeper step by step.

4. **Unified Tool Abstraction**: Complex modules like Memory, RAG, and MCP are all uniformly abstracted as "tools." This reduces abstraction layers and returns to the essence of an Agent — calling tools to accomplish tasks.

## Architecture Layers

```
hello_agents/
├── core/          # Core framework layer (Agent base class, LLM interface, message system, config management)
├── agents/        # Agent implementation layer (Simple, ReAct, Reflection, PlanAndSolve)
└── tools/         # Tool system layer (base, registry, async execution, built-in tools)
```

The three-layer separation allows each layer to be extended independently: you can add a new LLM provider without touching Agent logic, or add a new Agent paradigm without modifying the tool system.

## Why Build Your Own Framework?

Mainstream frameworks (like LangChain) have the following pain points:

- **Over-abstraction**: Too many concepts — even simple tasks require understanding a large amount of prerequisite knowledge
- **API Instability**: Rapid version iteration with high maintenance costs
- **Black-box Logic**: Core implementations are opaque, making deep customization difficult
- **Dependency Complexity**: Large package sizes with frequent dependency conflicts

The value of building your own framework lies in: deep understanding of how Agents work; complete control; and cultivating systems design skills. Especially in vertical domains (finance, healthcare, education), customization needs often far exceed the flexibility that general-purpose frameworks can provide.

## Related

- [[agent-paradigms]] — Agent paradigms supported by HelloAgents
- [[agent-llm-abstraction]] — Multi-provider LLM abstraction layer design
