# Enterprise Workflow Automation Programme
## AI-Powered Operational Efficiency Transformation

### Business Problem
- Manual processes: 4.2-hour average cycle time per job
- Output: 120 jobs/day with 12 manual touch-points per job
- Staff frustration: 55% report time wasted on manual work
- No visibility into bottlenecks or exceptions

### Solution
Designed and implemented workflow automation platform using AI-assisted process analysis, resulting in:
- **40% output increase** (120 → 168 jobs/day)
- **31% cycle time reduction** (4.2hrs → 2.9hrs)
- **58% fewer manual touch-points** (12 → 5 per job)
- **23.2x ROI** in first 3 months (£68k investment, £1.58M annual benefit)

### Architecture
**System Design:**
- Workflow automation platform (low-code)
- Real-time agility dashboards
- Exception handling & escalation framework
- Integration with existing systems (ERP, CRM, dispatch)

**Key Capabilities:**
- Process redesign with automation mapping
- Agile workflow execution (checkpoint-based, not batch)
- Real-time KPI tracking
- Automated escalation for exceptions
- Staff training & change management

### Results (3 months)
| Metric | Baseline | Month 3 | Improvement |
|--------|----------|---------|-------------|
| Jobs/day | 120 | 168 | +40% ✅ |
| Cycle time | 4.2 hrs | 2.9 hrs | -31% ✅ |
| Manual touch-points | 12 | 5 | -58% ✅ |
| Rework rate | 8% | 3.5% | -56% ✅ |
| Staff utilisation | 75% | 89% | +11% ✅ |
| **Annual ROI** | — | — | **23.2x** ✅ |

### Challenges & Learnings
**What went well:**
- Peer champions model drove 88% adoption (target 70%)
- Rapid iteration (1-week release cycles) improved quality week-over-week
- Strong sponsor engagement enabled quick decision-making

**What didn't go well:**
- Vendor integration complexity underestimated (3-week delay)
- Data quality assessment should have happened earlier
- Change management underestimated job security concerns (2-week union delay)

**Key lessons:**
- Invest in peer champions; they drive adoption
- Budget integration work heavily; legacy systems are complex
- Engage change stakeholders (unions, HR) early, not late
- Fast iteration works; quality improved week-over-week

### Portfolio Artefacts
- **Demo video:** 90-second walkthrough of automation platform and AI-assisted analysis
- **Programme documents:**
  - RAID Log (risks, assumptions, issues, dependencies)
  - Status Reports (Month 1: Green | Month 3: Yellow/manageable)
  - SOP (Standard Operating Procedure for platform operations)
  - Project Charter (business case, objectives, timeline, budget)
  - Meeting Notes (stakeholder requirements workshop)
  - Lessons Learned (retrospective with recommendations)

### Technologies & Skills Demonstrated
- **Programme management:** RAID tracking, risk management, dependency mapping, stakeholder engagement
- **Business transformation:** Process redesign, workflow automation, agile adoption, change management
- **AI/automation:** Process automation analysis, workflow design, exception handling, user adoption
- **Delivery:** Phase-based implementation, team scaling (20 → 60 staff), budget tracking, ROI measurement
- **Leadership:** Sponsor engagement, peer champion model, escalation management, team sustainability

### What I'd Do Differently (Phase 3)
1. Conduct full data audit in Phase 1 (discovered issues late)
2. Engage unions and change stakeholders 12 weeks before go-live (not 6)
3. Budget 4 weeks for UAT minimum (don't compress timelines)
4. Add SLA penalties to vendor contracts (incentivise performance)
5. Assess team workload early; hire support roles proactively (avoid burnout)

### Why This Matters
This programme demonstrates the intersection of **enterprise transformation + AI + delivery excellence** that modern Solutions Architects need. It's not just about technology — it's about:
- Understanding the business problem (cycle time, capacity, cost)
- Designing the right solution (automation, not just technology)
- Managing the human/organisational change (adoption, sustainability)
- Measuring what matters (ROI, not just feature count)
- Leading through complexity (vendor delays, scope changes, escalations)

---## RAG + Agent Orchestration (agent_orchestration_build.ipynb)

A working retrieval-augmented generation system with LangGraph agent
orchestration, built on Azure OpenAI (gpt-5-mini).

**Architecture:** guardrail → retrieve → grade → rewrite (if needed) → answer

- **Preventative control:** guardrail node blocks unsafe/malicious queries
  before retrieval
- **Detective control:** retrieval grading scores relevance before
  generating an answer
- **Corrective control:** low-relevance retrieval triggers an automatic
  query rewrite and retry (max 2 attempts)
- **Grounding:** answers are generated only from retrieved document
  context, with source citation; the system explicitly refuses to answer
  when it lacks sufficient grounded information, rather than hallucinating

**Data pipeline:** source documents were scanned PDFs with no text layer;
built an OCR ingestion step (Tesseract) to extract text before chunking
and retrieval — a common real-world RAG ingestion challenge.

**Known limitation:** retrieval uses TF-IDF (keyword-based) rather than
semantic embeddings, since no embedding model was deployed for this
build. A production version would use Azure AI Search with vector
embeddings for stronger semantic matching.

Maps directly to the Trust & Controls threat model
(`docs/trust-controls-threat-model.md`) — this notebook is a working
implementation of 3 of the 6 documented risk controls.

**Programme Manager | Enterprise Transformation | AI-Assisted Automation | Process Design**
**Event-driven processing:** claim events are submitted to an Azure
Storage Queue (`claims-intake-queue`) rather than triggering the agent
directly — a producer/consumer pattern that decouples submission from
processing. The consumer polls the queue, runs each event through the
full agent pipeline, and deletes the message once processed.

**Production evolution:** this notebook polls manually; a production
deployment would use an Azure Function with a Queue trigger to process
events automatically as they arrive, removing the need for manual
polling.

