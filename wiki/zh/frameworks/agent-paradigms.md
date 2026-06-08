---
title: "Agent 范式"
category: concepts
date: 2026-06-08
updated: 2026-06-08
tags: [agent-paradigms, react, reflection, plan-and-solve, function-calling]
source: "Datawhale《Hello Agents》第七章 — 构建你的Agent框架"
source_url: "https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter7/第七章%20构建你的Agent框架.md"
---

# Agent 范式

## 概述

HelloAgents 框架实现了五种主流 Agent 范式，从简单对话到复杂的规划-执行，展示了 AI Agent 设计模式的演进路径。所有范式共享统一的 `Agent` 抽象基类接口，可以按需切换。

## 五种范式

### 1. SimpleAgent — 基础对话 + 工具调用

最基础的 Agent 实现。支持可选工具调用，工具调用格式为 `[TOOL_CALL:tool_name:parameters]`。核心方法 `_run_with_tools()` 实现多轮工具调用解析和执行，最多支持 `max_tool_iterations` 次迭代。

适用场景：简单问答、单步工具调用。

### 2. ReActAgent — 推理 + 行动

引入结构化的 Thought/Action 循环。通过专门的系统提示词模板强制 LLM 按以下格式输出：

```
Thought: 我需要思考的问题...
Action: tool_name[parameters]
Observation: 工具返回的结果
...（循环直到）
Thought: 我现在知道最终答案了
Action: Finish[最终回答]
```

ReAct 是目前最广泛使用的 Agent 范式之一（来自 Yao et al., 2023），它将推理过程显式化，提高了可解释性和准确性。

### 3. ReflectionAgent — 执行-反思-优化

三段式流程：Initial → Reflect → Refine。

1. **Initial**：生成初始输出
2. **Reflect**：对初始输出进行自我评估，识别问题
3. **Refine**：基于反思结果生成改进版本

可适应代码生成、文本创作等需要迭代改进的场景。支持自定义各阶段的提示词。

### 4. PlanAndSolveAgent — 规划并执行

将复杂任务分解为规划（Planning）和执行（Solving）两个阶段：

- **Planner**：输出 Python 列表格式的计划，提高解析稳定性
- **Executor**：按计划逐步求解，只输出当前步骤答案

这种分离使得规划质量可以独立评估和优化，也方便人工审查计划后再执行。

### 5. FunctionCallAgent — OpenAI 原生函数调用

基于 OpenAI 的 `tools` 参数的 Function Calling 能力。与纯 prompt 约束方式相比，原生函数调用鲁棒性更强，不需要解析自定义格式，JSON schema 由 API 保证。

## 对比

| 范式 | 核心机制 | 优势 | 适用场景 |
|------|---------|------|---------|
| SimpleAgent | 单轮/多轮工具调用 | 简单直接 | 基础问答 |
| ReActAgent | Thought→Action 循环 | 推理可解释 | 多步推理 |
| ReflectionAgent | 生成→反思→优化 | 自我改进 | 内容创作 |
| PlanAndSolveAgent | 先规划再执行 | 结构化 | 复杂任务 |
| FunctionCallAgent | 原生 Function Calling | 鲁棒性强 | 需要稳定工具调用 |

## Related

- [[hello-agents-framework]] — HelloAgents 框架总览
- [[agent-llm-abstraction]] — LLM 抽象层设计
