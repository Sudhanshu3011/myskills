# AGENTS.md — Agent Playbook & Skill Directory

This document serves as the **operational playbook and help book** for AI coding agents operating within this workspace.

---

## Mandatory Post-Code Verification Gate (The Filter)

> **CRITICAL RULES FOR ALL AGENTS:**
> 1. **Post-Code Verification**: Whenever you create, modify, or refactor code in this workspace, **you MUST NOT conclude your response or claim the task is done** until you have passed your changes through this **4-Stage Verification Filter**.
> 2. **Strict No-Emoji Policy**: **DO NOT USE EMOJIS ANYWHERE**. This applies universally to all code, comments, docstrings, markdown documentation, commit messages, file names, terminal output, and conversational responses.

```
[ Code Modified / Created ]
            │
            ▼
┌────────────────────────────────────────────────────────┐
│  Stage 1: Anti-Patterns & Code Style                   │
│  - Check python-anti-patterns & python-code-style      │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│  Stage 2: Type Safety & Contract Integrity             │
│  - Check python-type-safety & pydantic-models-py       │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│  Stage 3: Error Handling & Resilience                  │
│  - Check python-error-handling & python-resilience     │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│  Stage 4: Tests & Systematic Debugging                 │
│  - Check pytest-skill & python-testing-patterns        │
│  - If failures occur: trigger systematic-debugging     │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
                 [ Conclude & Report ]
```

### 1. Static Hygiene & Anti-Patterns Check
- **Relevant Skills**: [`python-anti-patterns`](.agents/skills/python-anti-patterns/SKILL.md), [`python-code-style`](.agents/skills/python-code-style/SKILL.md)
- **Checklist**:
  - [ ] No mutable default arguments (`def func(x=[]):`).
  - [ ] No bare `except:` clauses or catching raw `Exception` without re-raising or structured logging.
  - [ ] No blocking I/O calls inside async coroutines (e.g. `requests.get` inside `async def`).
  - [ ] Clean imports sorted, unused variables removed, and consistent PEP 8 / Ruff styling.

### 2. Type Safety & Contracts Check
- **Relevant Skills**: [`python-type-safety`](.agents/skills/python-type-safety/SKILL.md), [`pydantic-models-py`](.agents/skills/pydantic-models-py/SKILL.md)
- **Checklist**:
  - [ ] All functions and public methods have explicit parameter types and return type annotations.
  - [ ] Pydantic models follow V2 idioms (`model_validator`, `Field` descriptions, immutable configurations where appropriate).
  - [ ] Generics, `Optional`/`| None`, and structural protocols used accurately without implicit `Any`.

### 3. Error Handling & Resilience Check
- **Relevant Skills**: [`python-error-handling`](.agents/skills/python-error-handling/SKILL.md), [`python-resilience`](.agents/skills/python-resilience/SKILL.md)
- **Checklist**:
  - [ ] Custom domain exceptions inherit from a common base exception class.
  - [ ] Network requests, external API calls, and DB operations have explicit timeouts and retry/backoff policies.
  - [ ] Partial failures in batches are isolated so one item's failure does not crash the entire operation.

### 4. Test Execution & Debugging Check
- **Relevant Skills**: [`pytest-skill`](.agents/skills/pytest-skill/SKILL.md), [`python-testing-patterns`](.agents/skills/python-testing-patterns/SKILL.md), [`systematic-debugging`](.agents/skills/systematic-debugging/SKILL.md)
- **Checklist**:
  - [ ] Write or update corresponding `pytest` tests using proper fixtures and parametrization.
  - [ ] Run the test suite to ensure no regressions.
  - [ ] If any test fails, apply [`systematic-debugging`](.agents/skills/systematic-debugging/SKILL.md) root-cause analysis before making patch edits.

---

## Skill Directory (Help Book)

Below is the complete reference of all 49 skills in `.agents/skills`, categorized by their domain and usage trigger.

### 1. Python Language, Idioms & Architecture
| Skill | Purpose & Trigger |
| :--- | :--- |
| [`python-pro`](.agents/skills/python-pro/SKILL.md) | Modern Python 3.12+ features, standard library mastery, and production idioms. |
| [`python-patterns`](.agents/skills/python-patterns/SKILL.md) | Core Python design patterns and architectural decision-making principles. |
| [`python-project-structure`](.agents/skills/python-project-structure/SKILL.md) | Package scaffolding, public API definitions (`__all__`), and directory layout. |
| [`python-development`](.agents/skills/python-development/SKILL.md) | Project architecture setup with modern tools (`uv`, `FastAPI`, `ruff`). |
| [`architecture-patterns`](.agents/skills/architecture-patterns/SKILL.md) | Clean Architecture, Hexagonal, and Domain-Driven Design (DDD) for backend services. |
| [`async-python-patterns`](.agents/skills/async-python-patterns/SKILL.md) | High-performance non-blocking async/await, concurrency models, and asyncio patterns. |
| [`python-configuration`](.agents/skills/python-configuration/SKILL.md) | Typed configuration management via `pydantic-settings` and environment variables. |
| [`python-code-style`](.agents/skills/python-code-style/SKILL.md) | Code formatting, linting rules, naming conventions, and docstrings. |
| [`python-anti-patterns`](.agents/skills/python-anti-patterns/SKILL.md) | Catalog of code anti-patterns and code smells to avoid or refactor. |
| [`python-type-safety`](.agents/skills/python-type-safety/SKILL.md) | Advanced typing, generics, protocols, and mypy/pyright compliance. |
| [`python-error-handling`](.agents/skills/python-error-handling/SKILL.md) | Exception hierarchies, input validation, and graceful failure patterns. |
| [`python-resilience`](.agents/skills/python-resilience/SKILL.md) | Circuit breakers, retries, exponential backoff, and timeout decorators. |

### 2. Web APIs & Backend Services
| Skill | Purpose & Trigger |
| :--- | :--- |
| [`fastapi-pro`](.agents/skills/fastapi-pro/SKILL.md) | High-performance async APIs with FastAPI, SQLAlchemy 2.0, and WebSockets. |
| [`fastapi-router-py`](.agents/skills/fastapi-router-py/SKILL.md) | Standardized FastAPI router structure with dependency injection and status codes. |
| [`fastapi-templates`](.agents/skills/fastapi-templates/SKILL.md) | Production templates and blueprints for scalable FastAPI service backends. |
| [`api-design-principles`](.agents/skills/api-design-principles/SKILL.md) | RESTful and GraphQL API design best practices, resource naming, and contracts. |
| [`pydantic-models-py`](.agents/skills/pydantic-models-py/SKILL.md) | Multi-model Pydantic request/response schema design and data validation. |
| [`backend-architect`](.agents/skills/backend-architect/SKILL.md) | Distributed system design, microservices communication, and scalability planning. |

### 3. RAG, Vector Search & Embeddings
| Skill | Purpose & Trigger |
| :--- | :--- |
| [`rag-engineer`](.agents/skills/rag-engineer/SKILL.md) | End-to-end RAG architecture, chunking strategies, and retrieval evaluation. |
| [`rag-implementation`](.agents/skills/rag-implementation/SKILL.md) | Grounded LLM knowledge integration, semantic search, and document Q&A. |
| [`faiss`](.agents/skills/faiss/SKILL.md) | Facebook AI Similarity Search: Flat, IVF, and HNSW indexes for billions of vectors. |
| [`embedding-strategies`](.agents/skills/embedding-strategies/SKILL.md) | Selecting, evaluating, and fine-tuning dense embedding models. |
| [`hybrid-search-implementation`](.agents/skills/hybrid-search-implementation/SKILL.md) | Combining dense vector search with sparse keyword search (BM25) via Reciprocal Rank Fusion. |
| [`similarity-search-patterns`](.agents/skills/similarity-search-patterns/SKILL.md) | Nearest-neighbor algorithms, metric distance selection (Cosine, L2, IP). |
| [`vector-database-engineer`](.agents/skills/vector-database-engineer/SKILL.md) | Vector database deployment (Qdrant, Pinecone, Weaviate, Milvus, pgvector). |
| [`vector-index-tuning`](.agents/skills/vector-index-tuning/SKILL.md) | HNSW hyperparameter tuning (M, efConstruction, efSearch) for latency vs. recall. |

### 4. AI Engineering & LLM Application Development
| Skill | Purpose & Trigger |
| :--- | :--- |
| [`ai-engineer`](.agents/skills/ai-engineer/SKILL.md) | Multi-modal AI pipelines, vector search integrations, and enterprise AI systems. |
| [`ai-engineering-toolkit`](.agents/skills/ai-engineering-toolkit/SKILL.md) | Prompt evaluation scoring, context budget management, and agent security audits. |
| [`pydantic-ai`](.agents/skills/pydantic-ai/SKILL.md) | Type-safe tool calling, structured model outputs, and multi-model agent orchestration. |
| [`llm-app-patterns`](.agents/skills/llm-app-patterns/SKILL.md) | Architectural sketches for LLM tools, retrieval boundaries, and guardrails. |
| [`prompt-engineering`](.agents/skills/prompt-engineering/SKILL.md) | Advanced prompting patterns (few-shot, chain-of-thought, system prompt tuning). |
| [`huggingface-best`](.agents/skills/huggingface-best/SKILL.md) | Open-source model selection, leaderboard evaluation, and task-model matching. |
| [`ai-inference-service-mesh`](.agents/skills/ai-inference-service-mesh/SKILL.md) | Inference traffic routing, canary releases, and cross-cluster AI resilience. |
| [`machine-learning-ops-ml-pipeline`](.agents/skills/machine-learning-ops-ml-pipeline/SKILL.md) | Complete MLOps pipelines: training, tracking, model registry, and serving. |

### 5. Databases & Storage
| Skill | Purpose & Trigger |
| :--- | :--- |
| [`database-design`](.agents/skills/database-design/SKILL.md) | Relational schema design, normalization, indexing strategies, and ORM choice. |
| [`postgres-best-practices`](.agents/skills/postgres-best-practices/SKILL.md) | Query optimization, `EXPLAIN ANALYZE`, connection pooling, and pgvector tips. |

### 6. Testing, Quality & Debugging
| Skill | Purpose & Trigger |
| :--- | :--- |
| [`pytest-skill`](.agents/skills/pytest-skill/SKILL.md) | Writing idiomatic pytest fixtures, parameterization, markers, and mocks. |
| [`python-testing-patterns`](.agents/skills/python-testing-patterns/SKILL.md) | Unit, integration, and contract test design following TDD principles. |
| [`systematic-debugging`](.agents/skills/systematic-debugging/SKILL.md) | Root-cause hypothesis testing and methodical bug isolation before patching. |

### 7. Observability, Performance & Operations
| Skill | Purpose & Trigger |
| :--- | :--- |
| [`observability-engineer`](.agents/skills/observability-engineer/SKILL.md) | Metrics, distributed tracing, structured logging, and SLO/SLI definition. |
| [`python-observability`](.agents/skills/python-observability/SKILL.md) | Implementing OpenTelemetry, structlog, and Prometheus metrics in Python. |
| [`performance-engineer`](.agents/skills/performance-engineer/SKILL.md) | System profiling, bottleneck identification, and capacity planning. |
| [`python-performance-optimization`](.agents/skills/python-performance-optimization/SKILL.md) | Python memory profilers, cProfile analysis, and algorithmic speedups. |
| [`k6-load-testing`](.agents/skills/k6-load-testing/SKILL.md) | Writing and executing load, stress, and spike test scripts with Grafana k6. |
| [`docker-expert`](.agents/skills/docker-expert/SKILL.md) | Multi-stage Dockerfile optimization, non-root security, and compose setups. |
| [`deployment-procedures`](.agents/skills/deployment-procedures/SKILL.md) | Zero-downtime deployment workflows, rollbacks, and release verifications. |

### 8. Security & Authorization
| Skill | Purpose & Trigger |
| :--- | :--- |
| [`api-security-best-practices`](.agents/skills/api-security-best-practices/SKILL.md) | OWASP API Top 10 mitigation, rate limiting, and input sanitization. |
| [`auth-implementation-patterns`](.agents/skills/auth-implementation-patterns/SKILL.md) | JWT, OAuth2, RBAC, and secure session management boundaries. |
| [`security-auditor`](.agents/skills/security-auditor/SKILL.md) | DevSecOps audit, vulnerability scanning, and compliance verification. |

---

## End-to-End Task Lifecycle

When fulfilling any software task, follow this standard progression:

1. **Phase 1: Skill Discovery**
   - Identify the primary domain skills needed from the directory above (e.g. `fastapi-pro` + `rag-implementation`).
2. **Phase 2: Implementation**
   - Write clean, modular, and idiomatic code adhering to the domain recommendations.
3. **Phase 3: Post-Code Verification Gate (MANDATORY)**
   - Run through the 4-stage filter (`python-anti-patterns` -> `python-type-safety` -> `python-resilience` -> `pytest-skill`).
   - If tests or checks fail, resolve root causes with `systematic-debugging`.
4. **Phase 4: Conclude**
   - Summarize the changes and report successful verification results.
