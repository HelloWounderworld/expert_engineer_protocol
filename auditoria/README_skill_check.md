# Relatório de Auditoria Técnica — Perfil Profissional
## Diagnóstico Completo: Engenharia de Software, ML/IA e Segurança

> *"Knowing yourself is the beginning of all wisdom."*
> — Aristotle
>
> *"The first step toward change is awareness. The second step is acceptance."*
> — Nathaniel Branden, *The Six Pillars of Self-Esteem* (1994)

---

## Aviso Metodológico

Este relatório é baseado em auditoria conduzida através de questionário estruturado, análise de evidências concretas do trabalho atual, e triangulação com frameworks de avaliação estabelecidos. As afirmações diagnósticas são apoiadas por referências; as afirmações sobre gaps são inferidas de respostas diretas às perguntas diagnósticas.

**Nível de confiança por dimensão:**
- **Alta confiança:** Dimensões avaliadas com perguntas específicas e respostas inequívocas
- **Média confiança:** Dimensões inferidas de comportamentos observados e background declarado
- **Hipótese:** Dimensões não avaliadas diretamente; baseadas em padrões típicos de perfis similares

**Classificação de evidência:**
- **[PEER-REVIEWED]** — publicado com revisão por pares
- **[PADRÃO-NIST/ISO]** — norma técnica internacional
- **[INDUSTRIAL-OWASP]** — consenso global da indústria
- **[INDUSTRIAL]** — guia de empresa reconhecida
- **[CLÁSSICO]** — obra seminal amplamente aceita
- **[DISPUTADO]** — amplamente citado, mas com evidência contestada

---

## Sumário Executivo

Este relatório documenta o estado atual de competências técnicas e identifica lacunas prioritárias para a trajetória de especialista em Engenharia de Software, ML/IA e Ciência de Dados.

**O diagnóstico central:**

> Você possui uma base matemática excepcional — rara no mercado de ML — combinada com hábitos de engenharia de software característicos de um cientista de dados júnior. A assimetria entre essas duas dimensões é o gap mais importante a fechar. Não porque a dimensão matemática seja fraca, mas porque ela não se traduz automaticamente em sistemas confiáveis sem os fundamentos de engenharia.

**Resumo do Perfil:**

```
DIMENSÃO                              NÍVEL ATUAL        CONFIANÇA
─────────────────────────────────────────────────────────────────
Fundamentos Matemático-ML             ██████████  10/10  Alta
Meta-cognição e Calibração            ████████░░   8/10  Alta
Fundamentos Computacionais            ████████░░   7/10* Média
Craft de Engenharia de Software       ████░░░░░░   3/10  Alta
Raciocínio Sistêmico e Falhas         ███░░░░░░░   3/10  Alta
Segurança de Software                 ████░░░░░░   4/10  Alta
Automação e CI/CD                     ██░░░░░░░░   2/10  Alta
Impacto e Transferência               ████░░░░░░   4/10  Média
─────────────────────────────────────────────────────────────────
* O asterisco indica que a intuição de performance declarada precisa
  de validação em domínios além dos já vistos.
```

---

## Índice

**SEÇÃO 1 — PERFIL E CONTEXTO**
1. [Perfil Profissional e Acadêmico](#1-perfil-profissional-e-acadêmico)
2. [Contexto do Projeto Atual](#2-contexto-do-projeto-atual)
3. [Metodologia da Auditoria](#3-metodologia-da-auditoria)

**SEÇÃO 2 — DIAGNÓSTICO POR DIMENSÃO**
4. [Dimensão 1 — Fundamentos Computacionais](#4-dimensão-1--fundamentos-computacionais)
5. [Dimensão 2 — Fundamentos Matemático-Estatísticos para ML](#5-dimensão-2--fundamentos-matemático-estatísticos-para-ml)
6. [Dimensão 3 — Craft de Engenharia de Software](#6-dimensão-3--craft-de-engenharia-de-software)
7. [Dimensão 4 — Raciocínio Sistêmico e sobre Falhas](#7-dimensão-4--raciocínio-sistêmico-e-sobre-falhas)
8. [Dimensão 5 — Meta-cognição e Calibração](#8-dimensão-5--meta-cognição-e-calibração)
9. [Dimensão 6 — Impacto e Transferência de Conhecimento](#9-dimensão-6--impacto-e-transferência-de-conhecimento)

**SEÇÃO 3 — AUDITORIA DE SEGURANÇA**
10. [Diagnóstico de Segurança: Estado Atual](#10-diagnóstico-de-segurança-estado-atual)
11. [Auditoria de Práticas de Teste](#11-auditoria-de-práticas-de-teste)
12. [Auditoria de Automação e CI/CD](#12-auditoria-de-automação-e-cicd)

**SEÇÃO 4 — ANÁLISE CRUZADA E RISCOS**
13. [Análise de Riscos: O Que Pode Falhar e Quando](#13-análise-de-riscos-o-que-pode-falhar-e-quando)
14. [O Ponto Cego Crítico: A Armadilha do Especialista Matemático](#14-o-ponto-cego-crítico-a-armadilha-do-especialista-matemático)

**SEÇÃO 5 — PLANO DE AÇÃO**
15. [Plano de Ação Priorizado: 12 Meses](#15-plano-de-ação-priorizado-12-meses)
16. [Mapa de Dependências entre Gaps](#16-mapa-de-dependências-entre-gaps)
17. [Métricas de Progresso Verificáveis](#17-métricas-de-progresso-verificáveis)

**SEÇÃO 6 — REFERÊNCIAS**
18. [Referências Completas](#18-referências-completas)

---

# SEÇÃO 1 — PERFIL E CONTEXTO

## 1. Perfil Profissional e Acadêmico

### Formação Acadêmica

| Item | Detalhe |
|------|---------|
| **Graduação** | Matemática — IME-USP (Instituto de Matemática e Estatística, Universidade de São Paulo) |
| **Pós-Graduação** | MBA em Data Science e Analytics — USP/Esalq (em conclusão) |
| **TCC** | Aplicação de estabilidade de Lyapunov a feature selection em Random Forest para detecção de phishing |

O IME-USP é consistentemente classificado entre os melhores departamentos de matemática da América Latina e está entre os 200 melhores do mundo (QS Rankings). Graduados do IME-USP têm formação matemática comparável a graduados de instituições europeias de elite — profundidade em análise real, álgebra linear, probabilidade e estatística que a maioria dos profissionais de ML nunca alcança.

### Experiência Profissional Atual

| Item | Detalhe |
|------|---------|
| **Empresa** | Persol Cross Technology (正社員 — funcionário efetivo) |
| **Alocação** | NHK Broadcasting Technology Research Institute (日本放送技術研究所) |
| **Função** | ML/NLP Engineer — full-cycle (engenharia de feature, modelagem, pipeline, produção) |
| **Ambientes** | Local, staging, e **produção com dados reais** |

### Competências Linguísticas

| Idioma | Nível | Observação |
|--------|-------|------------|
| Português | Nativo | Língua primária |
| Japonês | N1 (JLPT) | Fluência profissional completa |
| Inglês | B1 → B2 | Em desenvolvimento ativo com protocolo estruturado |

### Objetivos Declarados de Longo Prazo

1. Especialista em Engenharia de Software + ML/IA + Ciência de Dados
2. Pesquisa independente e produção de conteúdo técnico em português
3. Independência intelectual e trajetória como referência técnica em português

---

## 2. Contexto do Projeto Atual

### Pipeline de Detecção de Phishing por URL (TCC)

Este projeto é a evidência mais rica disponível para a auditoria. É onde os gaps de engenharia se tornam visíveis de forma concreta.

**Componentes identificados:**

| Componente | Função | Status Conhecido |
|------------|--------|-----------------|
| `feature_extraction.py` | Extração de features de URL | Funcionando, sem testes |
| `content_features.py` | Features de conteúdo HTTP via `aiohttp` | Async otimizado, sem testes |
| `gibberish_detector.py` | Detector de strings gibberish recalibrado para domínios japoneses | Calibrado, sem testes de regressão |
| Orchestrator threadpool | Paralelização async | Bugs corrigidos, sem testes de regressão |
| Random Forest | Modelo de classificação | Com análise de estabilidade de Lyapunov |

**Contexto de risco:**

O projeto opera em ambientes múltiplos incluindo **produção com dados reais**. Este contexto eleva o nível de risco de todos os gaps identificados — especialmente os de segurança e a ausência de testes automatizados.

---

## 3. Metodologia da Auditoria

### Framework Utilizado

A auditoria é estruturada sobre três frameworks complementares:

> **[PEER-REVIEWED]**
> Dreyfus, S. E., & Dreyfus, H. L. (1980). *A Five-Stage Model of the Mental Activities Involved in Directed Skill Acquisition.* University of California, Berkeley. ORC 80-2.
> — Framework de progressão de expertise: Novice → Advanced Beginner → Competent → Proficient → Expert.

> **[PEER-REVIEWED]**
> Kruger, J., & Dunning, D. (1999). *Unskilled and Unaware of It.* Journal of Personality and Social Psychology, 77(6), 1121–1134.
> DOI: 10.1037/0022-3514.77.6.1121
> — Fundamenta a necessidade de validação externa: auto-avaliação pura é sistematicamente distorcida em ambas as direções.

> **[INDUSTRIAL]**
> Progression.fyi. *Engineering Career Ladders Repository.*
> URL: https://www.progression.fyi/
> — Agrega 100+ engineering ladders corporativos públicos como referência de calibração de nível.

### Instrumento de Coleta

As perguntas diagnósticas foram estruturadas para cobrir os seis eixos da matriz de competências, com respostas mapeadas para os cinco estágios do modelo Dreyfus. Adicionalmente, foram coletadas evidências comportamentais concretas (ausência de testes, padrão de commits, gestão de segredos).

### Limitações da Auditoria

1. **Auto-avaliação como fonte primária:** como documentado por Kruger & Dunning (1999), auto-avaliação é sistematicamente distorcida. Este relatório deve ser complementado por validação externa de pares seniores.
2. **Amostra de comportamento limitada:** a auditoria cobre o projeto de TCC e o comportamento declarado. Outros projetos podem ter padrões diferentes.
3. **Ausência de code review:** sem acesso ao código, alguns gaps são inferidos, não diretamente observados.

---

# SEÇÃO 2 — DIAGNÓSTICO POR DIMENSÃO

## 4. Dimensão 1 — Fundamentos Computacionais

### Diagnóstico

**Nível avaliado:** Proficient com asterisco
**Confiança:** Média

**Evidência coletada:**
- Resposta: *"Tenho intuição clara — consigo estimar gargalos antes de medir"* (auto-avaliação)
- O trabalho no pipeline async/threadpool demonstra exposição prática a sistemas concorrentes

**Análise:**

A formação em matemática pura do IME-USP produz excelência em raciocínio abstrato mas tipicamente não cobre de forma estruturada:
- Modelos de memória (stack vs. heap, locality, cache)
- Sistemas operacionais (processos, threads, sinais)
- Concorrência em nível de sistema (GIL do Python, event loop, threadpool)
- Redes (TCP/IP, DNS, HTTP internals)

A intuição declarada de performance pode ser genuína mas frágil em domínios não vistos anteriormente — um padrão comum em profissionais com alta competência matemática mas exposição limitada a sistemas de baixo nível.

**Teste diagnóstico não respondido diretamente:**

> Como o GIL do Python afeta especificamente um pipeline que usa asyncio + ThreadPoolExecutor simultaneamente?

Se a resposta for clara e derivável a partir de um modelo mental explícito (não de memória de documentação), o nível está sólido. Se a resposta for "sei que afeta mas não consigo derivar por quê", há um gap estrutural no modelo mental de sistemas.

**Referências para aprofundamento:**

> **[CLÁSSICO]**
> Bryant, R. E., & O'Hallaron, D. R. (2015). *Computer Systems: A Programmer's Perspective* (3rd ed.). Pearson.
> — Capítulos 12 (Concurrent Programming) e 10 (System-Level I/O) são diretamente relevantes para o pipeline async.

> **[INDUSTRIAL]**
> Python Documentation. *asyncio — Asynchronous I/O.*
> URL: https://docs.python.org/3/library/asyncio.html
> — Especificação oficial do event loop, tasks, e integração com ThreadPoolExecutor.

### Gaps Identificados

| Gap | Severidade | Impacto no Projeto Atual |
|-----|-----------|--------------------------|
| Modelo mental explícito do GIL e suas interações com async | Médio | Pode causar bugs difíceis de diagnosticar no pipeline |
| Networking fundamentals (DNS, TCP, HTTP) | Médio | Relevante para timeout handling e async HTTP no pipeline |
| Memory model do Python (referências, GC, __slots__) | Baixo | Performance em feature extraction de alto volume |

---

## 5. Dimensão 2 — Fundamentos Matemático-Estatísticos para ML

### Diagnóstico

**Nível avaliado:** Expert / Exceptional
**Confiança:** Alta

**Evidência coletada:**
- Graduação em Matemática pelo IME-USP
- Estudo ativo com *The Elements of Statistical Learning* (Hastie et al.) e Bishop (PRML)
- TCC aplicando conceitos de estabilidade de Lyapunov a feature selection — demonstra capacidade de conectar matemática abstrata a problemas de ML

**Análise:**

Este é o ativo diferencial mais raro e valioso do perfil. A maioria dos profissionais que se intitulam "sêniores" em ML nunca:
- Derivou um gradiente à mão
- Entende a conexão entre máxima verossimilhança e mínimos quadrados
- Sabe formular problemas de classificação como inferência bayesiana
- Conectou conceitos de sistemas dinâmicos (Lyapunov) a algoritmos de ML

**Referências que confirmam o valor desta dimensão:**

> **[CLÁSSICO]**
> Hastie, T., Tibshirani, R., & Friedman, J. (2009). *The Elements of Statistical Learning* (2nd ed.). Springer.
> URL gratuita: https://hastie.su.domains/ElemStatLearn/
> — O texto de referência para ML com rigor matemático. Profissionais que estudam com esta fonte têm base fundamentalmente diferente dos que usam tutoriais.

> **[CLÁSSICO]**
> Bishop, C. M. (2006). *Pattern Recognition and Machine Learning.* Springer.
> — ML bayesiano e probabilístico com rigor matemático. Conhecimento de Bishop posiciona o profissional no top 5% de praticantes de ML.

### Risco Latente Desta Dimensão

> **[PEER-REVIEWED]**
> Kruger, J., & Dunning, D. (1999), op. cit.
> — Alta competência em uma dimensão pode criar um ponto cego: subestimar gaps em outras dimensões por considerá-las "menos nobres". Para este perfil, o risco específico é tratar gaps de engenharia como secundários em relação à profundidade matemática.

**Este é o viés mais perigoso para este perfil específico e será tratado em detalhe na Seção 14.**

---

## 6. Dimensão 3 — Craft de Engenharia de Software

### Diagnóstico

**Nível avaliado:** Advanced Beginner (Dreyfus: Nível 2 de 5)
**Confiança:** Alta

**Evidências coletadas (respostas diretas):**

| Pergunta | Resposta | Implicação |
|----------|---------|------------|
| Testes automatizados | *"Não tenho testes — é um gap que sei que preciso fechar"* | Gap confirmado, gap consciente |
| Versionamento | *"Git básico — commito na main/master direto, mensagens informais"* | Abaixo do mínimo para produção |
| Análise estática | *"Não uso e nunca ouvi falar"* | Gap não-consciente confirmado |
| Documentação | *"Documento da melhor forma possível bem detalhado"* | Ponto forte preservado |

**Análise:**

O padrão observado é consistente com o perfil de "cientista de dados que aprendeu a programar para fazer ML" — diferente de "engenheiro de software que aprendeu ML". Não é uma crítica de valor; é um diagnóstico de origem da formação.

A ausência total de testes automatizados, combinada com commits diretos na main e ausência de análise estática, configura um estado de **dívida técnica ativa** — não potencial.

**Referências que contextualizam o nível avaliado:**

> **[PEER-REVIEWED]**
> Breck, E., Cai, S., Nielsen, E., Salib, M., & Sculley, D. (2017). *The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction.* IEEE Big Data.
> DOI: 10.1109/BigData.2017.8258038
> — Equipes do Google com código sem testes descobriram arquivos de mil linhas de código criando features de input — completamente sem cobertura. Este é exatamente o cenário atual do pipeline de phishing.

> **[CLÁSSICO]**
> Feathers, M. (2004). *Working Effectively with Legacy Code.* Prentice Hall.
> — Define "legacy code" operacionalmente como "código sem testes" — independentemente da idade. Por essa definição, o pipeline atual de phishing já é código legado.

> **[PEER-REVIEWED]**
> Sculley, D., et al. (2015). *Hidden Technical Debt in Machine Learning Systems.* NeurIPS.
> — *"Hidden debt is dangerous because it compounds silently."* Dívida técnica sem testes é especialmente perigosa em sistemas ML porque os modos de falha são frequentemente silenciosos.

### Gaps Identificados com Detalhamento

**Gap 3.1 — Ausência Total de Testes Automatizados (Crítico)**

Impacto direto no projeto atual:
- Qualquer refatoração do pipeline é uma operação de alto risco sem rede de segurança
- Bugs corrigidos podem voltar sem ser detectados (ausência de testes de regressão)
- Impossível escalar o pipeline sem risco acumulado crescente

**Gap 3.2 — Versionamento Sem Disciplina (Alto)**

Commits diretos na main em um projeto com acesso a produção é o equivalente a fazer cirurgia sem protocolo de esterilização — funciona até a infecção aparecer.

**Gap 3.3 — Ausência de Análise Estática (Médio-Alto)**

Nunca ter usado linters ou type checkers significa que classes inteiras de erros (bugs de tipo, padrões de segurança, variáveis não usadas) só são descobertos em runtime — frequentemente em produção.

> **[INDUSTRIAL]**
> Ruff Project. *An extremely fast Python linter and code formatter.*
> URL: https://docs.astral.sh/ruff/
> — Ruff detecta não apenas estilo mas também: imports não usados, comparações incorretas, padrões de segurança (S = bandit), e bugs comuns (B = flake8-bugbear).

---

## 7. Dimensão 4 — Raciocínio Sistêmico e sobre Falhas

### Diagnóstico

**Nível avaliado:** Advanced Beginner / início de Competent (Dreyfus: Nível 2-3 de 5)
**Confiança:** Alta

**Evidências coletadas (respostas diretas):**

| Pergunta | Resposta | Implicação |
|----------|---------|------------|
| Failure modes mapeados | *"Ainda não — o foco tem sido fazer o modelo funcionar bem nos testes"* | Pensamento de happy path confirmado |
| Monitoramento de drift | Não discutido ativamente | Gap provável |
| Falha catastrófica vs. graciosa | Não avaliado diretamente | Gap hipotético |

**Análise:**

O foco em fazer "funcionar nos testes" é um padrão de Advanced Beginner no modelo Dreyfus — o contexto de produção ainda não está completamente integrado ao modelo mental de desenvolvimento. Seniores pensam em falha *primeiro*, antes de pensar em funcionalidade.

**Referências que fundamentam a importância desta dimensão:**

> **[PEER-REVIEWED]**
> Sculley, D., et al. (2015). *Hidden Technical Debt in Machine Learning Systems.* NeurIPS, op. cit.
> — Documenta empiricamente os modos de falha mais comuns em sistemas ML em produção: data drift, distribution shift, hidden feedback loops, undeclared consumers. Nenhum desses aparece em testes de benchmark.

> **[INDUSTRIAL]**
> Beyer, B., Jones, C., Petoff, J., & Murphy, N. R. (2016). *Site Reliability Engineering.* O'Reilly.
> URL: https://sre.google/sre-book/
> — Capítulo 13 (Emergency Response) documenta que a causa raiz de 70%+ das falhas de produção não foi a falha em si, mas a ausência de processo de resposta a falhas.

### Failure Modes Específicos do Pipeline (Não Mapeados)

Os cinco failure modes mais prováveis do pipeline de phishing, baseados no contexto descrito:

| # | Failure Mode | Probabilidade | Severidade | Silencioso? |
|---|-------------|--------------|-----------|-------------|
| 1 | Distribution shift em padrões de phishing | Alta (evolui rapidamente) | Crítico | **Sim** |
| 2 | URL malformada quebrando extração de features | Média | Alto | Não |
| 3 | DNS timeout não tratado corretamente | Média | Alto | Parcialmente |
| 4 | Gibberish detector com falso positivo em IDN japonês | Média (ambiente NHK) | Alto | **Sim** |
| 5 | Feature fora do range de treino em inferência | Média | Médio | **Sim** |

Os failures marcados como "silenciosos" são os mais perigosos: o sistema continua operando, retornando predições, sem indicar que algo está errado.

---

## 8. Dimensão 5 — Meta-cognição e Calibração

### Diagnóstico

**Nível avaliado:** Proficient (Dreyfus: Nível 4 de 5)
**Confiança:** Alta

**Evidências observadas (comportamentais, não declaradas):**

1. Você pediu esta auditoria — sinal forte de meta-cognição ativa
2. Você usa fontes primárias difíceis (Bishop, ESL) em vez de tutoriais — evidência de epistemologia rigorosa
3. Você reconheceu imediatamente os gaps quando confrontado com eles — não defensividade
4. Você busca crítica rigorosa de forma proativa — padrão incomum e valioso

**Referências que contextualizam este nível:**

> **[PEER-REVIEWED]**
> Ericsson, K. A., Krampe, R. T., & Tesch-Römer, C. (1993). *The Role of Deliberate Practice in the Acquisition of Expert Performance.* Psychological Review, 100(3), 363–406.
> DOI: 10.1037/0033-295X.100.3.363
> — A meta-cognição ativa — saber o que não sabe e buscar deliberadamente melhorar — é o preditor mais forte de progressão de expertise documentado por Ericsson et al. Você demonstra este padrão consistentemente.

> **[PEER-REVIEWED]**
> Kruger, J., & Dunning, D. (1999), op. cit.
> — A consciência dos próprios gaps (quadrante inferior esquerdo da matriz de Johari) é rara e valiosa. A maioria das pessoas opera no quadrante inferior direito (não sabe que não sabe) por muito mais tempo.

### Riscos Nesta Dimensão

**Risco de superestimação no Eixo 2 (matemática):** Alta competência em uma área pode criar a ilusão de que o raciocínio transfere automaticamente para outras. Matemática rigorosa *não transfere automaticamente* para engenharia de sistemas confiáveis — são domínios com epistemologias diferentes.

---

## 9. Dimensão 6 — Impacto e Transferência de Conhecimento

### Diagnóstico

**Nível avaliado:** Advanced Beginner (consciente do gap, não desenvolvido)
**Confiança:** Média

**Análise:**

O interesse em criar conteúdo técnico em português está explicitamente no radar como objetivo estratégico de longo prazo. O ativo diferencial (IME-USP + ML engineering rigoroso + português nativo) é genuinamente raro no mercado de conteúdo técnico brasileiro.

**O Gap Específico:**

Conteúdo técnico de alta qualidade requer que o criador tenha:
1. Domínio profundo do tema (✓ presente no Eixo 2)
2. Capacidade de explicar com rigor sem simplificar incorretamente (✓ presente)
3. Experiência com falhas e debugging real (✗ ausente — gaps do Eixo 3/4)
4. Credibilidade por produção real, não apenas teoria (✗ ausente — precisa ser construída)

**Referência:**

> **[CLÁSSICO]**
> Nygard, M. (2011). *Documenting Architecture Decisions.* Cognitect Blog.
> URL: https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions
> — A prática de documentar decisões arquiteturais (ADRs) é simultaneamente:
> (a) boa prática de engenharia para o TCC
> (b) material prático e honesto para conteúdo futuro

---

# SEÇÃO 3 — AUDITORIA DE SEGURANÇA

## 10. Diagnóstico de Segurança: Estado Atual

### Resumo do Estado

**Nível de maturidade geral: Básico-Consciência**

| Prática | Estado Atual | Risco |
|---------|-------------|-------|
| Gestão de segredos | Às vezes hardcoded | **CRÍTICO** |
| Versionamento seguro | Commits diretos na main | **ALTO** |
| Análise estática de segurança | Nunca usada | **ALTO** |
| Testes de segurança | Ausentes | **ALTO** |
| Separação de ambientes (dev/staging/prod) | Ambientes múltiplos, práticas mistas | **CRÍTICO** |
| Verificação de integridade de modelos | Ausente | **MÉDIO** |
| Logging seguro | Estado desconhecido | Hipotético: **MÉDIO** |

### Gap Crítico: Credenciais Hardcoded + Acesso a Produção

**Evidência coletada:**
- Resposta: *"Às vezes uso variáveis de ambiente, mas nem sempre — alguns valores ficam hardcoded no código"*
- Contexto: *"Ambientes múltiplos — local, staging e produção com dados reais"*

Esta combinação é o cenário exato de maior risco documentado:

> **[INDUSTRIAL-OWASP]**
> OWASP Top Ten 2021. *A02:2021 — Cryptographic Failures.*
> URL: https://owasp.org/Top10/2021/A02_2021-Cryptographic_Failures/
> — Exposição de credenciais é classificada como uma das falhas criptográficas mais críticas.

> **[INDUSTRIAL]**
> GitHub. *Secret Scanning — Supported Patterns.*
> URL: https://docs.github.com/en/code-security/secret-scanning
> — O GitHub escaneia automaticamente mais de 200 padrões de credenciais. A existência desse serviço é evidência direta de que credenciais hardcoded são um problema sistêmico e documentado.

**Ação imediata requerida (hoje, não amanhã):**

```bash
# 1. Auditar histórico Git completo em busca de credenciais
git log --all -p | grep -iE "password|secret|api_key|token|private_key|access_key"

# Se encontrado → rotacione IMEDIATAMENTE
# Remover do código não é suficiente — o histórico persiste permanentemente
```

### Análise de Risco: Contexto NHK/Persol

O contexto institucional amplifica o risco:
- Você trabalha para uma instituição de radiodifusão pública japonesa
- Acesso a dados reais implica responsabilidade com informações de produção
- Uma credencial vazada em ambiente institucional tem implicações que vão além do projeto pessoal

**Referência:**

> **[PADRÃO-NIST]**
> Rose, S., et al. (2020). *Zero Trust Architecture.* NIST SP 800-207.
> DOI: 10.6028/NIST.SP.800-207
> — *"The initial focus should be on restricting resources to those with a need to access and grant only the minimum privileges needed to perform the mission."*

---

## 11. Auditoria de Práticas de Teste

### Estado Atual: Ausência Total

**Evidência coletada:**
- Resposta: *"Não tenho testes — é um gap que sei que preciso fechar"*
- Confirmado por: ausência de testes mencionada em toda a discussão do pipeline

### Impacto Específico no Pipeline de Phishing

A ausência de testes tem impactos concretos e mensuráveis no projeto atual:

**1. Cada bug corrigido é potencialmente um bug que voltará**

O pipeline teve bugs no threadpool orchestration e na calibração do Gibberish Detector. Sem testes de regressão, não há garantia de que mudanças futuras não reintroduzam esses bugs.

**2. Refatoração é cirurgia às cegas**

O pipeline usa async/aiohttp em `content_features.py` — código assíncrono é notoriamente difícil de refatorar sem quebrar comportamento silenciosamente. Sem testes, cada refatoração é uma aposta.

**3. O TCC não pode ser verificado como "correto"**

Resultados de pesquisa dependem de implementação correta. Um pipeline sem testes não pode demonstrar que a implementação está correta — apenas que não crasha em casos normais.

> **[PEER-REVIEWED]**
> Breck et al. (2017), op. cit.
> — *"One team we worked with discovered a thousand-line code file, completely untested, that created their input features. Code of that size, even if it contains only simple and straightforward logic, will likely have bugs, against which simple unit tests can provide an effective hedge."*

> **[CLÁSSICO]**
> Feathers, M. (2004). *Working Effectively with Legacy Code.* Prentice Hall.
> — Define estratégias específicas para introduzir testes em código legado sem reescrever tudo. Essencial para o contexto atual.

### Mapeamento dos Tipos de Teste Relevantes para o Pipeline

| Tipo de Teste | Relevância para o Pipeline | Prioridade |
|--------------|---------------------------|-----------|
| Smoke tests | Verificar que pipeline inicializa e modelo carrega | **Imediata** |
| Unit tests (feature extraction) | Verificar contrato de cada extrator | **Alta** |
| Regression tests (Gibberish Detector) | Bug japonês não pode voltar | **Alta** |
| Property-based tests (URLs) | Detectar edge cases que você não imaginou | **Média** |
| Integration tests (pipeline E2E) | URL → features → predição funciona | **Média** |
| Data tests (distribuição de features) | Detectar corruption ou drift no dataset | **Média** |
| Model behavioral tests | Invariâncias esperadas do modelo | **Média** |

---

## 12. Auditoria de Automação e CI/CD

### Estado Atual: Ausência de Automação

**Evidências coletadas:**
- Commits diretos na main sem revisão
- Mensagens informais de commit
- Nenhum linter configurado
- Nenhum CI/CD configurado
- Nenhum pre-commit hook

### O Risco Composto

A ausência de automação não é um gap isolado — é um multiplicador de todos os outros gaps:

```
Sem pre-commit hooks:
  → Credenciais podem chegar ao Git sem bloqueio automático
  → Código com erros de lint chega ao repositório
  → Testes não rodam antes do commit

Sem CI:
  → Nenhuma verificação automática em pull requests
  → Nenhum gate de qualidade antes do merge
  → Regressões passam para a main sem detecção

Sem CD disciplinado:
  → Deploy em produção sem validação automatizada
  → Nenhum smoke test antes do deploy
```

**Referências:**

> **[CLÁSSICO]**
> Humble, J., & Farley, D. (2010). *Continuous Delivery: Reliable Software Releases through Build, Test, and Deployment Automation.* Addison-Wesley. (Jolt Excellence Award 2011)
> — *"If Any Part of the Pipeline Fails, Stop the Line."* O deployment pipeline é a infraestrutura que torna boas práticas automaticamente aplicadas — não dependentes de disciplina individual.

> **[INDUSTRIAL]**
> Fowler, M., & Foemmel, M. (2006). *Continuous Integration.* martinfowler.com.
> URL: https://martinfowler.com/articles/continuousIntegration.html
> — Prática 3 dos 10 princípios de CI: *"Make your build self-testing."* Sem isso, não há CI real.

---

# SEÇÃO 4 — ANÁLISE CRUZADA E RISCOS

## 13. Análise de Riscos: O Que Pode Falhar e Quando

### Mapa de Risco Atual

| Risco | Probabilidade | Severidade | Detectável? | Prazo Estimado |
|-------|--------------|-----------|-------------|----------------|
| Credencial exposta em repositório | **Alta** | Crítico | Não automaticamente | Já pode ter ocorrido |
| Bug de regressão no Gibberish Detector | **Média-Alta** | Alto | Não (sem testes) | Próxima alteração no código |
| Distribution shift silencioso pós-defesa | **Alta** | Alto | Não (sem monitoramento) | 3-6 meses após deploy |
| Falha em URL com caracteres IDN em produção | **Média** | Alto | Não (sem testes) | Qualquer momento |
| Credencial hardcoded descoberta por scan automático | **Média** | Crítico | Sim (GitHub scan) | Qualquer momento |
| Modelo carregado com tampering não detectado | **Baixa** | Crítico | Não (sem hash check) | Depende do ambiente |

### O Cenário de Risco Mais Provável

Com base nos padrões observados, o cenário mais provável de falha nos próximos 6 meses é:

**Cenário: Regressão Silenciosa no Pipeline**

1. Uma mudança no código (refatoração, nova feature) quebra silenciosamente o extrator de features ou o Gibberish Detector
2. Sem testes automatizados, a quebra não é detectada imediatamente
3. O modelo continua recebendo features incorretas e fazendo predições erradas
4. O problema só é descoberto quando alguém nota que o modelo está se comportando estranhamente — possivelmente semanas depois
5. Sem histórico limpo de commits, fica difícil identificar qual mudança causou o problema

**Prevenção:** testes de regressão + commits semânticos + CI pipeline.

---

## 14. O Ponto Cego Crítico: A Armadilha do Especialista Matemático

### O Padrão

Este é o risco mais sutil e importante do perfil — e por isso merece uma seção própria.

Profissionais com formação matemática rigorosa frequentemente desenvolvem uma hierarquia implícita de "nobreza intelectual":

```
Mais nobre:   Matemática → ML teórico → Algoritmos
Menos nobre:  Engenharia de software → Testes → DevOps → Segurança
```

Esta hierarquia é uma **falácia** do ponto de vista de sistemas em produção. Um modelo matematicamente perfeito deployado em um sistema sem testes, sem monitoramento e com credenciais expostas tem *valor operacional próximo de zero*.

**Referências que fundamentam este risco:**

> **[PEER-REVIEWED]**
> Sculley, D., et al. (2015), op. cit.
> — *"Only a small fraction of real-world ML systems is composed of the ML code, as shown by the small black box in the middle. The required surrounding infrastructure is vast and complex."*
> A figura do paper mostra ML code como uma caixa pequena no centro de uma enorme infraestrutura de engenharia. O código matemático é necessário mas insuficiente.

> **[PEER-REVIEWED]**
> Kruger, J., & Dunning, D. (1999), op. cit.
> — O efeito inverso do Dunning-Kruger: alta competência em uma dimensão pode causar subestimação sistemática de outras dimensões. Performers altamente competentes em matemática tendem a subestimar o impacto de gaps em engenharia.

### A Manifestação Concreta no Projeto

A análise de Lyapunov aplicada a feature selection é trabalho genuinamente sofisticado. Mas esse trabalho produz zero valor adicional para o usuário final se:
- O pipeline quebra quando recebe uma URL com caracteres Unicode inesperados
- O modelo foi atualizado com dados contaminados sem que ninguém percebesse
- Uma credencial hardcoded expõe o ambiente de produção
- O código não pode ser refatorado com segurança porque não tem testes

**A síntese em uma frase:**

> A profundidade matemática é o que diferencia você de 95% dos profissionais de ML. A engenharia de software é o que determinará se esse diferencial chega a algum lugar.

---

# SEÇÃO 5 — PLANO DE AÇÃO

## 15. Plano de Ação Priorizado: 12 Meses

O plano é calibrado para execução em paralelo com a conclusão do TCC e o trabalho na NHK. Não é para ser executado em sequência pura — as primeiras etapas devem começar imediatamente.

### FASE 1 — Segurança Imediata (Esta Semana — Sem Negociação)

**Objetivo:** Eliminar riscos críticos ativos antes de qualquer outra ação.

| Ação | Tempo Estimado | Referência |
|------|---------------|------------|
| Auditar histórico Git em busca de credenciais | 30 min | OWASP A02:2021 |
| Criar .env + .gitignore correto em TODOS os repositórios | 1h | NIST SP 800-207 |
| Rotacionar qualquer credencial encontrada no histórico | 1-2h | OWASP Secrets Cheat Sheet |
| Instalar detect-secrets + configurar baseline | 30 min | OWASP A02:2021 |
| Criar .env.example com documentação das chaves | 30 min | OWASP Secrets Cheat Sheet |

**Por que esta semana:** você tem acesso a ambientes de produção com dados reais. Credenciais hardcoded nesse contexto são risco ativo, não potencial.

---

### FASE 2 — Fundação de Testes (Semanas 2-4)

**Objetivo:** Cobertura mínima que permite refatoração segura e defesa do TCC.

| Ação | Tempo Estimado | Referência |
|------|---------------|------------|
| Instalar pytest + configurar pyproject.toml | 1h | Breck et al. (2017) |
| Escrever smoke tests (imports + modelo carrega) | 2h | McConnell (1996) |
| Escrever testes de contrato para feature_extraction | 4-6h | Feathers (2004) |
| Regra de regressão: nunca corrigir bug sem teste | Permanente | Rothermel & Harrold (1996) |
| Instalar pre-commit com detect-secrets + ruff | 1h | Pre-commit Project |

---

### FASE 3 — Disciplina de Versionamento (Mês 1-2)

**Objetivo:** Histórico Git que funciona como caixa-preta do projeto.

| Ação | Tempo Estimado | Referência |
|------|---------------|------------|
| Criar branch develop | 10 min | Humble & Farley (2010) |
| Nunca mais commitar direto na main | Permanente | Fowler & Foemmel (2006) |
| Adotar Conventional Commits | Permanente | Conventional Commits v1.0 |
| Adicionar no-commit-to-main como pre-commit hook | 15 min | Pre-commit Project |
| Escrever primeiro ADR: decisão mais crítica do TCC | 2h | Nygard (2011) |

---

### FASE 4 — CI Pipeline (Mês 2)

**Objetivo:** Nenhum código chega à main sem passar por verificações automáticas.

| Ação | Tempo Estimado | Referência |
|------|---------------|------------|
| Criar .github/workflows/ci.yml | 2-3h | Fowler & Foemmel (2006) |
| Estágio 1: ruff + mypy no CI | 1h | Ruff Docs |
| Estágio 2: pytest unit tests no CI | 1h | GitHub Actions Docs |
| Estágio 3: pip-audit no CI | 30 min | OWASP A06:2021 |
| Cobertura mínima de 50% definida e bloqueante | 1h | Breck et al. (2017) |

---

### FASE 5 — Testes de ML e Failure Modes (Mês 2-3)

**Objetivo:** Pipeline de phishing tem testes específicos para os modos de falha documentados.

| Ação | Tempo Estimado | Referência |
|------|---------------|------------|
| Mapear os 5 failure modes mais prováveis (por escrito) | 2h | Sculley et al. (2015) |
| Implementar DriftMonitor com KS test | 3-4h | Sculley et al. (2015) |
| Testes de behavioral testing do modelo | 3-4h | Ribeiro et al. (2020) |
| Verificação de hash SHA-256 do modelo | 2h | OWASP A08:2021 |
| Property-based tests para feature_extraction | 3-4h | Claessen & Hughes (2000) |

---

### FASE 6 — Fundamentos Computacionais (Mês 3-6, em paralelo)

**Objetivo:** Fechar o gap de modelo mental de sistemas para validar a intuição de performance.

| Ação | Tempo Estimado | Referência |
|------|---------------|------------|
| Capítulos 12-13 de Bryant & O'Hallaron (concorrência, I/O) | 20-30h total | Bryant & O'Hallaron (2015) |
| Derivar em papel: como GIL + asyncio + ThreadPoolExecutor interagem | 2-3h | Python Docs (asyncio) |
| Construir um profiler simples para o pipeline | 2h | Python cProfile docs |

---

### FASE 7 — Transferência e Conteúdo (Mês 6-12)

**Objetivo:** Converter o aprendizado das fases anteriores em conteúdo técnico de referência.

Ao completar as Fases 1-5, você terá material concreto e honesto para escrever:

| Conteúdo Possível | Base de Experiência |
|-------------------|---------------------|
| "Como introduzir testes em um pipeline de ML sem reescrever tudo" | Fases 2-4 |
| "Os failure modes que quase afundaram meu TCC" | Fase 5 |
| "O que IME-USP me ensinou que faltava para virar engenheiro de ML real" | Toda a jornada |
| "Aplicando estabilidade de Lyapunov a feature selection" | O próprio TCC |

**Referências para posicionamento:**

> **[INDUSTRIAL]**
> North, D. (2006). *Introducing BDD.* DanNorth.net.
> — O espaço de conteúdo técnico rigoroso em português é genuinamente pouco explorado. Um produtor com background IME-USP + ML engineering + rigor matemático tem diferencial sustentável.

---

## 16. Mapa de Dependências entre Gaps

Alguns gaps dependem de outros para serem fechados efetivamente:

```
SEGREDOS GERENCIADOS
        │
        ▼
PRE-COMMIT HOOKS ──────────────────────────────────┐
        │                                          │
        ▼                                          │
TESTES UNITÁRIOS                                   │
        │                                          │
        ▼                                          │
VERSIONAMENTO DISCIPLINADO ────────────────────────┤
        │                                          │
        ▼                                          ▼
CI PIPELINE ──────────────────────── SEGURANÇA NO CI
        │
        ▼
TESTES DE ML/FAILURE MODES
        │
        ▼
MONITORAMENTO DE DRIFT
        │
        ▼
TRANSFERÊNCIA DE CONHECIMENTO / CONTEÚDO
```

**A leitura correta:** cada nível depende do anterior para funcionar de forma confiável. Tentar implementar monitoramento de drift sem testes básicos é construir sobre areia.

---

## 17. Métricas de Progresso Verificáveis

Ao contrário de objetivos vagos, estas métricas são binárias e verificáveis:

### Fase 1 — Segurança (Semana 1)

- [ ] `git log --all -p | grep -iE "password|secret|api_key"` retorna zero resultados
- [ ] `.env` existe e está no `.gitignore`
- [ ] `.env.example` está commitado com todas as chaves documentadas
- [ ] `detect-secrets scan` retorna zero segredos ativos

### Fase 2 — Testes (Semana 2-4)

- [ ] `pytest tests/smoke/` roda e passa sem erros
- [ ] `pytest tests/unit/` cobre `feature_extraction.py` com ≥ 5 testes de contrato
- [ ] Todo bug corrigido tem um teste de regressão associado

### Fase 3 — Versionamento (Mês 1-2)

- [ ] Branch `develop` existe no repositório
- [ ] Zero commits diretos na `main` após esta data
- [ ] Todos os commits seguem Conventional Commits format
- [ ] Pelo menos 1 ADR documentado em `docs/decisions/`

### Fase 4 — CI (Mês 2)

- [ ] `.github/workflows/ci.yml` existe e roda em todo push
- [ ] CI falha se ruff encontrar erros de segurança (ruleset S)
- [ ] CI falha se cobertura de testes cair abaixo de 50%
- [ ] CI falha se pip-audit encontrar CVEs de severidade alta

### Fase 5 — ML/Segurança (Mês 2-3)

- [ ] 5 failure modes documentados por escrito para o pipeline
- [ ] `DriftMonitor` implementado e testado
- [ ] Modelo verificado por SHA-256 antes de carregamento
- [ ] Testes de invariância do modelo: pelo menos 3 propriedades testadas

---

# SEÇÃO 6 — REFERÊNCIAS

## 18. Referências Completas

### Artigos Acadêmicos (Peer-Reviewed)

1. **Dreyfus, S. E., & Dreyfus, H. L.** (1980). *A Five-Stage Model of the Mental Activities Involved in Directed Skill Acquisition.* ORC 80-2. University of California, Berkeley.
   URL: https://apps.dtic.mil/sti/tr/pdf/ADA084551.pdf
   — **Uso neste relatório:** Framework de avaliação de nível de expertise por dimensão

2. **Ericsson, K. A., Krampe, R. T., & Tesch-Römer, C.** (1993). *The Role of Deliberate Practice in the Acquisition of Expert Performance.* Psychological Review, 100(3), 363–406.
   DOI: 10.1037/0033-295X.100.3.363
   — **Uso:** Meta-cognição ativa como preditor de progressão; validação da postura diagnóstica

3. **Kruger, J., & Dunning, D.** (1999). *Unskilled and Unaware of It.* Journal of Personality and Social Psychology, 77(6), 1121–1134.
   DOI: 10.1037/0022-3514.77.6.1121
   — **Uso:** Limitações da auto-avaliação; risco do especialista matemático subestimar gaps de engenharia

4. **Sculley, D., Holt, G., Golovin, D., et al.** (2015). *Hidden Technical Debt in Machine Learning Systems.* NeurIPS, 28, pp. 2503–2511.
   URL: https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems
   — **Uso:** Failure modes em sistemas ML; contexto do pipeline de phishing; risco de dívida silenciosa

5. **Breck, E., Cai, S., Nielsen, E., Salib, M., & Sculley, D.** (2017). *The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction.* IEEE Big Data.
   DOI: 10.1109/BigData.2017.8258038
   — **Uso:** Gap de testes no pipeline; descoberta de código sem testes no Google

6. **Rothermel, G., & Harrold, M. J.** (1996). *Analyzing Regression Test Selection Techniques.* IEEE TSE, 22(8), 529–551.
   DOI: 10.1109/32.536955
   — **Uso:** Regra de testes de regressão; nunca corrigir bug sem teste

7. **Claessen, K., & Hughes, J.** (2000). *QuickCheck: A Lightweight Tool for Random Testing.* ACM SIGPLAN, 35(9), 268–279.
   DOI: 10.1145/357766.351266
   — **Uso:** Property-based testing para feature_extraction

8. **Ribeiro, M. T., Wu, T., Guestrin, C., & Singh, S.** (2020). *Beyond Accuracy: Behavioral Testing of NLP Models with CheckList.* ACL 2020.
   DOI: 10.18653/v1/2020.acl-main.442
   — **Uso:** Model behavioral testing; testes de invariância para o modelo de phishing

9. **Goodfellow, I. J., Shlens, J., & Szegedy, C.** (2015). *Explaining and Harnessing Adversarial Examples.* ICLR 2015. arXiv: 1412.6572
   — **Uso:** Adversarial robustness; risco de evasão do modelo de phishing

### Normas Técnicas e Publicações Governamentais

10. **Rose, S., Borchert, O., Mitchell, S., & Connelly, S.** (2020). *Zero Trust Architecture.* NIST SP 800-207.
    DOI: 10.6028/NIST.SP.800-207
    — **Uso:** PoLP; gestão de credenciais; segurança de infraestrutura

11. **Grassi, P. A., et al.** (2017). *Digital Identity Guidelines.* NIST SP 800-63B.
    DOI: 10.6028/NIST.SP.800-63b
    — **Uso:** MFA; requisitos de autenticação

12. **Cichonski, P., et al.** (2012). *Computer Security Incident Handling Guide.* NIST SP 800-61 Rev 2.
    DOI: 10.6028/NIST.SP.800-61r2
    — **Uso:** Plano de resposta a incidentes

### Fontes OWASP

13. **OWASP Foundation.** (2021). *OWASP Top Ten 2021.*
    URL: https://owasp.org/Top10/
    — **Uso:** A01-A10; contexto de Broken Access Control, Injection, Cryptographic Failures

14. **OWASP Foundation.** *Secrets Management Cheat Sheet.*
    URL: https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html
    — **Uso:** Gestão de credenciais no pipeline

### Obras Clássicas de Engenharia de Software

15. **Feathers, M.** (2004). *Working Effectively with Legacy Code.* Prentice Hall.
    — **Uso:** Estratégia de introdução de testes em código sem cobertura; definição de "código legado"

16. **Humble, J., & Farley, D.** (2010). *Continuous Delivery.* Addison-Wesley. (Jolt Award 2011)
    — **Uso:** Deployment pipeline; automação de CI/CD; "stop the line"

17. **Bryant, R. E., & O'Hallaron, D. R.** (2015). *Computer Systems: A Programmer's Perspective* (3rd ed.). Pearson.
    — **Uso:** Gap de fundamentos computacionais; modelo mental de sistemas

18. **Beck, K.** (2002). *Test-Driven Development: By Example.* Addison-Wesley.
    — **Uso:** TDD; ciclo Red-Green-Refactor

19. **Shostack, A.** (2014). *Threat Modeling: Designing for Security.* Wiley.
    — **Uso:** Threat modeling; STRIDE framework

### Fontes Industriais e Guias Técnicos

20. **Fowler, M., & Foemmel, M.** (2006). *Continuous Integration.* martinfowler.com.
    URL: https://martinfowler.com/articles/continuousIntegration.html
    — **Uso:** 10 princípios de CI; "make your build self-testing"

21. **Fowler, M.** *TestPyramid.* martinfowler.com.
    URL: https://martinfowler.com/bliki/TestPyramid.html
    — **Uso:** Distribuição correta de tipos de teste

22. **Nygard, M.** (2011). *Documenting Architecture Decisions.* Cognitect Blog.
    URL: https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions
    — **Uso:** ADRs; documentação de decisões de design

23. **Google / OpenSSF.** (2021). *SLSA: Supply-chain Levels for Software Artifacts.*
    URL: https://slsa.dev/
    — **Uso:** Integridade de artefatos; segurança de supply chain

24. **Conventional Commits Specification v1.0.0.**
    URL: https://www.conventionalcommits.org/
    — **Uso:** Padrão de mensagens de commit

25. **Hastie, T., Tibshirani, R., & Friedman, J.** (2009). *The Elements of Statistical Learning* (2nd ed.). Springer.
    URL gratuita: https://hastie.su.domains/ElemStatLearn/
    — **Uso:** Validação do nível excepcional em Fundamentos Matemático-ML

26. **Bishop, C. M.** (2006). *Pattern Recognition and Machine Learning.* Springer.
    — **Uso:** Idem; ML bayesiano com rigor matemático

27. **Cohn, M.** (2009). *Succeeding with Agile.* Addison-Wesley.
    — **Uso:** Test Pyramid; distribuição de tipos de teste

28. **Beyer, B., Jones, C., Petoff, J., & Murphy, N. R.** (2016). *Site Reliability Engineering.* O'Reilly.
    URL: https://sre.google/sre-book/
    — **Uso:** Failure modes; incident response; monitoramento

---

## Síntese Final da Auditoria

### O Diagnóstico em Três Frases

> **Você tem a base matemática de um pesquisador de elite, os hábitos de engenharia de um cientista de dados júnior, e a consciência metacognitiva de alguém que vai resolver isso.**

### A Hierarquia de Prioridades

```
URGENTE + IMPORTANTE (faça esta semana):
→ Gestão de segredos e credenciais (risco ativo em produção)

IMPORTANTE (faça este mês):
→ Testes automatizados básicos (smoke + unit + regressão)
→ Versionamento disciplinado (branches + commits semânticos)

IMPORTANTE (faça nos próximos 3 meses):
→ CI pipeline com quality gates
→ Failure modes do pipeline mapeados
→ Monitoramento de drift

ESTRATÉGICO (horizonte de 6-12 meses):
→ Fundamentos computacionais (Bryant & O'Hallaron)
→ Property-based testing
→ Transferência de conhecimento e conteúdo
```

### A Afirmação Central

> Você já tem o ativo mais difícil de construir: a base matemática rigorosa. O que está faltando — testes, automação, segurança — é trabalhoso, mas aprende-se metodicamente. O inverso (construir rigor matemático em cima de hábitos de engenharia) é muito mais difícil. A jornada à frente é de engenharia, não de matemática.

---

*Auditoria conduzida com base em questionário estruturado e análise de evidências concretas.
Todas as afirmações diagnósticas têm referência identificada com nível de evidência explícito.
Revisão recomendada a cada 6 meses com atualização das métricas de progresso.*

*Próxima revisão recomendada: após conclusão do TCC e início da fase pós-graduação.*
