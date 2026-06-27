# Skill-Check de Data Scientist — Parte 3
## Arquitetura Completa de Competências com Escala Dreyfus Ancorada

> *"The goal is to turn data into information, and information into insight."*
> — Carly Fiorina
>
> *"Correlation does not imply causation — but it sure is a hint."*
> — Edward Tufte, sobre o cerne do que torna a Ciência de Dados difícil

---

## Como Este Documento Funciona

Este é o mapa de competências da terceira e última especialidade: **Data Scientist**. Como há sobreposição natural com a Parte 2 (estatística, ML, modelagem), este documento foca deliberadamente no que é **genuinamente distinto** da carreira de Ciência de Dados — do mesmo modo que o Middle-End foi construído para complementar o Back-End sem repeti-lo.

**A distinção fundamental entre Data Scientist e AI Developer:**

```
AI Developer    →  constrói MODELOS que PREDIZEM ou GERAM
Data Scientist  →  extrai INSIGHT e informa DECISÕES a partir de dados
```

Essa diferença de propósito reorganiza tudo. Onde a Parte 2 tratava estatística como base para *funções de perda* e modelagem como busca de *performance preditiva*, a Parte 3 trata estatística como ferramenta de *inferência e decisão*, e modelagem com ênfase em *interpretação e causalidade*. Onde há genuína sobreposição (ex: ML preditivo), este documento referencia a Parte 2 e foca no ângulo de Ciência de Dados.

As competências mais distintivas desta carreira — e que mal tocamos na Parte 2 — são: **inferência causal, design experimental e A/B testing, análise exploratória, e tradução para decisão de negócio**. São essas que recebem maior profundidade aqui.

São **5 camadas com 5-6 competências cada** (~29 competências), todas com conceito, por que existe, profundidade, conexões, erro/sênior, e progressão Dreyfus completa (0-5) com teste de validação.

A escala é a mesma — Dreyfus (1980) + BARS (Smith & Kendall, 1963), com a ressalva de Kruger & Dunning (1999). Planilha de auto-auditoria no fim.

---

## A Escala de 6 Níveis (referência rápida)

| Nível | Dreyfus | Âncora Comportamental |
|-------|---------|----------------------|
| **0** | Desconhecido | Não reconheço o conceito |
| **1** | Novice | Explico o que é, mas preciso de guia |
| **2** | Advanced Beginner | Uso com documentação; não diagnostico falhas |
| **3** | Competent | Implemento sozinho; depuro |
| **4** | Proficient | Projeto antecipando trade-offs e falhas |
| **5** | Expert | Ensino, reconheço quando o padrão está errado, contribuo com o estado da arte |

> **Fundamentação verificada:** Dreyfus & Dreyfus (1980), UC Berkeley **[PEER-REVIEWED]**; Smith & Kendall (1963), JAP 47(2), DOI: 10.1037/h0047060 **[PEER-REVIEWED]**; Kruger & Dunning (1999), JPSP 77(6) **[PEER-REVIEWED]**.

---

## Visão Geral das 5 Camadas

```
CAMADA 5 · Data Science Aplicado ao Negócio
CAMADA 4 · Engenharia de Dados
CAMADA 3 · Modelagem e Causalidade
CAMADA 2 · Análise e Exploração de Dados (EDA)
CAMADA 1 · Fundamentos Estatísticos para Decisão
```

A lógica do empilhamento é distinta da Parte 2. Aqui a progressão é do *rigor estatístico* (camada 1) ao *impacto no negócio* (camada 5), passando pelo *craft de entender dados* (camada 2), a *inferência sobre o que causa o quê* (camada 3), e a *infraestrutura que torna os dados utilizáveis* (camada 4).

**A régua de especialista em Data Science** tem um perfil característico: profundidade nas camadas 1-3 (rigor estatístico, EDA, causalidade — a base científica) E força nas camadas 5 (tradução para negócio — o que torna o trabalho útil). A camada 4 (engenharia de dados) é frequentemente compartilhada com engenheiros de dados dedicados. O que define o *cientista* de dados, distinto do *engenheiro* de dados ou do *engenheiro* de ML, é a combinação de rigor inferencial (camadas 1, 3) com impacto de negócio (camada 5).

**Referências base de toda a disciplina:**
> **[CLÁSSICO]**
> Tukey, J. W. (1977). *Exploratory Data Analysis.* Addison-Wesley.
> — A obra que fundou a análise exploratória de dados como disciplina.

> **[CLÁSSICO]**
> Pearl, J. (2009). *Causality: Models, Reasoning, and Inference* (2nd ed.). Cambridge University Press.
> — A referência definitiva para inferência causal formal.

> **[INDUSTRIAL]**
> Provost, F., & Fawcett, T. (2013). *Data Science for Business.* O'Reilly.
> — A referência para a aplicação de ciência de dados a problemas de negócio.

---

# CAMADA 1 — Fundamentos Estatísticos para Decisão

> *O rigor inferencial. Aqui a estatística não serve para funções de perda (como na Parte 2), mas para inferir, decidir e quantificar incerteza. Sua formação IME-USP é um diferencial raro.*

**Nota de relação com a Parte 2:** a Camada 1 da Parte 2 tratava probabilidade/estatística como base de ML (MLE → loss functions). Aqui o foco é estatística para *inferência e decisão* — testes, experimentos, intervalos de confiança para sustentar conclusões de negócio. O ferramental matemático se sobrepõe; o propósito e a prática divergem.

---

## 1.1 Estatística Descritiva e Análise Univariada/Bivariada

**Conceito + por que existe:** Resumir e descrever dados — medidas de tendência central e dispersão, distribuições, correlações, e a relação entre pares de variáveis. Existe porque entender a estrutura básica dos dados (sua forma, centro, espalhamento, e relações) é o primeiro passo de qualquer análise, e descrições mal-interpretadas (média vs mediana em dados assimétricos) levam a conclusões erradas.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → EDA (2.3), → Visualização (2.4), → Inferência (1.2)

**Erro de iniciante → Marca do sênior:** O iniciante reporta a média de dados assimétricos (enganosa) ou confunde correlação com relação. O sênior escolhe a estatística apropriada à distribuição (mediana para assimétricos), entende as limitações da correlação (linear, sensível a outliers), e sempre olha a distribuição antes de resumir.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço estatística descritiva | — |
| **1** | Sei calcular média, sem entender quando usar | Calculo a média de uma coluna |
| **2** | Uso estatísticas descritivas; não escolho pela distribuição | Reportei média e desvio de dados |
| **3** | Escolho a estatística pela distribuição; entendo correlação e suas limitações | Usei mediana em dados assimétricos justificadamente |
| **4** | Analiso a estrutura dos dados rigorosamente; antecipo armadilhas (Simpson, outliers) | Detectei o paradoxo de Simpson numa análise |
| **5** | Domino análise descritiva; reconheço resumos enganosos por inspeção; ensino o craft | Projeto a análise descritiva de datasets complexos |

---

## 1.2 Inferência Estatística e Estimação

**Conceito + por que existe:** Inferir propriedades de uma população a partir de uma amostra — estimação pontual e por intervalo, intervalos de confiança, e a quantificação da incerteza amostral. Existe porque trabalhamos com amostras mas queremos concluir sobre populações, e a inferência fornece o framework rigoroso para fazer essa generalização com incerteza quantificada — a base de toda conclusão baseada em dados.

**Profundidade esperada:** Avançado · **Conexões:** → Probabilidade (Parte 2, 1.3), → Testes de hipótese (1.3), → Poder amostral (1.6)

**Erro de iniciante → Marca do sênior:** O iniciante reporta uma estimativa pontual sem intervalo de confiança (esconde a incerteza). O sênior sempre quantifica a incerteza com intervalos de confiança, entende o que um IC realmente significa (e o que não significa), e raciocina sobre o tamanho da amostra necessário.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço inferência estatística | — |
| **1** | Sei que amostras representam populações, sem formalismo | Explico que "a amostra representa o todo" |
| **2** | Calculo intervalos seguindo fórmulas, sem entender | Calculei um IC seguindo uma fórmula |
| **3** | Entendo estimação e ICs; interpreto corretamente | Reportei uma estimativa com IC e o interpretei certo |
| **4** | Quantifico incerteza rigorosamente; uso bootstrap; antecipo limitações | Usei bootstrap para quantificar incerteza de uma estimativa complexa |
| **5** | Domino inferência; reconheço interpretações errôneas de IC; ensino o framework | Projeto a estratégia de inferência de análises críticas |

> *Para o seu perfil: a interpretação correta de um intervalo de confiança (que NÃO é "95% de chance de o parâmetro estar no intervalo") é o tipo de rigor que sua formação matemática garante — e que a maioria dos praticantes erra.*

---

## 1.3 Testes de Hipótese e Significância

**Conceito + por que existe:** O framework para testar afirmações sobre dados — hipótese nula/alternativa, p-valores, erros tipo I/II, e significância estatística. Existe porque decisões baseadas em dados exigem distinguir efeitos reais de flutuações aleatórias, e os testes de hipótese fornecem o procedimento formal para essa distinção — embora sejam amplamente mal-interpretados.

**Profundidade esperada:** Avançado · **Conexões:** → Inferência (1.2), → A/B testing (1.4), → Poder amostral (1.6)

**Erro de iniciante → Marca do sênior:** O iniciante interpreta p < 0.05 como "a hipótese é verdadeira" ou faz p-hacking (testar até dar significativo). O sênior entende o que um p-valor realmente significa, distingue significância estatística de relevância prática, e reconhece os problemas de múltiplas comparações e p-hacking.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço testes de hipótese | — |
| **1** | Ouvi falar de p-valor, sem entender | Explico vagamente "ver se é significativo" |
| **2** | Rodo testes; interpreto p < 0.05 como "verdade" | Rodei um teste-t e olhei o p-valor |
| **3** | Entendo p-valores corretamente; distingo significância de relevância | Expliquei o que um p-valor realmente significa |
| **4** | Projeto testes; corrijo múltiplas comparações; antecipo p-hacking | Apliquei correção de Bonferroni/FDR em múltiplos testes |
| **5** | Domino testes de hipótese; reconheço p-hacking e má interpretação; ensino o framework | Projeto a estratégia de teste estatístico de experimentos |

> *Para o seu perfil: a crise de reprodutibilidade em ciência é em grande parte sobre má interpretação de p-valores e p-hacking. Seu rigor matemático te posiciona para entender por que p < 0.05 não significa o que a maioria pensa — uma competência rara e valiosa.*

---

## 1.4 Design Experimental e A/B Testing

**Conceito + por que existe:** Projetar experimentos controlados para estabelecer causalidade — randomização, grupos de controle, A/B testing, e os princípios de design experimental. Existe porque a forma mais confiável de saber se uma intervenção *causa* um efeito é um experimento controlado randomizado, e o A/B testing é a aplicação industrial desse princípio para decisões de produto.

**Profundidade esperada:** Avançado · **Conexões:** → Testes de hipótese (1.3), → Causalidade (3.2), → Métricas de negócio (5.2)

**Referência:**
> **[INDUSTRIAL — Referência Definitiva]**
> Kohavi, R., Tang, D., & Xu, Y. (2020). *Trustworthy Online Controlled Experiments: A Practical Guide to A/B Testing.* Cambridge University Press.
> — A referência definitiva para experimentação online, baseada na experiência de A/B testing em escala na Microsoft, Amazon e Google.

**Erro de iniciante → Marca do sênior:** O iniciante roda um A/B test sem cálculo de tamanho de amostra (para o teste cedo demais, ou olha resultados continuamente — peeking). O sênior projeta o experimento corretamente (tamanho de amostra pré-calculado, randomização adequada, métricas definidas a priori), e entende as armadilhas (peeking, efeitos de novidade, contaminação).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço design experimental | — |
| **1** | Ouvi falar de A/B testing, sem entender | Explico que "compara duas versões" |
| **2** | Rodo um A/B test sem cálculo de amostra nem rigor | Já parei um teste cedo ao ver um resultado bom |
| **3** | Projeto A/B tests com tamanho de amostra; entendo randomização | Calculei o tamanho de amostra antes de rodar um teste |
| **4** | Projeto experimentos rigorosos; antecipo armadilhas (peeking, contaminação) | Desenhei um experimento controlado evitando peeking e contaminação |
| **5** | Domino experimentação; reconheço experimentos falhos por inspeção; ensino as práticas | Estabeleci a plataforma/cultura de experimentação de uma organização |

> *Para o seu perfil: o design experimental conecta diretamente ao seu rigor matemático e ao seu TCC (que tem considerações metodológicas de split cronológico). É a ponte entre estatística e decisão causal — uma das competências mais valiosas e mais raras em Data Science.*

---

## 1.5 Regressão como Ferramenta de Inferência

**Conceito + por que existe:** Usar modelos de regressão para *entender relações*, não apenas prever — interpretação de coeficientes, controle de variáveis, e regressão como ferramenta inferencial. Existe porque, diferente do uso preditivo (Parte 2), em Ciência de Dados a regressão frequentemente serve para responder "qual o efeito de X sobre Y, controlando por Z?" — uma pergunta inferencial, não preditiva.

**Profundidade esperada:** Avançado · **Conexões:** → Aprendizado supervisionado (Parte 2, 2.1), → Causalidade (3.2), → Confounders (3.3)

**Nota de relação com a Parte 2:** lá, regressão era um algoritmo preditivo avaliado por erro. Aqui, é uma ferramenta para *interpretar relações* — o foco está nos coeficientes e seu significado, não na acurácia de predição.

**Erro de iniciante → Marca do sênior:** O iniciante interpreta coeficientes de regressão causalmente sem justificativa (omite variáveis de confusão). O sênior entende que coeficientes são associações condicionais, sabe quando podem ser interpretados causalmente (e quando não), e controla variáveis com base em raciocínio causal, não estatístico.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei usar regressão para inferência | — |
| **1** | Sei que regressão "ajusta uma linha", sem interpretar | Explico que "regressão relaciona variáveis" |
| **2** | Interpreto coeficientes causalmente sem cuidado | Já disse "X causa Y" baseado num coeficiente |
| **3** | Interpreto coeficientes como associações condicionais; controlo variáveis | Interpretei um coeficiente corretamente como efeito condicional |
| **4** | Uso regressão para inferência rigorosa; raciocino sobre o que controlar | Escolhi variáveis de controle com base em raciocínio causal |
| **5** | Domino regressão inferencial; reconheço interpretações causais indevidas; ensino o rigor | Projeto análises de regressão para questões inferenciais complexas |

---

## 1.6 Análise de Poder e Tamanho de Amostra

**Conceito + por que existe:** Determinar quantos dados são necessários para detectar um efeito — poder estatístico, tamanho de efeito, e cálculo de tamanho de amostra. Existe porque experimentos subdimensionados não detectam efeitos reais (falso negativo) e desperdiçam recursos, enquanto o cálculo de poder garante que o experimento tenha chance de responder à pergunta antes de gastar tempo e dinheiro.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Testes de hipótese (1.3), → A/B testing (1.4), → Inferência (1.2)

**Erro de iniciante → Marca do sênior:** O iniciante roda um teste com a amostra que tem e conclui "não há efeito" quando na verdade o teste não tinha poder para detectá-lo. O sênior calcula o tamanho de amostra necessário antes do experimento, entende a relação entre poder, tamanho de efeito e amostra, e distingue "ausência de evidência" de "evidência de ausência".

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço análise de poder | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "quantos dados preciso" |
| **2** | Uso a amostra que tenho, sem calcular poder | Já concluí "sem efeito" sem checar o poder |
| **3** | Calculo tamanho de amostra; entendo poder e tamanho de efeito | Calculei o tamanho de amostra para um teste |
| **4** | Projeto experimentos com poder adequado; distingo ausência de evidência | Desenhei um experimento garantindo poder para o efeito esperado |
| **5** | Domino análise de poder; reconheço estudos subdimensionados; ensino o framework | Projeto a estratégia de dimensionamento de experimentos de uma organização |

---

# CAMADA 2 — Análise e Exploração de Dados (EDA)

> *O craft de entender dados antes de modelá-los. A habilidade mais subestimada e mais característica do cientista de dados. Onde a maioria do trabalho real acontece.*

**Referência base:**
> **[CLÁSSICO]**
> Tukey, J. W. (1977). *Exploratory Data Analysis.* Addison-Wesley. — a obra fundadora.

---

## 2.1 Coleta e Aquisição de Dados

**Conceito + por que existe:** Obter dados de diversas fontes — APIs, bancos de dados, web scraping, arquivos, e a compreensão da proveniência e do processo gerador dos dados. Existe porque toda análise começa com dados, e entender *como* os dados foram coletados (e seus vieses de coleta) é fundamental para interpretar corretamente — dados não caem do céu, são gerados por processos com características próprias.

**Profundidade esperada:** Intermediário · **Conexões:** → SQL (4.5), → Limpeza (2.2), → Qualidade de dados (4.4)

**Erro de iniciante → Marca do sênior:** O iniciante usa dados sem questionar como foram coletados (e herda vieses invisíveis). O sênior investiga a proveniência dos dados, entende o processo gerador e seus vieses de coleta (survivorship bias, selection bias), e documenta as limitações da fonte.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei como obter dados | — |
| **1** | Uso datasets prontos, sem questionar a origem | Carrego um CSV existente |
| **2** | Coleto dados de fontes simples; não questiono vieses de coleta | Coletei dados de uma API seguindo tutorial |
| **3** | Obtenho dados de múltiplas fontes; considero a proveniência | Documentei a origem e o processo de coleta de um dataset |
| **4** | Projeto a estratégia de coleta; identifico vieses de coleta; valido a fonte | Identifiquei um viés de seleção na forma como os dados foram coletados |
| **5** | Domino aquisição de dados; reconheço vieses de coleta por inspeção; ensino o rigor | Estabeleço a estratégia de coleta de dados de projetos complexos |

---

## 2.2 Limpeza e Tratamento de Dados (Data Wrangling)

**Conceito + por que existe:** Transformar dados brutos e bagunçados em formato analisável — tratar valores faltantes, inconsistências, duplicatas, tipos errados, e outliers. Existe porque dados do mundo real são quase sempre sujos, e a limpeza consome tipicamente a maior parte do tempo de um cientista de dados — e fazê-la incorretamente (imputação ingênua, remoção descuidada) corrompe toda a análise subsequente.

**Profundidade esperada:** Avançado · **Conexões:** → Coleta (2.1), → Qualidade (4.4), → Feature engineering (Parte 2, 2.5)

**Erro de iniciante → Marca do sênior:** O iniciante remove linhas com valores faltantes ou preenche com a média sem pensar (introduz viés). O sênior entende os mecanismos de dados faltantes (MCAR, MAR, MNAR), escolhe a estratégia de tratamento apropriada, e documenta o impacto das decisões de limpeza.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei limpar dados | — |
| **1** | Sei que dados têm problemas, sem saber tratar | Explico que "os dados precisam de limpeza" |
| **2** | Removo nulos ou preencho com a média sem critério | Já removi linhas com nulos sem pensar |
| **3** | Trato dados faltantes com método; entendo os mecanismos | Escolhi a imputação considerando o mecanismo de ausência |
| **4** | Projeto a estratégia de limpeza; antecipo o impacto; documento decisões | Desenhei o tratamento de dados de um projeto considerando vieses |
| **5** | Domino data wrangling; reconheço limpeza problemática; ensino o craft | Estabeleço os padrões de tratamento de dados de um time |

> *Para o seu perfil: você já desenvolveu utilitários de data wrangling para o seu TCC (projeção de colunas, ordenação por data, balanceamento de classes, splits estratificados) — esta é uma competência com prática real, e sua atenção a splits cronológicos mostra consciência de nível 4.*

---

## 2.3 Análise Exploratória de Dados (EDA)

**Conceito + por que existe:** Investigar dados sistematicamente para descobrir padrões, anomalias, relações e hipóteses — antes de qualquer modelagem formal. Existe porque entender os dados profundamente é pré-requisito para modelá-los corretamente, e a EDA (no espírito de Tukey) é o processo de "deixar os dados falarem" — frequentemente revelando que o problema é diferente do que se imaginava.

**Profundidade esperada:** Avançado · **Conexões:** → Descritiva (1.1), → Visualização (2.4), → Modelagem (Camada 3)

**Erro de iniciante → Marca do sênior:** O iniciante pula direto para a modelagem sem explorar (e perde padrões críticos). O sênior investe tempo substancial em EDA, gera e testa hipóteses iterativamente, e deixa a exploração informar a estratégia de modelagem — entendendo que o insight frequentemente vem da exploração, não do modelo.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é EDA | — |
| **1** | Ouvi falar, sem método | Explico vagamente "olhar os dados" |
| **2** | Faço gráficos básicos sem estratégia | Plotei alguns histogramas |
| **3** | Exploro sistematicamente; gero e testo hipóteses | Conduzi uma EDA que revelou um padrão inesperado |
| **4** | Projeto a exploração; deixo-a informar a modelagem; antecipo armadilhas | Usei EDA para reformular o problema de modelagem |
| **5** | Domino EDA; reconheço análises superficiais; ensino o craft de Tukey | Estabeleço a prática de exploração de dados de um time |

---

## 2.4 Visualização de Dados

**Conceito + por que existe:** Representar dados visualmente de forma que revele padrões e comunique insight — escolha de gráficos, princípios de design visual, e a gramática dos gráficos. Existe porque o sistema visual humano é poderoso para detectar padrões, e uma visualização bem projetada revela o que tabelas de números escondem — mas visualizações mal projetadas enganam tanto quanto esclarecem.

**Profundidade esperada:** Avançado · **Conexões:** → EDA (2.3), → Comunicação (2.5), → Descritiva (1.1)

**Referência:**
> **[CLÁSSICO]**
> Tufte, E. R. (2001). *The Visual Display of Quantitative Information* (2nd ed.). Graphics Press. — a referência sobre princípios de visualização.

**Erro de iniciante → Marca do sênior:** O iniciante usa gráficos inadequados (pizza para muitas categorias, eixos truncados que enganam) ou os enche de "chartjunk". O sênior escolhe o gráfico pela mensagem e pelos dados, segue princípios de design (maximizar data-ink ratio), e evita representações que distorcem.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei visualizar dados | — |
| **1** | Faço gráficos no Excel sem critério | Fiz um gráfico de pizza |
| **2** | Uso bibliotecas de plotagem seguindo exemplos | Plotei dados com matplotlib seguindo tutorial |
| **3** | Escolho o gráfico pela mensagem; sigo princípios de design | Escolhi a visualização certa para revelar um padrão |
| **4** | Projeto visualizações para insight e comunicação; evito distorções | Desenhei uma visualização que revelou um insight não-óbvio |
| **5** | Domino visualização; reconheço gráficos enganosos por inspeção; ensino os princípios | Estabeleço os padrões de visualização de um time |

---

## 2.5 Comunicação e Storytelling com Dados

**Conceito + por que existe:** Traduzir análises técnicas em narrativas claras que informam e persuadem — estruturar a mensagem, adaptar à audiência, e contar a história que os dados revelam. Existe porque uma análise brilhante que não é compreendida não gera valor, e a habilidade de comunicar insight de forma clara e acionável é o que transforma análise em impacto — frequentemente o diferencial entre cientistas de dados.

**Profundidade esperada:** Avançado · **Conexões:** → Visualização (2.4), → Comunicação executiva (5.5), → Tomada de decisão (5.4)

**Erro de iniciante → Marca do sênior:** O iniciante apresenta todos os detalhes técnicos sem narrativa (perde a audiência). O sênior estrutura a comunicação em torno da mensagem central e da decisão, adapta o nível técnico à audiência, e conta uma história clara — liderando com a conclusão, não com a metodologia.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei comunicar análises | — |
| **1** | Apresento números sem narrativa | Mostrei resultados como uma lista de métricas |
| **2** | Organizo a apresentação, mas com excesso técnico | Apresentei uma análise com muitos detalhes |
| **3** | Estruturo em torno da mensagem; adapto à audiência | Comuniquei uma análise liderando com a conclusão |
| **4** | Projeto a narrativa para a decisão; persuado com dados; antecipo objeções | Desenhei uma apresentação que levou a uma decisão |
| **5** | Domino storytelling com dados; reconheço comunicação ineficaz; ensino o craft | Estabeleço os padrões de comunicação de insight de um time |

> *Para o seu perfil: esta competência conecta ao seu objetivo de criação de conteúdo técnico. Comunicar análises de dados com clareza e rigor é uma habilidade transferível para o conteúdo que você quer produzir — e é onde o Eixo 6 (transferência) do seu diagnóstico se manifesta.*

---

## 2.6 Detecção de Qualidade e Anomalias nos Dados

**Conceito + por que existe:** Identificar problemas de qualidade e anomalias que comprometem análises — outliers, erros de medição, inconsistências, e drift nos dados. Existe porque dados problemáticos levam a conclusões falsas, e detectar proativamente problemas de qualidade (antes que corrompam a análise) é uma habilidade que distingue o cientista de dados cuidadoso do descuidado.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Limpeza (2.2), → Qualidade de dados (4.4), → Drift (Parte 2, 4.4)

**Erro de iniciante → Marca do sênior:** O iniciante aceita os dados como corretos e não detecta anomalias até elas distorcerem o resultado. O sênior verifica sistematicamente a qualidade dos dados, distingue outliers genuínos de erros, e investiga anomalias antes de prosseguir — sabendo que "dados estranhos" frequentemente revelam problemas no processo de coleta.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei detectar problemas nos dados | — |
| **1** | Assumo que os dados estão corretos | Uso dados sem verificar qualidade |
| **2** | Noto problemas óbvios; não verifico sistematicamente | Já notei um valor absurdo por acaso |
| **3** | Verifico qualidade sistematicamente; distingo outliers de erros | Detectei e investiguei anomalias antes de analisar |
| **4** | Projeto verificações de qualidade; antecipo problemas; investigo a causa | Desenhei verificações que pegaram um problema de coleta |
| **5** | Domino detecção de qualidade; reconheço dados problemáticos por inspeção; ensino o rigor | Estabeleço os padrões de qualidade de dados de um time |

---

# CAMADA 3 — Modelagem e Causalidade

> *Onde a Ciência de Dados mais se distingue da IA. O foco não é predizer, mas entender o que causa o quê — a pergunta mais difícil e mais valiosa em dados.*

**Nota de relação com a Parte 2:** a modelagem preditiva (algoritmos, avaliação, deep learning) foi coberta na Parte 2. Esta camada foca no que é distinto da Ciência de Dados: **interpretabilidade e, sobretudo, causalidade** — inferir relações causais, não apenas associações preditivas.

**Referência base:**
> **[CLÁSSICO]**
> Pearl, J. (2009). *Causality: Models, Reasoning, and Inference* (2nd ed.). Cambridge University Press.

> **[INDUSTRIAL — acessível]**
> Pearl, J., & Mackenzie, D. (2018). *The Book of Why: The New Science of Cause and Effect.* Basic Books.

---

## 3.1 Modelos Estatísticos e Interpretabilidade

**Conceito + por que existe:** Modelos cuja estrutura permite entender *por que* fazem uma predição — modelos lineares, GLMs, e modelos estatísticos interpretáveis. Existe porque, em muitos contextos de decisão, entender o mecanismo importa mais que a acurácia bruta (um modelo que diz "negado" precisa explicar por quê), e modelos interpretáveis dão transparência que caixas-pretas não dão.

**Profundidade esperada:** Avançado · **Conexões:** → Regressão inferencial (1.5), → Explicabilidade (3.6), → Aprendizado supervisionado (Parte 2, 2.1)

**Erro de iniciante → Marca do sênior:** O iniciante usa o modelo mais complexo disponível sem considerar interpretabilidade. O sênior escolhe o nível de interpretabilidade pela necessidade do contexto (decisões de alto risco exigem transparência), entende o trade-off interpretabilidade vs performance, e prefere o modelo mais simples que resolve o problema.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço modelos estatísticos interpretáveis | — |
| **1** | Sei que existem modelos simples, sem entender o valor | Explico que "alguns modelos são mais simples" |
| **2** | Uso modelos sem considerar interpretabilidade | Treinei o modelo mais complexo disponível |
| **3** | Escolho pelo trade-off interpretabilidade/performance | Escolhi um modelo interpretável para uma decisão de alto risco |
| **4** | Projeto pela necessidade de transparência; justifico a escolha | Justifiquei modelo simples vs complexo pelo contexto de decisão |
| **5** | Domino o trade-off; reconheço quando interpretabilidade é essencial; ensino o critério | Estabeleço os critérios de escolha de modelo de uma organização |

---

## 3.2 Inferência Causal

**Conceito + por que existe:** O framework para inferir relações de causa e efeito a partir de dados — o modelo causal de Pearl (DAGs, do-calculus), contrafactuais, e a distinção fundamental entre correlação e causação. Existe porque a maioria das decisões importantes é causal ("se mudarmos X, o que acontece com Y?"), e correlação não responde a isso — a inferência causal é o que permite raciocinar sobre intervenções a partir de dados.

**Profundidade esperada:** Avançado · **Conexões:** → Design experimental (1.4), → Confounders (3.3), → Regressão inferencial (1.5)

**Referência:**
> **[CLÁSSICO]**
> Hernán, M. A., & Robins, J. M. (2020). *Causal Inference: What If.* Chapman & Hall/CRC. URL gratuita: https://www.hsph.harvard.edu/miguel-hernan/causal-inference-book/
> — referência moderna e rigorosa para inferência causal aplicada.

**Erro de iniciante → Marca do sênior:** O iniciante conclui causalidade de correlação (o erro mais comum e mais custoso em dados). O sênior entende as condições para inferência causal, usa DAGs para raciocinar sobre relações causais, distingue associação de causação rigorosamente, e sabe quando dados observacionais permitem (ou não) conclusões causais.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço inferência causal | — |
| **1** | Sei que "correlação não é causação", como slogan | Repito o slogan sem aplicá-lo |
| **2** | Confundo correlação com causação na prática | Já conclui causa de uma correlação |
| **3** | Entendo as condições para causalidade; uso o raciocínio contrafactual | Distingui rigorosamente associação de causação numa análise |
| **4** | Uso DAGs e do-calculus; projeto análises causais; identifico quando é possível | Usei um DAG para identificar a estratégia de estimação causal |
| **5** | Domino inferência causal; reconheço conclusões causais indevidas; ensino o framework de Pearl | Projeto análises causais para questões complexas de negócio |

> *Para o seu perfil: a inferência causal é matematicamente rica (DAGs, do-calculus, contrafactuais) e é onde sua formação dá vantagem direta. É também uma das competências mais raras e mais valiosas em Data Science — a maioria dos praticantes opera apenas com correlação. Dominar Pearl te colocaria num grupo seleto.*

---

## 3.3 Confounders, Vieses e Validade

**Conceito + por que existe:** Identificar e controlar os fatores que distorcem inferências — variáveis de confusão (confounders), vieses de seleção, e as ameaças à validade interna e externa. Existe porque inferências de dados observacionais são constantemente ameaçadas por fatores não-observados que criam associações espúrias, e reconhecer e controlar esses fatores é o que separa uma conclusão válida de uma falaciosa.

**Profundidade esperada:** Avançado · **Conexões:** → Inferência causal (3.2), → Regressão inferencial (1.5), → Design experimental (1.4)

**Erro de iniciante → Marca do sênior:** O iniciante não considera variáveis de confusão (e atribui a X um efeito que é de Z). O sênior identifica confounders potenciais via raciocínio causal, controla-os adequadamente (sem condicionar em colliders, que introduzem viés), e entende as ameaças à validade de cada conclusão.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço confounders | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "fator que confunde" |
| **2** | Não considero variáveis de confusão | Já atribuí a X um efeito que era de outra variável |
| **3** | Identifico e controlo confounders; entendo os vieses | Identifiquei e controlei um confounder numa análise |
| **4** | Raciocino sobre validade via DAGs; evito condicionar em colliders | Reconheci um collider e evitei controlá-lo |
| **5** | Domino o raciocínio sobre vieses; reconheço ameaças à validade por inspeção; ensino o framework | Projeto análises robustas a vieses de confusão e seleção |

---

## 3.4 Experimentos vs Dados Observacionais

**Conceito + por que existe:** Entender quando e como inferir causalidade de cada tipo de dado — a superioridade de experimentos randomizados, e os métodos quasi-experimentais para dados observacionais (diff-in-diff, matching, variáveis instrumentais, RDD). Existe porque experimentos nem sempre são viáveis (éticos, caros, impossíveis), e métodos quasi-experimentais permitem inferência causal aproximada de dados observacionais — com pressupostos que precisam ser entendidos.

**Profundidade esperada:** Avançado · **Conexões:** → Design experimental (1.4), → Inferência causal (3.2), → Confounders (3.3)

**Referência:**
> **[CLÁSSICO]**
> Angrist, J. D., & Pischke, J.-S. (2009). *Mostly Harmless Econometrics: An Empiricist's Companion.* Princeton University Press.
> — a referência para métodos quasi-experimentais de inferência causal.

**Erro de iniciante → Marca do sênior:** O iniciante trata dados observacionais como se fossem experimentais (conclui causalidade sem os métodos apropriados). O sênior reconhece a diferença fundamental, usa métodos quasi-experimentais apropriados quando experimentos não são possíveis, e entende os pressupostos (e suas vulnerabilidades) de cada método.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei a diferença entre experimentos e observação | — |
| **1** | Ouvi falar, sem entender as implicações | Explico vagamente "experimento é melhor" |
| **2** | Trato dados observacionais como experimentais | Já conclui causa de dados observacionais sem método |
| **3** | Entendo a diferença; conheço métodos quasi-experimentais | Apliquei diff-in-diff ou matching conscientemente |
| **4** | Escolho o método pela situação; entendo os pressupostos; valido-os | Usei variáveis instrumentais justificando os pressupostos |
| **5** | Domino métodos causais; reconheço pressupostos violados; ensino o framework | Projeto estratégias de inferência causal para dados observacionais complexos |

> *Para o seu perfil: estes métodos (diff-in-diff, IV, RDD) são matematicamente sofisticados e econométricos — território onde sua base matemática brilha. É a fronteira entre estatística aplicada e inferência causal rigorosa.*

---

## 3.5 Modelagem Preditiva Aplicada

**Conceito + por que existe:** Aplicar modelos preditivos (cobertos em profundidade na Parte 2) ao contexto de Ciência de Dados, com ênfase em problemas de negócio e interpretação dos resultados. Existe porque o cientista de dados frequentemente constrói modelos preditivos, mas com um foco distinto do engenheiro de ML — a ênfase está em resolver o problema de negócio e interpretar o que o modelo revela, não em otimizar a infraestrutura de serving.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Toda a Camada 2 da Parte 2, → Métricas de negócio (5.2), → Interpretabilidade (3.1)

**Nota de relação com a Parte 2:** esta competência é deliberadamente leve aqui — a profundidade de ML preditivo está na Parte 2 (camadas 2-3). O que se adiciona é o ângulo de aplicação a problemas de negócio e a tradução dos resultados.

**Erro de iniciante → Marca do sênior:** O iniciante otimiza métricas técnicas (AUC) sem conectar ao valor de negócio. O sênior conecta a métrica do modelo ao objetivo de negócio, escolhe o limiar de decisão pelo custo dos erros no contexto real, e comunica o que o modelo significa para a decisão.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei aplicar modelos preditivos a negócio | — |
| **1** | Sei treinar um modelo, sem conectar ao negócio | Treinei um modelo sem pensar no uso |
| **2** | Otimizo métricas técnicas isoladas | Otimizei AUC sem contexto de negócio |
| **3** | Conecto métricas ao objetivo; escolho limiares pelo custo | Escolhi o limiar de decisão pelo custo real dos erros |
| **4** | Projeto a modelagem em torno da decisão de negócio | Desenhei um modelo otimizando o valor de negócio, não só a métrica |
| **5** | Domino modelagem aplicada; reconheço desconexão técnica-negócio; ensino a tradução | Estabeleço como modelos preditivos servem decisões na organização |

---

## 3.6 Interpretação e Explicabilidade de Modelos

**Conceito + por que existe:** Explicar por que um modelo (mesmo complexo) faz suas predições — técnicas de explicabilidade (SHAP, LIME, feature importance) e a comunicação dessas explicações. Existe porque modelos complexos são caixas-pretas, mas decisões importantes exigem explicação (regulatória, ética, de confiança), e as técnicas de explicabilidade tornam modelos opacos parcialmente transparentes.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Interpretabilidade (3.1), → Comunicação (2.5), → Ética (5.6)

**Erro de iniciante → Marca do sênior:** O iniciante usa SHAP/LIME como caixa-preta e interpreta os resultados ingenuamente (ou causalmente). O sênior entende o que cada técnica de explicabilidade realmente mede (e suas limitações), não confunde importância de feature com causalidade, e comunica explicações honestamente.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei explicar modelos | — |
| **1** | Ouvi falar de explicabilidade, sem usar | Nomeio SHAP ou feature importance |
| **2** | Uso SHAP/LIME como caixa-preta | Gerei um gráfico SHAP seguindo exemplo |
| **3** | Entendo o que as técnicas medem; interpreto corretamente | Interpretei valores SHAP sem confundir com causalidade |
| **4** | Escolho a técnica apropriada; comunico explicações honestamente | Expliquei as decisões de um modelo a stakeholders corretamente |
| **5** | Domino explicabilidade; reconheço interpretações enganosas; ensino as limitações | Estabeleço os padrões de explicabilidade de modelos de uma organização |

---

# CAMADA 4 — Engenharia de Dados

> *A infraestrutura que torna os dados utilizáveis em escala. Frequentemente compartilhada com engenheiros de dados dedicados, mas o cientista de dados precisa de fluência aqui.*

**Nota de relação com a Parte 1:** há sobreposição com Infraestrutura/DevOps (pipelines, bancos) e com Back-End (persistência). O foco aqui é especificamente sobre o fluxo e a qualidade de *dados* para análise, não sobre a operação de sistemas em geral.

**Referência base:**
> **[INDUSTRIAL]**
> Reis, J., & Housley, M. (2022). *Fundamentals of Data Engineering.* O'Reilly.
> — a referência moderna para o ciclo de vida da engenharia de dados.

---

## 4.1 Pipelines de Dados e ETL/ELT

**Conceito + por que existe:** Os fluxos automatizados que movem e transformam dados de fontes para destinos analisáveis — ETL (extract-transform-load), ELT, e orquestração de pipelines. Existe porque dados precisam ser movidos de sistemas operacionais para sistemas analíticos de forma confiável e repetível, e os pipelines são a infraestrutura que torna dados disponíveis para análise de forma consistente.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Pipelines de ML (Parte 2, 4.1), → Qualidade (4.4), → CI/CD (Parte 1, Infra 7)

**Erro de iniciante → Marca do sênior:** O iniciante faz transformações ad-hoc e manuais (não-reproduzíveis). O sênior constrói pipelines idempotentes, versionados e monitorados, com tratamento de falhas e a capacidade de reprocessar — tratando o pipeline de dados com o mesmo rigor de engenharia de software.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é um pipeline de dados | — |
| **1** | Faço transformações manuais ad-hoc | Transformei dados manualmente uma vez |
| **2** | Escrevo scripts de transformação sem orquestração | Escrevi um script de ETL simples |
| **3** | Construo pipelines orquestrados; trato falhas | Construí um pipeline com orquestração (Airflow, etc.) |
| **4** | Projeto a arquitetura de pipelines; idempotência e reprocessamento | Desenhei um pipeline de dados robusto e reprocessável |
| **5** | Domino pipelines de dados; reconheço fragilidade; ensino as práticas | Estabeleço a arquitetura de pipelines de dados de uma organização |

---

## 4.2 Modelagem e Armazenamento de Dados (Warehouses, Lakes)

**Conceito + por que existe:** Como organizar e armazenar dados para análise em escala — data warehouses (estruturados, OLAP), data lakes (brutos, flexíveis), modelagem dimensional (star schema), e lakehouses. Existe porque dados analíticos têm padrões de acesso diferentes de dados transacionais (agregações sobre grandes volumes), e arquiteturas de armazenamento especializadas tornam a análise em escala viável e performática.

**Profundidade esperada:** Intermediário · **Conexões:** → Banco (Parte 1, Back-End 4), → Pipelines (4.1), → SQL (4.5)

**Erro de iniciante → Marca do sênior:** O iniciante usa um banco transacional para análise (lento em agregações) ou despeja tudo num data lake sem estrutura (data swamp). O sênior escolhe a arquitetura pelo padrão de uso, modela dados dimensionalmente para análise, e entende os trade-offs entre warehouse, lake e lakehouse.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço arquiteturas de dados analíticos | — |
| **1** | Ouvi falar de data warehouse, sem entender | Nomeio data warehouse ou data lake |
| **2** | Uso o que está disponível sem entender as diferenças | Consultei um data warehouse existente |
| **3** | Entendo warehouse vs lake; modelo dimensionalmente | Modelei dados em star schema para análise |
| **4** | Projeto a arquitetura de armazenamento; escolho por padrão de uso | Desenhei a estratégia de armazenamento analítico de um projeto |
| **5** | Domino arquiteturas de dados; reconheço escolhas inadequadas; ensino os trade-offs | Estabeleço a arquitetura de dados analíticos de uma organização |

---

## 4.3 Processamento Distribuído (Spark, Big Data)

**Conceito + por que existe:** Processar volumes de dados que não cabem em uma máquina — frameworks de processamento distribuído (Spark), o modelo MapReduce, e a computação paralela sobre clusters. Existe porque alguns datasets são grandes demais para uma máquina, e o processamento distribuído permite analisá-los dividindo o trabalho entre múltiplas máquinas — com complexidade própria (shuffles, particionamento).

**Profundidade esperada:** Intermediário · **Conexões:** → Sistemas distribuídos (Parte 1, Back-End 8), → Pipelines (4.1), → Concorrência (Parte 1, Back-End 1.1)

**Erro de iniciante → Marca do sênior:** O iniciante usa Spark para dados que caberiam em memória (overhead desnecessário) ou escreve transformações que causam shuffles massivos. O sênior sabe quando o processamento distribuído é necessário, entende o modelo de execução (lazy evaluation, shuffles), e otimiza para minimizar movimentação de dados.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço processamento distribuído | — |
| **1** | Ouvi falar de Spark/Hadoop, sem entender | Nomeio uma ferramenta de big data |
| **2** | Uso Spark seguindo tutoriais; não entendo o modelo | Rodei um job Spark seguindo exemplo |
| **3** | Entendo o modelo de execução; processo dados distribuídos | Escrevi transformações Spark entendendo lazy evaluation |
| **4** | Projeto para escala; otimizo shuffles e particionamento | Otimizei um job Spark reduzindo shuffles |
| **5** | Domino processamento distribuído; reconheço uso inadequado; ensino a otimização | Estabeleço a estratégia de processamento de big data de uma organização |

---

## 4.4 Qualidade e Governança de Dados

**Conceito + por que existe:** Garantir que os dados sejam confiáveis e bem gerenciados — testes de qualidade de dados, validação de schema, linhagem (lineage), e governança. Existe porque decisões baseadas em dados ruins são piores que decisões sem dados, e a qualidade de dados (validada continuamente, não assumida) é a base de toda análise confiável — "garbage in, garbage out" aplicado em escala.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Detecção de qualidade (2.6), → Limpeza (2.2), → Pipelines (4.1)

**Erro de iniciante → Marca do sênior:** O iniciante assume que os dados do pipeline estão corretos (e descobre problemas quando análises dão errado). O sênior implementa testes de qualidade de dados no pipeline (validação de schema, ranges, completude), rastreia a linhagem dos dados, e trata qualidade de dados como uma propriedade monitorada continuamente.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não penso em qualidade de dados sistematicamente | — |
| **1** | Sei que qualidade importa, sem método | Explico que "dados ruins dão problema" |
| **2** | Verifico qualidade manualmente, esporadicamente | Já verifiquei dados antes de uma análise |
| **3** | Implemento testes de qualidade no pipeline | Adicionei validação de schema e ranges ao pipeline |
| **4** | Projeto a estratégia de qualidade; rastreio linhagem; monitoro continuamente | Desenhei testes de qualidade de dados automatizados |
| **5** | Domino qualidade de dados; reconheço lacunas de validação; ensino governança | Estabeleço a estratégia de qualidade e governança de dados de uma organização |

---

## 4.5 SQL Avançado para Análise

**Conceito + por que existe:** Usar SQL para análise de dados complexa — window functions, CTEs, agregações avançadas, e queries analíticas. Existe porque SQL é a língua franca dos dados, e a maior parte da análise de dados em empresas é feita em SQL sobre data warehouses — dominar SQL analítico avançado é uma das competências mais práticas e demandadas do cientista de dados.

**Profundidade esperada:** Avançado · **Conexões:** → SQL (Parte 1, Back-End 4.2), → Warehouses (4.2), → EDA (2.3)

**Nota de relação com a Parte 1:** o Back-End cobriu SQL para aplicações (queries transacionais, índices). Aqui o foco é SQL *analítico* — window functions, agregações complexas, queries que respondem perguntas de negócio sobre grandes volumes.

**Erro de iniciante → Marca do sênior:** O iniciante extrai dados com SQL básico e faz o resto em Python (ineficiente). O sênior usa SQL avançado (window functions, CTEs) para fazer a análise pesada no banco, escreve queries analíticas complexas e legíveis, e entende a performance de queries analíticas.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei SQL | — |
| **1** | Faço SELECT básico | Faço uma query simples |
| **2** | Uso JOINs e GROUP BY; extraio dados para processar fora | Extraí dados com SQL e processei em Python |
| **3** | Uso window functions e CTEs; faço análise no banco | Escrevi uma query analítica com window functions |
| **4** | Escrevo queries analíticas complexas e performáticas | Resolvi uma análise complexa inteiramente em SQL |
| **5** | Domino SQL analítico; reconheço queries ineficientes; ensino os padrões | Estabeleço os padrões de SQL analítico de um time |

---

# CAMADA 5 — Data Science Aplicado ao Negócio

> *O que transforma análise em impacto. A camada que mais distingue o cientista de dados do estatístico ou do engenheiro — a tradução entre dados e decisão.*

**Referência base:**
> **[INDUSTRIAL]**
> Provost, F., & Fawcett, T. (2013). *Data Science for Business.* O'Reilly.

---

## 5.1 Definição e Enquadramento de Problemas

**Conceito + por que existe:** Traduzir um problema de negócio vago em uma pergunta de dados bem definida e respondível — enquadramento, formulação, e a tradução entre o objetivo de negócio e a análise. Existe porque o problema apresentado raramente é o problema real, e a habilidade de fazer as perguntas certas e enquadrar o problema corretamente determina se a análise será útil — é frequentemente a parte mais difícil e mais valiosa do trabalho.

**Profundidade esperada:** Avançado · **Conexões:** → Métricas de negócio (5.2), → Tomada de decisão (5.4), → Complexidade (Seção 3 do README — qual problema resolver)

**Erro de iniciante → Marca do sênior:** O iniciante aceita o problema como apresentado e mergulha na análise. O sênior questiona e reformula o problema, identifica qual pergunta realmente importa para a decisão, e enquadra o problema de forma respondível — entendendo que resolver o problema errado com perfeição não tem valor.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei enquadrar problemas | — |
| **1** | Aceito o problema como apresentado | Trabalho no problema exatamente como me foi dado |
| **2** | Faço algumas perguntas, mas sigo o enquadramento dado | Pedi alguns esclarecimentos sobre a tarefa |
| **3** | Reformulo o problema; identifico a pergunta real | Reformulei um problema vago numa pergunta respondível |
| **4** | Projeto o enquadramento em torno da decisão; antecipo o que importa | Reenquadrei um problema, mudando o foco da análise para o que importava |
| **5** | Domino o enquadramento; reconheço problemas mal formulados; ensino o craft | Estabeleço como problemas de negócio viram perguntas de dados numa organização |

> *Para o seu perfil: esta competência conecta diretamente à reformulação de problemas que você valoriza (e que pratico nas respostas seguindo suas preferências). Enquadrar bem é meio caminho — e é uma habilidade de raciocínio, não de ferramenta.*

---

## 5.2 Métricas de Negócio e KPIs

**Conceito + por que existe:** Definir e escolher as métricas que realmente medem o sucesso — KPIs, métricas norte (north star), e a distinção entre métricas que importam e métricas de vaidade. Existe porque o que se mede direciona o comportamento, e escolher a métrica errada (ou uma métrica de vaidade) leva a otimizar a coisa errada — definir as métricas certas é uma decisão estratégica que molda toda a análise e ação.

**Profundidade esperada:** Avançado · **Conexões:** → Definição de problemas (5.1), → A/B testing (1.4), → ROI (5.3)

**Erro de iniciante → Marca do sênior:** O iniciante usa métricas fáceis de medir (vaidade — total de usuários) em vez das que importam (retenção, valor). O sênior escolhe métricas que capturam o valor real, entende a diferença entre métricas de vaidade e acionáveis, e reconhece quando uma métrica está sendo "gamed" (lei de Goodhart).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei definir métricas de negócio | — |
| **1** | Uso a métrica que me dão, sem questionar | Reporto a métrica pedida |
| **2** | Uso métricas óbvias (totais), sem distinguir vaidade | Reportei total de usuários como sucesso |
| **3** | Distingo métricas de vaidade de acionáveis; escolho as que importam | Propus uma métrica acionável em vez de uma de vaidade |
| **4** | Projeto sistemas de métricas; antecipo gaming; alinho à estratégia | Desenhei os KPIs de um projeto alinhados ao valor real |
| **5** | Domino definição de métricas; reconheço métricas enganosas; ensino o pensamento estratégico | Estabeleço o framework de métricas de uma organização |

---

## 5.3 Análise de ROI e Impacto

**Conceito + por que existe:** Quantificar o valor e o retorno de iniciativas de dados — análise de ROI, estimativa de impacto, e a tradução de resultados analíticos em valor financeiro. Existe porque recursos são limitados e iniciativas competem por investimento, e a habilidade de quantificar o impacto esperado e realizado de um projeto de dados é o que justifica o investimento e prioriza o trabalho.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Métricas (5.2), → Tomada de decisão (5.4), → Inferência causal (3.2)

**Erro de iniciante → Marca do sênior:** O iniciante não quantifica o impacto do seu trabalho (e não consegue justificá-lo). O sênior estima o ROI esperado antes de iniciar (para priorizar), mede o impacto realizado depois (atribuindo causalmente o efeito à intervenção), e comunica o valor em termos que o negócio entende.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei analisar ROI | — |
| **1** | Não quantifico o impacto do trabalho | Faço análises sem estimar o valor |
| **2** | Menciono benefícios vagamente | Disse que uma análise "ajudaria" sem quantificar |
| **3** | Estimo impacto; quantifico ROI básico | Estimei o ROI de uma iniciativa de dados |
| **4** | Projeto a análise de impacto; atribuo causalmente; priorizo por ROI | Medi o impacto causal realizado de um projeto |
| **5** | Domino análise de impacto; reconheço estimativas infladas; ensino o rigor | Estabeleço como o valor de dados é quantificado numa organização |

---

## 5.4 Tomada de Decisão Orientada a Dados

**Conceito + por que existe:** Usar dados para informar decisões reais sob incerteza — a ponte entre análise e ação, decisão sob incerteza, e o equilíbrio entre dados e julgamento. Existe porque o objetivo final da Ciência de Dados é melhorar decisões, e isso exige entender como dados informam (mas não substituem) o julgamento, como decidir sob incerteza, e quando os dados são suficientes para agir.

**Profundidade esperada:** Avançado · **Conexões:** → Inferência (1.2), → Definição de problemas (5.1), → Comunicação (5.5)

**Erro de iniciante → Marca do sênior:** O iniciante ou ignora dados (decisão por intuição) ou trata dados como verdade absoluta (ignorando incerteza e contexto). O sênior integra dados e julgamento, quantifica a incerteza da recomendação, e sabe quando os dados são suficientes para decidir e quando mais análise não mudaria a decisão.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conecto dados a decisões | — |
| **1** | Apresento dados sem recomendação | Mostro análises sem sugerir ação |
| **2** | Faço recomendações sem considerar incerteza | Recomendei uma ação sem qualificar a incerteza |
| **3** | Integro dados e contexto; quantifico incerteza na recomendação | Fiz uma recomendação qualificando a incerteza |
| **4** | Projeto a análise para a decisão; sei quando dados bastam | Determinei que mais análise não mudaria a decisão e recomendei agir |
| **5** | Domino decisão orientada a dados; reconheço uso ingênuo de dados; ensino o equilíbrio | Estabeleço a cultura de decisão orientada a dados de uma organização |

---

## 5.5 Comunicação Executiva e Influência

**Conceito + por que existe:** Comunicar com lideranças e influenciar decisões estratégicas — adaptar a mensagem a executivos, traduzir análise técnica em implicações estratégicas, e influenciar sem autoridade. Existe porque as decisões de maior impacto são tomadas por lideranças que não são técnicas, e a habilidade de comunicar insight de forma que influencie essas decisões é o que dá ao cientista de dados impacto organizacional real.

**Profundidade esperada:** Avançado · **Conexões:** → Storytelling (2.5), → Tomada de decisão (5.4), → Transferência (Eixo 6 do diagnóstico)

**Erro de iniciante → Marca do sênior:** O iniciante apresenta a executivos com detalhe técnico e metodologia (perde a audiência e a oportunidade). O sênior lidera com a implicação estratégica e a recomendação, traduz a análise em termos de negócio, e estrutura a comunicação para influenciar a decisão — entendendo que executivos querem a conclusão e a confiança, não a derivação.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei comunicar com lideranças | — |
| **1** | Apresento detalhes técnicos a qualquer audiência | Apresentei metodologia a executivos |
| **2** | Tento simplificar, mas ainda excessivamente técnico | Simplifiquei, mas perdi a audiência executiva |
| **3** | Lidero com a implicação; adapto a executivos | Apresentei a executivos liderando com a recomendação |
| **4** | Projeto a comunicação para influenciar; traduzo em estratégia | Influenciei uma decisão estratégica com uma apresentação |
| **5** | Domino comunicação executiva; reconheço comunicação ineficaz; ensino a influência | Sou procurado para comunicar dados a lideranças em decisões críticas |

---

## 5.6 Ética, Privacidade e Responsabilidade em Dados

**Conceito + por que existe:** Usar dados de forma ética e responsável — privacidade, viés algorítmico, fairness, e as implicações sociais e legais do uso de dados. Existe porque dados e modelos têm poder de causar dano (discriminação, violação de privacidade, decisões injustas), e a responsabilidade ética — entender e mitigar esses riscos — é parte integral do trabalho, não um adendo opcional.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Explicabilidade (3.6), → Confounders/vieses (3.3), → Privacidade (Guia de Segurança)

**Erro de iniciante → Marca do sênior:** O iniciante não considera viés ou privacidade até virar um problema. O sênior avalia proativamente o viés dos dados e modelos, considera a privacidade desde o design, entende as implicações de fairness das decisões algorítmicas, e reconhece os limites éticos do que deve ser feito (não apenas do que pode).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não considero ética em dados | — |
| **1** | Sei que existe a questão, sem aplicá-la | Explico vagamente que "tem que ter cuidado com dados" |
| **2** | Considero ética só quando levantada por outros | Reagi a uma preocupação de privacidade levantada |
| **3** | Avalio viés e privacidade proativamente | Avaliei o viés de um modelo antes de implantá-lo |
| **4** | Projeto para fairness e privacidade; antecipo implicações | Desenhei uma análise considerando fairness e privacidade desde o início |
| **5** | Domino ética em dados; reconheço riscos éticos por inspeção; ensino a responsabilidade | Estabeleço os princípios éticos de uso de dados de uma organização |

> *Para o seu perfil: o viés algorítmico conecta a fundamentos estatísticos (a Camada 3 sobre confounders e validade) — entender por que um modelo é enviesado é, em parte, entender vieses estatísticos. Sua base te dá acesso à dimensão técnica da fairness, complementando a dimensão ética.*

---

# Planilha de Auto-Auditoria — Data Scientist

Registre seu nível (0-5) em cada competência. **Regra:** não marque um nível sem passar no teste de validação. Anote a evidência concreta.

## Camada 1 — Fundamentos Estatísticos para Decisão

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 1.1 Estatística Descritiva | ___ | |
| 1.2 Inferência e Estimação | ___ | |
| 1.3 Testes de Hipótese | ___ | |
| 1.4 Design Experimental e A/B Testing | ___ | |
| 1.5 Regressão como Inferência | ___ | |
| 1.6 Análise de Poder e Tamanho de Amostra | ___ | |

## Camada 2 — Análise e Exploração de Dados (EDA)

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 2.1 Coleta e Aquisição | ___ | |
| 2.2 Limpeza e Tratamento (Wrangling) | ___ | |
| 2.3 Análise Exploratória (EDA) | ___ | |
| 2.4 Visualização de Dados | ___ | |
| 2.5 Comunicação e Storytelling | ___ | |
| 2.6 Detecção de Qualidade e Anomalias | ___ | |

## Camada 3 — Modelagem e Causalidade

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 3.1 Modelos Estatísticos e Interpretabilidade | ___ | |
| 3.2 Inferência Causal | ___ | |
| 3.3 Confounders, Vieses e Validade | ___ | |
| 3.4 Experimentos vs Dados Observacionais | ___ | |
| 3.5 Modelagem Preditiva Aplicada | ___ | |
| 3.6 Interpretação e Explicabilidade | ___ | |

## Camada 4 — Engenharia de Dados

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 4.1 Pipelines de Dados e ETL/ELT | ___ | |
| 4.2 Modelagem e Armazenamento (Warehouses/Lakes) | ___ | |
| 4.3 Processamento Distribuído (Spark) | ___ | |
| 4.4 Qualidade e Governança de Dados | ___ | |
| 4.5 SQL Avançado para Análise | ___ | |

## Camada 5 — Data Science Aplicado ao Negócio

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 5.1 Definição e Enquadramento de Problemas | ___ | |
| 5.2 Métricas de Negócio e KPIs | ___ | |
| 5.3 Análise de ROI e Impacto | ___ | |
| 5.4 Tomada de Decisão Orientada a Dados | ___ | |
| 5.5 Comunicação Executiva e Influência | ___ | |
| 5.6 Ética, Privacidade e Responsabilidade | ___ | |

---

## Interpretação do Resultado

- **Especialista em Data Science** tem um perfil característico que o distingue tanto do estatístico puro quanto do engenheiro de ML: **nível 4-5 nas camadas 1 e 3** (rigor estatístico e causalidade — a base científica) E **nível 4-5 na camada 5** (tradução para negócio — o que torna o trabalho útil). A camada 2 (EDA) deve estar em nível 4+ (é o craft central), e a camada 4 (engenharia de dados) em nível 3+ (frequentemente compartilhada com engenheiros dedicados).

- **A combinação rara que define o cientista de dados** é rigor inferencial (camadas 1, 3) + impacto de negócio (camada 5). Um estatístico tem as camadas 1-3 mas não a 5; um engenheiro de dados tem a 4 mas não as 1, 3; um analista de negócio tem a 5 mas não o rigor das 1, 3. O cientista de dados completo combina o rigor científico com o impacto organizacional.

- **A causalidade (camada 3) é o divisor de águas intelectual.** A maioria dos praticantes de dados opera apenas com correlação e modelagem preditiva. Dominar inferência causal (Pearl, métodos quasi-experimentais) é o que separa o cientista de dados que pode responder "o que acontece se mudarmos X?" do que só pode dizer "X está associado a Y". É a competência mais difícil e mais valiosa.

- **Para o seu perfil específico — onde sua matemática mais brilha:**
  - **Camada 1 (estatística para decisão):** sua formação te coloca potencialmente em nível 5 — a interpretação rigorosa de p-valores, intervalos de confiança e poder estatístico é exatamente o que sua base garante e o que a maioria erra.
  - **Camada 3 (causalidade):** território matematicamente rico (DAGs, do-calculus, econometria) onde você tem vantagem direta. É também, provavelmente, uma área de *exposição limitada* — você tem a capacidade de raciocínio, mas pode não ter praticado inferência causal formal. Um alvo de alto valor.
  - **Camada 5 (negócio):** provavelmente sua área de menor exposição (seu trabalho é técnico/pesquisa, não consultoria de negócio), mas onde o Eixo 6 (transferência) do seu diagnóstico se aplica. A comunicação e o enquadramento são habilidades de raciocínio transferíveis ao seu objetivo de conteúdo.

- **A síntese para suas três especialidades:** comparando as três Partes, emerge um padrão. Sua força central (matemática + rigor) é um *substrato compartilhado* que beneficia as três carreiras de formas diferentes — em Engenharia de Software, fundamenta o raciocínio arquitetural/topológico; em IA, fundamenta o entendimento de modelos; em Data Science, fundamenta a inferência e a causalidade. A Parte 4 (matriz comparativa) tornará esse padrão explícito.

---

## Referências

| # | Fonte | Tipo | Uso |
|---|-------|------|-----|
| 1 | Dreyfus & Dreyfus (1980). *Five-Stage Model of Skill Acquisition.* UC Berkeley. | **PEER-REVIEWED** | Escala de progressão |
| 2 | Smith & Kendall (1963). *Retranslation of Expectations.* JAP, 47(2). DOI: 10.1037/h0047060 | **PEER-REVIEWED** | Âncoras comportamentais (BARS) |
| 3 | Kruger & Dunning (1999). *Unskilled and Unaware of It.* JPSP, 77(6). | **PEER-REVIEWED** | Viés de auto-avaliação |
| 4 | Tukey, J. W. (1977). *Exploratory Data Analysis.* Addison-Wesley. | **CLÁSSICO** | Camada 2 (EDA) |
| 5 | Pearl, J. (2009). *Causality* (2nd ed.). Cambridge University Press. | **CLÁSSICO** | Camada 3 (inferência causal) |
| 6 | Pearl, J., & Mackenzie, D. (2018). *The Book of Why.* Basic Books. | **INDUSTRIAL** | Camada 3 (causalidade, acessível) |
| 7 | Hernán, M. A., & Robins, J. M. (2020). *Causal Inference: What If.* Chapman & Hall/CRC. | **CLÁSSICO** | Camada 3.2 (inferência causal aplicada) |
| 8 | Angrist, J. D., & Pischke, J.-S. (2009). *Mostly Harmless Econometrics.* Princeton. | **CLÁSSICO** | Camada 3.4 (métodos quasi-experimentais) |
| 9 | Kohavi, R., Tang, D., & Xu, Y. (2020). *Trustworthy Online Controlled Experiments.* Cambridge. | **INDUSTRIAL** | Camada 1.4 (A/B testing) |
| 10 | Tufte, E. R. (2001). *The Visual Display of Quantitative Information* (2nd ed.). Graphics Press. | **CLÁSSICO** | Camada 2.4 (visualização) |
| 11 | Reis, J., & Housley, M. (2022). *Fundamentals of Data Engineering.* O'Reilly. | **INDUSTRIAL** | Camada 4 (engenharia de dados) |
| 12 | Provost, F., & Fawcett, T. (2013). *Data Science for Business.* O'Reilly. | **INDUSTRIAL** | Camada 5 (aplicação a negócio) |

---

*Parte 3 de 3 das especialidades. **Parte 3 (Data Scientist) COMPLETA**: 5 camadas, 29 competências, todas com progressão Dreyfus 0-5.*
*Concluídas: Parte 1 (Engenharia de Software), Parte 2 (Desenvolvedor de IA) e Parte 3 (Data Scientist) — as três especialidades. Próximas: as sínteses (Partes 4-7: matriz comparativa, arquitetura de maturidade, checklist consolidado, análise final).*
*Escala ancorada em Dreyfus (1980) + BARS (Smith & Kendall, 1963). Auto-avaliação deve ser complementada por validação externa de pares seniores (Kruger & Dunning, 1999).*
*Revisão recomendada a cada 6 meses, registrando a evolução de nível e a nova evidência concreta.*
