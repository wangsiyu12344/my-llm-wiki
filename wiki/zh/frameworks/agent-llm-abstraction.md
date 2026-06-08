---
title: "Agent LLM 抽象层"
category: concepts
date: 2026-06-08
updated: 2026-06-08
tags: [llm-abstraction, multi-provider, local-models, openai-compatible]
source: "Datawhale《Hello Agents》第七章 — 构建你的Agent框架"
source_url: "https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter7/第七章%20构建你的Agent框架.md"
---

# Agent LLM 抽象层

## 概述

HelloAgents 通过 `HelloAgentsLLM` 类实现统一的 LLM 抽象层，屏蔽不同提供商之间的差异，让 Agent 无需关心底层调用的是 OpenAI、ModelScope、VLLM 还是 Ollama。

## 设计核心

### 继承扩展机制

不修改框架源码，通过继承 `HelloAgentsLLM` 并重写 `__init__` 来添加新提供商支持：

```python
class MyLLM(HelloAgentsLLM):
    def __init__(self, ..., provider="auto", **kwargs):
        if provider == "modelscope":
            # 自定义处理 ModelScope 的凭证和默认值
            self._client = OpenAI(api_key=..., base_url=...)
        else:
            super().__init__(...)
```

关键点：`else` 分支回退到父类，确保未匹配的 provider 走默认逻辑。

### 自动检测机制

`_auto_detect_provider` 按优先级自动推断服务商：

1. **环境变量检查**：`OPENAI_API_KEY` / `MODELSCOPE_API_KEY` 等特定变量
2. **base_url 特征匹配**：`:11434` → Ollama，`:8000` → VLLM
3. **API 密钥格式**：如 `ms-` 前缀辅助判断
4. **默认回退**：`'auto'`，使用通用配置

检测后 `_resolve_credentials` 根据推断结果补全默认 `base_url` 和 API 密钥。

### 本地模型支持

支持两种本地推理方案：

- **VLLM**：高性能推理框架，通过 `python -m vllm.entrypoints.openai.api_server` 启动 OpenAI 兼容服务
- **Ollama**：一键式本地模型管理，`ollama run llama3` 即可启动

两者均通过标准 OpenAI 接口接入，框架无需特殊处理。

## 设计原则

1. **零代码接入**：通过环境变量配置即可切换提供商
2. **Provider 透明**：Agent 代码不感知底层使用哪个 LLM
3. **易于扩展**：继承一个类、重写一个方法即可添加新提供商
4. **合理默认值**：每个 provider 都有预设的 base_url 和默认模型

## Related

- [[hello-agents-framework]] — HelloAgents 框架总览
- [[agent-paradigms]] — 使用此 LLM 层的五种 Agent 范式
