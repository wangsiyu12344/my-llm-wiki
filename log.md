# Log — 时间线 / Timeline / タイムライン

> Append-only chronological record of all wiki operations.

---

## [2026-06-08] ingest | Agent 沙盒开发 (SIYU)

- **Source**: SIYU — Discord #my-knowledge-base
- **Created**:
  - [[ai-development/sandbox-development]] (zh/en/ja) — 沙盒开发：隔离环境、挂载目录持久化
- **Updated**: *none*
- **Conflict**: *none*
- **Key takeaway**: 开发用沙盒 + 挂载目录（方案 A）是最佳实践，兼顾安全隔离和代码持久化。

---

## [2026-06-08] update | AGENTS.md improvements + multi-level dir support

- **Changes**:
  - AGENTS.md: added git-history-based integration step, multi-level directory support, PR workflow
  - Moved all pages into `frameworks/` subdirectory to dogfood multi-level structure
  - Updated INDEX.md with new directory structure
- **Conflict**: none

---

## [2026-06-08] fix | Trilingual consistency — en/ja pages rewritten from zh source

- **Changes**:
  - `wiki/en/hello-agents-framework.md`, `wiki/en/agent-paradigms.md`, `wiki/en/agent-llm-abstraction.md`
  - `wiki/ja/hello-agents-framework.md`, `wiki/ja/agent-paradigms.md`, `wiki/ja/agent-llm-abstraction.md`
  - All rewritten as faithful translations from the Chinese source
- **Conflict**: none

---

## [2026-06-08] ingest | 第七章 构建你的Agent框架 (Datawhale Hello Agents)

- **Source**: [GitHub - datawhalechina/hello-agents](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter7/第七章%20构建你的Agent框架.md)
- **Created**:
  - [[frameworks/hello-agents-framework]] (zh/en/ja) — HelloAgents 框架概览
  - [[frameworks/agent-paradigms]] (zh/en/ja) — 五种 Agent 范式
  - [[frameworks/agent-llm-abstraction]] (zh/en/ja) — LLM 抽象层设计
- **Updated**: *none (first ingest)*
- **Conflict**: *none (empty wiki)*
- **Key takeaway**: HelloAgents 以「万物皆为工具」核心理念统一抽象 Memory/RAG/MCP，通过继承扩展 + 自动检测实现多提供商 LLM 支持，渐进式实现五种 Agent 范式。
