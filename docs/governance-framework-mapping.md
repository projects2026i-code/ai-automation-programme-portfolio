# Governance Framework Mapping

This document maps this project's Trust & Controls design to three
major AI governance frameworks referenced in enterprise AI architecture
roles: ISO/IEC 42001, the NIST AI Risk Management Framework, and the
EU AI Act.

## ISO/IEC 42001 (AI Management System)

| Clause area | How this project addresses it |
|---|---|
| Risk assessment | Threat model (see trust-controls-threat-model.md) identifies 6 core AI risks |
| Roles & responsibilities | Architecture documented via ADRs, assigning ownership of each control |
| Operational controls | Guardrail, content filter, output validation steps designed into the pipeline |
| Continuous improvement | Golden evaluation set enables ongoing measurement of retrieval/answer quality |

## NIST AI Risk Management Framework (Govern / Map / Measure / Manage)

| Function | How this project addresses it |
|---|---|
| Govern | Trust & Controls threat model defines ownership and intended controls |
| Map | Architecture diagram + NFR table identify where risks enter the system |
| Measure | Golden evaluation set measures retrieval hit-rate and answer quality |
| Manage | Guardrail/grading/rewrite steps actively respond to detected issues at runtime |

## EU AI Act

| Consideration | How this project addresses it |
|---|---|
| Risk tiering | This system (internal knowledge assistant) sits at limited/minimal risk tier, not high-risk (no automated decisions affecting individuals' legal rights) |
| Transparency | Users are informed they are interacting with an AI-grounded assistant with citations |
| Human oversight | Insecure/uncertain outputs are flagged rather than auto-actioned; human review retained for high-stakes decisions |

**Status:** this mapping documents architectural intent and vocabulary
alignment for a portfolio project. It is not a formal compliance
assessment.
