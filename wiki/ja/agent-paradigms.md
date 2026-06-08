---
title: "エージェントパラダイム"
category: concepts
date: 2026-06-08
updated: 2026-06-08
tags: [agent-paradigms, react, reflection, plan-and-solve, function-calling]
source: "Datawhale《Hello Agents》第7章 — エージェントフレームワークの構築"
source_url: "https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter7/第七章%20构建你的Agent框架.md"
---

# エージェントパラダイム

## 概要

HelloAgents は、シンプルな会話から複雑な計画-実行まで、5つの主要なエージェントパラダイムを実装し、AI エージェント設計パターンの進化を示しています。すべてのパラダイムは統一された `Agent` 抽象基底クラスインターフェースを共有し、必要に応じて切り替え可能です。

## 5つのパラダイム

### 1. SimpleAgent — 基本会話 + ツール呼び出し

最も基本的なエージェント実装。`[TOOL_CALL:tool_name:parameters]` 形式でオプションのツール呼び出しをサポート。コアメソッド `_run_with_tools()` が複数ラウンドのツール呼び出し解析と実行を処理し、`max_tool_iterations` で制限可能。

適した場面：単純な Q&A、単一ステップのツール使用。

### 2. ReActAgent — 推論 + 行動

構造化された Thought/Action ループを導入。専用のシステムプロンプトテンプレートが LLM に以下の形式での出力を強制します：

```
Thought: 推論すべきこと...
Action: tool_name[parameters]
Observation: ツールの出力
...（以下ループ）
Thought: 最終的な答えがわかった
Action: Finish[最終回答]
```

ReAct（Yao et al., 2023）は最も広く使用されているエージェントパラダイムの一つです。推論プロセスを明示化し、解釈可能性と正確性を向上させます。

### 3. ReflectionAgent — 実行-内省-改善

3段階パイプライン：Initial → Reflect → Refine。

1. **Initial**：初期出力を生成
2. **Reflect**：初期出力を自己評価し、問題点を特定
3. **Refine**：内省に基づいて改善版を生成

コード生成やテキスト作成など、反復的な改善が必要なシナリオに適応可能。各段階のプロンプトはカスタマイズ可能。

### 4. PlanAndSolveAgent — 計画してから実行

複雑なタスクを計画（Planning）と実行（Solving）の2段階に分解：

- **Planner**：Python リスト形式で計画を出力し、解析の安定性を向上
- **Executor**：計画に従って段階的に解決し、現在のステップの回答のみを出力

この分離により、計画の品質を独立して評価・最適化できます。実行前の計画の人間によるレビューも可能です。

### 5. FunctionCallAgent — OpenAI ネイティブ関数呼び出し

OpenAI の `tools` パラメータを活用したネイティブ関数呼び出し。純粋なプロンプト制約アプローチと比較して、ネイティブ関数呼び出しはより堅牢で、カスタム形式の解析が不要で、JSON スキーマが API によって保証されます。

## 比較

| パラダイム | コアメカニズム | 強み | 適した場面 |
|-----------|-------------|------|----------|
| SimpleAgent | 単一/複数ラウンドのツール呼び出し | シンプルで直接的 | 基本的な Q&A |
| ReActAgent | Thought→Action ループ | 説明可能な推論 | 多段階推論 |
| ReflectionAgent | 生成→内省→改善 | 自己改善 | コンテンツ作成 |
| PlanAndSolveAgent | 計画してから実行 | 構造化 | 複雑なタスク |
| FunctionCallAgent | ネイティブ関数呼び出し | 堅牢性 | 安定したツール呼び出し |

## Related

- [[hello-agents-framework]] — HelloAgents フレームワーク概要
- [[agent-llm-abstraction]] — LLM 抽象化層の設計
