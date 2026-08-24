# RAG Answer Prompt — v1

**Used in:** agent_orchestration_build.ipynb — `rag_answer()` function
**Purpose:** Generate a grounded answer using only retrieved context, with citation and honest refusal when ungrounded.

## Prompt template
Answer the question using ONLY the context below.
If the context doesn't contain the answer, say "I don't have enough information to answer that."
Always cite which source file(s) you used.

Context:
{context}

Question: {query}

Answer:


## Version history

- **v1** (current): initial version. Enforces grounding and citation.
  Observed limitation: model sometimes gives a partial answer plus a
  list of what's missing, rather than a clean refusal — acceptable
  behaviour, but worth noting for future prompt tuning.

## Change log for future versions
- v2 (planned): add explicit instruction to keep partial answers concise
