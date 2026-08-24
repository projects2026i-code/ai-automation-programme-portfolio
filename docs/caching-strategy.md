# Caching Strategy

This document describes the caching design intent for the RAG agent
(agent_orchestration_build.ipynb), addressing the LLMOps requirement
for cost and latency management in production AI systems.

## Current state (portfolio build)

No caching is implemented in this notebook — each query triggers a
fresh retrieval and a fresh LLM call, appropriate for a demonstration
build with low query volume.

## Production design

| Layer | Strategy | Rationale |
|---|---|---|
| Exact-match query cache | Cache the final answer keyed on the exact normalized query string, TTL 1 hour | Repeated identical questions (common in support/FAQ-style usage) avoid a redundant LLM call entirely |
| Retrieval cache | Cache retrieval results (top-k chunks) keyed on query, separate from the answer cache, TTL 1 hour | Allows reuse of retrieval results even if the answer-generation prompt changes (e.g. during prompt iteration) |
| Embedding cache | Not applicable to this build (TF-IDF, not embeddings) — in a production version using Azure AI Search with vector embeddings, document embeddings would be cached/persisted rather than recomputed per query | Embedding computation is the most expensive step in a true semantic RAG pipeline |
| Invalidation | Cache invalidated on source document update (new/changed PDF ingested) | Prevents serving stale answers after the knowledge base changes |

## Where this would live in production

Azure Cache for Redis, keyed by a hash of the normalized query string,
sitting between the guardrail node and the retrieve node in the
LangGraph pipeline — a cache hit would skip directly to the answer
node.
