# Protocolo Universal de Boas Práticas para Desenvolvimento de Software, IA e Ciência de Dados

### Com Referências Acadêmicas e Industriais Verificadas

> *"It is common to incur massive ongoing maintenance costs in real-world ML systems."*
> — Sculley et al., Google (NeurIPS 2015)

---

## Aviso de Rigor Epistemológico

Este documento adota uma postura deliberadamente honesta sobre o nível de evidência de cada afirmação. Afirmações são classificadas em:

- **[PEER-REVIEWED]** — publicado em conferência ou periódico com revisão por pares
- **[INDUSTRIAL]** — guia ou white paper de empresa reconhecida, sem revisão formal
- **[DISPUTADO]** — amplamente citado, mas com proveniência questionada na literatura
- **[CLÁSSICO]** — obra seminal da área, amplamente aceita como referência fundacional

Nenhuma afirmação central deste protocolo depende exclusivamente de fontes disputadas.

---

## Sumário

1. [Motivação: Por Que um Protocolo Universal?](#1-motivação-por-que-um-protocolo-universal)
2. [O Conceito de Dívida Técnica](#2-o-conceito-de-dívida-técnica)
3. [Dívida Técnica em Sistemas ML/IA — O Paper Fundacional](#3-dívida-técnica-em-sistemas-mlia--o-paper-fundacional)
4. [Dimensão 1 — Segurança Fundamental](#4-dimensão-1--segurança-fundamental)
5. [Dimensão 2 — Testes Automatizados](#5-dimensão-2--testes-automatizados)
6. [Dimensão 3 — Versionamento Disciplinado](#6-dimensão-3--versionamento-disciplinado)
7. [Dimensão 4 — Análise Estática de Código](#7-dimensão-4--análise-estática-de-código)
8. [Dimensão 5 — Documentação de Decisões (ADRs)](#8-dimensão-5--documentação-de-decisões-adrs)
9. [Dimensão 6 — Observabilidade e Monitoramento](#9-dimensão-6--observabilidade-e-monitoramento)
10. [Mapa de Confiabilidade das Afirmações](#10-mapa-de-confiabilidade-das-afirmações)
11. [Checklist Operacional por Dimensão](#11-checklist-operacional-por-dimensão)
12. [Aplicabilidade por Área Técnica](#12-aplicabilidade-por-área-técnica)
13. [Referências Completas](#13-referências-completas)

---

## 1. Motivação: Por Que um Protocolo Universal?

O argumento central deste documento é que dívida técnica e vulnerabilidade de segurança têm a mesma natureza estrutural: ambas são **custo diferido com juros compostos**. A diferença entre elas é apenas no modo de pagamento:

- **Dívida técnica** é paga em tempo de engenharia e velocidade de desenvolvimento degradada.
- **Vulnerabilidade de segurança** pode ser paga em reputação institucional, exposição de dados e, nos piores casos, comprometimento total de credenciais.

Ambas compartilham uma característica crítica: **o custo de correção cresce com o tempo**. Esse princípio é universal — aplica-se igualmente ao desenvolvimento de software, construção de modelos de ML/IA, administração de servidores, infraestrutura de segurança e ciência de dados.

O protocolo apresentado aqui é, portanto, uma coleção de práticas que qualquer profissional sênior ou especialista deve operar como pré-requisito, independentemente da área de atuação específica.

---

## 2. O Conceito de Dívida Técnica

### Origem

O conceito de *technical debt* foi introduzido formalmente por **Ward Cunningham** em 1992, na conferência OOPSLA, como metáfora para descrever o custo implícito de escolhas de implementação expedientes sobre soluções mais robustas.

> **Referência [CLÁSSICO]:**
> Cunningham, W. (1992). *The WyCash Portfolio Management System*. OOPSLA '92 Experience Report. ACM.

A metáfora é deliberadamente financeira: assim como dívida fiscal, dívida técnica acumula juros. Não pagar a dívida (via refatoração, documentação, testes) resulta em custos crescentes no futuro. O problema é que, ao contrário de dívidas financeiras, **dívida técnica não tem um extrato mensal** — ela se acumula silenciosamente.

### A Expansão do Conceito para Sistemas ML

O conceito ganhou uma dimensão adicional crítica com o crescimento de sistemas baseados em aprendizado de máquina. A razão: em sistemas ML, o comportamento não é especificado diretamente no código — é *aprendido a partir dos dados*. Isso cria categorias inteiramente novas de dívida que não existem em software convencional.

---

## 3. Dívida Técnica em Sistemas ML/IA — O Paper Fundacional

### Referência Principal

> **[PEER-REVIEWED]**
> Sculley, D., Holt, G., Golovin, D., Davydov, E., Phillips, T., Ebner, D., Chaudhary, V., Young, M., Crespo, J-F., & Dennison, D. (2015).
> **"Hidden Technical Debt in Machine Learning Systems."**
> *Advances in Neural Information Processing Systems (NeurIPS)*, 28, pp. 2503–2511.
> Google, Inc.
> Disponível em: https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems

Este paper, produzido por engenheiros do Google, é o trabalho mais citado sobre manutenibilidade de sistemas ML. Sua contribuição central é demonstrar empiricamente que:

1. Sistemas ML têm capacidade especial de acumular dívida técnica porque herdam todos os problemas de manutenção de código convencional, mais um conjunto adicional de problemas específicos de ML.

2. Apenas uma fração pequena de um sistema ML real consiste no código de ML propriamente dito — a infraestrutura circundante é vasta e complexa.

3. A dívida oculta é especialmente perigosa porque **se acumula silenciosamente** e existe no nível do sistema, não do código.

### Tipos de Dívida Específicos de ML Identificados pelo Paper

| Tipo de Dívida | Descrição | Risco |
|----------------|-----------|-------|
| **Boundary Erosion** | Limites entre componentes se corrompem com o tempo | Alto |
| **Entanglement** | Mudança em qualquer feature pode afetar todo o sistema | Alto |
| **Hidden Feedback Loops** | Output do modelo influencia dados futuros de treino | Crítico |
| **Undeclared Consumers** | Sistemas externos consomem output do modelo sem registro | Alto |
| **Data Dependencies** | Dependências instáveis de dados externos | Alto |
| **Data Testing Debt** | Ausência de testes para dados de input | Alto |
| **Distribution Shift** | Distribuição de produção diverge do treino ao longo do tempo | Crítico |
| **Reproducibility Debt** | Impossibilidade de reproduzir experimentos | Médio |
| **Configuration Debt** | Configurações críticas sem controle de versão ou teste | Alto |

---

## 4. Dimensão 1 — Segurança Fundamental

### Justificativa

Credenciais expostas são o modo de falha mais custoso e mais evitável em qualquer sistema. Ao contrário de bugs funcionais, que degradam a experiência, vazamentos de credenciais podem comprometer sistemas inteiros de forma irreversível e imediata.

### Referências

> **[PEER-REVIEWED — CONTEXTO AMPLO]**
> Dawson, M., et al. (2010). *Integrating Software Assurance into the Software Development Life Cycle (SDLC)*. Journal of Information Systems Technology and Planning.

> **[INDUSTRIAL]**
> OWASP Foundation. *OWASP Top Ten Project*.
> Disponível em: https://owasp.org/www-project-top-ten/
> — O item **A02:2021 Cryptographic Failures** e **A07:2021 Identification and Authentication Failures** cobrem diretamente o risco de credenciais expostas. O OWASP Top Ten é o framework de referência de segurança de aplicações mais amplamente adotado no mundo.

> **[INDUSTRIAL]**
> GitHub. *Secret Scanning — Supported Patterns*.
> Disponível em: https://docs.github.com/en/code-security/secret-scanning
> — O GitHub escaneia automaticamente repositórios em busca de padrões de mais de 200 provedores de serviço. A existência desse serviço é evidência direta de que credenciais hardcoded são um problema sistêmico e documentado.

### Práticas Mandatórias com Justificativa

**1. Variáveis de Ambiente**

```python
# ERRADO — credencial hardcoded
API_KEY = "sk-proj-xxxxxxxxxxxxxxxxxxx"

# CORRETO — variável de ambiente
from dotenv import load_dotenv
import os

load_dotenv()
API_KEY = os.getenv("API_KEY")
if not API_KEY:
    raise EnvironmentError("API_KEY não definida. Verifique .env")
```

*Justificativa:* Credenciais hardcoded persistem no histórico Git mesmo após remoção do arquivo. `git log --all` preserva todo o histórico, tornando a remoção posterior ineficaz sem rotação da credencial.

**2. Auditoria do Histórico Git**

```bash
# Verificar se credenciais foram commitadas no passado
git log --all --full-history -p | grep -i "password\|secret\|api_key\|token\|credential"
```

**3. Estrutura de Ambientes**

```
projeto/
├── .env.example        ← COMMITADO (apenas nomes das chaves, sem valores)
├── .env.local          ← NÃO commitado (desenvolvimento local)
├── .env.staging        ← NÃO commitado (staging)
├── .env.production     ← NÃO commitado, preferencialmente nunca local
└── .gitignore          ← contém: .env, .env.*, *.pem, *.key, secrets/
```

**4. Verificação de Integridade de Artefatos (relevante para ML)**

```python
import hashlib, joblib

def load_model_safe(path: str, expected_sha256: str):
    """Carrega modelo com verificação de integridade."""
    with open(path, "rb") as f:
        data = f.read()
    actual = hashlib.sha256(data).hexdigest()
    if actual != expected_sha256:
        raise SecurityError(f"Hash do modelo não confere. Possível tampering.")
    return joblib.load(path)
```

*Justificativa:* Modelos serializados com `pickle` executam código arbitrário ao serem carregados. Um modelo comprometido (substituído por um adversário) pode ser usado para execução remota de código.

---

## 5. Dimensão 2 — Testes Automatizados

### Justificativa e Nível de Evidência

#### Custo de Correção de Bugs por Fase — Evidência e Limitações

Esta é uma área onde a honestidade epistemológica é necessária. A afirmação amplamente circulada de que "bugs custam 100x mais para corrigir em produção do que no design" tem **proveniência disputada**.

> **[DISPUTADO — uso com cautela]**
> A afirmação é frequentemente atribuída ao "IBM Systems Sciences Institute". Laurent Bossavit, em seu trabalho *"Leprechauns of Software Engineering"* (2016), investigou a origem e concluiu que o instituto não produziu um estudo publicado e revisado por pares — a referência original apontava para notas de curso internas.

O que as evidências *verificáveis* sustentam:

> **[INDUSTRIAL — evidência moderada]**
> NIST. (2002). *The Economic Impacts of Inadequate Infrastructure for Software Testing*. National Institute of Standards and Technology, U.S. Department of Commerce.
> — Demonstra aumento de esforço para correção de defeitos conforme o software avança pelas fases de desenvolvimento.

> **[INDUSTRIAL]**
> IBM Rational Software. (2008). *Minimizing Code Defects to Improve Software Quality and Lower Development Costs*. IBM White Paper RAW14109USEN.
> — "Os custos de descobrir defeitos após o lançamento são significativos: até 30 vezes mais do que se forem detectados na fase de design e arquitetura."

**Conclusão honesta:** A direção da afirmação é sólida e amplamente corroborada — detectar bugs cedo é mais barato do que tarde. O múltiplo exato (10x, 30x, 100x) varia por contexto e não deve ser tratado como fato preciso.

#### Evidência Mais Robusta: Testes em Sistemas ML

> **[PEER-REVIEWED]**
> Breck, E., Cai, S., Nielsen, E., Salib, M., & Sculley, D. (2017).
> **"The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction."**
> *Proceedings of IEEE International Conference on Big Data*, pp. 1123–1132.
> Google, Inc.
> Disponível em: https://research.google/pubs/the-ml-test-score-a-rubric-for-ml-production-readiness-and-technical-debt-reduction/

Este paper apresenta 28 testes específicos derivados de experiência com sistemas ML em produção no Google. Os autores avaliaram 36 equipes internas e identificaram que mesmo equipes experientes tinham gaps significativos de cobertura de testes.

**Achado crítico do paper:** Uma equipe descobriu um arquivo de mil linhas de código — completamente sem testes — que criava suas features de input. Código desse tamanho, mesmo contendo lógica simples, provavelmente contém bugs contra os quais testes unitários simples forneceriam proteção eficaz.

### Os 4 Tipos de Teste Fundamentais (baseados em Breck et al.)

```
TIPO DE TESTE        PERGUNTA QUE RESPONDE           QUANDO ESCREVER
─────────────────────────────────────────────────────────────────────
Fumaça (Smoke)       O sistema inicializa sem erro?   Antes de tudo
Contrato (Contract)  Cada interface honra seu contrato?  Com cada módulo
Regressão            O bug corrigido não volta?        A cada bug corrigido
Integração           Os módulos funcionam juntos?      Após integrar componentes
```

### Protocolo de Introdução Gradual (para código sem cobertura)

```
SEMANA 1: Testes de fumaça
  → Objetivo: verificar que o sistema importa e inicializa
  → Ferramenta: pytest
  → Meta: 0 → 3 testes cobrindo imports e inicialização

SEMANA 2-3: Testes de contrato nos módulos mais críticos
  → Objetivo: verificar que interfaces se comportam como prometido
  → Foco: módulos mais determinísticos (feature extraction, parsers)
  → Meta: cobertura nos caminhos críticos

A PARTIR DE AGORA: Testes de regressão para cada bug
  → Regra absoluta: nunca corrigir bug sem escrever o teste que o reproduz primeiro
  → Commits: "test(módulo): reproduz bug X" → "fix(módulo): corrige bug X"
```

---

## 6. Dimensão 3 — Versionamento Disciplinado

### Justificativa

Git disciplinado não é questão de preferência estética — é rastreabilidade de engenharia. Sem histórico limpo, debugging em produção se torna arqueologia: você não sabe o que mudou, quando, por que, ou quem aprovou.

### Referências

> **[CLÁSSICO]**
> Chacon, S., & Straub, B. (2014). *Pro Git* (2nd ed.). Apress.
> Disponível gratuitamente em: https://git-scm.com/book/en/v2
> — Referência definitiva para Git. Cobre branching strategies, commits atômicos e workflow disciplinado.

> **[INDUSTRIAL]**
> Conventional Commits Specification v1.0.0.
> Disponível em: https://www.conventionalcommits.org/
> — Especificação de commits semânticos adotada por milhares de projetos open-source.

### Padrão de Commits Semânticos (Conventional Commits)

```
FORMATO: tipo(escopo): descrição imperativa no presente

TIPOS:
  feat     → nova funcionalidade
  fix      → correção de bug
  test     → adição ou correção de testes
  docs     → documentação
  security → correção de vulnerabilidade
  refactor → refatoração sem mudança de comportamento
  perf     → melhoria de performance
  chore    → manutenção (atualização de deps, config)

EXEMPLOS:
  feat(feature-extraction): adiciona cálculo de entropia de domínio
  fix(gibberish-detector): corrige falso positivo para domínios japoneses
  test(content-features): adiciona testes para URLs com redirect
  security(env): remove credencial hardcoded do config.py
  docs(pipeline): documenta decisão de usar aiohttp vs requests (ADR-002)
```

### Estratégia de Branches Mínima Viável

```
main          ← produção. Nunca commitado diretamente. Apenas merges.
│
├── develop   ← integração. Base para features.
│   │
│   ├── feature/nome-descritivo    ← uma feature = uma branch
│   ├── fix/descricao-do-bug       ← um bug = uma branch
│   └── experiment/hipotese-x      ← experimento isolado
│
└── hotfix/nome ← emergência em produção
```

### Pre-Commit Hooks — Automação que Previne Erros

```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.5.0
    hooks:
      - id: detect-private-key        # bloqueia chaves privadas
      - id: check-added-large-files   # bloqueia arquivos > 500KB por padrão
      - id: check-merge-conflict      # detecta markers de merge não resolvidos
      - id: no-commit-to-branch       # impede commit direto na main
        args: ['--branch', 'main', '--branch', 'master']

  - repo: https://github.com/Yelp/detect-secrets
    rev: v1.4.0
    hooks:
      - id: detect-secrets
```

```bash
# Ativar no repositório
pip install pre-commit
pre-commit install
```

---

## 7. Dimensão 4 — Análise Estática de Código

### Justificativa

Análise estática detecta classes inteiras de erros antes da execução: variáveis não usadas, tipos incompatíveis, padrões de vulnerabilidade conhecidos, importações órfãs, comparações incorretas. Não é questão de estilo — é prevenção automática de bugs.

### Referências

> **[INDUSTRIAL]**
> IBM Rational Software. (2008). *Minimizing Code Defects to Improve Software Quality and Lower Development Costs*. IBM White Paper.
> — Descreve como análise estática pode identificar e erradicar falhas antes do deployment, durante a fase de codificação.

> **[INDUSTRIAL]**
> OWASP. *Static Application Security Testing (SAST)*.
> Disponível em: https://owasp.org/www-community/Source_Code_Analysis_Tools
> — Referência de referência para ferramentas de análise estática orientadas a segurança.

> **[INDUSTRIAL]**
> Google. *Google Engineering Practices — Code Review*.
> Disponível em: https://google.github.io/eng-practices/
> — Documenta a prática de code review como complemento à análise estática automatizada.

### Stack Recomendado para Python

```toml
# pyproject.toml — configuração unificada
[tool.ruff]
line-length = 88
select = [
    "E",   # pycodestyle errors
    "F",   # pyflakes (erros lógicos, imports não usados)
    "W",   # pycodestyle warnings
    "I",   # isort (ordenação de imports)
    "N",   # pep8-naming
    "UP",  # pyupgrade (modernização de sintaxe)
    "S",   # bandit (security issues) ← CRÍTICO
    "B",   # flake8-bugbear (bugs comuns) ← CRÍTICO
]

[tool.mypy]
python_version = "3.11"
warn_return_any = true
warn_unused_ignores = true
# Comece sem strict=true, adicione gradualmente

[tool.black]
line-length = 88

[tool.isort]
profile = "black"
```

```bash
# Instalação
pip install ruff mypy black isort

# Uso inicial — ver erros sem modificar
ruff check .

# Corrigir automaticamente o que é seguro
ruff check --fix .

# Formatar código
black . && isort .

# Verificar tipos
mypy src/
```

### Exemplos de Erros que Análise Estática Detecta

```python
# ERRO detectado por ruff (S324) — uso de hash MD5 para segurança
import hashlib
hashlib.md5(data)  # Inseguro para fins criptográficos

# ERRO detectado por ruff (S101) — assert em código de produção
assert len(features) > 0  # assert é ignorado com python -O

# ERRO detectado por mypy — tipo errado
def extract_features(url: str) -> dict[str, float]:
    return []  # ERROR: incompatible return type

# ERRO detectado por ruff (B006) — mutable default argument
def process(items: list = []):  # Bug clássico em Python
    items.append(1)
```

---

## 8. Dimensão 5 — Documentação de Decisões (ADRs)

### Justificativa

O código diz **o quê** foi implementado. A documentação de decisões diz **por quê** foi implementado daquela forma. Sem o porquê, decisões tomadas com razões válidas são revertidas por novos membros da equipe que não têm o contexto — um fenômeno que Nygard chama de "what were they thinking?"

### Referências

> **[INDUSTRIAL — Amplamente Adotado]**
> Nygard, M. (2011). *"Documenting Architecture Decisions."*
> Cognitect Blog, 15 de novembro de 2011.
> Disponível em: https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions
> — Post seminal que definiu o formato ADR e popularizou a prática. Sete anos após a publicação, o Thoughtworks Technology Radar colocou ADRs na categoria "Adopt".

> **[INDUSTRIAL]**
> Fowler, M. *"Architecture Decision Record."* Martin Fowler's Bliki.
> Disponível em: https://martinfowler.com/bliki/ArchitectureDecisionRecord.html
> — Martin Fowler (ThoughtWorks) documenta ADRs com contexto e exemplos práticos.

> **[INDUSTRIAL]**
> Amazon Web Services. *"Use architectural decision records to streamline technical decision-making."*
> AWS Prescriptive Guidance.
> Disponível em: https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/welcome.html
> — AWS recomenda ADRs como prática padrão para projetos de software.

> **[ACADÊMICO]**
> Zdun, U., et al. (2013). *"Sustainable Architectural Decisions."*
> IEEE Software, 30(6), pp. 46–53.
> — Base acadêmica para práticas de registro de decisões arquiteturais.

### Template ADR (baseado em Nygard, 2011)

```markdown
# ADR-001: [Título que descreve a decisão, não o problema]

**Data:** YYYY-MM-DD
**Status:** Proposto | Aceito | Supersedido por ADR-XXX

## Contexto

[Descreva a situação, forças e restrições que levaram a esta decisão.
Seja específico sobre constraints técnicas, organizacionais e temporais.]

## Decisão

[Declare claramente a decisão tomada em voz ativa.
"Nós decidimos usar X" — não "Pode-se considerar usar X".]

## Consequências

**Positivas:**
- [Benefício 1]
- [Benefício 2]

**Negativas / Trade-offs conscientes:**
- [Custo 1]
- [Custo 2]

## Alternativas Consideradas

**Alternativa A — [Nome]:**
- Descartada porque: [razão específica]

**Alternativa B — [Nome]:**
- Descartada porque: [razão específica]
```

### Estrutura de Diretório

```
projeto/
└── docs/
    └── decisions/
        ├── ADR-001-aiohttp-vs-requests.md
        ├── ADR-002-gibberish-threshold-recalibration.md
        ├── ADR-003-random-forest-vs-xgboost.md
        └── ADR-004-feature-extraction-async-strategy.md
```

### O Que Documentar (e o Que Não Documentar)

**Documente:**
- Decisões com impacto no design estrutural do sistema
- Decisões onde alternativas plausíveis foram descartadas
- Decisões tomadas sob pressão de tempo com trade-offs explícitos
- Qualquer decisão que futuros membros da equipe possam querer reverter

**Não documente:**
- Detalhes de implementação que o código já expressa claramente
- Decisões triviais sem trade-offs relevantes
- Preferências de estilo cobertas por formatters automáticos

---

## 9. Dimensão 6 — Observabilidade e Monitoramento

### Justificativa

"Você não pode melhorar o que não consegue observar" é uma variação do princípio de gestão de Drucker, adaptado para engenharia. Em sistemas ML, a observabilidade tem uma dimensão adicional crítica: modelos degradam silenciosamente quando a distribuição dos dados em produção diverge da distribuição de treino.

### Referências

> **[PEER-REVIEWED]**
> Sculley et al. (2015), op. cit.
> — O paper identifica explicitamente "Data Testing Debt" como uma dimensão crítica: testes de dados de input devem incluir verificações básicas e testes que monitoram *mudanças nas distribuições de input* — a base do que hoje chamamos de monitoramento de drift.

> **[PEER-REVIEWED]**
> Breck et al. (2017), op. cit.
> — A seção de monitoramento do ML Test Score define testes específicos para detecção de degradação de modelos em produção.

> **[INDUSTRIAL]**
> Google. *Site Reliability Engineering (SRE) Book*, O'Reilly, 2016.
> Disponível gratuitamente em: https://sre.google/sre-book/table-of-contents/
> — Capítulo 6 (Monitoring Distributed Systems) e Capítulo 26 (Data Integrity) definem as práticas de observabilidade que se tornaram padrão da indústria. Inclui os conceitos de SLI (Service Level Indicators), SLO (Service Level Objectives) e error budgets.

> **[INDUSTRIAL]**
> OpenTelemetry Project. *What is Observability?*
> Disponível em: https://opentelemetry.io/docs/concepts/observability-primer/
> — Define os três pilares de observabilidade: logs, métricas e traces.

### Os Três Pilares de Observabilidade

```
LOGS          → O QUE aconteceu, com contexto suficiente para reproduzir
MÉTRICAS      → O QUÊ está acontecendo agora (saúde do sistema em tempo real)
TRACES        → POR QUÊ está acontecendo (rastreamento de causa raiz)
```

### Monitoramento Específico para ML/IA

```python
# Exemplo mínimo de monitoramento de drift para pipeline de classificação

import numpy as np
from scipy import stats

class DriftMonitor:
    """Detecta desvio estatístico entre distribuição de referência e atual."""

    def __init__(self, reference_features: np.ndarray, alpha: float = 0.05):
        self.reference = reference_features
        self.alpha = alpha  # nível de significância para alertas

    def check_drift(self, current_features: np.ndarray) -> dict:
        results = {}
        for i, col in enumerate(current_features.T):
            ref_col = self.reference[:, i]
            ks_stat, p_value = stats.ks_2samp(ref_col, col)
            results[f"feature_{i}"] = {
                "ks_statistic": ks_stat,
                "p_value": p_value,
                "drift_detected": p_value < self.alpha
            }
        return results

# Uso: checar drift a cada N predições em produção
monitor = DriftMonitor(reference_features=X_train)
drift_report = monitor.check_drift(current_batch)
```

### Estrutura Mínima de Logs Estruturados

```python
import json
import logging
from datetime import datetime, timezone

def log_prediction(url: str, features: dict, prediction: int,
                   confidence: float, latency_ms: float):
    """Log estruturado para cada predição — rastreável e auditável."""
    record = {
        "timestamp": datetime.now(timezone.utc).isoformat(),
        "event": "prediction",
        "url_hash": hashlib.sha256(url.encode()).hexdigest()[:16],  # nunca logar URL raw
        "prediction": prediction,
        "confidence": round(confidence, 4),
        "latency_ms": round(latency_ms, 2),
        "feature_count": len(features),
        "model_version": MODEL_VERSION
    }
    logging.info(json.dumps(record))
```

---

## 10. Mapa de Confiabilidade das Afirmações

Esta tabela resume o nível de evidência para cada afirmação central do protocolo:

| Afirmação | Fonte Principal | Nível de Evidência | Nota |
|-----------|----------------|-------------------|------|
| Sistemas ML acumulam dívida técnica massiva | Sculley et al., NeurIPS 2015 | **PEER-REVIEWED** | Altamente citado, Google |
| Testes são pré-requisito para ML em produção | Breck et al., IEEE Big Data 2017 | **PEER-REVIEWED** | 28 testes derivados empiricamente |
| Detectar bugs cedo é mais barato que tarde | NIST (2002), IBM White Paper (2008) | **INDUSTRIAL** | Direção sólida, múltiplo exato incerto |
| O múltiplo "100x mais caro em produção" | Atribuído a IBM SSI | **DISPUTADO** | Proveniência não verificada (Bossavit, 2016) |
| ADRs preservam contexto de decisões | Nygard (2011), Fowler | **INDUSTRIAL** | ThoughtWorks "Adopt", AWS recomenda |
| Monitoramento de drift é necessário para ML | Sculley et al. + Breck et al. | **PEER-REVIEWED** | Documentado empiricamente |
| Credenciais hardcoded são risco sistêmico | OWASP Top Ten (A02, A07) | **INDUSTRIAL** | Adotado mundialmente |
| Análise estática reduz bugs pré-execução | IBM Rational (2008), OWASP SAST | **INDUSTRIAL** | Evidência empírica de campo |
| Complexidade acidental vs. essencial | Brooks (1986), *No Silver Bullet* | **CLÁSSICO** | Fundacional da engenharia de software |

---

## 11. Checklist Operacional por Dimensão

### Como Usar

Para cada item, marque:
- `[x]` — implementado e funcionando
- `[-]` — parcialmente implementado
- `[ ]` — não implementado (gap confirmado)

A prioridade de ataque deve ser: segurança primeiro (risco irreversível), testes segundo (base para refatoração segura), restante em paralelo.

---

### ✅ Dimensão 1 — Segurança Fundamental

```
[ ] Variáveis de ambiente em uso (.env + python-dotenv ou equivalente)
[ ] .gitignore cobre: .env, .env.*, *.pem, *.key, secrets/
[ ] .env.example commitado com todas as chaves (sem valores)
[ ] Histórico Git auditado em busca de segredos anteriores
[ ] Credenciais rotacionadas se encontradas no histórico
[ ] detect-secrets instalado e configurado como pre-commit hook
[ ] Princípio do menor privilégio aplicado (DB, APIs, cloud)
[ ] Separação de credenciais por ambiente (dev ≠ staging ≠ prod)
[ ] Modelos ML verificados por hash SHA-256 antes do carregamento
```

### ✅ Dimensão 2 — Testes Automatizados

```
[ ] pytest instalado e configurado
[ ] Testes de fumaça: sistema importa e inicializa sem erro
[ ] Testes de contrato: interfaces principais testadas
[ ] Regra de regressão em vigor: nenhum bug corrigido sem teste
[ ] CI/CD roda testes automaticamente a cada push
[ ] Cobertura mínima definida para módulos críticos
[ ] Para ML: distribuições de features testadas nos dados de entrada
[ ] Para ML: output do modelo testado contra limites esperados
```

### ✅ Dimensão 3 — Versionamento Disciplinado

```
[ ] Nenhum commit direto na main/master
[ ] Conventional Commits adotados (feat/fix/test/docs/security)
[ ] pre-commit instalado (detect-secrets + no-commit-to-main)
[ ] Uma feature/bug por branch
[ ] Tags de versão em artefatos deployados (modelos, APIs)
[ ] Mensagens de commit explicam o PORQUÊ, não apenas o O QUÊ
```

### ✅ Dimensão 4 — Análise Estática

```
[ ] ruff configurado e rodando no CI/CD
[ ] Regras de segurança (S) e bugbear (B) habilitadas no ruff
[ ] mypy configurado (sem strict inicialmente)
[ ] black + isort configurados e rodando automaticamente
[ ] pip-audit ou safety verificando dependências regularmente
[ ] Análise estática bloqueando merges com erros críticos
```

### ✅ Dimensão 5 — Documentação de Decisões

```
[ ] Diretório docs/decisions/ criado no repositório
[ ] ADR-001 documenta a decisão mais crítica já tomada
[ ] Failure modes mapeados explicitamente por componente
[ ] Runbook para procedimentos operacionais principais
[ ] Changelog mantido para mudanças de interface ou comportamento
[ ] .env.example atualizado a cada nova variável adicionada
```

### ✅ Dimensão 6 — Observabilidade e Monitoramento

```
[ ] Logs estruturados (JSON) em todos os componentes críticos
[ ] Métricas de latência e taxa de erro coletadas
[ ] Alertas configurados nos failure modes mapeados
[ ] Para ML: monitoramento de drift implementado (ao menos KS test)
[ ] Para ML: versão do modelo incluída em cada log de predição
[ ] Dashboard mínimo mostrando saúde do sistema
[ ] Rastreabilidade: cada ação identificável por quem, quando, o quê
```

---

## 12. Aplicabilidade por Área Técnica

### Princípio de Aplicação

O protocolo é universal — as seis dimensões se aplicam a todas as áreas. O que varia são as ferramentas específicas e os modos de falha dominantes em cada contexto.

| Dimensão | Software Geral | ML / IA | Data Science | Infraestrutura |
|----------|---------------|---------|--------------|----------------|
| Segurança | .env, OWASP | .env + hash de modelos | .env + dados sensíveis | Vault, IAM, LSP |
| Testes | pytest, jest | pytest + ML Test Score | pytest + great_expectations | Terraform test, Inspec |
| Versionamento | Git branches | Git + DVC (dados/modelos) | Git + DVC | Git + IaC versionado |
| Análise Estática | ruff, mypy | ruff + mypy | ruff + mypy | tflint, checkov |
| Documentação | ADRs | ADRs + model cards | ADRs + data lineage | ADRs + runbooks |
| Observabilidade | Logs + métricas | Drift + performance | Data quality checks | Prometheus + Grafana |

### Ferramentas Específicas por Área

**Para ML / IA:**
- `dvc` — versionamento de datasets e modelos
- `mlflow` ou `wandb` — tracking de experimentos
- `evidently` ou `whylogs` — monitoramento de drift
- `great_expectations` — testes de qualidade de dados

**Para Infraestrutura:**
- `checkov` — análise estática de Terraform/CloudFormation
- `tflint` — linter para Terraform
- `trivy` — scan de vulnerabilidades em containers
- `HashiCorp Vault` — gestão centralizada de segredos

**Para Data Science:**
- `great_expectations` — contratos de dados
- `pandas-profiling` / `ydata-profiling` — análise de distribuição
- `DVC` — reprodutibilidade de pipelines

---

## 13. Referências Completas

### Artigos Acadêmicos (Peer-Reviewed)

1. **Sculley, D., Holt, G., Golovin, D., Davydov, E., Phillips, T., Ebner, D., Chaudhary, V., Young, M., Crespo, J-F., & Dennison, D.** (2015). *Hidden Technical Debt in Machine Learning Systems.* Advances in Neural Information Processing Systems (NeurIPS), 28, pp. 2503–2511. Google, Inc.
   - DOI / URL: https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems
   - **Relevância:** Fundação teórica e empírica para dívida técnica em ML

2. **Breck, E., Cai, S., Nielsen, E., Salib, M., & Sculley, D.** (2017). *The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction.* Proceedings of IEEE International Conference on Big Data, pp. 1123–1132. Google, Inc.
   - DOI: 10.1109/BigData.2017.8258038
   - URL: https://research.google/pubs/the-ml-test-score-a-rubric-for-ml-production-readiness-and-technical-debt-reduction/
   - **Relevância:** 28 testes concretos para sistemas ML em produção

3. **Zdun, U., Capilla, R., Tran, H., & Zimmermann, O.** (2013). *Sustainable Architectural Decisions.* IEEE Software, 30(6), pp. 46–53.
   - **Relevância:** Base acadêmica para registro de decisões arquiteturais

### Obras de Referência Clássicas

4. **Cunningham, W.** (1992). *The WyCash Portfolio Management System.* OOPSLA '92 Experience Report. ACM.
   - **Relevância:** Origem do conceito de technical debt

5. **Brooks, F.P.** (1986). *No Silver Bullet: Essence and Accidents of Software Engineering.* Proceedings of the IFIP Tenth World Computing Conference, pp. 1069–1076.
   - **Relevância:** Distinção fundacional entre complexidade essencial e acidental

6. **Beck, K.** (1999). *Extreme Programming Explained: Embrace Change.* Addison-Wesley.
   - **Relevância:** Base para práticas de TDD e iteração curta

### Fontes Industriais e Guias Técnicos

7. **NIST.** (2002). *The Economic Impacts of Inadequate Infrastructure for Software Testing.* National Institute of Standards and Technology, U.S. Department of Commerce. NIST Planning Report 02-3.
   - URL: https://www.nist.gov/system/files/documents/director/planning/report02-3.pdf
   - **Relevância:** Evidência institucional para custo de bugs por fase (moderada)

8. **IBM Rational Software.** (2008). *Minimizing Code Defects to Improve Software Quality and Lower Development Costs.* IBM White Paper RAW14109USEN.
   - URL: https://public.dhe.ibm.com/software/rational/info/do-more/RAW14109USEN.pdf
   - **Relevância:** Análise estática como prática de prevenção de defeitos

9. **OWASP Foundation.** (2021). *OWASP Top Ten 2021.*
   - URL: https://owasp.org/www-project-top-ten/
   - **Relevância:** Framework padrão de segurança de aplicações; A02 e A07 cobrem credenciais

10. **Nygard, M.** (2011). *Documenting Architecture Decisions.* Cognitect Blog.
    - URL: https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions
    - **Relevância:** Origem e definição do formato ADR

11. **Fowler, M.** *Architecture Decision Record.* Martin Fowler's Bliki.
    - URL: https://martinfowler.com/bliki/ArchitectureDecisionRecord.html
    - **Relevância:** Documentação e contextualização de ADRs por autoridade da indústria

12. **Beyer, B., Jones, C., Petoff, J., & Murphy, N.R.** (Eds.) (2016). *Site Reliability Engineering: How Google Runs Production Systems.* O'Reilly Media.
    - URL: https://sre.google/sre-book/table-of-contents/
    - **Relevância:** Capítulos 6 e 26: monitoramento, logs estruturados, observabilidade

13. **Amazon Web Services.** *Use architectural decision records to streamline technical decision-making.* AWS Prescriptive Guidance.
    - URL: https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/
    - **Relevância:** Validação industrial de ADRs por AWS

14. **Conventional Commits Specification v1.0.0.**
    - URL: https://www.conventionalcommits.org/
    - **Relevância:** Especificação de commits semânticos

15. **OpenTelemetry Project.** *Observability Primer.*
    - URL: https://opentelemetry.io/docs/concepts/observability-primer/
    - **Relevância:** Definição dos três pilares de observabilidade (logs, métricas, traces)

### Fontes Sobre Limitações e Controvérsias

16. **Bossavit, L.** (2016). *The Leprechauns of Software Engineering: How folklore turns into fact and what to do about it.* LeanPub.
    - **Relevância:** Investigação sobre a proveniência disputada do estudo IBM sobre custo de bugs

17. **Wayne, M.** (2021). *"Everyone Cites That 'Bugs Are 100x More Expensive To Fix in Production' Research, But the Study Might Not Even Exist."* The Register, 22 de julho de 2021.
    - URL: https://www.theregister.com/2021/07/22/bugs_expense_bs/
    - **Relevância:** Questionamento da proveniência da afirmação "100x"

---

## Nota Final

Este documento representa um protocolo vivo — não um conjunto de regras imutáveis. Cada dimensão deve ser calibrada ao contexto específico do sistema, equipe e organização. O que não deve ser negociado são os **princípios subjacentes**: segurança como pré-requisito, testes como base de refatoração segura, rastreabilidade como fundação de debugging, e observabilidade como condição de melhoria contínua.

A pergunta operacional correta não é "devo implementar este protocolo?" mas sim:

> **"Qual é o custo esperado de *não* implementar esta prática no meu contexto específico — e sou capaz de arcar com ele quando o momento de pagamento chegar?"**

---

*Documento produzido com base em análise de literatura técnica e acadêmica. Última revisão: 2026. Revisão recomendada a cada 12 meses ou após mudança significativa de stack tecnológico.*
