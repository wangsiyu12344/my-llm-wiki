---
title: "Agent Paradigms"
category: concepts
date: 2026-06-08
updated: 2026-06-08
tags: [agent-paradigms, react, reflection, plan-and-solve, function-calling]
source: "Datawhale《Hello Agents》Chapter 7 — Building Your Agent Framework"
source_url: "https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter7/第七章%20构建你的Agent框架.md"
---

# Agent Paradigms

## Overview

HelloAgents implements five mainstream agent paradigms, from simple conversation to complex plan-and-execute, illustrating the evolution of AI agent design patterns. All paradigms share a unified `Agent` abstract base class interface, allowing them to be swapped as needed.

## Five Paradigms

### 1. SimpleAgent — Basic Conversation + Tool Calling

The most fundamental agent implementation. Supports optional tool calling with the format `[TOOL_CALL:tool_name:parameters]`. The core `_run_with_tools()` method handles multi-turn tool call parsing and execution, with a configurable `max_tool_iterations` limit.

Best for: simple Q&A, single-step tool use.

### 2. ReActAgent — Reasoning + Acting

Introduces a structured Thought/Action loop. A specialized system prompt template enforces LLM output in the following format:

```
Thought: what I need to reason about...
Action: tool_name[parameters]
Observation: tool output
... (loop until)
Thought: I now know the final answer
Action: Finish[final answer]
```

ReAct (from Yao et al., 2023) is one of the most widely used agent paradigms. It makes the reasoning process explicit, improving interpretability and accuracy.

### 3. ReflectionAgent — Execute-Reflect-Refine

A three-stage pipeline: Initial → Reflect → Refine.

1. **Initial**: Generate an initial output
2. **Reflect**: Self-evaluate the initial output, identifying issues
3. **Refine**: Generate an improved version based on the reflection

Adaptable to code generation, text creation, and other scenarios requiring iterative improvement. Each stage's prompt is customizable.

### 4. PlanAndSolveAgent — Plan Then Execute

Decomposes complex tasks into two phases: Planning and Solving.

- **Planner**: Outputs a plan in Python list format for reliable parsing
- **Executor**: Solves step by step, outputting only the current step's answer

This separation allows plan quality to be independently evaluated and optimized. It also enables human review of plans before execution.

### 5. FunctionCallAgent — Native OpenAI Function Calling

Leverages OpenAI's `tools` parameter for native function calling. Compared to pure prompt-constrained approaches, native function calling is more robust — no custom format parsing needed, and JSON schema is guaranteed by the API.

## Comparison

| Paradigm | Core Mechanism | Strengths | Best For |
|----------|---------------|-----------|----------|
| SimpleAgent | Single/multi-turn tool calls | Simple and direct | Basic Q&A |
| ReActAgent | Thought→Action loop | Explainable reasoning | Multi-step reasoning |
| ReflectionAgent | Generate→Reflect→Refine | Self-improvement | Content creation |
| PlanAndSolveAgent | Plan first, then execute | Structured | Complex tasks |
| FunctionCallAgent | Native Function Calling | Robustness | Stable tool calling |

## Related

- [[hello-agents-framework]] — HelloAgents framework overview
- [[agent-llm-abstraction]] — LLM abstraction layer design
