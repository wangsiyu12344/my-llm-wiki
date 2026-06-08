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

HelloAgents は `HelloAgentsLLM` クラスを通じて統一された LLM 抽象化層を実装し、プロバイダー固有の差異をエージェントから隠蔽します。エージェントは、裏側の呼び出しが OpenAI、ModelScope、VLLM、Ollama のいずれかを知る必要がありません。

## コア設計

### 継承ベースの拡張

フレームワークのソースコードを変更せずに、`HelloAgentsLLM` をサブクラス化して `__init__` をオーバーライドすることで新しいプロバイダーを追加します：

```python
class MyLLM(HelloAgentsLLM):
    def __init__(self, ..., provider="auto", **kwargs):
        if provider == "modelscope":
            # ModelScope の認証情報とデフォルト値をカスタム処理
            self._client = OpenAI(api_key=..., base_url=...)
        else:
            super().__init__(...)
```

重要な点：`else` 分岐が親クラスにフォールバックし、未一致のプロバイダーがデフォルトロジックに従うことを保証します。

### 自動検出メカニズム

`_auto_detect_provider` が優先順位に従ってプロバイダーを推論：

1. **環境変数チェック**：`OPENAI_API_KEY` / `MODELSCOPE_API_KEY` など
2. **base_url パターンマッチング**：`:11434` → Ollama、`:8000` → VLLM
3. **API キー形式のヒント**：例：`ms-` プレフィックス
4. **デフォルトフォールバック**：`'auto'`（汎用設定）

検出後、`_resolve_credentials` が推論結果に基づいてデフォルトの `base_url` と API キーを補完します。

### ローカルモデル対応

2つのローカル推論バックエンドがサポートされています：

- **VLLM**：高性能推論、`python -m vllm.entrypoints.openai.api_server` で起動し、OpenAI 互換エンドポイントを公開
- **Ollama**：ワンクリックのローカルモデル管理 — `ollama run llama3` でサービス起動

両方とも標準の OpenAI インターフェースを通じて接続され、フレームワーク側の特別な処理は不要です。

## 設計原則

1. **ゼロコード切替**：環境変数のみでプロバイダーを変更
2. **プロバイダー透過性**：エージェントコードはどの LLM を使用しているかを認識しない
3. **容易な拡張**：1クラスのサブクラス化、1メソッドのオーバーライドでプロバイダーを追加
4. **適切なデフォルト**：各プロバイダーに事前設定された base_url とデフォルトモデル

## Related

- [[hello-agents-framework]] — HelloAgents フレームワーク概要
- [[agent-paradigms]] — この LLM 層を使用する5つのエージェントパラダイム
