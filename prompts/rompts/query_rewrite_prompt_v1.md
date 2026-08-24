# Query Rewrite Prompt — v1

**Used in:** agent_orchestration_build.ipynb — `rewrite_node()` function
**Purpose:** Reformulate a query into a single, more specific search query when retrieval grading scores it as poor — a corrective control in the agent's orchestration loop.

## Prompt template
Rewrite this question as ONE single, more specific search query for a document retrieval system.
Return ONLY the rewritten query text, nothing else — no options, no explanation, no numbering.

Original question: '{original}'

Rewritten query:

## Version history

- **v1** (current): fixed a bug where the model returned multiple
  candidate rewrites instead of one. Added explicit "ONLY... nothing
  else" instruction to force single-output behaviour.

## Change log for future versions
- v2 (planned): experiment with including the failed retrieval's top
  source filenames as a hint, to steer the rewrite toward better
  terminology
