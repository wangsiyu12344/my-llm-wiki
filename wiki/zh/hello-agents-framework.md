---
title: "HelloAgents 框架"
category: concepts
date: 2026-06-08
updated: 2026-06-08
tags: [agent-framework, open-source, education, tool-abstraction]
source: "Datawhale《Hello Agents》第七章 — 构建你的Agent框架"
source_url: "https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter7/第七章%20构建你的Agent框架.md"
---

# HelloAgents 框架

## 概述

HelloAgents 是 Datawhale《Hello Agents》教程中引导读者从零构建的轻量级 AI Agent 框架。它不是用于生产的重型框架，而是**教学导向**的框架，核心理念是「万物皆为工具」（Everything is a Tool）。

## 设计理念

1. **轻量级 + 教学友好**：核心代码按章节组织，依赖极简（仅 OpenAI SDK 等必要库），可读性高。学习者可以定位到具体代码行而非在成千上万行框架代码中迷失。

2. **基于标准 API**：完全兼容 OpenAI 接口规范，迁移和集成成本低。任何兼容 OpenAI API 的服务（包括本地模型）都可接入。

3. **渐进式学习路径**：框架通过 pip 版本迭代（如 `hello-agents==0.1.1`），每个版本对应一个学习章节，学习者可逐步深入。

4. **统一的工具抽象**：Memory、RAG、MCP 等复杂模块都被统一抽象为「工具」。这降低了抽象层数，回归了 Agent 的本质——调用工具完成任务。

## 架构分层

```
hello_agents/
├── core/          # 核心框架层（Agent基类、LLM接口、消息系统、配置管理）
├── agents/        # Agent 实现层（Simple, ReAct, Reflection, PlanAndSolve）
└── tools/         # 工具系统层（基类、注册、异步执行、内置工具）
```

三层分离的设计使得每一层都可以独立扩展：你可以新增一个 LLM 提供商而不触及 Agent 逻辑，也可以添加新的 Agent 范式而不改动工具系统。

## 为什么自建框架？

市面上主流框架（如 LangChain）存在以下痛点：

- **过度抽象**：概念繁多，简单任务需要理解大量前置知识
- **API 不稳定**：版本迭代快，维护成本高
- **黑盒逻辑**：核心实现不透明，难以深度定制
- **依赖复杂**：包体积大，容易产生依赖冲突

自建框架的价值在于：深度理解 Agent 工作原理；获得完全控制权；培养系统设计能力。尤其在垂直领域（金融、医疗、教育），定制化需求往往远超通用框架能提供的灵活性。

## Related

- [[agent-paradigms]] — HelloAgents 支持的多种 Agent 范式
- [[agent-llm-abstraction]] — 多提供商 LLM 抽象层设计
