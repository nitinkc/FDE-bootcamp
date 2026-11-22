# Lesson 03 — Cloud Core

*Phase 1 · Cloud questions — cloud-agnostic, with GCP / AWS / Azure service names.*

## Compute: pick the right abstraction

Same three choices on every cloud — managed containers, Kubernetes, raw VMs:

| Abstraction | GCP | AWS | Azure |
| --- | --- | --- | --- |
| Serverless containers | **Cloud Run** | App Runner / Fargate (on ECS) | Container Apps |
| Managed Kubernetes | **GKE** | EKS | AKS |
| Virtual machines | **Compute Engine (GCE)** | EC2 | Virtual Machines |
| Functions (bonus) | Cloud Functions | Lambda | Azure Functions |

**Decision logic (same everywhere):**

- **Serverless containers** — default for stateless HTTP services: scale-to-zero,
  pay-per-request, minimal ops. Trade-offs: cold starts, request time limits,
  less control.
- **Kubernetes** — when you need orchestration control: long-running processes,
  custom networking, sidecars, stateful workloads, existing k8s estate. Costs
  you real ops burden.
- **VMs** — workloads that don't fit containers or need specific OS/hardware.
- **Answer style:** name the default *and* the trade-offs — don't recite
  feature lists.

## Private DB connectivity + secrets

The question "how does a service securely reach a private database and a
password?" has the same three-part answer on every cloud:

| Need | GCP | AWS | Azure |
| --- | --- | --- | --- |
| Private network path | VPC connector / private IP | VPC, PrivateLink, RDS in private subnet | VNet integration, Private Endpoint |
| Secrets store | **Secret Manager** | Secrets Manager | **Key Vault** |
| Workload identity | Service account | IAM role / instance profile | **Managed Identity** |

- DB lives on **private IP only**, never publicly exposed.
- Secret mounted as env var/volume; the workload identity gets read access to
  *that secret only*.
- Dedicated identity per service, least-privilege — e.g. a DB-client role, not
  broad admin.

## Messaging vs direct HTTP

| Pattern | GCP | AWS | Azure |
| --- | --- | --- | --- |
| Pub/sub messaging | **Pub/Sub** | SNS + SQS | Service Bus / Event Grid |
| Direct call | HTTP/gRPC | HTTP/gRPC | HTTP/gRPC |

Use a queue/topic when you need:

- **Decoupling** — producer doesn't know or wait for consumers.
- **Retries & backpressure** — messages buffer when consumers are slow/down.
- **Fan-out** — one event, many independent consumers.
- **Async work** — kick off slow jobs without holding a request open.

**Cost:** added operational complexity (ordering, dedup, DLQs, lag monitoring).
Direct HTTP is fine for synchronous request/reply where the caller needs the
result now.

## Least-privilege IAM

Same rules on every cloud:

- One **identity per service/function** — no shared credentials (SA / IAM role
  / managed identity).
- **Fine-grained roles over broad ones** — e.g. read-one-bucket, never
  owner/editor/AdministratorAccess/Contributor-at-subscription.
- **Never embed keys in code or images** — use attached identities (attached
  SA, instance profile/IRSA, managed identity). No downloadable key files.
- Grant on the **narrowest resource** possible (one bucket/container, not the
  project/account/subscription).
- **Audit logging on:** Cloud Audit Logs / CloudTrail / Azure Activity Log.
- Review permissions periodically — privilege accumulates.

## Quick glossary

Object storage: **GCS / S3 / Blob Storage** · Data warehouse: **BigQuery /
Redshift / Synapse (Fabric)** · Managed K8s: **GKE / EKS / AKS** ·
Container registry: **Artifact Registry / ECR / ACR** ·
Secrets: **Secret Manager / Secrets Manager / Key Vault**.
