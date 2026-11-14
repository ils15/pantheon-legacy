# FAQ

> Conteúdo da v4.0 (legacy), originalmente publicado no README raiz.

**Quanto custa?**
Você precisa de uma assinatura existente para o seu editor de código com IA (Copilot,
Claude Pro, Cursor Pro ou OpenCode). O Pantheon em si é gratuito e open-source (MIT).

**Posso usar fora do VS Code?**
Sim — 7 plataformas suportadas (VS Code, OpenCode, Claude Code, Cursor, Windsurf, Cline,
Continue.dev). Veja [Platform Setup Guides](platforms/).

**Como as configs de plataforma são sincronizadas?**
Edite `agents/*.agent.md` (o formato canônico) e rode `npm run sync`. O motor de sync
transforma os agentes no formato nativo de cada plataforma.

**Posso ignorar o code review da Themis?**
Você pode prosseguir além do gate de review mesmo com apontamentos da Themis — exceto
cobertura de testes. Abaixo de 80% de cobertura é bloqueio rígido, por design.

**Quanto tempo leva uma feature típica?**
Endpoints simples: 2–4 horas. Features completas (backend + frontend + banco): 6–8 horas.
Sistemas grandes: 20–30 horas, distribuídas em várias sessões de sprint.

**E se a sessão do editor for interrompida?**
As fases abertas pausam. O memory bank guarda o último estado commitado. Retome lendo
`01-active-context.md` no início da próxima sessão. Veja [MEMORY.md](MEMORY.md).

---

Este repositório está em modo legacy. Para desenvolvimento ativo, use
[pantheon-opencode](https://github.com/ils15/pantheon-opencode).
