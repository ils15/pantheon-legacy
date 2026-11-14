# Pantheon

Sistema de 14 agentes de IA especializados que planejam, implementam, testam e revisam
software com TDD obrigatório e aprovação humana em cada etapa — para quem programa com
VS Code Copilot, OpenCode, Claude Code, Cursor, Windsurf, Cline ou Continue.dev.

[![Licença](https://img.shields.io/badge/licen%C3%A7a-MIT-blue)](LICENSE)
[![Node](https://img.shields.io/badge/node-%E2%89%A518-339933)](package.json)
[![Agentes](https://img.shields.io/badge/agentes-14-purple)](agents/README.md)
[![Plataformas](https://img.shields.io/badge/plataformas-7-green)](docs/PLATFORMS.md)

> **Versão legacy.** O desenvolvimento deste repositório está pausado. A linha ativa
> continua em [pantheon-opencode](https://github.com/ils15/pantheon-opencode). A v4.0
> fica preservada para referência e arquivo.

## O que é

Um agente único tentando planejar, implementar, testar, revisar e documentar ao mesmo
tempo produz contexto fragmentado, testes pulados e código genérico. O Pantheon separa
essas responsabilidades em agentes especializados que trabalham num padrão
conductor-delegate: Zeus orquestra, Athena planeja, Hermes/Aphrodite/Demeter implementam
em paralelo, Themis audita e você aprova cada transição. Nenhuma fase avança sem
cobertura mínima de 80% de testes e sem o seu aval. É um framework de configuração —
não há runtime próprio: os agentes vivem como markdown/YAML dentro do seu editor.

## Instalação

Requisitos: Node.js ≥ 18. O modo `full` também cria um venv Python para os servidores MCP.

```bash
git clone https://github.com/ils15/pantheon-legacy.git
cd pantheon-legacy
npm install

npm run install:lite      # agentes + skills + instruções (sem MCP)
npm run install:full      # tudo: agentes, skills, MCP servers, venv Python
npm run install:runtime   # apenas a infraestrutura MCP
```

Guia detalhado por plataforma: [docs/INSTALLATION.md](docs/INSTALLATION.md) e
[docs/platforms/](docs/platforms/).

## Uso

Com os agentes carregados no editor, invoque o orquestrador:

```
@zeus: Implemente autenticação JWT com refresh tokens e rate limiting
```

O fluxo é: Athena planeja → **você aprova** → Hermes/Aphrodite/Demeter executam em
paralelo → Themis audita → **você aprova** → deploy → **você commita**. Comandos
nativos existem apenas no OpenCode (`/pantheon-*`); nas demais plataformas use
linguagem natural. Lista completa em [docs/COMMANDS.md](docs/COMMANDS.md) e o
detalhamento das fases em [docs/WORKFLOW.md](docs/WORKFLOW.md).

## Estrutura

```
agents/        14 definições .agent.md (formato canônico)
skills/        40 skills multiplataforma, uma por diretório (SKILL.md)
instructions/  10 padrões de código por domínio
commands/      14 comandos /pantheon-*
platform/      configs geradas por plataforma + forge.json (presets de modelo)
scripts/       instalador, motor de sync e hooks de ciclo de vida
docs/          documentação
```

Árvore completa: [docs/REPOSITORY-STRUCTURE.md](docs/REPOSITORY-STRUCTURE.md).

## Documentação

| Comece por | Detalhes técnicos |
|---|---|
| [Quick Start](docs/QUICKSTART.md) | [Arquitetura](docs/ARCHITECTURE.md) |
| [Instalação](docs/INSTALLATION.md) | [Workflow e approval gates](docs/WORKFLOW.md) |
| [Plataformas](docs/PLATFORMS.md) | [Princípios e comparativo](docs/PRINCIPLES.md) |
| [Referência de agentes](agents/README.md) | [Tiers e presets de modelo](docs/MODEL-TIERS.md) |
| [Referência de skills](skills/README.md) | [Sistema de memória](docs/MEMORY.md) |
| [Comandos](docs/COMMANDS.md) | [Segurança e hooks](docs/SECURITY.md) |
| [Manutenção e extensão](docs/MAINTAINING.md) | [FAQ](docs/FAQ.md) |

Índice completo: [docs/INDEX.md](docs/INDEX.md) · Notas da v4.0:
[docs/RELEASE-4.0.md](docs/RELEASE-4.0.md) · Histórico: [CHANGELOG.md](CHANGELOG.md).

## Licença

MIT — veja [LICENSE](LICENSE).
