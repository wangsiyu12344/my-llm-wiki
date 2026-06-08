---
title: "エージェント LLM 抽象化層"
category: concepts
date: 2026-06-08
updated: 2026-06-08
tags: [llm-abstraction, multi-provider, local-models, openai-compatible]
source: "Datawhale《Hello Agents》第7章 — エージェントフレームワークの構築"
source_url: "https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter7/第七章%20构建你的Agent框架.md"
---

# エージェント LLM 抽象化層

## 概要

HelloAgents は `HelloAgentsLLM` クラスを通じて統一された LLM 抽象化層を実装し、異なるプロバイダー間の差異を隠蔽します。エージェントは、裏側の呼び出しが OpenAI、ModelScope、VLLM、Ollama のいずれかを気にする必要がありません。

## コア設計

### 継承ベースの拡張メカニズム

フレームワークのソースコードを変更せずに、`HelloAgentsLLM` を継承して `__init__` をオーバーライドすることで新しいプロバイダーサポートを追加します：

```python
class MyLLM(HelloAgentsLLM):
    def __init__(self, ..., provider="auto", **kwargs):
        if provider == "modelscope":
            # ModelScope の認証情報とデフォルト値をカスタム処理
            self._client = OpenAI(api_key=..., base_url=...)
        else:
            super().__init__(...)
```

重要なポイント：`else` 分岐が親クラスにフォールバックし、一致しないプロバイダーがデフォルトロジックに従うことを保証します。

### 自動検出メカニズム

`_auto_detect_provider` が優先順位に従って自動的にプロバイダーを推論：

1. **環境変数チェック**：`OPENAI_API_KEY` / `MODELSCOPE_API_KEY` などの特定の変数
2. **base_url パターンマッチング**：`:11434` → Ollama、`:8000` → VLLM
3. **API キー形式**：例：`ms-` プレフィックスによる補助判断
4. **デフォルトフォールバック**：`'auto'`、汎用設定を使用

検出後、`_resolve_credentials` が推論結果に基づいてデフォルトの `base_url` と API キーを補完します。

### ローカルモデルサポート

2つのローカル推論ソリューションがサポートされています：

- **VLLM**：高性能推論フレームワーク、`python -m vllm.entrypoints.openai.api_server` で OpenAI 互換サービスを起動
- **Ollama**：ワンクリックのローカルモデル管理 — `ollama run llama3` でサービスを起動

両方とも標準の OpenAI インターフェースを通じて接続され、フレームワーク側で特別な処理は不要です。

## 設計原則

1. **ゼロコード統合**：環境変数の設定だけでプロバイダーを切り替え可能
2. **プロバイダー透過性**：エージェントコードはどの LLM が使用されているかを認識しない
3. **容易な拡張**：1つのクラスを継承し、1つのメソッドをオーバーライドするだけで新しいプロバイダーを追加
4. **適切なデフォルト**：各プロバイダーにプリセットの base_url とデフォルトモデル

## Related

- [[hello-agents-framework]] — HelloAgents フレームワーク概要
- [[agent-paradigms]] — この LLM 層を使用する5つのエージェントパラダイム
