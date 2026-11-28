# FDE Prep Journal

**specialization**: Generative AI, Agentic Systems, Cloud AI Platforms, Enterprise AI Deployments.

A Forward Deployed Engineer (FDE) operates at the intersection of **Senior Software Engineering**, **Applied AI/Data
Systems**, and **Client-Facing Solutions Architecture**.

Unlike internal platform developers, an FDE must rapidly ingest legacy enterprise data,
build production-grade AI/data pipelines, and deploy secure architectures directly into varied customer
environments under real-world constraints.

---

### Stages & Milestones

#### STAGE 1: LEARN — Systems Foundations, Data Engineering & Cloud

##### The FDE Mindset & Advanced Production Python

* **FDE Role Dynamics:** FDE vs. Software Engineer, Applied AI Scientist, and Solutions Architect; cultivating a
  **customer-first engineering mindset** and decomposing **ambiguous** business outcomes into technical specifications.
* **Modern Python Deep Dive:** Structural pattern matching, Protocol classes (structural subtyping), async/await
  execution patterns (`asyncio`), strict type enforcement (`mypy`), Pydantic V2 models.
* **Production Standards:** Structured logging (`structlog`), defensive exception handling, package isolation (`uv` or
  `poetry`), unit and integration test suites with `pytest` (fixtures, mocking, parameterized tests).

**Hands-on Lab:** Build an asynchronous, production-hardened Python utility library with automated schema validation,
error boundaries, and >90% test coverage.

##### Enterprise API Engineering with FastAPI

* **API Architecture:** REST principles, ASGI lifecycle management, asynchronous request handling, dependency injection
  paradigms.
* **Security & Access Control:** OAuth2 with JWT bearer tokens, role-based access control (RBAC), API key generation and
  rotation, TLS/SSL termination concepts.
* **Production Operations:** API versioning patterns (`/api/v1`), automated OpenAPI/Swagger generation, rate limiting
  (Redis token-bucket algorithm), custom middleware (correlation IDs, request latency tracing).

**Hands-on Lab:** Develop and test a secure, multi-tenant FastAPI backend service featuring authentication, rate
limiting, and dynamic Swagger documentation.

##### Enterprise Data Ingestion, Processing & Delta Lake

* **Databases & Query Optimization:** Advanced SQL (CTEs, Window functions, indexing strategies, query execution plan
  analysis).
* **Data Processing Frameworks:** Batch vs. Streaming, ETL vs. ELT architectures, schema drift handling, Pandas vs.
  Polars vs. PySpark.
* **Lakehouse Fundamentals:** Delta Lake core mechanics (ACID transactions, time travel, Parquet layout), Databricks
  workspace fundamentals.
* **Data Quality & Validation:** Great Expectations / Pydantic schema validation, handling corrupted records, Dead
  Letter Queue (DLQ) implementations.

**Hands-on Lab:** Construct an enterprise data pipeline that cleans, validates, and ingests dirty semi-structured data
into Delta tables, quarantining corrupt rows into a DLQ.

##### Dual-Cloud Infrastructure (AWS & Azure Foundations)

* **AWS Core Services:** IAM least-privilege policies, S3 lifecycle management, Lambda serverless triggers, API Gateway
  routing, VPC networking and endpoints.
* **Azure Core Services:** Azure Blob Storage, Azure Functions, Key Vault secrets management, Managed Identities, Azure
  AI Foundry/Services setup.
* **Infrastructure as Code (IaC):** Terraform basics for cloud provisioning and environment reproducibility.

**Hands-on Lab:** Provision infrastructure and deploy a containerized backend service across both an AWS (ECS/Fargate)
and Azure (Container Apps) environment using Terraform.

---

#### STAGE 2: BUILD — Applied GenAI, RAG, Multi-Agent Systems & Connectors

##### LLM Architectures, Prompt Engineering & Model Selection

* **Model Mechanics:** Context window management, attention mechanisms, BPE tokenization, structured JSON schema outputs
  (`instructor`, native tool calling).
* **Prompt Engineering & Strategies:** Few-shot prompting, chain-of-thought, system prompt design, prompt decomposition.
* **Model Selection Economics:** Frontier models (GPT-4o, Claude 3.5 Sonnet, Gemini 1.5 Pro) vs. Open-Weights (Llama
  3.1, Mistral); tokens-per-second, time-to-first-token (TTFT), and cost-per-million-tokens analysis.

**Hands-on Lab:** Build an automated evaluation harness that benchmarks 4 models across structured data extraction
accuracy, latency, and cost for a domain-specific dataset.

##### Production Retrieval-Augmented Generation (RAG)

* **Ingestion & Parsing:** Chunking heuristics (semantic, recursive character, layout-aware), tabular data parsing,
  metadata tagging.
* **Dense, Sparse & Hybrid Search:** Dense embeddings (`text-embedding-3-large`), BM25 lexical search, reciprocal rank
  fusion (RRF), cross-encoder re-ranking (Cohere Rerank).
* **Vector Store Management:** HNSW vs. IVFFlat indexing, hands-on configuration of pgvector, Pinecone, Chroma, and
  Azure AI Search.
* **Mitigating Failure Modes:** Hallucination reduction, citation grounding, guardrailed document search via LangChain
  and LlamaIndex.

**Hands-on Lab:** Build an enterprise Document Assistant capable of hybrid search, cross-encoder re-ranking, and
verified source-citation attribution over technical policy PDFs.

##### Autonomous Agents & Multi-Agent Orchestration

* **Agent Architecture:** ReAct loop, tool calling, execution planning, reflection/critic loops, short-term vs.
  long-term memory management.
* **Multi-Agent Coordination:** Agent-to-Agent (A2A) handoffs, role specializations, Model Context Protocol (MCP)
  standards.
* **Framework Implementations:** LangGraph, CrewAI, OpenAI Agents SDK, and Amazon Bedrock Agents.
* **Human-in-the-Loop (HITL):** State interruption, approval checkpoints, dynamic human override routing.

**Hands-on Lab:** Build a multi-agent analyst team in LangGraph that breaks down complex research tasks, executes
SQL/web tool searches, reflects on accuracy, and requires human sign-off before publishing findings.

##### Enterprise Platform Connectors & Systems Integration

* **Workplace Ecosystems:** Microsoft Graph API, SharePoint folder sync, Slack Bolt SDK, and Microsoft Teams bot
  integrations.
* **Enterprise SaaS Platforms:** Jira and Confluence REST APIs, ServiceNow incident routing, Salesforce CRM query
  pipelines, SAP connectivity patterns.
* **Data Warehouse Access:** Query federation with Databricks SQL warehouses and Snowflake.

**Hands-on Lab:** Connect your multi-agent system to ingest incidents from Jira, cross-reference documentation in
Confluence/SharePoint, and stage draft resolution messages in Slack.

---

#### STAGE 3: DEPLOY — Containers, Kubernetes & Production CI/CD

##### Docker, Kubernetes & Packaging

* **Containerization:** Multi-stage Docker builds, image size optimization, non-root user execution, vulnerability
  scanning (Trivy).
* **Orchestration Fundamentals:** Kubernetes pods, deployments, services, ingress controllers, config maps, and cloud
  secrets integration.

**Hands-on Lab:** Containerize the full multi-agent application and deploy it locally on Minikube/k3s with
health/readiness probes and horizontal pod autoscaling rules.

##### CI/CD Pipelines & GitOps

* **Automated Pipelines:** GitHub Actions workflows (linting, automated testing, container build, image push to
  ECR/ACR).
* **Production Deployment Strategies:** Rolling updates, Blue/Green deployments, Canary rollouts, automated rollback
  triggers.

**Hands-on Lab:** Build an end-to-end GitHub Actions pipeline that runs test suites on PRs, builds signed containers,
and executes zero-downtime deployments to a cloud staging cluster.

---

#### STAGES 4 & 5: MONITOR & OPTIMIZE — Security, Observability & Tuning

##### Enterprise AI Security, Governance & Guardrails

* **Threat Modeling:** Prompt injection attacks (direct/indirect), jailbreaks, data exfiltration, adversarial payload
  detection.
* **AI Guardrails:** NeMo Guardrails, Llama Guard, PII/PHI automated redaction/tokenization (HIPAA/SOC2 compliance),
  Role-Based Access Control (RBAC) at the retrieval level.
* **Responsible AI & Governance:** Audit trails, determinism bounds, license compliance.

**Hands-on Lab:** Build an inline security proxy that enforces enterprise RBAC, sanitizes incoming queries against
prompt injections, and masks sensitive PII before upstream inference.

##### Observability, LLMOps & Cost/Latency Optimization

* **Distributed Tracing:** OpenTelemetry, Langfuse / Arize Phoenix integration, visualizing full execution graphs, token
  consumption, and step latencies.
* **Evaluation Frameworks:** RAGAS (Faithfulness, Answer Relevance, Context Recall), DeepEval, regression CI/CD gates.
* **Cost & Latency Engineering:** Semantic caching with Redis, prompt compression, intelligent model routing (triage
  with light models $\rightarrow$ escalate to frontier models).

**Hands-on Lab:** Instrument the agent pipeline with Langfuse, run a 100-query automated evaluation suite, and implement
semantic caching to reduce API costs by 30%+.

---

#### STAGE 6: PRESENT — Customer Discovery, Architecture & Proposal Defense

##### Customer Discovery Workshops & Technical Architecture

* **Discovery Methodologies:** Requirements gathering, business process mapping, identifying technical vs.
  organizational bottlenecks.
* **Handling Ambiguity:** Converting high-level, vague customer requests into concrete, measurable Technical
  Architecture Documents (TADs).
* **Architecture Communication:** High-level executive diagrams vs. low-level technical sequence diagrams, data flow
  modeling, risk and dependency matrices.

**Workshop:** Given an ambiguous 1-page business scenario, lead a mock discovery session and produce an end-to-end
Technical Architecture Document.

##### Technical Proposal Writing & Client Demos

* **Proposal Development:** Executive summaries, technical feasibility, project phasing, ROI calculations, and total
  cost of ownership (TCO) modeling.
* **Rapid Prototyping & Demos:** Building executive-ready user interfaces (Streamlit / Next.js / Chainlit) designed for
  non-technical buyer validation.
* **Change Management:** Planning customer onboarding, training, and production support handovers.

**Workshop:** Deliver a 30-minute mock executive pitch proposing an enterprise AI solution, defending business ROI,
latency benchmarks, and data safety to a non-technical board.

---

#### STAGE 7: GET HIRED / CLIENT DEPLOYED — Capstone & Technical Defense

##### Enterprise Capstone Project & Production Gate

Engineers pick one enterprise scenario and execute it across all 5 operational phases:

* **Phase 1 – Discovery:** Client discovery, requirements matrix, business process mapping.
* **Phase 2 – Solution Design:** Solution architecture, data flow diagrams, integration design, threat modeling.
* **Phase 3 – Development:** Secure FastAPI backend, RAG pipeline, multi-agent systems, enterprise connectors.
* **Phase 4 – Deployment:** Cloud deployment (AWS/Azure), CI/CD, Langfuse observability, security validation.
* **Phase 5 – Delivery:** Customer demo, business ROI presentation, technical runbook documentation, handover.

---

### 3. Financial Budget & Cost Breakdown

The table below outlines the estimated budget - working in a dedicated sandbox environment across the entire program.

| Category                           | Component / Service                                              | Purpose                                                  | Estimated Cost (USD) |
|:-----------------------------------|:-----------------------------------------------------------------|:---------------------------------------------------------|:---------------------|
| **Cloud Infrastructure**           | Compute (ECS Fargate / small EKS cluster, 2–4 vCPU nodes)        | Lab microservice and pipeline hosting                    | $140 – $180          |
|                                    | Storage & Serverless (S3, RDS PostgreSQL / Aurora Serverless v2) | Raw file storage, relational data, and vector indexing   | $60 – $80            |
|                                    | Networking & Security (NAT Gateway, VPC endpoints, ALB)          | Secure environment isolation & routing                   | $40 – $60            |
| **Model & Inference APIs**         | OpenAI / Anthropic APIs (GPT-4o, Claude 3.5 Sonnet)              | Query routing, agentic execution, and response synthesis | $100 – $150          |
|                                    | Embedding APIs (text-embedding-3-large, Cohere Rerank)           | Semantic search & chunk evaluation                       | $20 – $30            |
|                                    | Open-Source GPU Lab (RunPod / Modal / on-demand g5.xlarge)       | 20–30 hours of open-source hosting (vLLM, Llama-3.1-8B)  | $50 – $75            |
| **Tooling & SaaS Sandboxes**       | Managed Vector DB (Pinecone / Qdrant Cloud - Standard tier)      | Vector persistence and hybrid query labs                 | $30 – $50            |
|                                    | LLMOps & Observability (Langfuse / Arize / Postman Team)         | Trace analysis, latency inspection, and evals            | $0 – $25             |
| **Total Estimated Cost per Batch** |                                                                  |                                                          | **$440 – $600**      |

### 4. Capstone Projects (Select 1)

Each engineer chooses one real-world enterprise scenario to implement:

#### Option A: The Legacy Enterprise Operational Copilot (RAG & Security Focus)

* **Scenario:** A customer has a decade of semi-structured operational case notes distributed across relational tables,
  PDF summaries, and CSV exports.
* **Core Requirements:**
    1. Build an automated ingestion pipeline that cleans, deduplicates, and chunks historical records.
    2. Implement an agentic query engine that handles both temporal filters (e.g., *"Show occurrences in Q3 2024"*) and
       dense semantic retrieval.
    3. Enforce strict PII/PHI redaction prior to passing payloads to external LLM endpoints.
    4. Create an automated evaluation suite testing 50+ golden queries on context recall, answer relevance, and
       faithfulness.

* **Pass Standard:** Sub-1.5s p95 latency, 0% PII leakage, and >90% faithfulness on RAGAS benchmarks.

#### Option B: Real-Time Telemetry & Alerting Agent (Streaming & Automation Focus)

* **Scenario:** A client requires an autonomous monitoring system that continuously processes operational telemetry,
  flags anomalies, and prepares automated incident reports.
* **Core Requirements:**
    1. Build a Kafka/Kinesis stream processing synthetic application logs.
    2. Implement a sliding-window anomaly detector using Polars/DuckDB.
    3. When an anomaly triggers, dispatch an LLM-powered incident diagnostic agent that pulls relevant runbooks,
       generates a root-cause summary, and constructs a validated Jira/Slack payload.
    4. Package the infrastructure in Terraform for deployment into a customer AWS account.

* **Pass Standard:** Zero message loss during simulated 5x traffic spikes; fully deterministic, schema-valid payload
  delivery.

---

### Readiness Gate: Final Deployment Verification

To complete the program and be cleared for live enterprise client engagements, the engineer must pass three gates:

1. **Production Code Audit:** Peer review of the capstone repository assessing modularity, error recovery, Docker
   security, and >85% test coverage.
2. **"The Hot Seat" Architecture Defense:** A 60-minute technical session where senior leads roleplay as enterprise
   customer architects, probing security boundaries, disaster recovery, latency bottlenecks, and cloud cost scaling.
3. **Turnkey Operational Runbook:** Verification of an operational deployment guide allowing another engineer to
   provision, run, and trace the entire capstone stack with reproducible IaC scripts.