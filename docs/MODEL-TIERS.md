# Model tiers e presets (`/forge`)

> Conteúdo da v4.0 (legacy), originalmente publicado no README raiz.

Os agentes declaram tiers abstratos de modelo (`fast` / `default` / `coding` / `premium`)
em vez de nomes fixos. O modelo concreto resolvido para cada tier depende da assinatura
da sua plataforma (OpenCode Go, Copilot Pro, Claude Pro etc.).

| Tier | Propósito | Agentes | Modelos típicos |
|------|---------|--------|----------------|
| `premium` | Raciocínio profundo, crítico | Zeus, Athena, Themis | DeepSeek V4 Pro, Claude Opus, o3 |
| `default` | Equilíbrio qualidade/velocidade | Hermes, Aphrodite, Demeter, Prometheus, Hephaestus, Gaia | Kimi K2.6, Claude Sonnet, GPT-4o |
| `coding` | Tarefas pesadas de código | Hermes, Aphrodite, Demeter, Prometheus, Hephaestus, Talos | DeepSeek V4 Flash, Claude Sonnet |
| `fast` | Operações rápidas e baratas | Apollo, Iris, Mnemosyne, Talos, Nyx | DeepSeek V4 Flash, MiniMax M2.7, Gemini Flash |

---

## `/forge` — presets de modelo

Os presets nomeados ficam em `platform/forge.json`. Cada preset mapeia os 4 tiers para
modelos concretos nos 14 agentes.

> Na v4.0 o comando `/forge` saiu do conjunto principal de 14 comandos; as definições
> sobrevivem nos adaptadores `.cursor/commands/forge.md` e `.continue/commands/forge.md`.
> Veja [RELEASE-4.0.md](RELEASE-4.0.md).

**Uso:**

```
/forge opencode-go     ← Apply a preset (12 available)
/forge default          ← Reset to account defaults (no models set)
/forge list             ← List all available presets
/forge status           ← Show current model configuration
/forge deepseek-flash   ← Single model for all agents
/forge --zeus anthropic/claude-opus-4-6  ← Override a single agent
```

**Presets disponíveis:**

| Preset | Premium | Default | Coding | Fast | Requires |
|--------|---------|---------|--------|------|----------|
| `default` | — | — | — | — | Account defaults |
| `opencode-go` | DeepSeek V4 Pro | Kimi K2.6 | DeepSeek V4 Flash | MiniMax M2.7 | OpenCode Go |
| `deepseek-flash` | DeepSeek V4 Flash | DeepSeek V4 Flash | DeepSeek V4 Flash | DeepSeek V4 Flash | OpenCode Go |
| `kimi` | Kimi K2.6 | Kimi K2.5 | Kimi K2.6 | MiniMax M2.7 | OpenCode Go |
| `qwen` | Qwen3.6 Plus | Qwen3.5 Plus | Qwen3.6 Plus | DeepSeek V4 Flash | OpenCode Go |
| `opencode-co` | DeepSeek V4 Pro | Kimi K2.6 | Kimi K2.6 | MiniMax M2.7 | OpenCode Go |
| `claude-pro` | Claude Opus-4 🤔 | Claude Sonnet-4 🤔 | Claude Sonnet-4 🤔 | Claude Haiku-4 🤔 | Anthropic key |
| `openai` | o3 (high) | GPT-4o | GPT-4o | GPT-4o-mini | OpenAI key |
| `gemini` | Gemini 3.5 Flash | Gemini 2.5 Flash | Gemini 2.5 Flash | Gemini 3.1 Flash-Lite | Google AI key |
| `github-copilot` | Claude Opus-4 | GPT-4o | GPT-4o | GPT-4o-mini | Copilot ($10/m) |
| `byok-best` | Claude Opus-4 🤔 | GPT-4o | GPT-4o | GPT-4o-mini | Anthropic + OpenAI |
| `together-moe` | DeepSeek V4 | Llama 4 Scout | Llama 4 Scout | Llama 3.2 3B | Together key |

> 🤔 = thinking habilitado

Definições completas em `platform/forge.json`; configuração por plataforma em
[docs/platforms/](platforms/). Análise detalhada de roteamento por plano de assinatura
em [reference/model-routing.md](reference/model-routing.md).
