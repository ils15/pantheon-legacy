# Workflow: como uma feature atravessa o Pantheon

> Conteúdo da v4.0 (legacy), originalmente publicado no README raiz.

O sistema opera em fases definidas e controladas por você. Dentro de cada fase os
agentes trabalham em paralelo; toda transição é bloqueada até sua aprovação explícita.

```mermaid
---
config:
  look: classic
  theme: dark
  layout: elk
---
flowchart TD
    classDef user fill:#2d5a8c,stroke:#5a8ac4,stroke-width:2px,color:#e2e8f0
    classDef core fill:#1f2937,stroke:#4b5563,stroke-width:2px,color:#f3f4f6,font-weight:bold
    classDef planner fill:#1e3a5f,stroke:#3b82f6,stroke-width:2px,color:#dbeafe
    classDef ai fill:#4a1a3f,stroke:#c084fc,stroke-width:2px,color:#f3e8ff
    classDef executor fill:#7c2d12,stroke:#ea580c,stroke-width:2px,color:#fed7aa
    classDef qa fill:#3f1a3e,stroke:#d946a6,stroke-width:2px,color:#f5d1f8
    classDef infra fill:#1e3a3f,stroke:#14b8a6,stroke-width:2px,color:#ccfbf1
    classDef ops fill:#1e294b,stroke:#60a5fa,stroke-width:1px,color:#bfdbfe
    classDef gate fill:#1f1f1f,stroke:#fbbf24,stroke-width:2px,color:#fbbf24,stroke-dasharray: 5 5

    User["You / Human"]:::user
    Gate0{{"⏸️ Gate 0<br/>Approve Decision"}}:::gate
    Gate1{{"⏸️ Gate 1<br/>Approve Plan"}}:::gate
    Gate2{{"⏸️ Gate 2<br/>Approve Review"}}:::gate
    Gate3{{"⏸️ Gate 3<br/>Commit"}}:::gate

    subgraph Orchestrator["Orchestrator"]
        Zeus["Zeus<br/>Central Coordinator"]:::core
    end

    subgraph Plan["Planning & Discovery"]

        Athena["Athena<br/>Strategic Planner"]:::planner
        Apollo["Apollo<br/>Codebase Scout"]:::planner
        Nyx["Nyx<br/>Observability"]:::planner
    end

    subgraph AI["AI Infrastructure"]
        Hephaestus["Hephaestus<br/>AI Pipelines<br/>RAG / LangChain"]:::ai
    end

    subgraph Impl["Implementation<br/>Parallel Execution"]
        Hermes["Hermes<br/>Backend APIs"]:::executor
        Aphrodite["Aphrodite<br/>Frontend UI"]:::executor
        Demeter["Demeter<br/>Database"]:::executor
    end

    subgraph Quality["Quality & Observability"]
        Themis["Themis<br/>Security & Coverage Audit"]:::qa
        Nyx["Nyx<br/>Observability<br/>Tracing & Cost"]:::qa
    end

    subgraph Deploy["Deployment & Release"]
        Prometheus["Prometheus<br/>Infrastructure<br/>Docker / CI/CD"]:::infra
        Iris["Iris<br/>GitHub Operations<br/>PR / Release"]:::ops
        Mnemosyne["Mnemosyne<br/>Documentation<br/>Memory Bank"]:::ops
    end

    subgraph Express["Express Lane"]
        Talos["Talos<br/>Rapid Hotfixes"]:::qa
    end

    subgraph Domain["Domain Specialist"]
        Gaia["Gaia<br/>Remote Sensing"]:::planner
    end

    User -->|"/implement-feature"| Zeus

    Gate0 -->|Approved| Zeus
    Zeus -->|Phase 1| Athena
    Athena -->|Discovers| Apollo
    Apollo -->|Findings| Athena
    Athena --> Gate1
    Gate1 -->|Approved| Zeus

    Zeus -->|"Phase 2 (AI Infrastructure)"| AI
    Hephaestus --> Zeus

    Zeus -->|"Phase 3 (Implementation)"| Impl
    Hermes & Aphrodite & Demeter --> Quality

    Impl -.->|Nested Apollo| Apollo

    Nyx --> Themis
    Themis --> Gate2
    Gate2 -->|Approved| Zeus

    Zeus -->|"Phase 4 (Deploy & Release)"| Deploy
    Prometheus & Iris & Mnemosyne --> Gate3
    Gate3 -->|"git commit"| User

    User -.->|"/fix"| Express
    User -.->|"/plan-architecture"| Domain
```

---

## Approval gates

| Gate | Fase | O que acontece |
|---|---|---|
| **Gate 1** | Depois do planejamento | Athena apresenta um plano TDD em fases. Você revisa e aprova (ou pede mudanças) antes de qualquer código ser escrito. |
| **Gate 2** | Depois da implementação e revisão | Themis audita todos os arquivos alterados para OWASP, cobertura >80% e qualidade. Você valida o que só você pode julgar. |
| **Gate 3** | Depois da preparação de deploy | O agente sugere uma mensagem de commit. Você executa `git commit` manualmente e decide quando fazer merge. |

---

## Fluxo padrão de uma feature

```
User → Zeus: "Implement email verification"


1. PLAN:       Zeus → Athena → Apollo → Athena → USER (approve gate 1)
2. AI INFRA:   Zeus → Hephaestus (if AI components needed)
3. BUILD:      Zeus → Hermes + Aphrodite + Demeter (parallel execution)
4. OBSERVE:    Nyx instruments tracing, cost, and metrics
5. REVIEW:     Themis audits all code → USER (approve gate 2)
6. DEPLOY:     Prometheus (infra) + Iris (release) + Mnemosyne (docs)
7. COMMIT:     USER (git commit gate 3)
```

---

## Invocação direta

Agentes também podem ser chamados diretamente para tarefas focadas:

```
@apollo: Find all authentication-related files and usages
@hermes: Create POST /products endpoint with cursor pagination
@aphrodite: Refactor ProductCard for WCAG AA compliance
@demeter: Analyze and fix N+1 queries on orders table
@hephaestus: Build a RAG pipeline with pgvector for product docs
@nyx: Set up OpenTelemetry tracing for the payment service
@themis: Review this PR for security vulnerabilities
@iris: Create branch feat/search and open a draft PR
@gaia: Analyze agreement metrics between MapBiomas and ESA WorldCover
```

---

## Hotfix express lane

Para correções triviais (typos de CSS, bugs simples de lógica), pule a orquestração completa:

```
@talos: Fix the missing breakpoint class on MobileMenuButton
```

Talos trabalha sozinho, sem subagentes e sem cerimônia de TDD. Se o problema crescer,
ele escala para Zeus.
