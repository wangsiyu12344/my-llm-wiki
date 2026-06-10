# LLM Wiki

My personal, compounding knowledge base for LLMs and AI — built following [Andrej Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

## Structure

```
wiki/
├── zh/                # 中文
├── en/                # English
└── ja/                # 日本語
```

Every topic exists in all three languages with semantically identical content.

## How It Works

- Content is sent via Discord and ingested by an AI agent
- The agent detects conflicts, cross-references, and merges intelligently
- Trilingual pages are created/updated automatically
- All changes go through PR review before merging

## Topics

→ **Frameworks** — Agent frameworks and their design (HelloAgents)
→ **AI Development** — Agent sandboxing, dev workflows
→ **Concepts** — LLM fundamentals, Transformer architecture, tokens

## Tech

→ MkDocs + Material theme for browsing
→ `[[wikilinks]]` for cross-referencing
→ GitHub Actions for auto-deploy
