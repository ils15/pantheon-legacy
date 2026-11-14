# Manutenção: documentação e extensão

> Conteúdo da v4.0 (legacy), originalmente publicado no README raiz.

## Mnemosyne é a dona da documentação

Ela mantém o README, o CHANGELOG, o memory bank e os ADRs. Nunca edite números de
badge nem contagens de agentes/skills à mão — delegue à Mnemosyne para que as contagens
permaneçam corretas e consistentes.

### Quando invocar a Mnemosyne

| Gatilho | Invocação |
|---|---|
| Agente adicionado ou removido | `@mnemosyne Update README agent count and tier overview` |
| Skill adicionada ou removida | `@mnemosyne Update README skills table and count` |
| Bump de versão | `@mnemosyne Update README version badge and CHANGELOG` |
| Fechamento de sprint | `@mnemosyne Update 01-active-context.md and append to 02-progress-log.md` |
| Decisão de arquitetura | `@mnemosyne Document decision: [topic]` |
| Registro de tarefa | `@mnemosyne Create task record: [feature] complete` |

### O que o CI garante

`release-gate.yml` valida que o número de versão é consistente em todos os manifestos
(`package.json`, `plugin.json`, `CHANGELOG.md` e o badge do README) a cada release. Se
divergirem, o release é bloqueado até a Mnemosyne reconciliar.

### Anti-patterns

```
# Errado — edição manual de badge cria drift
Edit README.md line 11: agents-17 → agents-18

# Certo — delegue à Mnemosyne
@mnemosyne Update README: added @ares agent, increment agent count to 18
```

```
# Errado — saída de sessão como arquivo
Create IMPLEMENTATION_SUMMARY.md with what we did

# Certo — use o memory bank
@mnemosyne Append to 02-progress-log.md: [summary of what was completed]
```

---

## Estendendo o framework

### Adicionar um agente

1. Crie `agents/<name>.agent.md` com frontmatter YAML (tools, model, handoffs)
2. Defina regras de comportamento e limites de contexto
3. Registre no Zeus adicionando-o à lista de delegação
4. Teste com uma tarefa de exemplo
5. Invoque `@mnemosyne Update README agent count and tier overview`

### Adicionar uma skill

1. Crie `skills/<name>/SKILL.md` com frontmatter YAML
2. Inclua visão geral de 2–3 frases, condições de uso e exemplos passo a passo
3. Referencie os agentes relevantes no corpo da skill
4. Invoque `@mnemosyne Update README skills table and count`

### Adicionar uma plataforma

1. Crie `platform/<name>/` com as configs específicas da plataforma
2. Adicione um guia de setup em `docs/platforms/<name>.md`
3. Estenda `scripts/install.mjs` e `scripts/sync-platforms.mjs`

O formato canônico é `agents/*.agent.md`; `npm run sync` gera a versão nativa de cada
plataforma. Detalhes do motor de sync em [ARCHITECTURE.md](ARCHITECTURE.md).
