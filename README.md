# LLM Wiki

My personal, compounding knowledge base for LLMs and AI — built following [Andrej Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

:rocket: **Live site:** [wangsiyu12344.github.io/my-llm-wiki](https://wangsiyu12344.github.io/my-llm-wiki/)

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

## Tech

→ MkDocs + Material theme for browsing
→ `[[wikilinks]]` for cross-referencing
→ GitHub Actions for auto-deploy
