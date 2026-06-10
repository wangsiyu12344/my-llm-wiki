---
title: "LLM Fundamentals"
category: concepts
date: 2026-06-08
updated: 2026-06-08
tags: [llm, transformer, tokenization, context-window, model-types]
source: "SIYU — Discord #my-knowledge-base"
---

# LLM Fundamentals

## What is an LLM?

A Large Language Model (LLM) is a neural network — specifically a Transformer architecture — that has been pre-trained on vast amounts of internet data. Through this training, its parameters are tuned to predict the most likely next token in a sequence with remarkable accuracy.

The name **GPT** (Generative Pre-trained Transformer) captures the essence:
- **Generative**: produces text token by token
- **Pre-trained**: trained on massive internet-scale data before any specific use
- **Transformer**: the underlying neural network architecture

LLMs generate text **one token at a time** — each output is a prediction of what comes next.

## Tokens

In typical English writing:
- 1 token ≈ 4 characters
- 1 token ≈ 0.75 words
- 1,000 tokens ≈ 750 words

## Transformer Architecture

The Transformer was proposed by the Google team and replaced earlier architectures like **LSTM** (Long Short-Term Memory). LSTM's key limitation was that it was very hard to parallelize — processing had to happen sequentially. The Transformer solved this, enabling the massive scale that produces not just plausible tokens but ones that imitate intelligence with surprising accuracy.

**Parameters** are the particular arrangement of weights inside the Transformer neural network. More parameters (with sufficient data) generally means more capable models.

## Three Flavors of LLMs

1. **Base Model**: Best for fine-tuning to learn a new skill. These are raw, pre-trained models without instruction tuning.

2. **Chat Model**: Best for interactive use cases and creative content generation — e.g., writing an email, brainstorming, conversation. These are instruction-tuned for dialogue.

3. **Reasoning Model**: Best for problem solving. These models are optimized for multi-step reasoning, math, coding, and logic tasks.

## Stateless by Design

Every call to an LLM is **stateless** — the model has no memory between calls. The illusion of memory comes from passing the entire conversation history in the input prompt each time. The LLM simply predicts the most likely next tokens given the full context.

Key implications:
- The conversation context IS the "memory"
- Longer conversations consume more tokens
- No state persists between API calls

## Context Window

The **context window** is the maximum number of tokens the model can consider when generating the next token. This includes both the input prompt and the generated output. If the conversation exceeds the context window, earlier parts are lost.

## Open-Source Models

| Model | Organization |
|-------|-------------|
| **Llama** | Meta |
| **Qwen** | Alibaba Cloud |
| **DeepSeek** | DeepSeek AI |
| **GPT-OSS** | OpenAI |

## Related

- [[en/frameworks/agent-llm-abstraction]] — How agent frameworks abstract away LLM providers
- [[en/frameworks/agent-paradigms]] — Agent paradigms that build on LLM capabilities
