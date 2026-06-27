# Skill-Check — Parte 5: Arquitetura de Maturidade
## Os Quatro Estágios — Básico, Independente, Avançado, Especialista — Através das Três Especialidades

> *"SFIA is unique in defining skill levels in terms of increasing responsibility, rather than simply depth of expertise."*
> — SFIA Foundation, sobre o que distingue maturidade de competência técnica

---

## O Que Este Documento Faz (e Por Que É Diferente das Partes 1-4)

As Partes 1-3 mediram **competências individuais** na escala Dreyfus de 0 a 5. A Parte 4 mapeou as **relações entre as áreas**. Esta Parte 5 responde a uma pergunta diferente:

> **Não "quão bom sou nesta competência específica?", mas "em que estágio geral de maturidade estou nesta carreira?"**

A distinção é fundamental e frequentemente confundida. Você pode ter nível 5 (Dreyfus) em álgebra linear e nível 1 em CI/CD — mas qual é a sua *maturidade como engenheiro de IA*? Não é a média (que seria enganosa), nem o máximo (que seria otimista demais), nem o mínimo (que seria pessimista demais). A maturidade é uma **propriedade emergente** do conjunto de competências combinada com a forma como você *opera* — sua autonomia, o escopo do seu impacto, e o tipo de problema que você consegue resolver.

Este documento define quatro estágios de maturidade — **Básico → Independente → Avançado → Especialista** — e os caracteriza de forma **transversal às três áreas**. O objetivo é permitir que você se localize não competência por competência (já fez isso nas Partes 1-3), mas no estágio geral de cada carreira — e, crucialmente, identifique o que especificamente falta para cruzar cada fronteira.

Estrutura:
1. **A diferença conceitual** — competência vs maturidade
2. **As duas dimensões da maturidade** — profundidade (Dreyfus) + autonomia/escopo (SFIA)
3. **A relação entre as escalas** — como os 4 níveis mapeiam Dreyfus 0-5 e SFIA 1-7
4. **Os quatro níveis — caracterização universal** — a assinatura de cada estágio
5. **A matriz 4×3** — cada nível através de Engenharia de Software, IA e Data Science
6. **Os marcos de transição** — o que muda em cada fronteira (a parte mais acionável)
7. **Como se localizar** — a metodologia (não é média; é por área; o elo mais fraco limita)
8. **Interpretação para o seu perfil** — o seu mapa de maturidade e o que cada transição exige

---

## Parte 1 — A Diferença Conceitual: Competência vs Maturidade

São duas coisas distintas, e confundi-las leva a auto-avaliações erradas.

| | Competência (Partes 1-3) | Maturidade (esta Parte 5) |
|---|--------------------------|---------------------------|
| **Unidade** | Uma habilidade específica | Uma carreira/papel inteiro |
| **Escala** | Dreyfus 0-5 | Básico → Especialista (4 estágios) |
| **Mede** | Profundidade naquela habilidade | Estágio geral de operação |
| **Exemplo** | "Nível 4 em Transformers" | "Avançado como Desenvolvedor de IA" |
| **Natureza** | Pontual, mensurável | Emergente, holística |

A relação entre as duas: **a maturidade emerge da distribuição das competências, modulada pela autonomia com que você opera.** Mas não é uma função simples da média. Duas pessoas com a mesma média de competências podem ter maturidades muito diferentes:

- **Pessoa A:** nível 4 em quase tudo, distribuído uniformemente → maturidade **Avançada** sólida.
- **Pessoa B:** nível 5 em alguns fundamentos, nível 1 em produção → maturidade **mista** (Especialista em teoria, Básico em operação), e o *papel inteiro* fica limitado pelo componente mais fraco que aquele papel exige.

Esta é a sua situação provável (perfil "pontudo"), e a razão pela qual a maturidade precisa ser avaliada *por área* e com atenção ao elo mais fraco — não pela média.

---

## Parte 2 — As Duas Dimensões da Maturidade

Maturidade profissional não é uma linha única — é a combinação de **duas dimensões ortogonais**, cada uma com fundamentação acadêmica própria.

### Dimensão 1 — Profundidade Cognitiva (Dreyfus)

> **[PEER-REVIEWED]**
> Dreyfus, S. E., & Dreyfus, H. L. (1980). *A Five-Stage Model of the Mental Activities Involved in Directed Skill Acquisition.* UC Berkeley. ORC 80-2.

Esta é a dimensão das Partes 1-3: como o processamento cognitivo evolui de seguir regras (Novice) para intuição fluida (Expert). Mede o quão *profundamente* você entende e domina uma habilidade.

A aplicação canônica do modelo Dreyfus ao desenvolvimento profissional foi feita por Patricia Benner na enfermagem:

> **[CLÁSSICO — Aplicação do modelo]**
> Benner, P. (1984). *From Novice to Expert: Excellence and Power in Clinical Nursing Practice.* Addison-Wesley.
> — Demonstrou que profissionais progridem pelos cinco estágios de Dreyfus na prática real, e que a passagem para Expert envolve uma mudança qualitativa: do raciocínio analítico explícito para o reconhecimento intuitivo de padrões.

### Dimensão 2 — Autonomia, Escopo e Responsabilidade (SFIA)

> **[INDUSTRIAL — Framework de Referência]**
> SFIA Foundation. *Skills Framework for the Information Age* (SFIA), desde 2000. https://sfia-online.org/
> — Framework global que define competência profissional em TI por meio de sete níveis de responsabilidade, caracterizados por cinco atributos genéricos: **autonomia, influência, complexidade, conhecimento, e habilidades de negócio**.

A contribuição decisiva do SFIA é o que ele explicita: **competência profissional não é só profundidade técnica — é responsabilidade.** Seus sete níveis são definidos não pela "quantidade de conhecimento", mas pelo grau de:

- **Autonomia** — de "trabalha sob direção próxima" (nível 1) a "autoridade sobre uma área significativa" (nível 7)
- **Influência** — de "interage com a equipe imediata" a "influencia desenvolvimentos da indústria"
- **Complexidade** — de "tarefas rotineiras estruturadas" a "estratégia e governança"

Os sete níveis do SFIA, com seus verbos-essência: (1) **Seguir**, (2) **Assistir**, (3) **Aplicar**, (4) **Habilitar**, (5) **Garantir/Aconselhar**, (6) **Iniciar/Influenciar**, (7) **Definir estratégia/Inspirar**.

### O Insight Central: As Duas Dimensões Precisam Subir Juntas

O SFIA estabelece um princípio que é o coração desta Parte 5:

> Para desempenhar uma habilidade no nível 4, o indivíduo precisa exibir *também* o nível 4 de autonomia, influência e complexidade. Níveis mais baixos de autonomia podem prejudicar o desempenho efetivo no nível superior, *mesmo com habilidade técnica suficiente*.

Em outras palavras: **profundidade técnica sem autonomia/escopo correspondente não constitui maturidade.** Um pesquisador com domínio matemático profundo (Dreyfus 5) que nunca operou um sistema em produção (SFIA 2 naquele contexto) não é "especialista" no sentido pleno — ele tem a profundidade, mas não o escopo. A maturidade é o ponto onde as duas dimensões se encontram.

Esta é, provavelmente, a observação mais importante deste documento para o seu caso — e voltaremos a ela na interpretação.

---

## Parte 3 — A Relação Entre as Escalas

Os quatro níveis de maturidade desta Parte 5 são uma síntese das duas dimensões — uma "coarsening" (agregação) que combina a profundidade Dreyfus com a responsabilidade SFIA. O mapeamento:

| Maturidade (Parte 5) | Dreyfus (profundidade) | SFIA (autonomia/escopo) | Verbo-essência |
|----------------------|------------------------|--------------------------|----------------|
| **Básico** | 1-2 (Novice / Adv. Beginner) | 1-2 (Seguir / Assistir) | Executa com guia |
| **Independente** | 3 (Competent) | 3 (Aplicar) | Entrega sozinho |
| **Avançado** | 4 (Proficient) | 4-5 (Habilitar / Garantir) | Projeta e orienta |
| **Especialista** | 5 (Expert) | 6-7 (Iniciar / Definir estratégia) | Define o padrão |

**Como ler este mapeamento:** cada nível de maturidade exige *ambas* as dimensões na faixa correspondente. Ser "Avançado" não é só ter competências Dreyfus 4 (profundidade) — é também operar com a autonomia SFIA 4-5 (projetar soluções, orientar outros, ser responsável por resultados além dos seus próprios). Alguém com Dreyfus 4 mas autonomia SFIA 2 está "preso" entre níveis: tem a profundidade de um Avançado, mas opera como um Básico.

---

## Parte 4 — Os Quatro Níveis: Caracterização Universal

Antes de descer às três áreas, a assinatura de cada estágio — o que é universalmente verdadeiro sobre operar em cada nível, independente da carreira.

### Nível 1 — BÁSICO

> **A assinatura:** *Executa tarefas definidas, com orientação. Opera dentro de padrões estabelecidos por outros.*

**Como opera:** Recebe a tarefa já enquadrada e a executa seguindo padrões e exemplos existentes. Precisa de revisão e direção. Quando algo sai do esperado, busca ajuda em vez de diagnosticar sozinho.

**Escopo de impacto:** A própria tarefa atribuída.

**Cognição (Dreyfus):** Segue regras contexto-livre; ainda não reconhece quando uma regra não se aplica.

**Autonomia (SFIA):** Trabalha sob supervisão próxima; trabalho é revisado de perto.

**O que NÃO consegue ainda:** Antecipar problemas, projetar soluções do zero, ou avaliar se a abordagem dada é a correta.

### Nível 2 — INDEPENDENTE

> **A assinatura:** *Entrega tarefas completas de forma autônoma. Depura os próprios problemas. Não precisa de orientação passo a passo.*

**Como opera:** Recebe um objetivo e o traduz em solução sozinho. Implementa, testa e depura sem supervisão constante. Resolve os problemas que surgem no caminho usando seu próprio julgamento.

**Escopo de impacto:** Componentes ou tarefas completas, entregues de ponta a ponta.

**Cognição (Dreyfus):** Planeja deliberadamente; escolhe entre abordagens conhecidas; depura com método.

**Autonomia (SFIA):** Trabalha sob direção geral, com discrição sobre o "como"; gerencia o próprio trabalho dentro de prazos.

**O que NÃO consegue ainda:** Antecipar modos de falha que ainda não viu; projetar para requisitos não-funcionais (escala, resiliência) que não foram explicitados; orientar outros de forma sistemática.

### Nível 3 — AVANÇADO

> **A assinatura:** *Projeta soluções antecipando trade-offs e modos de falha. Orienta outros. Toma decisões de arquitetura justificadas.*

**Como opera:** Não espera o problema aparecer — antecipa-o no design. Pensa em trade-offs (esta escolha otimiza X ao custo de Y), em modos de falha (o que acontece quando isto quebra), e em requisitos não-funcionais (escala, segurança, manutenibilidade) desde o início. Orienta pessoas menos experientes e eleva o nível da equipe.

**Escopo de impacto:** Sistemas inteiros + o desenvolvimento de outras pessoas.

**Cognição (Dreyfus):** Percepção holística; vê o problema como um todo, não como partes; reconhece o que importa em cada situação.

**Autonomia (SFIA):** Trabalha sob direção ampla; trabalho auto-iniciado; responsável por resultados que incluem o trabalho de outros.

**O que NÃO consegue ainda (a fronteira para Especialista):** Definir o que *é* a melhor prática (apenas aplica as existentes muito bem); reconhecer quando o próprio padrão estabelecido está errado; contribuir com o estado da arte.

### Nível 4 — ESPECIALISTA

> **A assinatura:** *Define os padrões que outros seguem. Reconhece quando o padrão estabelecido está errado. Contribui com o estado da arte. Autoridade reconhecida.*

**Como opera:** Não apenas aplica as melhores práticas — *define* o que são as melhores práticas no seu contexto. Tem a profundidade e a experiência para reconhecer quando uma abordagem amplamente aceita é inadequada para a situação. Ensina, estabelece direção, e é referência. Sua intuição, construída sobre milhares de casos, frequentemente precede a análise explícita.

**Escopo de impacto:** O padrão da organização (ou do campo); influencia além da própria equipe.

**Cognição (Dreyfus):** Intuição fluida; o domínio é tácito; reconhece padrões sem deliberação explícita; sabe quando "as regras" não se aplicam.

**Autonomia (SFIA):** Autoridade sobre uma área significativa; influencia desenvolvimentos da indústria; define estratégia.

**A marca distintiva:** A transição do "aplica as melhores práticas com excelência" (Avançado) para "define e questiona as melhores práticas" (Especialista). O Especialista não pergunta "qual é o padrão?" — ele é quem responde, e quem reconhece quando o padrão precisa mudar.

---

## Parte 5 — A Matriz 4×3: Os Níveis Através das Três Áreas

O coração deste documento. Para cada nível de maturidade, o que ele significa concretamente em cada uma das três especialidades. Use esta matriz para se localizar em cada carreira.

### ENGENHARIA DE SOFTWARE

| Nível | Como se manifesta na Engenharia de Software |
|-------|---------------------------------------------|
| **Básico** | Implementa features seguindo padrões existentes. Precisa de code review para detectar problemas. Usa frameworks sem entender os internals. Commits podem quebrar o build. Não escreve testes (ou os escreve mal). |
| **Independente** | Constrói features e componentes completos sozinho. Escreve código testado. Depura os próprios bugs. Usa Git, CI e linters como prática. Entende o que o framework faz por baixo. |
| **Avançado** | Projeta a arquitetura de sistemas antecipando trade-offs (consistência vs disponibilidade, acoplamento vs simplicidade). Antecipa modos de falha. Toma decisões de tecnologia justificadas. Faz code review que eleva a equipe. Pensa em escala, segurança e manutenibilidade desde o design. |
| **Especialista** | Define os padrões de arquitetura e qualidade da organização. Reconhece quando um padrão estabelecido (ex: microsserviços) é inadequado para o contexto. É referência em decisões técnicas difíceis. Contribui com práticas que outros adotam. |

### DESENVOLVEDOR DE IA

| Nível | Como se manifesta no Desenvolvimento de IA |
|-------|--------------------------------------------|
| **Básico** | Treina modelos seguindo tutoriais. Usa `model.fit()` sem entender o que acontece. Não diagnostica por que o treino não converge. Avalia com uma métrica agregada. Usa APIs de LLM sem entender os mecanismos. |
| **Independente** | Constrói um pipeline de ML completo (dados → treino → avaliação). Diagnostica problemas de treinamento. Valida modelos corretamente (evita leakage, escolhe métricas). Implementa fine-tuning e serving básico. |
| **Avançado** | Projeta a arquitetura de sistemas de ML antecipando drift, edge cases e training-serving skew. Escolhe abordagens por trade-off (modelo simples vs complexo, fine-tuning vs RAG). Deriva e raciocina sobre os fundamentos matemáticos. Orienta sobre design de ML. Pensa em monitoramento e retreino desde o início. |
| **Especialista** | Define a estratégia de ML da organização. Reconhece quando uma abordagem (ex: deep learning para um problema tabular) é inadequada. Contribui com o estado da arte (publicações, métodos). É autoridade sobre rigor matemático e design de sistemas de IA. |

### DATA SCIENTIST

| Nível | Como se manifesta na Ciência de Dados |
|-------|---------------------------------------|
| **Básico** | Roda análises seguindo receitas. Reporta resultados sem questionar a metodologia. Interpreta p-valores incorretamente. Confunde correlação com causação. Usa visualizações sem princípios. Aceita a pergunta de negócio como dada. |
| **Independente** | Conduz uma análise completa sozinho. Escolhe métodos estatísticos apropriados. Faz EDA sistemática. Comunica resultados com narrativa. Reconhece os limites das próprias conclusões. Valida estatisticamente. |
| **Avançado** | Projeta a abordagem analítica antecipando confounders e vieses. Raciocina causalmente (DAGs, métodos quasi-experimentais). Projeta experimentos (A/B) com rigor. Traduz análise em decisão de negócio. Orienta sobre rigor metodológico. Reenquadra problemas de negócio. |
| **Especialista** | Define a cultura analítica e de experimentação da organização. Avança métodos causais. Reconhece análises estatisticamente inválidas por inspeção. É autoridade sobre rigor e ética de dados. Influencia como a organização toma decisões baseadas em dados. |

**Padrão que emerge da matriz:** note que a progressão tem a *mesma estrutura* nas três áreas, apesar do conteúdo diferente:
- **Básico:** segue receitas/padrões sem entender por baixo.
- **Independente:** entrega autonomamente e depura.
- **Avançado:** projeta antecipando problemas e orienta.
- **Especialista:** define os padrões e reconhece quando eles falham.

Essa estrutura comum é o que torna a maturidade *transversal* — o estágio significa a mesma coisa qualitativa em qualquer carreira, mesmo que se manifeste em conteúdos diferentes.

---

## Parte 6 — Os Marcos de Transição

A parte mais acionável. O que *especificamente* muda em cada fronteira — porque saber o que distingue um nível do próximo é o que te diz o que precisa demonstrar para avançar.

### Transição 1 — De Básico para Independente

> **A mudança:** de "preciso que me digam os passos" para "recebo o objetivo e o resolvo sozinho".

**O marco-limiar:** *autonomia na execução.* Você cruza esta fronteira quando consegue receber um objetivo (não um passo a passo) e entregá-lo de ponta a ponta, depurando os problemas que surgem sem precisar de socorro constante.

**O que você precisa demonstrar:** entregar uma tarefa completa sem orientação passo a passo, e resolver os obstáculos do caminho com seu próprio julgamento.

**O obstáculo típico:** dependência de tutoriais/exemplos. Enquanto você precisa de um exemplo para cada coisa nova, ainda não cruzou. A independência começa quando você consegue derivar a solução dos princípios, não copiá-la de um modelo.

### Transição 2 — De Independente para Avançado

> **A mudança:** de "resolvo o problema que me deram" para "antecipo os problemas que ainda não apareceram".

**O marco-limiar:** *projetar para o que ainda não é visível.* Você cruza esta fronteira quando começa a pensar, no momento do design, nos modos de falha, trade-offs e requisitos não-funcionais que ninguém explicitou — porque a experiência te ensinou que eles virão.

**O que você precisa demonstrar:** projetar uma solução que antecipa falhas e trade-offs; tomar uma decisão de arquitetura justificada pelos seus efeitos de segunda ordem; elevar outra pessoa através de orientação.

**O obstáculo típico:** "happy-path thinking" — focar no caminho de sucesso. Esta é, não por coincidência, exatamente a fronteira do Eixo 4 (raciocínio sobre falhas) do seu diagnóstico. A transição para Avançado *é* a superação do pensamento de caminho-feliz.

### Transição 3 — De Avançado para Especialista

> **A mudança:** de "aplico as melhores práticas com excelência" para "defino o que é a melhor prática, e reconheço quando ela está errada".

**O marco-limiar:** *autoridade sobre o padrão.* Você cruza esta fronteira quando para de perguntar "qual é a melhor prática?" e passa a ser quem responde — e, mais importante, quem reconhece quando a prática estabelecida é inadequada para a situação.

**O que você precisa demonstrar:** definir um padrão que outros adotam; reconhecer e justificar quando uma abordagem amplamente aceita não se aplica; contribuir com algo que avança o campo (mesmo que localmente, na sua organização).

**O obstáculo típico:** esta é a transição mais difícil e mais lenta, porque depende de *volume de experiência* — a intuição do Especialista é construída sobre milhares de casos. Não há atalho; exige tempo e exposição a muitos problemas reais. É também a fronteira onde a profundidade técnica (Dreyfus 5) precisa se encontrar com o escopo/autoridade (SFIA 6-7) — ambos precisam estar presentes.

---

## Parte 7 — Como se Localizar (A Metodologia)

Quatro princípios para usar esta arquitetura honestamente.

### Princípio 1 — A maturidade é por ÁREA, não global

Você não tem "uma maturidade" — tem uma maturidade *por carreira*. É perfeitamente possível (e é o seu caso provável) ser Avançado/Especialista em uma dimensão de IA e Básico/Independente em Engenharia de Software. Avalie cada área separadamente usando a matriz 4×3.

### Princípio 2 — Não é a média; o elo mais fraco que o papel exige limita

A maturidade de um papel não é a média das competências — é limitada pelo componente mais fraco que *aquele papel exige*. Um "ML Engineer sênior" exige tanto profundidade de modelagem quanto competência de produção; se a produção está em Básico, o papel inteiro fica limitado a Básico-Independente, por mais profunda que seja a modelagem. (Princípio do elo mais fraco, já estabelecido nas interpretações das Partes 1-3.)

### Princípio 3 — As duas dimensões precisam estar presentes

Lembre-se do insight SFIA: ter a profundidade (Dreyfus) sem a autonomia/escopo (SFIA) não constitui o nível. Se você domina a teoria mas nunca operou com autonomia naquele contexto, você tem *meia* maturidade — a dimensão cognitiva, mas não a de responsabilidade. A maturidade plena exige as duas.

### Princípio 4 — Evidência, não percepção

Como em todo este projeto (Kruger & Dunning, 1999): não se atribua um nível sem evidência concreta. "Sou Avançado em IA" exige um artefato — um sistema que você projetou antecipando falhas, uma decisão de arquitetura que você justificou, alguém que você orientou. Sem evidência, é percepção, e a percepção é exatamente o que o viés distorce.

```
        PROFUNDIDADE (Dreyfus) →
        Básico    Independente   Avançado    Especialista
   ┌──────────────────────────────────────────────────────┐
 A │                                                        │
 U │   Quem tem profundidade mas baixa autonomia fica       │
 T │   "preso" abaixo da diagonal — tem o conhecimento,     │
 O │   mas não opera no nível correspondente.               │
 N │                                                        │
 O │              ▓▓▓ ZONA DE MATURIDADE PLENA ▓▓▓          │
 M │           (as duas dimensões sobem juntas)             │
 I │                                                        │
 A │   Quem tem autonomia mas baixa profundidade é a        │
   │   "zona de perigo" de Conway — opera com confiança     │
 ↓ │   sem entender o que faz.                               │
   └──────────────────────────────────────────────────────┘
```

---

## Parte 8 — Interpretação Para o Seu Perfil

Cruzando esta arquitetura com o seu diagnóstico (base matemática de pesquisador de elite + hábitos de engenharia a desenvolver), emerge um mapa de maturidade específico e revelador.

### 8.1 O seu perfil de maturidade é "pontudo" — e isso é diagnóstico, não defeito

Você não está uniformemente em um nível. O seu mapa de maturidade provável, por área:

| Área / Dimensão | Maturidade provável | Por quê |
|-----------------|--------------------|---------|
| **IA — fundamentos matemáticos** | **Especialista** (ou perto) | IME-USP + Bishop; profundidade rara |
| **IA — ML clássico / modelagem** | **Avançado** | Pipeline de phishing, Lyapunov, domínio teórico |
| **IA — produção / MLOps** | **Básico → Independente** | Exposição parcial; gap de Craft |
| **Eng. Software — craft** | **Básico → Independente** | Gap confirmado (Eixo 3): sem testes, sem linters |
| **Eng. Software — arquitetura** | **Independente** | Raciocínio estrutural forte, prática a desenvolver |
| **DS — estatística / inferência** | **Avançado** | Base matemática; rigor metodológico (TCC) |
| **DS — causalidade** | **Avançado (latente)** | Afinidade alta, mas a demonstrar |
| **DS — tradução para negócio** | **Básico** | Eixo 6 (impacto) não desenvolvido |

O padrão: **picos de Especialista/Avançado nos fundamentos científicos, vales de Básico/Independente na produção e no negócio.** Isto é a assinatura precisa do diagnóstico "base de pesquisador + hábitos de engenharia de cientista de dados júnior", agora expressa em termos de maturidade.

### 8.2 O insight SFIA aplicado a você: a profundidade está "represada" pela autonomia

Aqui está a observação mais importante. Pelo princípio SFIA, a sua profundidade matemática excepcional (Dreyfus 5) está, em contextos de produção, *represada* por uma autonomia/escopo menor (SFIA 2-3). Você tem o conhecimento de um Especialista em fundamentos, mas, quando o problema envolve levar isso à produção, opera mais perto de Independente — porque a dimensão de autonomia operacional ainda não subiu junto.

No diagrama da Parte 7, você está **acima da diagonal nos fundamentos** (profundidade altíssima) e **abaixo dela na produção** (a profundidade existe, mas a autonomia operacional não a acompanha ainda). A maturidade plena — estar na diagonal — exige trazer a dimensão de autonomia operacional para o nível da sua profundidade conceitual.

A boa notícia: subir a dimensão de autonomia é tipicamente mais rápido do que construir a profundidade, *quando a profundidade já existe*. Você não precisa aprender a matemática (já tem); precisa adquirir a prática operacional que converte conhecimento em autonomia de produção. Isso é questão de meses de prática deliberada, não de anos de fundamentos.

### 8.3 As três transições, na sua ordem de prioridade

Aplicando os marcos de transição (Parte 6) ao seu caso:

1. **A transição mais alavancada para você é Independente → Avançado na produção/craft.** Você já é Avançado nos fundamentos; o gap é levar a produção (MLOps, craft de engenharia) de Básico/Independente para Avançado. O marco-limiar dessa transição é *projetar antecipando falhas* (Eixo 4) — exatamente o seu gap diagnosticado. Cruzar esta fronteira na produção é o que unifica o seu perfil pontudo em um perfil sênior coerente.

2. **A transição Avançado (latente) → Avançado (demonstrado) em causalidade.** Em causalidade, você provavelmente tem a profundidade cognitiva (afinidade matemática + epistemológica), mas falta a *evidência* (Princípio 4) — análises causais reais que demonstrem o nível. A transição aqui não é aprender, é *aplicar e demonstrar* — idealmente no seu domínio de cibersegurança.

3. **A transição Básico → Independente em tradução para negócio.** O vale mais profundo (Eixo 6). Esta é a de menor prioridade técnica, mas a mais relevante para a sua meta de produto/conteúdo digital com renda passiva — porque "traduzir valor" é precisamente o que transforma competência técnica em produto que alguém paga.

### 8.4 O que a arquitetura de maturidade revela sobre a sua meta

Você busca autonomia intelectual como pesquisador independente, com renda passiva de um produto digital. A arquitetura de maturidade ilumina o que isso exige:

- **Pesquisa independente de qualidade** exige maturidade **Especialista** em pelo menos um cume — e você já tem isso (ou está perto) nos fundamentos de IA/DS. O caminho de conversão da sua TCC em preprint (Zenodo → arXiv) é, em termos desta arquitetura, um ato de operar como Especialista: contribuir com o estado da arte.

- **Produto digital com renda passiva** exige cruzar o vale de Básico em tradução para negócio (8.3, transição 3) — porque um produto é valor traduzido para quem paga. A sua maior lacuna de maturidade (negócio) é, não por coincidência, a que mais separa "pesquisador brilhante" de "pesquisador com produto sustentável".

- **A síntese:** a sua meta não exige subir uniformemente em tudo. Exige (a) consolidar o pico de Especialista que você já tem nos fundamentos, convertendo-o em contribuições reais (preprint, conteúdo); (b) elevar a produção/craft para Avançado, para que seus sistemas sejam reais e não protótipos; e (c) começar a escalar o vale de negócio, para que o valor técnico vire produto. Os três movimentos, na ordem das suas dependências, são o caminho da sua meta.

### O Mapa de Maturidade em Uma Frase

> O seu perfil é pontudo: Especialista nos fundamentos científicos, Básico na produção e no negócio. A sua profundidade está represada pela autonomia operacional — e destravá-la (mais rápido, porque a profundidade já existe) é o que unifica o perfil. As transições, na ordem: elevar a produção para Avançado (o gap do Eixo 4), demonstrar a causalidade latente, e começar a escalar o vale de negócio que separa pesquisa de produto.

---

## Referências

| # | Fonte | Tipo | Uso |
|---|-------|------|-----|
| 1 | Dreyfus, S. E., & Dreyfus, H. L. (1980). *A Five-Stage Model of Skill Acquisition.* UC Berkeley. ORC 80-2. | **PEER-REVIEWED** | Dimensão de profundidade cognitiva |
| 2 | SFIA Foundation. *Skills Framework for the Information Age* (desde 2000). https://sfia-online.org/ | **INDUSTRIAL — Framework** | Dimensão de autonomia/escopo (7 níveis de responsabilidade) |
| 3 | Benner, P. (1984). *From Novice to Expert: Excellence and Power in Clinical Nursing Practice.* Addison-Wesley. | **CLÁSSICO** | Aplicação canônica do modelo Dreyfus à maturidade profissional |
| 4 | Smith, P. C., & Kendall, L. M. (1963). *Retranslation of Expectations.* JAP, 47(2). DOI: 10.1037/h0047060 | **PEER-REVIEWED** | Âncoras comportamentais (BARS) — caracterização de cada nível |
| 5 | Kruger, J., & Dunning, D. (1999). *Unskilled and Unaware of It.* JPSP, 77(6). DOI: 10.1037/0022-3514.77.6.1121 | **PEER-REVIEWED** | Princípio 4: evidência, não percepção |
| 6 | Conway, D. (2010). *The Data Science Venn Diagram.* | **CLÁSSICO — Framework** | A "zona de perigo" no diagrama de localização (Parte 7) |

---

*Parte 5 de 7 do Skill-Check. **Síntese 2 de 4 concluída.** Concluídas: as três especialidades (Partes 1-3), a matriz comparativa (Parte 4) e a arquitetura de maturidade (Parte 5).*
*Próximas sínteses: Parte 6 (checklist consolidado de auto-auditoria — reunindo as 210 competências em um instrumento único de avaliação), Parte 7 (análise final integradora com pontos fortes, lacunas críticas e prioridades estratégicas).*
*Maturidade ancorada em Dreyfus (1980, profundidade) + SFIA (autonomia/escopo) + Benner (1984, aplicação profissional). Escala de competências: Dreyfus + BARS (Smith & Kendall, 1963).*
