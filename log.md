# Log — Timeline

> Append-only chronological record of all wiki operations.

---

## [2026-06-08] ingest | LLM Fundamentals (SIYU)

- **Source**: SIYU — Discord #my-knowledge-base
- **Created**:
  - [[concepts/llm-fundamentals]] (zh/en/ja) — Transformer architecture, tokens, context windows, model types
- **Updated**: *none*
- **Conflict**: *none*
- **Key takeaway**: LLM fundamentals — stateless design (context IS memory), three model flavors (Base/Chat/Reasoning), GPT = Generative Pre-trained Transformer

---

## [2026-06-08] ingest | Agent Sandbox Development (SIYU)

- **Source**: SIYU — Discord #my-knowledge-base
- **Created**:
  - [[ai-development/sandbox-development]] (zh/en/ja) — Sandbox development: isolated environments, directory mounting for persistence
- **Updated**: *none*
- **Conflict**: *none*
- **Key takeaway**: Sandbox + mounted directory (Approach A) is the best practice, balancing safety isolation with code persistence.

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

## [2026-06-08] ingest | Chapter 7: Building Your Agent Framework (Datawhale Hello Agents)

- **Source**: [GitHub - datawhalechina/hello-agents](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter7/第七章%20构建你的Agent框架.md)
- **Created**:
  - [[frameworks/hello-agents-framework]] (zh/en/ja) — HelloAgents framework overview
  - [[frameworks/agent-paradigms]] (zh/en/ja) — Five agent paradigms
  - [[frameworks/agent-llm-abstraction]] (zh/en/ja) — LLM abstraction layer design
- **Updated**: *none (first ingest)*
- **Conflict**: *none (empty wiki)*
- **Key takeaway**: HelloAgents uses "Everything is a Tool" as its core philosophy, unifying Memory/RAG/MCP abstractions, supporting multi-provider LLMs via inheritance + auto-detection, and progressively implementing five agent paradigms.
