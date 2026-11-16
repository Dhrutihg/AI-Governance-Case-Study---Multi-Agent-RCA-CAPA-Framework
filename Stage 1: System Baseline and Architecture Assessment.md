# AI Governance Portfolio — Stage 1: System Baseline and Architecture Assessment

## 1. Overview

This project is an AI-assisted, multi-agent Root Cause Analysis (RCA) and Corrective and Preventive Action (CAPA) framework designed to support software engineering quality processes.

The framework uses multiple specialised AI agents to analyse customer-reported software defects, identify similar historical issues, generate root cause hypotheses, classify defects and recommend corrective and preventive actions.

The objective is to reduce the manual effort involved in defect investigation, identify recurring and systemic issues, and help engineering and quality teams improve RCA effectiveness.

This assessment establishes the system's functional baseline, architecture, data flows, human decision boundaries and implementation maturity as the foundation for a structured AI governance assessment.

## 2. Business Purpose and Intended Users

The framework was developed to address three primary objectives:

- Reduce the time engineers spend investigating software defects.
- Identify recurring and systemic issues that require corrective action.
- Enable engineers to leverage historical defect information and similar-bug analysis to improve root cause investigations.

**Intended users:**

| User group | Intended use |
|---|---|
| Individual engineers | Investigate individual defects and review similar historical bugs |
| Management | Review systemic issues and defect trends |
| Quality Engineers | Use individual and systemic findings to drive CAPA activities |

## 3. Scope

The current framework focuses on selected firmware components:

- BIOS
- Connectivity
- Selected drivers

These components were selected because they experience relatively higher volumes of customer-reported defects compared with other software components.

The framework is not intended to process every software defect across the organisation.

## 4. System Architecture

The framework consists of eight specialised AI agents coordinated by an Orchestrator.

| Agent | Responsibility |
|---|---|
| Orchestrator Agent | Coordinates agent execution, manages workflow progression and displays agent-to-agent progress |
| Context Assembly Agent | Retrieves defect information, resolution comments, conversation comments and Git commit messages |
| Similarity Analysis Agent | Identifies similar historical defects using TF-IDF cosine similarity, rule-based and LLM-based methods, and Reciprocal Rank Fusion (RRF) |
| RCA Agent | Generates root cause analysis using an LLM-based approach, with rule-based fallback |
| Categorisation Agent | Classifies issues and root causes into predefined categories |
| CAPA Agent | Recommends corrective and preventive actions based on RCA and contextual information |
| Validation and Verification Agent | Checks defect-report completeness and evaluates RCA/CAPA confidence using relevance checks and evidence-based scoring |
| Reporting Agent | Generates reports and metrics using AI-generated information and human feedback |

### Technology Stack

| Technology / Component | Usage |
|---|---|
| OpenAI GPT-4 | LLM used for analysis and recommendations |
| Internal organisational AI gateway | Provides access to the LLM |
| SSO and Personal Access Token (PAT) | Authentication for gateway and Databricks access |
| TF-IDF cosine similarity | Text vectorisation and similarity calculation |
| ChromaDB | Vector database and storage of AI-generated outputs |
| Databricks | Source defect data and destination for human-approved outputs |
| VS Code | Current development and execution environment |

The framework is currently a development-stage prototype and has not yet been fully deployed.

## 5. Execution Workflow

The framework supports two execution modes.

**Individual defect analysis**
- User provides the bug tenant name and bug ID.
- The framework retrieves the corresponding defect information.
- The multi-agent workflow performs RCA and CAPA generation.

**Query-driven batch analysis**
- User enters a defect query through the web interface.
- Matching defects are extracted.
- The Orchestrator iterates through the returned defect list and initiates RCA for each defect.

The web interface displays agent-to-agent execution progress. Individual bug-level progress tracking is not currently available.

If processing fails for a defect during batch execution, the batch stops and displays an error. The user must refresh the webpage and repeat the operation.

## 6. Data Architecture and Storage

The framework uses Databricks and ChromaDB for different data-storage purposes.

| Data category | Storage location | Purpose |
|---|---|---|
| Original defect data | Databricks | Source engineering information |
| Vector data | ChromaDB | Similarity-based historical defect retrieval |
| AI-generated RCA/CAPA | ChromaDB | Storage of generated analysis |
| Human feedback and rejected outputs | ChromaDB | Retention of AI-generated and associated review information |
| Human-approved RCA/CAPA | Databricks | Accepted analysis transferred to the engineering data environment |

The vector database is incrementally updated with historical defect information. Only closed defects are indexed.

Pickle (`.pkl`) files are also present in the project directory; their exact role in the storage implementation remains to be verified.

## 7. Human Oversight and Decision Boundaries

The framework is designed as a decision-support system rather than an autonomous engineering system.

AI-generated RCA and corresponding CAPA recommendations are presented to the reviewer in tabular form, accompanied by reasoning and confidence scores.

The interface provides:
- Individual bug approval and rejection.
- Approve-all and reject-all options for batch processing.

**Human approval is required before AI-generated results are transferred to Databricks.**

The AI framework:
- Can retrieve and analyse defect information.
- Can identify similar historical defects.
- Can generate RCA and CAPA recommendations.
- Can categorise defects and calculate confidence scores.
- Cannot independently approve its recommendations.
- Cannot modify original defect records.
- Cannot independently write AI-generated results to Databricks.

Rejected AI-generated outputs remain in ChromaDB and are not transferred to Databricks.

This establishes a human approval boundary between AI-generated recommendations and accepted engineering records.

## 8. Implementation Status

An important part of the baseline assessment is distinguishing implemented functionality from planned enhancements.

### Implemented

- Eight-agent multi-agent architecture.
- Individual and query-driven batch RCA.
- Historical defect similarity analysis.
- LLM-based RCA and CAPA generation.
- Defect categorisation.
- Confidence-based validation and verification.
- Tabular presentation of RCA, CAPA, reasoning and confidence scores.
- Individual and batch-level human approval/rejection.
- Storage of AI-generated outputs in ChromaDB.
- Transfer of human-approved outputs to Databricks.
- Prevention of independent AI modification of engineering records.

### Planned but Not Implemented

A human feedback-driven reanalysis mechanism was part of the intended design but was not completed.

The proposed functionality includes:

1. Reviewer enters corrected RCA and CAPA when rejecting an AI-generated recommendation.
2. Corrected human input is fed back into the framework.
3. The framework performs one additional RCA/CAPA analysis.
4. If the second output is rejected, it remains outside the official Databricks records.

These capabilities are documented as planned enhancements and are not considered existing operational controls.

## 9. Initial Governance Assessment Boundaries

The baseline exercise identified several areas requiring further technical verification before governance conclusions can be drawn.

| Assessment area | Open questions |
|---|---|
| Data governance | What defect information is transmitted through the internal AI gateway? |
| Access management | How are PATs stored, rotated and revoked? |
| Database security | What authentication and access restrictions protect ChromaDB? |
| Data lineage | How are AI-generated, rejected and accepted records linked across ChromaDB and Databricks? |
| Model governance | How are model versions and changes managed? |
| Confidence assessment | How are confidence scores calculated, thresholded and validated? |
| Retrieval quality | How are historical defects selected and ranked, and are review outcomes distinguished? |
| Operational resilience | How are batch failures, partial results and duplicate processing handled? |
| Monitoring | What execution, quality and decision information is logged and monitored? |
| Deployment governance | What controls will be introduced before production deployment? |

These are open assessment questions, not confirmed system deficiencies.

## 10. Stage 1 Outcome

Stage 1 established a functional and architectural baseline of the AI-assisted RCA/CAPA framework.

The assessment documented:

- Business purpose and intended users.
- System scope and architecture.
- AI technology and data-storage components.
- Execution and processing workflows.
- Human oversight and decision boundaries.
- Implemented versus planned functionality.
- Areas requiring additional technical verification.

This baseline provides the reference point for the next stage: **AI Risk Identification and Assessment**.

The subsequent assessment will examine potential risks associated with data quality, model behaviour, retrieval accuracy, human oversight, security, operational reliability and AI-generated recommendations.

---

**Assessment approach:** Evidence-based, lifecycle-oriented AI governance.

**Current system maturity:** Development-stage prototype.

**Important limitation:** This assessment documents the architecture and functionality understood at the time of review. Technical controls not independently verified are explicitly retained as open questions.
