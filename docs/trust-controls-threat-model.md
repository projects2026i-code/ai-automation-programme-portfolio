# Trust & Controls Threat Model

This document maps the six core AI risk categories to the controls
implemented (or planned) in this RAG system.

| Risk | What it means | Control |
|---|---|---|
| Sensitive data leakage | The model exposes private/confidential info in its answer | Redact PII before logging queries/responses; restrict source documents to non-confidential content |
| Toxicity | Model produces offensive or harmful language | Output content filter (Azure AI Content Safety) checks responses before returning to user |
| Prompt injection | A malicious instruction hidden in a document or query tries to hijack the model | Guardrail step validates/sanitizes incoming queries before they reach retrieval |
| Jailbreaking | User tries to bypass the system's intended behaviour | System prompt hardened with explicit refusal instructions; tested against common jailbreak phrasing |
| Insecure outputs | Model output used downstream without validation (e.g. in code or automation) | Output schema/format validated before being passed to any downstream action |
| Model security | Unauthorized access to the model endpoint or leaked credentials | Model accessed via managed identity, not API keys hardcoded in code; access scoped via RBAC |

**Status:** controls marked above reflect the current design intent for
this portfolio project. Where a control is not yet implemented in code,
it is documented here as the intended architecture — consistent with
how enterprise AI Trust & Controls layers are typically designed before
full technical enforcement is built out.
