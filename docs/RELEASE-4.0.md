# Notas da v4.0

> Resumo da versão v4.0 (última linha deste repositório), originalmente publicado no
> README raiz. O `CHANGELOG.md` cobre o histórico até a 3.19.2; este documento descreve
> o que a 4.0 adicionou.

| Sprint | Recurso |
|--------|--------|
| 1 | Comandos de memória (`/pantheon-remember`, search, consolidate, forget) |
| 2 | Pacote npm `@pantheon/cli` |
| 3 | Themis 2.0 (review em 3 camadas + IntentGate) |
| 4 | Background Agents + TODO Enforcer + Hash Edits |
| 5 | Simplificação de memória (agentes read-only, WAL) |
| 6 | YAGNI + anti-overengineering (12 padrões) |

**Auditoria da Themis: 100/100**

**9 comandos removidos:** ping, stop-continuation, subtask, manifest, forge, mirrordeps,
praxis, metamorphosis, reflect

**14 comandos no total** — todos `/pantheon-*` (lista em [COMMANDS.md](COMMANDS.md)).

> Observação: o comando `/forge` foi removido na v4.0, mas os presets de modelo que ele
> aplicava continuam definidos em `platform/forge.json` e documentados em
> [MODEL-TIERS.md](MODEL-TIERS.md).

## Memória vetorial (Level 3)

A v4.0 introduziu um sistema de memória persistente em dois tiers com recuperação
semântica. Detalhes em [MEMORY.md](MEMORY.md).
