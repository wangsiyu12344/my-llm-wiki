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

HelloAgents implements five mainstream Agent paradigms, from simple conversation to complex planning-and-execution, illustrating the evolution path of AI Agent design patterns. All paradigms share a unified `Agent` abstract base class interface and can be switched as needed.

## Five Paradigms

### 1. SimpleAgent — Basic Conversation + Tool Calling

The most basic Agent implementation. Supports optional tool calling with the format `[TOOL_CALL:tool_name:parameters]`. The core method `_run_with_tools()` implements multi-turn tool call parsing and execution, supporting up to `max_tool_iterations` iterations.

Best for: simple Q&A, single-step tool calls.

### 2. ReActAgent — Reasoning + Acting

Introduces a structured Thought/Action loop. A specialized system prompt template forces the LLM to output in the following format:

```
Thought: the question I need to reason about...
Action: tool_name[parameters]
Observation: the result returned by the tool
... (loop until)
Thought: I now know the final answer
Action: Finish[final answer]
```

ReAct is one of the most widely used Agent paradigms (from Yao et al., 2023). It makes the reasoning process explicit, improving interpretability and accuracy.

### 3. ReflectionAgent — Execute-Reflect-Refine

A three-stage pipeline: Initial → Reflect → Refine.

1. **Initial**: Generate an initial output
2. **Reflect**: Self-evaluate the initial output and identify issues
3. **Refine**: Generate an improved version based on the reflection results

Adaptable to code generation, text creation, and other scenarios requiring iterative improvement. Supports customizing prompts for each stage.

### 4. PlanAndSolveAgent — Plan Then Execute

Decomposes complex tasks into two phases: Planning and Solving.

- **Planner**: Outputs a plan in Python list format for more reliable parsing
- **Executor**: Solves step by step according to the plan, outputting only the current step's answer

This separation allows plan quality to be independently evaluated and optimized, and makes it convenient for human review of plans before execution.

### 5. FunctionCallAgent — OpenAI Native Function Calling

Based on OpenAI's `tools` parameter for Function Calling capability. Compared to pure prompt-constrained approaches, native function calling is more robust — no need to parse custom formats, and the JSON schema is guaranteed by the API.

## Comparison

| Paradigm | Core Mechanism | Strength | Best For |
|----------|---------------|----------|----------|
| SimpleAgent | Single/multi-turn tool calls | Simple and direct | Basic Q&A |
| ReActAgent | Thought→Action loop | Explainable reasoning | Multi-step reasoning |
| ReflectionAgent | Generate→Reflect→Refine | Self-improvement | Content creation |
| PlanAndSolveAgent | Plan first, then execute | Structured | Complex tasks |
| FunctionCallAgent | Native Function Calling | High robustness | Stable tool calling |

## Related

- [[hello-agents-framework]] — HelloAgents framework overview
- [[agent-llm-abstraction]] — LLM abstraction layer design
