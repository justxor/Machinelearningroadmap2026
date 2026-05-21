# 🧠 LLM Engineering — a practical course on building applications on top of large language models

A course for developers who want more than "calling GPT over an API": building reliable LLM systems — RAG, agents, tools, quality evaluation, monitoring, fine-tuning, local inference. No hype, no "become a prompt engineer in 3 days" nonsense. Only what actually works in production.

## Who this is for

- Backend developers adding LLM features to existing services.
- ML engineers moving from classical models to the LLM stack.
- Tech leads who need to understand what they are signing up for before "bolting AI on".
- Anyone who finished the [neural networks](../neural-networks/) course and wants to use transformers in a product.

## What you will leave with

- A working RAG service over your documents with quality and cost metrics.
- An agent system with tools, orchestration, and protection against infinite loops.
- A set of evals (offline and online) that catch regressions before deployment.
- Experience with fine-tuning (LoRA/QLoRA) and local inference (llama.cpp, vLLM).
- Understanding of the real economics of LLM projects: latency, token cost, caching.

## Course structure

### Part 1. LLM engineering basics

- [01. What an LLM is and how it "thinks"](./01-llm-internals.md) — tokenization, context, sampling, temperature.
- [02. Provider APIs: OpenAI, Anthropic, Google, local](./02-providers.md) — choice, limits, pricing.
- [03. Prompt engineering as an engineering discipline](./03-prompt-engineering.md) — no magic, driven by tests.
- [04. Structured output: JSON mode, schemas, function calling](./04-structured-output.md).
- [05. Context and token management](./05-context-management.md) — window, budget, trimming.

### Part 2. RAG (Retrieval-Augmented Generation)

- [06. RAG architecture: when and why](./06-rag-architecture.md) — vs fine-tuning, vs long context.
- [07. Chunking and document preprocessing](./07-chunking.md) — strategies, sizes, overlap.
- [08. Embeddings and vector databases](./08-embeddings-vectordb.md) — pgvector, Qdrant, Weaviate.
- [09. Hybrid search: BM25 + vectors + reranking](./09-hybrid-search.md).
- [10. Advanced RAG: query rewriting, HyDE, multi-hop](./10-advanced-rag.md).

### Part 3. Agents and tools

- [11. Tools / function calling: the basics](./11-tools.md) — schemas, passing, error handling.
- [12. ReAct, planning, multi-step tasks](./12-agents-react.md).
- [13. Agent orchestration: LangGraph, state machines](./13-orchestration.md).
- [14. MCP (Model Context Protocol) and connecting external systems](./14-mcp.md).
- [15. Multi-agent systems: when they pay off and when they do not](./15-multi-agent.md).

### Part 4. Quality, security, production

- [16. Evals: offline quality metrics for LLM systems](./16-evals-offline.md).
- [17. LLM-as-a-judge and automatic labeling](./17-llm-as-judge.md).
- [18. Online metrics, A/B tests, user feedback](./18-online-metrics.md).
- [19. Security: prompt injection, jailbreaks, data leakage](./19-security.md).
- [20. Cost, latency, caching, batching](./20-cost-latency.md).

### Part 5. Customization and local inference

- [21. Fine-tuning: LoRA, QLoRA, when you actually need it](./21-fine-tuning.md).
- [22. Local inference: llama.cpp, vLLM, Ollama](./22-local-inference.md).
- [23. Monitoring LLM applications in production](./23-monitoring.md) — logging, tracing, alerts.

### Capstones

- [Capstone 1. RAG assistant over corporate documents](./capstone-1-rag.md).
- [Capstone 2. Agent for automating work tasks](./capstone-2-agent.md).
- [Capstone 3. Fine-tune + local deploy of a specialized model](./capstone-3-finetune.md).

## How to study

The course follows "minimum theory — maximum practice". Each lesson: short explanation → concrete code examples → anti-patterns → 6 practice tasks → checklist. Go in order, do not skip. RAG without understanding embeddings is not RAG — it is a lottery.

## The stack we will use

- Python 3.11+, `uv` or `poetry` for dependencies.
- APIs: OpenAI, Anthropic, locals via Ollama.
- RAG: `pgvector` or Qdrant, `sentence-transformers`, `rank_bm25`.
- Agents: LangGraph, plain Python (for understanding).
- Evals: `promptfoo`, `ragas`, your own scripts.
- Deploy: FastAPI, Docker, Prometheus + Grafana for metrics.

## What you will NOT get

- "10 prompts that will change your life". A prompt without evals is fortune-telling.
- Plug-and-play "copy and sell to clients" solutions. Understanding > copy-paste.
- Promises that an LLM will solve every problem. Sometimes a regex is the right answer.

## What's next

After the course you will be able to design LLM systems consciously, defend architectural decisions with numbers, and recognize when a task simply is not for an LLM. That is exactly the "vibe-coding guru who understands how AI works inside".

---

← [Back to the main roadmap](../README.md)
