# AI Governance Case Study: Multi-Agent RCA/CAPA Framework

## Overview

This repository presents an experience-based AI Governance case study of a multi-agent, AI-assisted Root Cause Analysis (RCA) and Corrective and Preventive Action (CAPA) framework designed to support software engineering quality processes.

The framework uses specialised AI agents to analyse software defects, retrieve similar historical issues, generate root cause hypotheses, categorise defects, and recommend corrective and preventive actions and generate reports and trends based on underlying data.

The system is designed as a decision-support solution, with human reviewers retaining authority over AI-generated recommendations and their acceptance into the engineering data environment.

This case study examines how AI governance principles can be evaluated and applied to a practical, multi-agent AI system.

## Objectives

The case study aims to:

- Document the architecture, functionality and decision boundaries of a multi-agent AI system.
- Identify potential AI risks across data, models, retrieval, security, human oversight and operational processes.
- Evaluate existing governance mechanisms within the described system.
- Identify governance gaps and areas requiring further technical verification.
- Recommend practical controls to improve responsible AI deployment and operation.
- Demonstrate the application of structured AI risk assessment and governance principles to an engineering use case.

## System at a Glance

| Attribute | Description |
|---|---|
| System type | Multi-agent AI decision-support framework |
| Business domain | Software Engineering Quality |
| Primary use case | Root Cause Analysis and CAPA |
| LLM | OpenAI GPT-4 |
| AI architecture | Eight specialised agents coordinated by an orchestrator |
| Vector database | ChromaDB |
| Data platform | Databricks |
| Similarity methods | TF-IDF, rule-based and LLM-based similarity, Reciprocal Rank Fusion |
| Human oversight | Human approval required before transferring AI-generated outputs to Databricks |
| Implementation maturity | Development-stage prototype |

## Governance Assessment Approach

The case study follows an evidence-based, lifecycle-oriented approach.

It distinguishes between:

1. **Existing system capabilities:** Functionality and controls understood to have been implemented.
2. **Governance assessment:** Independent evaluation of the described system architecture and behaviour.
3. **Identified risks:** Potential risks arising from the system design and its intended use.
4. **Recommended controls:** Proposed improvements to strengthen governance, accountability and operational reliability.

Unverified technical details are explicitly identified rather than assumed.

## Project Structure

| Document | Description |
|---|---|
| [Methodology and Limitations](https://github.com/Dhrutihg/AI-Governance-Case-Study---Multi-Agent-RCA-CAPA-Framework/blob/main/Methodology%20and%20Limitations.md) | Scope, evidence basis and limitations of the case study |
| [Stage 1: System Baseline](01-system-baseline.md) | Business purpose, architecture, technology stack, workflows and human decision boundaries |
| [Stage 2: AI Risk Assessment](02-ai-risk-assessment.md) | Identification and assessment of potential AI risks |
| [Stage 3: Governance Controls](03-governance-controls.md) | Proposed governance controls and mitigation strategies |
| [Stage 4: Monitoring and Evaluation](04-monitoring-and-evaluation.md) | Governance monitoring, performance evaluation and accountability mechanisms |
| Diagrams | System architecture, agent interactions and governance workflows |

*Documents will be added as the respective assessment stages are completed.*

## Key Governance Areas

The assessment will cover the following areas:

- Data governance and privacy
- Model behaviour and reliability
- Retrieval quality and knowledge-base integrity
- Human oversight and decision accountability
- AI security and access management
- Operational resilience and failure handling
- Transparency, traceability and auditability
- Lifecycle governance and change management

## Intended Audience

This case study is intended for AI Governance professionals, Responsible AI practitioners, AI risk management professionals and engineering quality practitioners interested in applying governance principles to practical AI systems.

## Methodology and Limitations

This case study is based on my professional experience working with and developing the AI-assisted RCA/CAPA framework.

The system architecture, agent responsibilities, workflows and implementation status have been documented from my direct involvement and recollection. Following my departure from the organisation, I no longer have access to its internal development environment, source code, infrastructure, screenshots or technical documentation.


For further details, refer to [Methodology and Limitations](https://github.com/Dhrutihg/AI-Governance-Case-Study---Multi-Agent-RCA-CAPA-Framework/blob/main/Methodology%20and%20Limitations.md).

---

**Author's perspective:** This project explores how established engineering quality and risk-management practices can be applied to the governance of AI-enabled decision-support systems.
