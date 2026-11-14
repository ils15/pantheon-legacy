# Estrutura do repositório

> Conteúdo da v4.0 (legacy), originalmente publicado no README raiz e conferido
> contra a árvore atual.

```
pantheon-legacy/
├── README.md                  — este arquivo
├── AGENTS.md                  — referência de agentes para o Cline
├── CHANGELOG.md               — histórico de releases
├── CONTRIBUTING.md            — como estender
├── ROADMAP.md                 — direção planejada
├── LICENSE                    — MIT
├── package.json               — tooling de sync e instalação
├── plugin.json                — manifesto do plugin
│
├── agents/                    — 14 definições (.agent.md, formato canônico)
│   ├── zeus.agent.md          — orquestrador
│   ├── athena.agent.md        — planejador estratégico
│   ├── apollo.agent.md        — descoberta de código e web
│   ├── nyx.agent.md           — observabilidade
│   ├── hermes.agent.md        — APIs de backend
│   ├── aphrodite.agent.md     — UI de frontend
│   ├── demeter.agent.md       — banco de dados
│   ├── themis.agent.md        — qualidade e segurança
│   ├── prometheus.agent.md    — infraestrutura
│   ├── iris.agent.md          — operações GitHub
│   ├── mnemosyne.agent.md     — memória e documentação
│   ├── talos.agent.md         — hotfixes
│   ├── gaia.agent.md          — sensoriamento remoto
│   ├── hephaestus.agent.md    — pipelines de IA
│   └── README.md
│
├── skills/                    — 40 módulos de skill multiplataforma
│   └── <nome>/SKILL.md        — ver skills/README.md
│
├── instructions/              — 10 padrões de código por domínio
│   ├── agent-return-format.instructions.md
│   ├── backend-standards.instructions.md
│   ├── checkpoint-standards.instructions.md
│   ├── documentation-standards.instructions.md
│   ├── frontend-standards.instructions.md
│   ├── memory-protocol.instructions.md
│   ├── zeus-anti-stall.instructions.md
│   ├── zeus-communication-rules.instructions.md
│   ├── zeus-council-synthesis.instructions.md
│   └── zeus-timeout-retry.instructions.md
│
├── prompts/                   — prompts de invocação dos agentes
│   ├── implement-feature.prompt.md
│   ├── orchestrate-with-zeus.prompt.md
│   ├── debug-issue.prompt.md
│   ├── plan-architecture.prompt.md
│   ├── optimize-database.prompt.md
│   ├── sketch.prompt.md
│   ├── focus.prompt.md
│   ├── subtask.prompt.md        * tarefa filha limitada
│   ├── quick-discovery-large-codebase.prompt.md
│   ├── quick-plan-large-feature.prompt.md
│   ├── semantic-summarize.md
│   ├── README.md
│   └── dynamic/               * prompts gerados
│
├── commands/                  — 14 comandos /pantheon-*
│
├── platform/                  — configurações por plataforma
│   ├── copilot/               * VS Code Copilot
│   ├── opencode/              * OpenCode
│   ├── claude/                * Claude Code
│   ├── cursor/                * Cursor
│   ├── windsurf/              * Windsurf
│   ├── cline/                 * Cline
│   ├── continue/              * Continue.dev
│   ├── mcp/                   * definições MCP
│   └── _template/             * template para novas plataformas
│
├── scripts/                   — tooling, automação e hooks
│   ├── install.mjs            * instalador multiplataforma
│   ├── sync-platforms.mjs     * motor de sync de formatos
│   ├── validate-sync.mjs      * checagem de integridade do sync
│   ├── doctor.mjs             * diagnóstico do ambiente
│   ├── memory_mcp_server.py   * servidor MCP de memória
│   ├── mcp_persistence_server.py
│   ├── mcp_resources_server.py
│   ├── code_mode_server.py
│   └── hooks/                 * hooks de ciclo de vida (8 scripts .sh)
│
├── packages/cli/               — pacote @pantheon/cli (bin/pantheon.js)
│
├── docs/                      — documentação
│   ├── INDEX.md               — índice da documentação
│   ├── INSTALLATION.md        — guia de instalação
│   ├── QUICKSTART.md          — início rápido
│   ├── PLATFORMS.md           — comparação de plataformas
│   ├── ARCHITECTURE.md        — arquitetura
│   ├── WORKFLOW.md            — fases e approval gates
│   ├── PRINCIPLES.md          — princípios de design
│   ├── MODEL-TIERS.md         — tiers e presets (/forge)
│   ├── COMMANDS.md            — comandos
│   ├── MEMORY.md              — sistema de memória
│   ├── SECURITY.md            — segurança e privacidade
│   ├── MAINTAINING.md         — manutenção e extensão
│   ├── FAQ.md                 — perguntas frequentes
│   ├── RELEASE-4.0.md         — notas da v4.0
│   ├── REPOSITORY-STRUCTURE.md — esta árvore
│   ├── RELEASING.md           — versionamento e release
│   ├── platforms/             — guias por plataforma (7 arquivos)
│   └── reference/             — análise de roteamento de modelos
│
├── memories/repo/             — memória nativa auto-indexada
│   ├── stack.md
│   ├── conventions.md
│   └── commands.md
│
├── tests/                     — testes Python dos servidores MCP e scripts
│
├── .pantheon/                 — estado do framework (code-mode, deepwork)
├── .opencode/plugins/         — plugin TUI (pantheon-tui)
│
└── .github/workflows/         — CI/CD (11 workflows)
```

## Notas de estrutura

- `docs/memory-bank/` **não é versionado**: é um template que cada projeto adotante
  inicializa com o próprio contexto. Veja [docs/README.md](README.md).
- O arquivo de prioridade do memory bank é `01-active-context.md`; agentes o leem antes
  de qualquer tarefa.
