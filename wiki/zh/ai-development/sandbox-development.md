---
title: "Agent 沙盒开发"
category: concepts
date: 2026-06-08
updated: 2026-06-08
tags: [sandbox, dev-ops, hermes, container, isolation]
source: "SIYU — Discord #my-knowledge-base"
---

# Agent 沙盒开发

## 概述

沙盒（Sandbox）开发是指让 AI Agent 在隔离的容器环境中执行代码，而非直接在宿主机上操作。这种做法在 AI Agent 辅助开发的场景中尤为重要，因为 Agent 执行的操作不可完全预测，沙盒提供了安全边界。

## 沙盒的优势

1. **隔离依赖**：`pip install`、`npm install` 的依赖不会污染宿主服务器。每个项目的依赖完全独立。

2. **安全边界**：无论 Agent 执行什么代码都不会损坏系统。即使运行了有问题的命令，影响范围也被限制在容器内。

3. **环境纯净**：切换项目时环境完全干净，不存在「上次装的旧版本冲突」问题。每次启动都是全新环境。

## 代码持久化

默认容器是**无状态**的——退出后所有文件消失。要在沙盒里做有意义的开发，需要解决代码持久化问题：

### 方案 A：挂载项目目录（推荐）

将宿主机目录挂载到容器内部，容器里的文件变更直接写入实际目录：

```bash
hermes -p <profile> config set terminal.cwd /home/ubuntu/projects/<project>
```

挂载后，容器里改的文件实时反映到实际目录，`git push` 与本地操作完全一致。这是最推荐的方案，因为同时获得了沙盒的安全隔离和本地开发的持久化便利。

### 方案 B：纯沙盒 + 及时 push

不挂载目录，在容器里写完代码后立刻 `commit` + `push`，不要等容器销毁。缺点是如果忘记 push 或网络中断，代码丢失。

## 小结

开发用沙盒优于直接在宿主机操作。方案 A（挂载目录）是推荐做法：写代码、测试、git push 都跟本地一样流畅，同时保护服务器不受误操作影响。

## Related

- [[../frameworks/hello-agents-framework]] — Agent 框架设计理念
- [[../frameworks/agent-paradigms]] — 五种 Agent 范式
