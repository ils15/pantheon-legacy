# Princípios: por que 14 agentes em vez de um

> Conteúdo da v4.0 (legacy), originalmente publicado no README raiz.

Agentes únicos tentam planejar, implementar, testar, revisar e documentar ao mesmo
tempo. O resultado é fragmentação de contexto, testes pulados e código genérico.
O Pantheon resolve isso por **especialização**: cada agente domina exatamente uma
coisa e é invocado apenas quando essa competência é necessária. Eles colaboram num
padrão conductor-delegate, no qual Zeus despacha trabalho para subagentes com janelas
de contexto isoladas, gates de qualidade e aprovação humana em cada transição.

---

## 1. Especialização

Cada agente tem contexto estreito e foco único. Hermes conhece padrões async de
FastAPI e nada de React. Aphrodite conhece acessibilidade WCAG e nada de índices de
banco. Gaia conhece sensoriamento remoto e nada de Docker. Isso produz código melhor
do que um generalista em cada camada.

## 2. TDD — obrigatório

Nenhuma fase avança sem cobertura mínima de 80%. O ciclo RED → GREEN → REFACTOR não
é opcional:

```python
# RED — Write a failing test first
def test_user_password_hashing():
    user = User(email="test@example.com", password="secret123")
    assert user.password != "secret123"   # Should be hashed
    assert user.verify_password("secret123")  # Verify works

# Run → FAILS ❌ (password is stored in plaintext)

# GREEN — Write the minimum implementation to make it pass
class User:
    def __init__(self, email, password):
        self.email = email
        self.password = hash_password(password)  # Minimal: just hash

    def verify_password(self, plaintext):
        return verify_hash(plaintext, self.password)

# Run → PASSES ✅

# REFACTOR — Improve without breaking the test
class User:
    def __init__(self, email: str, password: str):
        if not email or not password:
            raise ValueError("Email and password required")
        self.email = email
        self.password = self._hash_password(password)

    @staticmethod
    def _hash_password(plaintext: str) -> str:
        return bcrypt.hashpw(plaintext.encode(), bcrypt.gensalt())

    def verify_password(self, plaintext: str) -> bool:
        return bcrypt.checkpw(plaintext.encode(), self.password)

# Run → STILL PASSES ✅
```

## 3. Você permanece no controle

Toda fase produz um resumo estruturado ou artefato antes de prosseguir. Você revisa,
aprova ou pede mudanças — e só então a próxima fase começa. Existem quatro pontos de
pausa explícitos onde o sistema para e espera sua aprovação. A IA faz o trabalho; você
toma toda decisão de arquitetura e de commit. Ver [WORKFLOW.md](WORKFLOW.md).

---

## Comparativo de métricas

| Métrica | Agente único | Pantheon |
|--------|-------------|----------|
| Cobertura de testes média | 65–75% | **92%** |
| TDD | Opcional | **Obrigatório (RED→GREEN→REFACTOR)** |
| Cadência de code review | Fim da feature | **Depois de cada fase** |
| Bugs chegando à produção | 3–5 por feature | **Próximo de zero** |
| Eficiência de contexto | 10–20% de raciocínio | **70–80% de raciocínio** |
| Execução paralela | Apenas sequencial | **Paralela multiagente** |
| Documentação | Manual | **Auto-commitada no git** |
| Padrão de arquitetura | Monolítico | **Conductor-delegate especializado** |

> Métricas baseadas em benchmarks internos em 50+ implementações de features na suíte
> de testes do Pantheon. Seus resultados variam conforme a complexidade do código e o
> modelo escolhido.

---

## Comparação com outros frameworks

| Framework | Padrão | Diferença principal |
|---|---|---|
| **AutoGen** (Microsoft) | Conversas orientadas a eventos | Pesquisa, SDK Python; Pantheon é só configuração |
| **CrewAI** | Crews por papel | Editor visual, self-hosted; Pantheon vive dentro do seu editor |
| **LangGraph** | Grafos de atores com estado | DSL de grafo em código; Pantheon usa markdown + YAML |
| **MetaGPT** | Papéis de uma empresa de software | Simula uma empresa; Pantheon devolve a decisão a você em cada gate |
| **OpenAI Swarm** | Handoffs leves | Apenas sequencial; Pantheon suporta subagentes em paralelo |

### Decisões de projeto

- **Isolamento de contexto via subagentes** — Apollo roda em contexto isolado; só os achados retornam
- **Execução paralela** — escopos independentes rodam simultaneamente
- **Minimização de ferramentas** — cada agente tem a menor superfície de ferramentas necessária
- **Gates de aprovação humana** — sem auto-merge, sem commit fantasma
- **Alinhamento modelo-papel** — modelos rápidos para descoberta, poderosos para raciocínio
