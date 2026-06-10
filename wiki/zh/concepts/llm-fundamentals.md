---
title: "LLM 基础知识"
category: concepts
date: 2026-06-08
updated: 2026-06-08
tags: [llm, transformer, tokenization, context-window, model-types]
source: "SIYU — Discord #my-knowledge-base"
---

# LLM 基础知识

## 什么是 LLM？

大语言模型（LLM）是一种神经网络——具体来说是 Transformer 架构——在海量互联网数据上预训练而成。通过训练，其参数被调整到能够以惊人准确度预测序列中下一个 token 的程度。

**GPT**（Generative Pre-trained Transformer）这个名字概括了本质：
- **Generative（生成式）**：逐 token 生成文本
- **Pre-trained（预训练）**：在任何特定用途之前，已用互联网规模的数据训练
- **Transformer**：底层神经网络架构

LLM 是**一个 token 一个 token**生成的——每次输出都是对下一个内容的预测。

## Token

在典型英文写作中：
- 1 token ≈ 4 个字符
- 1 token ≈ 0.75 个单词
- 1000 token ≈ 750 个单词

## Transformer 架构

Transformer 由 Google 团队提出，取代了早期的 **LSTM**（长短期记忆网络）。LSTM 的核心问题是难以并行化——处理必须按顺序进行。Transformer 解决了这个问题，使得大规模训练成为可能，不仅产生合理的 token，而且能以惊人精度模仿智能。

**参数**是 Transformer 神经网络中权重的特定排列。更多参数（配合足够数据）通常意味着更强的模型能力。

## 三种 LLM 类型

1. **Base Model（基座模型）**：最适合微调以学习新技能。这些是原始的预训练模型，未经指令微调。

2. **Chat Model（对话模型）**：最适合交互式用例和创意内容生成——例如写邮件、头脑风暴、对话。这些模型经过指令微调，适合对话场景。

3. **Reasoning Model（推理模型）**：最适合问题求解。这些模型针对多步推理、数学、编程和逻辑任务进行了优化。

## 无状态设计

每次调用 LLM 都是**无状态**的——模型在两次调用之间没有记忆。记忆的假象来自于每次将整个对话历史传入输入 prompt。LLM 只是根据完整上下文预测最可能的下一个 token。

关键含义：
- 对话上下文就是"记忆"
- 越长对话消耗越多 token
- API 调用之间不保留任何状态

## 上下文窗口

**上下文窗口**是模型在生成下一个 token 时能考虑的最大 token 数量。这包括输入 prompt 和生成的输出。如果对话超出上下文窗口，较早的部分会被丢失。

## 开源模型

| 模型 | 组织 |
|------|------|
| **Llama** | Meta |
| **Qwen** | 阿里云 |
| **DeepSeek** | DeepSeek AI |
| **GPT-OSS** | OpenAI |

## Related

- [[zh/frameworks/agent-llm-abstraction]] — Agent 框架如何抽象 LLM 提供商
- [[zh/frameworks/agent-paradigms]] — 基于 LLM 能力构建的 Agent 范式
