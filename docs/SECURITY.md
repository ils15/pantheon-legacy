# Segurança e privacidade

> Conteúdo da v4.0 (legacy), originalmente publicado no README raiz.

- **Todo o processamento é local** — nenhum código é enviado a APIs externas além do provedor de IA do seu editor
- **Sem armazenamento ou rastreio de código** — os agentes operam inteiramente dentro da sua sessão
- **Sem commits automáticos** — você controla cada operação git
- **Sem treinamento de modelo** com o seu código (conforme os termos de serviço do seu editor)

## O que a Themis aplica em cada fase

- Conformidade com OWASP Top 10
- Prevenção de SQL injection, XSS e CSRF
- Detecção de segredos e credenciais hardcoded
- Cobertura mínima de testes de 80% (bloqueio rígido)

## Hooks de runtime

Os hooks shell ficam em [`scripts/hooks/`](../scripts/hooks/) e são acionados pelos
adaptadores de plataforma:

| Hook | Momento | Função |
|---|---|---|
| `scan-secrets.sh` | PreToolUse | Detecta segredos e credenciais hardcoded |
| `validate-talos-scope.sh` | PreToolUse | Restringe o escopo de hotfix do Talos |
| `on-subagent-delegation-start.sh` | PreToolUse | Registra o início da delegação |
| `format-multi-language.sh` | PostToolUse | Formata automaticamente os arquivos modificados |
| `log-session-start.sh` | PostToolUse | Trilha de auditoria das sessões |
| `on-subagent-delegation-stop.sh` | PostToolUse | Limpeza da delegação |

Também disponíveis: `audit-imports.sh` e `run-type-check.sh`.

> O bridge OpenCode que conectava esses scripts a eventos (`.opencode/plugins/pantheon-hooks.ts`)
> foi removido no cleanup da v4.0. O diretório `.opencode/plugins/` mantém apenas o plugin
> TUI (`pantheon-tui`).
