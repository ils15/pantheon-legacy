# Comandos

> Conteúdo da v4.0 (legacy), originalmente publicado no README raiz.

O Pantheon expõe 14 comandos via OpenCode. Nas demais plataformas (Copilot, Cursor,
Claude Code), use linguagem natural com o nome do agente.

| Comando | Agente | Descrição |
|---------|-------|-------------|
| `/pantheon` | zeus | Síntese multiperspectiva (Council) via agentes inline |
| `/pantheon-install` | zeus | Pipeline de sync + install + verify com `--tier` (none/essential/recommended/full), `--backup`, `--detect`, `--dry-run` |
| `/pantheon-update` | iris | Bump de versão + changelog + git tag + GitHub Release |
| `/pantheon-deepwork` | zeus | Tarefa pesada multifase com checkpoints persistidos |
| `/pantheon-focus` | zeus | Fixa uma meta de sessão |
| `/pantheon-sketch` | athena | Transforma ideia bruta em especificação |
| `/pantheon-audit` | themis | Code review + auditoria de segurança |
| `/pantheon-remember` | mnemosyne | Armazena uma nova entrada de memória |
| `/pantheon-search` | mnemosyne | Busca em todas as memórias |
| `/pantheon-consolidate` | mnemosyne | Comprime memórias antigas |
| `/pantheon-forget` | mnemosyne | Apaga uma memória específica |
| `/pantheon-optimize` | zeus | Otimização de contexto e auditoria de tokens |
| `/pantheon-status` | zeus | Saúde do sistema e status dos agentes |
| `/cancel` | zeus | Interrompe a auto-continuação |

> **Nota multiplataforma:** os comandos são nativos do OpenCode. No VS Code Copilot, use
> `@nome-do-agente` no chat. No Cursor ou Claude Code, descreva a tarefa em linguagem natural.

As definições ficam em [`commands/`](../commands/); os prompts de invocação em
[`prompts/`](../prompts/).

---

## TUI Sidebar Plugin (OpenCode) — temporariamente desativado

O TUI Sidebar Plugin está desativado no momento. Será reativado numa release futura,
quando a compatibilidade com o pacote TUI for resolvida. Para descobrir agentes, use
`AGENTS.md`, [agents/README.md](../agents/README.md) ou `/pantheon-status`.
