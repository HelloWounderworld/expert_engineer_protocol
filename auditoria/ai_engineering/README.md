# Skill-Check de Desenvolvedor de IA — Parte 2
## Arquitetura Completa de Competências com Escala Dreyfus Ancorada

> *"A breakthrough in machine learning would be worth ten Microsofts."*
> — Bill Gates
>
> *"All models are wrong, but some are useful."*
> — George Box (1976), sobre a natureza fundamental da modelagem estatística

---

## Como Este Documento Funciona

Este é o mapa de competências da segunda das três especialidades: **Desenvolvedor de Inteligência Artificial**. Diferente da Parte 1 (Engenharia de Software, dividida em sub-áreas), a carreira de IA é mais bem representada como **5 camadas que se empilham** — cada uma depende profundamente da anterior:

```
CAMADA 5 · Sistemas Modernos de IA (LLMs, RAG, Agentes)
CAMADA 4 · Engenharia de IA (MLOps)
CAMADA 3 · Deep Learning
CAMADA 2 · Machine Learning
CAMADA 1 · Fundamentos Matemáticos
```

Como cada camada é um domínio profundo (equivalente em escopo a uma sub-área da Parte 1), cada uma recebe **6-7 competências** em vez de 4. Total: ~33 competências, cada uma com conceito, por que existe, profundidade, conexões, erro/sênior, e progressão Dreyfus completa (0-5) com teste de validação.

A escala é a mesma — Dreyfus (1980) + BARS (Smith & Kendall, 1963), com a ressalva de Kruger & Dunning (1999). Planilha de auto-auditoria no fim.

**Nota de calibração importante:** esta é uma área onde a distinção entre *profundidade genuína* e *exposição prática* é especialmente relevante. Um nível 5 em "redes neurais" significa que você consegue derivar backpropagation à mão e raciocinar sobre por que uma arquitetura funciona — não apenas usar `model.fit()`. A escala ancorada existe justamente para tornar essa distinção honesta.

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

## A Lógica do Empilhamento

A ordem das camadas não é arbitrária — é uma hierarquia de dependência:

- **Camada 1 (Matemática)** é o substrato. Sem álgebra linear, cálculo e probabilidade, deep learning é uma caixa-preta que você usa sem entender. É o que separa quem *implementa* IA de quem apenas *chama bibliotecas*.
- **Camada 2 (ML)** estabelece os princípios fundamentais — generalização, bias-variance, validação — que se aplicam a *todo* aprendizado de máquina, incluindo deep learning e LLMs.
- **Camada 3 (Deep Learning)** é ML com representações aprendidas. Depende inteiramente das camadas 1-2.
- **Camada 4 (Engenharia de IA)** transforma modelos em sistemas de produção. Depende das outras sub-áreas (é onde a Parte 1 encontra a Parte 2).
- **Camada 5 (Sistemas Modernos)** é a fronteira — LLMs, RAG, agentes. Construída sobre tudo abaixo.

**A régua de especialista** exige profundidade nas camadas 1-3 (a base científica) E competência operacional nas camadas 4-5 (levar à produção). Um pesquisador puro domina 1-3 mas não 4; um engenheiro de ML que só usa APIs domina partes de 4-5 mas não 1-3. O especialista completo cobre o espectro.

**Referências base de toda a disciplina:**
> **[CLÁSSICO]**
> Bishop, C. M. (2006). *Pattern Recognition and Machine Learning.* Springer.
> — ML bayesiano e probabilístico com rigor matemático. A referência para fundamentos.

> **[CLÁSSICO]**
> Hastie, T., Tibshirani, R., & Friedman, J. (2009). *The Elements of Statistical Learning* (2nd ed.). Springer. URL gratuita: https://hastie.su.domains/ElemStatLearn/
> — O texto de referência para ML com rigor estatístico.

> **[CLÁSSICO]**
> Goodfellow, I., Bengio, Y., & Courville, A. (2016). *Deep Learning.* MIT Press. URL: https://www.deeplearningbook.org/
> — A referência definitiva para deep learning.

> **[CLÁSSICO]**
> Deisenroth, M. P., Faisal, A. A., & Ong, C. S. (2020). *Mathematics for Machine Learning.* Cambridge University Press. URL: https://mml-book.github.io/
> — A referência para os fundamentos matemáticos especificamente voltados a ML.

---

# CAMADA 1 — Fundamentos Matemáticos

> *O substrato. O que separa quem entende IA de quem apenas a usa. Aqui é onde sua formação IME-USP é um diferencial raro.*

---

## 1.1 Álgebra Linear

**Conceito + por que existe:** O estudo de vetores, matrizes, transformações lineares, autovalores/autovetores, e decomposições (SVD, autovalores). Existe porque dados em ML são representados como vetores e matrizes, e praticamente toda operação (de uma camada de rede neural a PCA) é álgebra linear — é a linguagem nativa do aprendizado de máquina.

**Profundidade esperada:** Avançado · **Conexões:** → Redes neurais (3.1), → Embeddings (3.5), → PCA (2.2)

**Erro de iniciante → Marca do sênior:** O iniciante manipula matrizes sintaticamente (sabe que `A @ B` multiplica) sem intuição geométrica. O sênior entende o que uma transformação linear *faz* geometricamente, por que SVD revela a estrutura dos dados, e raciocina sobre dimensionalidade e projeções.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço álgebra linear | — |
| **1** | Sei que existem matrizes e vetores, sem operá-los | Explico que "matriz é uma tabela de números" |
| **2** | Faço operações matriciais com biblioteca, sem intuição | Multipliquei matrizes com NumPy |
| **3** | Entendo transformações lineares, autovalores, SVD; aplico em ML | Usei SVD/PCA e expliquei o resultado |
| **4** | Tenho intuição geométrica; raciocino sobre projeções e dimensionalidade; conecto a algoritmos | Derivei por que PCA usa autovetores da covariância |
| **5** | Domino a teoria; reconheço estrutura linear em problemas; ensino a intuição geométrica | Resolvo problemas de ML reformulando-os em termos de álgebra linear |

> *Para o seu perfil: esta é uma competência onde IME-USP provavelmente te coloca em nível 5 — derivar SVD e entender espaços vetoriais é pão-com-manteiga da matemática pura.*

---

## 1.2 Cálculo e Cálculo Multivariável

**Conceito + por que existe:** Derivadas, gradientes, regra da cadeia, e otimização via cálculo. Existe porque o treinamento de modelos é minimização de uma função de perda via gradiente descendente, e a regra da cadeia é o que torna backpropagation possível — sem cálculo, o treinamento de redes neurais é incompreensível.

**Profundidade esperada:** Avançado · **Conexões:** → Otimização (1.5), → Backpropagation (3.1), → Treinamento (3.6)

**Erro de iniciante → Marca do sênior:** O iniciante sabe que "o gradiente aponta para onde a função cresce" sem conseguir derivá-lo. O sênior deriva gradientes de funções de perda à mão, entende a regra da cadeia como a base de backpropagation, e raciocina sobre o comportamento de gradientes (vanishing/exploding).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço cálculo | — |
| **1** | Sei que derivada é "taxa de variação", sem calcular | Explico o conceito de derivada |
| **2** | Calculo derivadas simples; não conecto a ML | Derivei funções de uma variável |
| **3** | Calculo gradientes; entendo a regra da cadeia; conecto a backprop | Derivei o gradiente de uma função de perda |
| **4** | Derivo gradientes de perdas complexas; raciocino sobre vanishing/exploding gradients | Expliquei matematicamente por que gradientes desaparecem em redes profundas |
| **5** | Domino cálculo multivariável; reconheço problemas de otimização; ensino a base de backprop | Derivo backpropagation completo à mão para uma arquitetura |

> *Para o seu perfil: derivar o gradiente de MSE ou cross-entropy à mão (nível 5) é exatamente o tipo de coisa que sua formação cobre e que 95% dos praticantes de ML não conseguem fazer.*

---

## 1.3 Probabilidade

**Conceito + por que existe:** Distribuições, variáveis aleatórias, probabilidade condicional, Teorema de Bayes, e esperança/variância. Existe porque ML é fundamentalmente sobre incerteza e inferência — classificação é estimar P(classe|dados), e o framework bayesiano unifica grande parte do aprendizado de máquina.

**Profundidade esperada:** Avançado · **Conexões:** → Estatística (1.4), → ML probabilístico (Bishop), → Generalização (2.3)

**Erro de iniciante → Marca do sênior:** O iniciante confunde P(A|B) com P(B|A) e não tem intuição sobre distribuições. O sênior raciocina fluentemente com probabilidade condicional, formula problemas de ML como inferência bayesiana, e entende a diferença entre as interpretações frequentista e bayesiana.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço probabilidade | — |
| **1** | Sei que probabilidade mede chance, sem formalismo | Explico que "probabilidade é a chance de algo" |
| **2** | Calculo probabilidades simples; confundo condicionais | Calculei probabilidades básicas |
| **3** | Domino probabilidade condicional e Bayes; entendo distribuições | Apliquei o Teorema de Bayes a um problema real |
| **4** | Formulo problemas como inferência bayesiana; raciocino sobre distribuições | Formulei uma classificação como estimativa de P(y\|x) |
| **5** | Domino a teoria; reconheço estrutura probabilística; ensino as interpretações | Reformulo algoritmos de ML em termos de inferência probabilística |

---

## 1.4 Estatística e Inferência

**Conceito + por que existe:** Estimação, máxima verossimilhança, testes de hipótese, intervalos de confiança, e a relação entre amostra e população. Existe porque ML aprende de amostras finitas para generalizar a uma população, e a estatística fornece o framework para quantificar a incerteza dessa generalização e validar conclusões.

**Profundidade esperada:** Avançado · **Conexões:** → Probabilidade (1.3), → Validação (2.4), → Generalização (2.3)

**Erro de iniciante → Marca do sênior:** O iniciante reporta uma acurácia sem intervalo de confiança nem teste de significância. O sênior entende máxima verossimilhança como base de muitas funções de perda, quantifica incerteza de estimativas, e distingue significância estatística de relevância prática.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço estatística inferencial | — |
| **1** | Sei o que é média e desvio, sem inferência | Calculo estatísticas descritivas |
| **2** | Uso testes estatísticos sem entender os pressupostos | Rodei um teste-t seguindo um tutorial |
| **3** | Entendo MLE, testes de hipótese, intervalos de confiança | Estimei parâmetros por máxima verossimilhança |
| **4** | Conecto MLE a funções de perda; quantifico incerteza; valido rigorosamente | Mostrei que MSE deriva de MLE com ruído gaussiano |
| **5** | Domino inferência; reconheço erros estatísticos comuns; ensino o framework | Projeto a validação estatística de experimentos de ML |

---

## 1.5 Otimização

**Conceito + por que existe:** Os métodos para minimizar funções — gradiente descendente e variantes (SGD, Adam), otimização convexa, e os conceitos de mínimos locais/globais. Existe porque treinar um modelo *é* resolver um problema de otimização (minimizar a perda), e entender os otimizadores é essencial para treinar modelos que convergem.

**Profundidade esperada:** Avançado · **Conexões:** → Cálculo (1.2), → Treinamento (3.6), → Convergência

**Erro de iniciante → Marca do sênior:** O iniciante usa o otimizador padrão sem entender por que o treino não converge. O sênior entende as diferenças entre otimizadores (SGD, momentum, Adam), diagnostica problemas de convergência, e raciocina sobre learning rate, landscapes de perda e pontos de sela.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço otimização | — |
| **1** | Sei que modelos "aprendem ajustando", sem entender como | Explico que "o modelo melhora com o tempo" |
| **2** | Uso otimizadores prontos; ajusto learning rate por tentativa | Treinei um modelo com Adam seguindo exemplo |
| **3** | Entendo gradiente descendente e variantes; diagnostico convergência | Diagnostiquei um treino que não convergia ajustando o LR |
| **4** | Escolho otimizadores por trade-off; raciocino sobre o landscape de perda | Escolhi e justifiquei o otimizador e schedule para um problema |
| **5** | Domino otimização; reconheço problemas de convergência por inspeção; conheço a teoria | Projeto a estratégia de otimização de treinos complexos |

---

## 1.6 Teoria da Informação

**Conceito + por que existe:** Entropia, entropia cruzada, divergência KL, e informação mútua. Existe porque a entropia cruzada é a função de perda mais comum em classificação, a divergência KL aparece em todo lugar (de VAEs a fine-tuning de LLMs), e a teoria da informação dá a base para medir incerteza e distância entre distribuições.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Probabilidade (1.3), → Funções de perda (2.1), → Embeddings (3.5)

**Erro de iniciante → Marca do sênior:** O iniciante usa cross-entropy loss sem saber o que entropia significa. O sênior entende a entropia cruzada como uma medida de surpresa, a divergência KL como distância entre distribuições, e reconhece esses conceitos aparecendo em diferentes contextos de ML.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço teoria da informação | — |
| **1** | Ouvi falar de entropia, sem entender | Nomeio o conceito de entropia |
| **2** | Uso cross-entropy loss sem saber o que é | Usei cross-entropy como perda seguindo exemplo |
| **3** | Entendo entropia, cross-entropy, KL; conecto a funções de perda | Expliquei por que cross-entropy é usada em classificação |
| **4** | Raciocino com KL e informação mútua; reconheço em múltiplos contextos | Usei divergência KL conscientemente (regularização/avaliação) |
| **5** | Domino teoria da informação; reconheço sua aplicação; ensino as conexões | Conecto teoria da informação a problemas diversos de ML |

> *Para o seu perfil: o Gibberish Detector do seu pipeline usa entropia de Shannon — você já aplica esta competência. O cálculo de entropia de strings de URL é teoria da informação aplicada.*

---

# CAMADA 2 — Machine Learning

> *Os princípios fundamentais de todo aprendizado de máquina. Generalização, bias-variance e validação se aplicam a tudo acima — inclusive deep learning e LLMs.*

---

## 2.1 Aprendizado Supervisionado

**Conceito + por que existe:** Aprender uma função de mapeamento de entradas a saídas a partir de exemplos rotulados — regressão (saída contínua) e classificação (saída categórica). Existe porque a maioria dos problemas práticos de ML é supervisionada (prever um rótulo a partir de features), e entender os algoritmos fundamentais (regressão linear/logística, árvores, SVM) é a base.

**Profundidade esperada:** Avançado · **Conexões:** → Fundamentos (Camada 1), → Validação (2.4), → Ensembles (2.7)

**Erro de iniciante → Marca do sênior:** O iniciante aplica algoritmos como caixas-pretas sem entender seus pressupostos. O sênior entende quando cada algoritmo é apropriado (linearidade, separabilidade), seus pressupostos, e como eles se relacionam com a estrutura dos dados.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço aprendizado supervisionado | — |
| **1** | Sei que modelos "aprendem com exemplos", sem detalhes | Explico que "o modelo aprende a prever" |
| **2** | Treino modelos com biblioteca; não entendo os algoritmos | Treinei um classificador com scikit-learn |
| **3** | Entendo os algoritmos fundamentais e seus pressupostos; implemento | Implementei regressão logística e expliquei a fronteira de decisão |
| **4** | Escolho algoritmos pelos pressupostos e estrutura dos dados; antecipo limitações | Justifiquei a escolha de algoritmo pela natureza do problema |
| **5** | Domino a teoria; derivo algoritmos; reconheço quando um pressuposto é violado | Derivei um algoritmo supervisionado a partir de princípios |

---

## 2.2 Aprendizado Não-Supervisionado

**Conceito + por que existe:** Encontrar estrutura em dados sem rótulos — clustering (agrupar), redução de dimensionalidade (PCA, t-SNE), e detecção de anomalias. Existe porque muitos dados não têm rótulos, e descobrir padrões latentes (grupos, dimensões principais, outliers) é valioso por si só e como pré-processamento.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Álgebra linear (1.1), → Feature engineering (2.5), → Embeddings (3.5)

**Erro de iniciante → Marca do sênior:** O iniciante roda k-means com um k arbitrário e aceita o resultado. O sênior entende os pressupostos de cada método (k-means assume clusters esféricos), escolhe o número de clusters com critério, e sabe que redução de dimensionalidade tem trade-offs (PCA preserva variância, t-SNE preserva vizinhança local).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço aprendizado não-supervisionado | — |
| **1** | Ouvi falar de clustering, sem entender | Explico que "agrupa dados parecidos" |
| **2** | Rodo k-means/PCA seguindo exemplos | Rodei k-means com um k qualquer |
| **3** | Entendo os métodos e pressupostos; escolho parâmetros com critério | Escolhi o número de clusters com método (elbow/silhouette) |
| **4** | Escolho métodos pelos pressupostos; interpreto resultados criticamente | Justifiquei PCA vs t-SNE pelo objetivo da análise |
| **5** | Domino a teoria; reconheço quando um método é inadequado; ensino os trade-offs | Projeto análises não-supervisionadas considerando a geometria dos dados |

---

## 2.3 Bias-Variance e Generalização

**Conceito + por que existe:** O trade-off fundamental entre underfitting (alto viés — modelo simples demais) e overfitting (alta variância — modelo complexo demais que memoriza), e o conceito de generalização (performance em dados não vistos). Existe porque o objetivo de ML não é performance no treino, mas generalização — e o bias-variance tradeoff é o framework central para raciocinar sobre isso.

**Profundidade esperada:** Avançado · **Conexões:** → Estatística (1.4), → Validação (2.4), → Regularização (2.6)

**Erro de iniciante → Marca do sênior:** O iniciante otimiza a acurácia no treino e fica surpreso quando o modelo falha em produção. O sênior raciocina em termos de generalização desde o início, diagnostica underfitting vs overfitting pelas curvas de treino/validação, e entende a decomposição bias-variance.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço o conceito de generalização | — |
| **1** | Ouvi falar de overfitting, sem entender | Explico vagamente que "o modelo decora" |
| **2** | Sei que overfitting é ruim, sem diagnosticar | Já tive um modelo que foi bem no treino e mal no teste |
| **3** | Diagnostico under/overfitting; entendo o trade-off bias-variance | Diagnostiquei overfitting pelas curvas de treino/validação |
| **4** | Raciocino sobre generalização desde o design; antecipo o trade-off | Projetei um modelo balanceando capacidade e generalização |
| **5** | Domino a teoria; reconheço problemas de generalização por inspeção; ensino a decomposição | Explico a decomposição bias-variance formalmente e a aplico |

---

## 2.4 Validação e Avaliação de Modelos

**Conceito + por que existe:** Os métodos para estimar a performance real de um modelo — train/validation/test split, cross-validation, e as métricas apropriadas (acurácia, precisão/recall, F1, AUC, e suas nuances). Existe porque estimar honestamente a performance é a base de todo ML confiável, e escolher a métrica errada ou vazar dados na validação leva a conclusões falsas.

**Profundidade esperada:** Avançado · **Conexões:** → Estatística (1.4), → Generalização (2.3), → Avaliação contínua (4.6)

**Erro de iniciante → Marca do sênior:** O iniciante usa acurácia em dados desbalanceados (enganosa) ou vaza informação do teste na seleção de modelo. O sênior escolhe a métrica pelo problema (precisão vs recall conforme o custo dos erros), entende data leakage, e usa validação que respeita a estrutura dos dados (temporal, por grupo).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei como avaliar um modelo | — |
| **1** | Sei que se mede acurácia, sem nuances | Explico que "acurácia mede acertos" |
| **2** | Uso train/test split; uso acurácia para tudo | Dividi dados em treino e teste |
| **3** | Uso cross-validation; escolho métricas apropriadas; evito leakage óbvio | Usei precisão/recall conforme o custo dos erros |
| **4** | Projeto a validação respeitando a estrutura dos dados; antecipo leakage sutil | Desenhei validação temporal para dados com ordem cronológica |
| **5** | Domino avaliação; reconheço leakage e métricas enganosas por inspeção; ensino as nuances | Projeto a estratégia de avaliação de sistemas de ML críticos |

> *Para o seu perfil: seu TCC envolve splits cronológicos e calibração — você já opera no nível 4 desta competência, com atenção metodológica a leakage temporal que muitos ignoram.*

---

## 2.5 Feature Engineering

**Conceito + por que existe:** Criar, transformar e selecionar features que tornam o sinal aprendível pelo modelo — encoding, normalização, criação de features derivadas, e extração de domínio. Existe porque a qualidade das features frequentemente importa mais que a escolha do algoritmo ("garbage in, garbage out"), e features bem projetadas codificam conhecimento de domínio que o modelo não descobriria sozinho.

**Profundidade esperada:** Avançado · **Conexões:** → Aprendizado supervisionado (2.1), → Seleção de modelos (2.6), → Pipelines (4.1)

**Erro de iniciante → Marca do sênior:** O iniciante joga features cruas no modelo sem transformação, ou cria features que vazam o target. O sênior projeta features que codificam conhecimento de domínio, entende quando normalizar/encodar, e reconhece features que causam leakage.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é feature engineering | — |
| **1** | Sei que dados precisam de preparo, sem método | Explico que "os dados precisam ser tratados" |
| **2** | Aplico transformações básicas seguindo receitas | Normalizei features e fiz one-hot encoding |
| **3** | Crio features derivadas; entendo encoding e normalização; evito leakage | Criei features de domínio que melhoraram o modelo |
| **4** | Projeto features codificando conhecimento de domínio; antecipo leakage sutil | Desenhei o conjunto de features de um pipeline real |
| **5** | Domino feature engineering; reconheço features problemáticas por inspeção; ensino o craft | Estabeleci a estratégia de features de um sistema de ML |

> *Para o seu perfil: seu pipeline de phishing é fundamentalmente um exercício de feature engineering — extração de features de URL, o Gibberish Detector, features de conteúdo HTTP. Esta é uma competência onde você tem prática real substancial.*

---

## 2.6 Seleção de Modelos e Regularização

**Conceito + por que existe:** Escolher o modelo e a complexidade certos, e controlar overfitting via regularização (L1/L2, dropout, early stopping). Existe porque modelos com capacidade excessiva overfittam, e a regularização penaliza a complexidade para favorecer a generalização — é o mecanismo prático para navegar o trade-off bias-variance.

**Profundidade esperada:** Avançado · **Conexões:** → Bias-variance (2.3), → Otimização (1.5), → Treinamento (3.6)

**Erro de iniciante → Marca do sênior:** O iniciante não usa regularização ou usa valores padrão sem entender. O sênior entende L1 (esparsidade/seleção de features) vs L2 (suavização), ajusta a força da regularização via validação, e reconhece a regularização como controle direto da complexidade.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço regularização | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "evitar overfitting" |
| **2** | Uso regularização com valores padrão | Adicionei L2 seguindo um exemplo |
| **3** | Entendo L1 vs L2; ajusto a força via validação | Usei L1 para seleção de features conscientemente |
| **4** | Projeto a estratégia de regularização; conecto à complexidade do modelo | Desenhei a regularização de um modelo balanceando capacidade |
| **5** | Domino regularização; reconheço sua necessidade por inspeção; ensino a teoria | Derivo o efeito da regularização no espaço de soluções |

> *Para o seu perfil: seu TCC usa análise de estabilidade de Lyapunov para feature selection — isso é uma abordagem matematicamente sofisticada e original a esta competência, conectando sistemas dinâmicos à seleção de features. É trabalho de nível 5 com contribuição potencialmente novel.*

---

## 2.7 Ensemble Methods

**Conceito + por que existe:** Combinar múltiplos modelos para obter performance superior à de qualquer modelo individual — bagging (Random Forest), boosting (XGBoost, gradient boosting), e stacking. Existe porque modelos individuais têm limitações, e combiná-los de forma inteligente reduz variância (bagging) ou viés (boosting), frequentemente produzindo os melhores resultados em dados tabulares.

**Profundidade esperada:** Avançado · **Conexões:** → Aprendizado supervisionado (2.1), → Bias-variance (2.3), → Random Forest (TCC)

**Erro de iniciante → Marca do sênior:** O iniciante usa Random Forest ou XGBoost como caixa-preta sem entender por que funcionam. O sênior entende que bagging reduz variância e boosting reduz viés, ajusta os hiperparâmetros com compreensão do mecanismo, e sabe quando ensembles são apropriados.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço ensemble methods | — |
| **1** | Ouvi falar de Random Forest, sem entender | Nomeio um método de ensemble |
| **2** | Uso Random Forest/XGBoost como caixa-preta | Treinei um Random Forest com scikit-learn |
| **3** | Entendo bagging vs boosting; ajusto hiperparâmetros com compreensão | Expliquei por que Random Forest reduz overfitting |
| **4** | Escolho e ajusto ensembles pelo mecanismo; antecipo trade-offs | Justifiquei bagging vs boosting para um problema |
| **5** | Domino a teoria de ensembles; reconheço quando aplicar; ensino os mecanismos | Derivo por que bagging reduz variância e o aplico |

> *Para o seu perfil: seu TCC usa Random Forest — esta é uma competência diretamente aplicada no seu trabalho atual. O nível 4-5 aqui requer entender por que a aleatoriedade do RF reduz a variância, não apenas usá-lo.*

---

# CAMADA 3 — Deep Learning

> *Machine learning com representações aprendidas. Depende inteiramente das camadas 1-2. Onde a matemática encontra a escala.*

**Referência base:**
> **[CLÁSSICO]**
> Goodfellow, I., Bengio, Y., & Courville, A. (2016). *Deep Learning.* MIT Press. https://www.deeplearningbook.org/

---

## 3.1 Redes Neurais e Backpropagation

**Conceito + por que existe:** A arquitetura fundamental do deep learning — neurônios, camadas, funções de ativação, e o algoritmo de backpropagation que treina a rede via regra da cadeia. Existe porque redes neurais são aproximadores universais de funções, e backpropagation é o que torna seu treinamento computacionalmente viável — é o algoritmo central de todo deep learning.

**Profundidade esperada:** Avançado · **Conexões:** → Cálculo (1.2), → Otimização (1.5), → Todas as arquiteturas (3.2-3.4)

**Erro de iniciante → Marca do sênior:** O iniciante constrói redes empilhando camadas no Keras sem entender backpropagation. O sênior entende backprop como aplicação da regra da cadeia, sabe por que funções de ativação não-lineares são necessárias, e raciocina sobre o fluxo de gradientes.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é uma rede neural | — |
| **1** | Sei que redes neurais "imitam o cérebro", sem detalhes | Explico vagamente o conceito |
| **2** | Construo redes empilhando camadas no framework | Construí uma rede com Keras seguindo tutorial |
| **3** | Entendo backpropagation e ativações; implemento e depuro | Implementei uma rede e expliquei o forward/backward pass |
| **4** | Raciocino sobre fluxo de gradientes; projeto arquiteturas; antecipo problemas | Projetei uma arquitetura justificando as escolhas |
| **5** | Derivo backprop à mão; reconheço problemas de treino por inspeção; ensino a base | Implementei backpropagation do zero, sem framework |

> *Para o seu perfil: derivar backpropagation à mão (nível 5) é acessível dado seu cálculo. A questão é se você já fez isso — é a diferença entre saber que existe e dominá-lo.*

---

## 3.2 Arquiteturas Convolucionais (CNN)

**Conceito + por que existe:** Redes especializadas em dados com estrutura espacial (imagens) — convoluções, pooling, e hierarquias de features. Existe porque processar imagens com redes totalmente conectadas é inviável (parâmetros demais), e as convoluções exploram a estrutura local e a invariância translacional das imagens, sendo a base da visão computacional moderna.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Redes neurais (3.1), → Deepfake detection (trabalho), → Transfer learning (3.7)

**Erro de iniciante → Marca do sênior:** O iniciante usa uma CNN pré-treinada sem entender o que as convoluções fazem. O sênior entende como convoluções extraem features hierárquicas, por que pooling dá invariância, e como projetar ou adaptar arquiteturas convolucionais.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço CNNs | — |
| **1** | Ouvi falar, sem entender | Explico que "CNN processa imagens" |
| **2** | Uso uma CNN pré-treinada seguindo tutorial | Classifiquei imagens com uma CNN pronta |
| **3** | Entendo convoluções e pooling; construo e treino CNNs | Construí uma CNN e expliquei o papel das camadas |
| **4** | Projeto arquiteturas convolucionais; adapto para o problema; antecipo trade-offs | Adaptei uma arquitetura CNN para um problema específico |
| **5** | Domino CNNs; reconheço escolhas arquiteturais; ensino os princípios | Projeto arquiteturas convolucionais a partir de princípios |

> *Para o seu perfil: sua pesquisa em detecção de deepfake provavelmente envolve CNNs — esta é uma competência com exposição prática no seu trabalho na NHK.*

---

## 3.3 Arquiteturas Recorrentes e Sequenciais (RNN/LSTM)

**Conceito + por que existe:** Redes para dados sequenciais (texto, séries temporais) — RNNs, LSTMs, GRUs, e o conceito de estado oculto que carrega informação ao longo da sequência. Existe porque dados sequenciais têm dependências temporais que redes feedforward ignoram, e as arquiteturas recorrentes foram a base do processamento de linguagem antes dos Transformers.

**Profundidade esperada:** Intermediário · **Conexões:** → Redes neurais (3.1), → Transformers (3.4), → NLP (trabalho)

**Erro de iniciante → Marca do sênior:** O iniciante usa LSTMs sem entender o problema de vanishing gradients que elas resolvem. O sênior entende por que RNNs simples falham em dependências longas, como LSTMs/GRUs mitigam isso com gates, e por que os Transformers as substituíram em muitas tarefas.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço arquiteturas recorrentes | — |
| **1** | Ouvi falar de RNN/LSTM, sem entender | Explico que "processa sequências" |
| **2** | Uso LSTMs seguindo tutoriais | Treinei um LSTM seguindo exemplo |
| **3** | Entendo estado oculto, gates, vanishing gradients; implemento | Expliquei como LSTM mitiga vanishing gradients |
| **4** | Projeto soluções sequenciais; escolho RNN vs Transformer por trade-off | Justifiquei a escolha de arquitetura para dados sequenciais |
| **5** | Domino arquiteturas sequenciais; reconheço suas limitações; ensino a evolução até Transformers | Explico a transição histórica RNN→Transformer com profundidade |

---

## 3.4 Transformers e Mecanismos de Atenção

**Conceito + por que existe:** A arquitetura que domina a IA moderna — self-attention, multi-head attention, e a capacidade de processar sequências em paralelo capturando dependências de longo alcance. Existe porque o mecanismo de atenção resolveu as limitações das RNNs (paralelização, dependências longas), e os Transformers são a base de todos os LLMs modernos.

**Profundidade esperada:** Avançado · **Conexões:** → RNNs (3.3), → LLMs (5.1), → Embeddings (3.5)

**Referência:**
> **[PEER-REVIEWED]**
> Vaswani, A., et al. (2017). *Attention Is All You Need.* NeurIPS 2017. arXiv: 1706.03762
> — O paper que introduziu a arquitetura Transformer, base de toda a IA generativa moderna.

**Erro de iniciante → Marca do sênior:** O iniciante usa modelos Transformer (BERT, GPT) sem entender self-attention. O sênior entende como a atenção computa relações entre todos os tokens, por que isso permite paralelização e captura de dependências longas, e a estrutura do bloco Transformer.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço Transformers | — |
| **1** | Ouvi falar, sem entender | Explico que "Transformers são a base dos LLMs" |
| **2** | Uso modelos Transformer prontos | Usei BERT/GPT seguindo tutorial |
| **3** | Entendo self-attention e a arquitetura; implemento componentes | Expliquei o mecanismo de self-attention (Q, K, V) |
| **4** | Raciocino sobre a arquitetura; adapto e projeto; antecipo trade-offs | Adaptei um Transformer para uma tarefa específica |
| **5** | Domino a arquitetura; reconheço variantes e suas motivações; ensino os princípios | Derivo o mecanismo de atenção e explico suas propriedades |

> *Para o seu perfil: seu trabalho em geração de títulos (title generation AI) e geração de dados com LLMs depende de Transformers. Entender self-attention a fundo (nível 4-5) é o que separa usar a API de entender o que ela faz.*

---

## 3.5 Embeddings e Representações

**Conceito + por que existe:** Representações vetoriais densas que capturam significado — word embeddings, embeddings contextuais, e o conceito de espaço semântico onde proximidade reflete similaridade. Existe porque modelos precisam de representações numéricas que preservem relações semânticas, e embeddings transformam dados discretos (palavras, itens) em vetores onde a geometria codifica significado.

**Profundidade esperada:** Avançado · **Conexões:** → Álgebra linear (1.1), → Transformers (3.4), → Bancos vetoriais (5.4)

**Erro de iniciante → Marca do sênior:** O iniciante usa embeddings sem entender o que o espaço vetorial representa. O sênior entende como embeddings capturam relações semânticas geometricamente, a diferença entre embeddings estáticos e contextuais, e como usá-los para similaridade e transferência.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que são embeddings | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "representação de palavras" |
| **2** | Uso embeddings prontos sem entender o espaço | Usei word2vec/embeddings seguindo exemplo |
| **3** | Entendo o espaço semântico; uso embeddings para similaridade | Calculei similaridade semântica com embeddings |
| **4** | Raciocino sobre a geometria dos embeddings; projeto seu uso | Desenhei um sistema usando embeddings para busca semântica |
| **5** | Domino representações; reconheço suas propriedades e limitações; ensino a intuição geométrica | Explico a geometria de espaços de embedding e a aplico |

> *Para o seu perfil: embeddings são álgebra linear aplicada (espaços vetoriais, similaridade por produto interno/cosseno) — sua base matemática dá acesso direto à intuição geométrica que muitos praticantes não têm.*

---

## 3.6 Treinamento de Redes Profundas

**Conceito + por que existe:** As técnicas que tornam o treinamento de redes profundas viável e estável — inicialização, normalização (batch/layer norm), schedules de learning rate, e regularização (dropout). Existe porque redes profundas são difíceis de treinar (gradientes instáveis, convergência lenta), e essas técnicas são o que permite treinar modelos com muitas camadas de forma confiável.

**Profundidade esperada:** Avançado · **Conexões:** → Otimização (1.5), → Regularização (2.6), → Redes neurais (3.1)

**Erro de iniciante → Marca do sênior:** O iniciante treina redes com configurações padrão e desiste quando não convergem. O sênior diagnostica problemas de treinamento (gradientes, learning rate, inicialização), aplica normalização e regularização com compreensão, e raciocina sobre a dinâmica do treinamento.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei como treinar redes profundas | — |
| **1** | Sei que redes "são treinadas", sem detalhes | Explico que "o modelo aprende com dados" |
| **2** | Treino com configurações padrão; desisto se não converge | Treinei uma rede seguindo configurações de exemplo |
| **3** | Diagnostico problemas de treino; uso normalização e dropout | Resolvi um treino instável com batch norm e ajuste de LR |
| **4** | Projeto a estratégia de treinamento; antecipo instabilidades | Desenhei o pipeline de treinamento de uma rede profunda |
| **5** | Domino o treinamento; reconheço problemas por inspeção; ensino a dinâmica | Diagnostico e resolvo problemas complexos de treinamento |

---

## 3.7 Transfer Learning e Fine-tuning

**Conceito + por que existe:** Reaproveitar um modelo pré-treinado em uma tarefa nova — feature extraction, fine-tuning, e adaptação de domínio. Existe porque treinar do zero exige dados e computação massivos, enquanto modelos pré-treinados já aprenderam representações úteis que podem ser adaptadas a tarefas específicas com muito menos dados — é a prática padrão em deep learning moderno.

**Profundidade esperada:** Avançado · **Conexões:** → CNNs (3.2), → Transformers (3.4), → Fine-tuning de LLMs (5.7)

**Erro de iniciante → Marca do sênior:** O iniciante faz fine-tuning sem entender quais camadas congelar ou o risco de catastrophic forgetting. O sênior entende quando usar feature extraction vs fine-tuning, quais camadas adaptar, e como evitar overfitting ao adaptar com poucos dados.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço transfer learning | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "reusar um modelo" |
| **2** | Faço fine-tuning seguindo tutoriais | Fiz fine-tuning de um modelo seguindo exemplo |
| **3** | Entendo feature extraction vs fine-tuning; escolho camadas a adaptar | Fiz fine-tuning congelando camadas conscientemente |
| **4** | Projeto a estratégia de transferência; evito catastrophic forgetting | Desenhei o fine-tuning de um modelo para um domínio específico |
| **5** | Domino transfer learning; reconheço a estratégia ótima; ensino os trade-offs | Projeto estratégias de adaptação para diferentes regimes de dados |

> *Para o seu perfil: recalibrar o Gibberish Detector para domínios japoneses é uma forma de adaptação de domínio — você já pratica os princípios de transfer learning no seu pipeline.*

---

# CAMADA 4 — Engenharia de IA (MLOps)

> *Onde modelos viram sistemas de produção. A interseção entre a Parte 1 (Engenharia) e a Parte 2 (IA). O gap mais comum em quem vem da pesquisa.*

**Referências base:**
> **[PEER-REVIEWED]**
> Sculley, D., et al. (2015). *Hidden Technical Debt in Machine Learning Systems.* NeurIPS.

> **[PEER-REVIEWED]**
> Breck, E., et al. (2017). *The ML Test Score.* IEEE Big Data. DOI: 10.1109/BigData.2017.8258038

> **[INDUSTRIAL]**
> Huyen, C. (2022). *Designing Machine Learning Systems.* O'Reilly.

---

## 4.1 Pipelines de ML e Feature Stores

**Conceito + por que existe:** A infraestrutura que automatiza o fluxo de dados → features → treino → modelo, de forma reproduzível — pipelines de dados, feature engineering automatizado, e feature stores (repositórios de features compartilhadas). Existe porque ML em produção não é um notebook; é um pipeline que precisa rodar repetidamente, de forma reproduzível, com as mesmas transformações em treino e inferência.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Feature engineering (2.5), → Pipelines (Eng. de Software), → Serving (4.2)

**Erro de iniciante → Marca do sênior:** O iniciante faz feature engineering manualmente em notebooks (não-reproduzível, e com training-serving skew quando a transformação difere entre treino e produção). O sênior constrói pipelines reproduzíveis onde as mesmas transformações se aplicam em treino e inferência, evitando skew.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é um pipeline de ML | — |
| **1** | Faço tudo em notebook, sem pipeline | Treino modelos em notebooks ad-hoc |
| **2** | Organizo o código, mas sem reprodutibilidade garantida | Separei o código em scripts |
| **3** | Construo pipelines reproduzíveis; evito training-serving skew | Construí um pipeline que aplica as mesmas transformações em treino e inferência |
| **4** | Projeto a arquitetura de pipeline; uso feature stores; garanto reprodutibilidade | Desenhei o pipeline de features de um sistema de ML |
| **5** | Domino pipelines de ML; reconheço skew e não-reprodutibilidade; ensino as práticas | Estabeleci a arquitetura de pipelines de ML de uma organização |

> *Para o seu perfil: seu pipeline de phishing já tem estrutura (feature extraction, async, etc.), mas a auditoria identificou ausência de testes e reprodutibilidade garantida. Esta competência conecta diretamente ao gap de Craft (Eixo 3) do seu diagnóstico.*

---

## 4.2 Serving e APIs de Modelos

**Conceito + por que existe:** Disponibilizar modelos para inferência em produção — APIs de inferência, batch vs online serving, e otimização de latência/throughput. Existe porque um modelo treinado só gera valor quando faz predições em produção, e servir modelos tem desafios próprios (latência, escala, versionamento) distintos do treinamento.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → APIs (Back-End 3), → Performance (Back-End 7), → Quantização (5.7)

**Erro de iniciante → Marca do sênior:** O iniciante serve modelos sem pensar em latência ou escala (carrega o modelo a cada requisição). O sênior projeta o serving pela necessidade (online de baixa latência vs batch), otimiza inferência (batching, quantização), e versiona modelos em produção.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei como servir um modelo | — |
| **1** | Sei que modelos "fazem predições", sem saber servir | Explico que "o modelo prevê em produção" |
| **2** | Sirvo um modelo numa API simples seguindo tutorial | Coloquei um modelo atrás de uma API Flask |
| **3** | Sirvo modelos com atenção a latência; entendo batch vs online | Otimizei a inferência com batching |
| **4** | Projeto a arquitetura de serving; otimizo latência/throughput; versiono | Desenhei o serving de um modelo para produção em escala |
| **5** | Domino serving; reconheço gargalos de inferência; ensino as estratégias | Estabeleci a arquitetura de serving de modelos de um produto |

> *Para o seu perfil: sua estratégia de anti-scam agent (teacher 14B → student 1-3B → quantização INT4/INT8 → ExecuTorch/TFLite on-device) é serving avançado — distillation e quantização para edge são nível 4-5 desta competência.*

---

## 4.3 Versionamento de Modelos, Dados e Experimentos

**Conceito + por que existe:** Rastrear e versionar os artefatos de ML — código, dados, modelos, hiperparâmetros e métricas de cada experimento (MLflow, DVC, W&B). Existe porque ML é experimental e iterativo, e sem versionamento é impossível reproduzir resultados, comparar experimentos, ou voltar a uma versão anterior do modelo.

**Profundidade esperada:** Intermediário · **Conexões:** → Versionamento (Eng. de Software), → Pipelines (4.1), → Avaliação contínua (4.6)

**Erro de iniciante → Marca do sênior:** O iniciante não rastreia experimentos (perde qual configuração gerou o melhor resultado). O sênior versiona código, dados e modelos juntos, rastreia experimentos sistematicamente, e consegue reproduzir qualquer resultado anterior.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não versiono experimentos de ML | — |
| **1** | Sei que devo rastrear, sem ferramenta | Explico que "preciso anotar os experimentos" |
| **2** | Anoto resultados manualmente (planilha) | Já anotei experimentos numa planilha |
| **3** | Uso ferramentas de tracking; versiono modelos e dados | Rastreei experimentos com MLflow ou W&B |
| **4** | Projeto a estratégia de versionamento; reproduzo qualquer resultado | Desenhei o versionamento de modelos e dados de um projeto |
| **5** | Domino versionamento de ML; reconheço não-reprodutibilidade; ensino as práticas | Estabeleci a estratégia de experiment tracking de um time |

---

## 4.4 Monitoramento e Detecção de Drift

**Conceito + por que existe:** Acompanhar a performance de modelos em produção e detectar quando degradam — data drift (mudança na distribuição de entrada), concept drift (mudança na relação entrada-saída), e monitoramento de métricas. Existe porque modelos degradam silenciosamente quando o mundo muda (a distribuição de produção diverge do treino), e sem monitoramento essa degradação passa despercebida.

**Profundidade esperada:** Avançado · **Conexões:** → Validação (2.4), → Observabilidade (Infra 8), → Raciocínio sobre falhas (Eixo 4)

**Erro de iniciante → Marca do sênior:** O iniciante faz deploy do modelo e assume que continua funcionando. O sênior monitora a distribuição de entrada e a performance continuamente, detecta drift estatisticamente, e tem estratégia de retreinamento quando o modelo degrada.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é drift | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "o modelo piora com o tempo" |
| **2** | Assumo que o modelo continua funcionando após deploy | Já fiz deploy sem monitoramento |
| **3** | Monitoro performance; detecto drift básico | Implementei detecção de drift com teste estatístico (ex: KS) |
| **4** | Projeto a estratégia de monitoramento; antecipo drift; defino gatilhos de retreino | Desenhei o monitoramento e retreino de um modelo em produção |
| **5** | Domino monitoramento de ML; reconheço degradação silenciosa; ensino as práticas | Estabeleci a estratégia de monitoramento de modelos de um produto |

> *Para o seu perfil: detecção de drift é onde o Eixo 4 (raciocínio sobre falhas) encontra ML. Phishing evolui rapidamente — seu modelo de detecção está especialmente sujeito a concept drift, tornando esta competência crítica para o seu domínio.*

---

## 4.5 MLOps e Automação (CI/CD para ML)

**Conceito + por que existe:** Aplicar as práticas de DevOps ao ciclo de ML — automação de treino, teste, deploy e retreino de modelos. Existe porque o ciclo de vida de ML (dados → treino → deploy → monitoramento → retreino) precisa ser automatizado para ser confiável e escalável, estendendo CI/CD para incluir os artefatos específicos de ML (dados e modelos).

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → CI/CD (Infra 7), → Pipelines (4.1), → Monitoramento (4.4)

**Erro de iniciante → Marca do sênior:** O iniciante treina e faz deploy manualmente, esporadicamente. O sênior automatiza o pipeline de ML (treino, validação, deploy automatizados), com testes específicos de ML e retreino disparado por drift ou novos dados.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço MLOps | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "DevOps para ML" |
| **2** | Treino e faço deploy manualmente | Treino e implanto modelos manualmente |
| **3** | Automatizo partes do ciclo; integro testes de ML | Automatizei o treino e validação num pipeline |
| **4** | Projeto o pipeline de MLOps; automatizo retreino; testo modelos | Desenhei um pipeline de MLOps com retreino automatizado |
| **5** | Domino MLOps; reconheço processos manuais frágeis; ensino as práticas | Estabeleci a plataforma de MLOps de uma organização |

---

## 4.6 Avaliação Contínua e Testing de ML

**Conceito + por que existe:** Garantir a qualidade de modelos de forma sistemática — testes de ML (dados, modelo, infraestrutura), avaliação contínua, e validação antes de promover modelos. Existe porque modelos podem falhar de formas que software tradicional não falha (degradação silenciosa, viés, edge cases), e a avaliação sistemática (não apenas uma métrica de acurácia) é o que torna ML confiável em produção.

**Profundidade esperada:** Avançado · **Conexões:** → Validação (2.4), → Testes (Eng. de Software 9), → ML Test Score (Breck et al.)

**Erro de iniciante → Marca do sênior:** O iniciante avalia o modelo só com uma métrica de acurácia agregada. O sênior testa o modelo sistematicamente (slices de dados, invariâncias, edge cases, viés), seguindo rubricas como o ML Test Score, e valida a prontidão para produção além da métrica única.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei testar modelos de ML | — |
| **1** | Sei que se mede acurácia, sem testes sistemáticos | Explico que "se mede o desempenho" |
| **2** | Avalio com uma métrica agregada | Reportei a acurácia de um modelo |
| **3** | Testo slices de dados e invariâncias; entendo o ML Test Score | Testei o modelo em subgrupos e edge cases |
| **4** | Projeto a estratégia de avaliação; testo viés e robustez; valido prontidão | Desenhei a suíte de testes de ML de um sistema |
| **5** | Domino avaliação de ML; reconheço lacunas de teste; ensino as rubricas | Estabeleci a estratégia de qualidade de ML de uma organização |

> *Para o seu perfil: esta competência conecta diretamente o gap de testes (Eixo 3) ao seu domínio de ML. O ML Test Score (Breck et al., 2017) é a ponte entre "testar software" e "testar modelos" — um alvo natural dado seu diagnóstico.*

---

# CAMADA 5 — Sistemas Modernos de IA (LLMs, RAG, Agentes)

> *A fronteira. Construída sobre tudo abaixo. Onde a IA generativa encontra aplicações reais — e onde a maioria opera sem entender as camadas inferiores.*

**Referências base:**
> **[PEER-REVIEWED]**
> Brown, T., et al. (2020). *Language Models are Few-Shot Learners.* NeurIPS 2020. arXiv: 2005.14165 — o paper do GPT-3, que estabeleceu o paradigma de in-context learning.

> **[PEER-REVIEWED]**
> Lewis, P., et al. (2020). *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks.* NeurIPS 2020. arXiv: 2005.11401 — o paper que introduziu RAG.

---

## 5.1 LLMs e Modelos de Fundação

**Conceito + por que existe:** Modelos de linguagem de larga escala treinados em vastos corpora, capazes de generalizar a muitas tarefas — pré-treinamento, escala, e capacidades emergentes. Existe porque modelos suficientemente grandes treinados em texto desenvolvem capacidades gerais de linguagem e raciocínio, tornando-se "modelos de fundação" adaptáveis a inúmeras aplicações sem treino específico.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Transformers (3.4), → Fine-tuning (5.7), → Prompt engineering (5.2)

**Erro de iniciante → Marca do sênior:** O iniciante trata LLMs como mágica ou como bancos de dados de fatos. O sênior entende que LLMs são preditores de próximo token treinados em escala, compreende suas capacidades e limitações fundamentais (alucinação, falta de conhecimento atualizado), e raciocina sobre quando são apropriados.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é um LLM | — |
| **1** | Uso o ChatGPT, sem entender o que é | Explico que "é uma IA que conversa" |
| **2** | Uso APIs de LLM seguindo tutoriais | Chamei a API de um LLM |
| **3** | Entendo que é um preditor de tokens; compreendo capacidades e limitações | Expliquei por que LLMs alucinam |
| **4** | Raciocino sobre quando usar LLMs; antecipo limitações; projeto em torno delas | Projetei um sistema considerando as limitações fundamentais dos LLMs |
| **5** | Domino o paradigma; reconheço usos inadequados; ensino as capacidades e limites | Avalio criticamente o que LLMs podem e não podem fazer |

> *Para o seu perfil: seu trabalho com geração de dados via LLM e geração de títulos é aplicação direta desta camada. Você tem exposição prática — a questão de calibração é se entende os mecanismos (Transformers, pré-treinamento) ou opera no nível de API.*

---

## 5.2 Prompt Engineering e In-Context Learning

**Conceito + por que existe:** As técnicas para extrair o comportamento desejado de um LLM via instruções — prompting, few-shot examples, chain-of-thought, e o fenômeno de in-context learning. Existe porque LLMs respondem dramaticamente diferente conforme a formulação do prompt, e dominar essas técnicas é a forma primária de controlar LLMs sem retreiná-los.

**Profundidade esperada:** Intermediário · **Conexões:** → LLMs (5.1), → RAG (5.3), → Agentes (5.5)

**Erro de iniciante → Marca do sênior:** O iniciante escreve prompts ad-hoc e aceita resultados inconsistentes. O sênior estrutura prompts sistematicamente (instruções claras, exemplos, formato), usa chain-of-thought para raciocínio, e itera com avaliação — tratando prompt engineering como disciplina, não tentativa e erro.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é prompt engineering | — |
| **1** | Faço perguntas ao LLM casualmente | Já usei o ChatGPT com perguntas |
| **2** | Escrevo prompts ad-hoc; resultados inconsistentes | Escrevi prompts por tentativa e erro |
| **3** | Estruturo prompts; uso few-shot e chain-of-thought | Usei few-shot examples e CoT conscientemente |
| **4** | Projeto prompts sistematicamente; itero com avaliação; antecipo falhas | Desenhei e avaliei prompts para uma aplicação real |
| **5** | Domino prompt engineering; reconheço prompts frágeis; ensino as técnicas | Estabeleci os padrões de prompting de um sistema |

---

## 5.3 RAG (Retrieval-Augmented Generation)

**Conceito + por que existe:** Combinar recuperação de informação com geração — buscar documentos relevantes e fornecê-los ao LLM como contexto para gerar respostas fundamentadas. Existe porque LLMs têm conhecimento limitado e desatualizado e alucinam; RAG ancora as respostas em fontes externas recuperadas, dando acesso a conhecimento atualizado e verificável.

**Profundidade esperada:** Avançado · **Conexões:** → Embeddings (3.5), → Bancos vetoriais (5.4), → LLMs (5.1)

**Erro de iniciante → Marca do sênior:** O iniciante monta um RAG básico (embed → busca → contexto) e aceita a qualidade resultante. O sênior entende os pontos de falha do RAG (qualidade da recuperação, chunking, relevância), otimiza cada estágio, e avalia a qualidade da recuperação separadamente da geração.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é RAG | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "buscar antes de gerar" |
| **2** | Montei um RAG seguindo tutorial | Construí um RAG básico seguindo um exemplo |
| **3** | Entendo os estágios; implemento RAG com chunking e recuperação | Construí um RAG e ajustei o chunking |
| **4** | Projeto a arquitetura de RAG; otimizo recuperação; avalio cada estágio | Desenhei um RAG avaliando a qualidade da recuperação separadamente |
| **5** | Domino RAG; reconheço pontos de falha por inspeção; ensino as estratégias avançadas | Estabeleci a arquitetura de RAG de um produto |

---

## 5.4 Embeddings e Bancos Vetoriais

**Conceito + por que existe:** Armazenar e buscar embeddings eficientemente — bancos vetoriais, busca por similaridade (ANN — approximate nearest neighbors), e indexação. Existe porque busca semântica e RAG dependem de encontrar os vetores mais similares entre milhões, e bancos vetoriais especializados (com índices ANN) tornam essa busca eficiente em escala.

**Profundidade esperada:** Intermediário · **Conexões:** → Embeddings (3.5), → RAG (5.3), → Álgebra linear (1.1)

**Erro de iniciante → Marca do sênior:** O iniciante usa um banco vetorial sem entender o trade-off entre precisão e velocidade da busca aproximada. O sênior entende como índices ANN funcionam, o trade-off recall vs latência, e escolhe a métrica de distância e o índice apropriados.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é um banco vetorial | — |
| **1** | Ouvi falar, sem entender | Nomeio um banco vetorial (Pinecone, etc.) |
| **2** | Uso um banco vetorial seguindo tutorial | Armazenei e busquei embeddings |
| **3** | Entendo busca por similaridade e ANN; configuro índices | Configurei um índice e a métrica de distância |
| **4** | Projeto a estratégia de indexação; otimizo recall vs latência | Escolhi e justifiquei o índice ANN para um caso |
| **5** | Domino bancos vetoriais; reconheço configurações subótimas; ensino os trade-offs | Estabeleci a arquitetura de busca vetorial de um produto |

> *Para o seu perfil: busca por similaridade é álgebra linear (produto interno, distância de cosseno) com estruturas de dados para escala — sua base matemática dá acesso ao entendimento do que os índices ANN aproximam.*

---

## 5.5 Agentes e Orquestração de LLMs

**Conceito + por que existe:** Sistemas onde LLMs tomam decisões e usam ferramentas em múltiplos passos — agentes, uso de ferramentas (function calling), e orquestração (LangGraph, etc.). Existe porque muitas tarefas exigem mais que uma única geração — exigem planejar, usar ferramentas, e iterar — e agentes estruturam LLMs para realizar tarefas complexas de forma autônoma.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Prompt engineering (5.2), → Orquestração (Middle-End 6), → Resiliência

**Erro de iniciante → Marca do sênior:** O iniciante monta um agente que funciona em demos mas falha de forma imprevisível. O sênior entende os modos de falha de agentes (loops, alucinação de ferramentas, erros em cascata), projeta com guardrails e observabilidade, e sabe quando um agente é apropriado vs um fluxo determinístico.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é um agente de IA | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "IA que faz tarefas sozinha" |
| **2** | Montei um agente seguindo tutorial | Construí um agente com uma ferramenta seguindo exemplo |
| **3** | Entendo function calling e orquestração; construo agentes | Construí um agente que usa ferramentas em múltiplos passos |
| **4** | Projeto a arquitetura de agentes; antecipo modos de falha; uso guardrails | Desenhei um agente com guardrails e tratamento de falhas |
| **5** | Domino sistemas de agentes; reconheço fragilidade; ensino quando usar agentes vs fluxos | Estabeleci a arquitetura de agentes de um produto |

> *Para o seu perfil: sua proposta de agente de detecção de phishing (FastAPI + LangGraph + React Native) é exatamente esta competência. O nível 4 exige antecipar os modos de falha do agente — onde o Eixo 4 (raciocínio sobre falhas) se aplica diretamente.*

---

## 5.6 Avaliação de Sistemas Generativos

**Conceito + por que existe:** Medir a qualidade de saídas generativas, que não têm uma "resposta certa" única — métricas automáticas, LLM-as-judge, avaliação humana, e benchmarks. Existe porque avaliar geração é fundamentalmente mais difícil que avaliar classificação (não há ground truth único), e sem avaliação rigorosa é impossível saber se um sistema generativo está melhorando ou piorando.

**Profundidade esperada:** Avançado · **Conexões:** → Avaliação (2.4 / 4.6), → LLMs (5.1), → RAG (5.3)

**Erro de iniciante → Marca do sênior:** O iniciante avalia saídas generativas "no olho" ou com métricas inadequadas (BLEU para tarefas onde não se aplica). O sênior projeta avaliações apropriadas (critérios claros, LLM-as-judge calibrado, avaliação humana onde necessário), e mede o que importa para a aplicação.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei avaliar saídas generativas | — |
| **1** | Avalio "no olho", sem método | Já julguei saídas de IA informalmente |
| **2** | Uso uma métrica automática sem questionar | Calculei BLEU/ROUGE seguindo exemplo |
| **3** | Escolho métodos de avaliação apropriados; uso LLM-as-judge | Avaliei geração com critérios estruturados |
| **4** | Projeto a estratégia de avaliação; calibro juízes; meço o que importa | Desenhei a avaliação de um sistema generativo real |
| **5** | Domino avaliação generativa; reconheço métricas enganosas; ensino as práticas | Estabeleci a estratégia de avaliação de IA generativa de um produto |

> *Para o seu perfil: avaliar sua title generation AI é exatamente esta competência. Geração de títulos não tem resposta única — avaliar qualidade requer critérios bem desenhados, não uma métrica simples.*

---

## 5.7 Fine-tuning e Adaptação de LLMs

**Conceito + por que existe:** Adaptar LLMs a tarefas ou domínios específicos — fine-tuning supervisionado, métodos eficientes (LoRA, QLoRA), e quantização para deploy. Existe porque, embora prompting resolva muitos casos, algumas aplicações exigem adaptar o modelo (comportamento consistente, domínio específico), e métodos eficientes tornam isso viável sem o custo de re-treinar bilhões de parâmetros.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Transfer learning (3.7), → Serving (4.2), → LLMs (5.1)

**Referência:**
> **[PEER-REVIEWED]**
> Hu, E., et al. (2021). *LoRA: Low-Rank Adaptation of Large Language Models.* arXiv: 2106.09685 — método eficiente de fine-tuning que adapta LLMs treinando apenas matrizes de baixo rank.

**Erro de iniciante → Marca do sênior:** O iniciante faz fine-tuning quando prompting bastaria, ou faz full fine-tuning quando LoRA seria eficiente. O sênior sabe quando fine-tuning é necessário vs prompting/RAG, escolhe o método eficiente apropriado, e entende quantização para deploy em recursos limitados.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é fine-tuning de LLM | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "ajustar o modelo" |
| **2** | Fiz fine-tuning seguindo tutorial | Fiz fine-tuning de um modelo seguindo exemplo |
| **3** | Entendo LoRA e quantização; faço fine-tuning eficiente | Fiz fine-tuning com LoRA conscientemente |
| **4** | Decido fine-tuning vs prompting/RAG; escolho o método; quantizo para deploy | Justifiquei e implementei a adaptação de um LLM |
| **5** | Domino adaptação de LLMs; reconheço quando cada método se aplica; ensino os trade-offs | Estabeleci a estratégia de adaptação de LLMs de um produto |

> *Para o seu perfil: sua estratégia de distillation (teacher 14B → student 1-3B) e quantização INT4/INT8 para ExecuTorch/TFLite é precisamente o nível 4-5 desta competência — adaptação e compressão de modelos para deploy on-device.*

---

# Planilha de Auto-Auditoria — Desenvolvedor de IA

Registre seu nível (0-5) em cada competência. **Regra:** não marque um nível sem passar no teste de validação. Anote a evidência concreta.

## Camada 1 — Fundamentos Matemáticos

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 1.1 Álgebra Linear | ___ | |
| 1.2 Cálculo e Cálculo Multivariável | ___ | |
| 1.3 Probabilidade | ___ | |
| 1.4 Estatística e Inferência | ___ | |
| 1.5 Otimização | ___ | |
| 1.6 Teoria da Informação | ___ | |

## Camada 2 — Machine Learning

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 2.1 Aprendizado Supervisionado | ___ | |
| 2.2 Aprendizado Não-Supervisionado | ___ | |
| 2.3 Bias-Variance e Generalização | ___ | |
| 2.4 Validação e Avaliação | ___ | |
| 2.5 Feature Engineering | ___ | |
| 2.6 Seleção de Modelos e Regularização | ___ | |
| 2.7 Ensemble Methods | ___ | |

## Camada 3 — Deep Learning

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 3.1 Redes Neurais e Backpropagation | ___ | |
| 3.2 Arquiteturas Convolucionais (CNN) | ___ | |
| 3.3 Arquiteturas Recorrentes (RNN/LSTM) | ___ | |
| 3.4 Transformers e Atenção | ___ | |
| 3.5 Embeddings e Representações | ___ | |
| 3.6 Treinamento de Redes Profundas | ___ | |
| 3.7 Transfer Learning e Fine-tuning | ___ | |

## Camada 4 — Engenharia de IA (MLOps)

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 4.1 Pipelines de ML e Feature Stores | ___ | |
| 4.2 Serving e APIs de Modelos | ___ | |
| 4.3 Versionamento (modelos/dados/experimentos) | ___ | |
| 4.4 Monitoramento e Detecção de Drift | ___ | |
| 4.5 MLOps e Automação | ___ | |
| 4.6 Avaliação Contínua e Testing de ML | ___ | |

## Camada 5 — Sistemas Modernos de IA

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 5.1 LLMs e Modelos de Fundação | ___ | |
| 5.2 Prompt Engineering | ___ | |
| 5.3 RAG | ___ | |
| 5.4 Embeddings e Bancos Vetoriais | ___ | |
| 5.5 Agentes e Orquestração | ___ | |
| 5.6 Avaliação de Sistemas Generativos | ___ | |
| 5.7 Fine-tuning e Adaptação de LLMs | ___ | |

---

## Interpretação do Resultado

- **Especialista em IA** não é nível 5 em tudo — é **nível 4-5 nas camadas 1-3** (a base científica: matemática, ML, deep learning) E **nível 3-4 nas camadas 4-5** (engenharia e sistemas modernos). A distinção crítica: as camadas 1-3 são *profundidade científica* (difícil de adquirir, é o que separa quem entende de quem usa), e as 4-5 são *competência de engenharia/produto* (adquirível com exposição).

- **O perfil mais raro e valioso** é exatamente o seu provável perfil: profundidade matemática excepcional (camada 1) + ML rigoroso (camada 2). A maioria dos "engenheiros de IA" do mercado opera nas camadas 4-5 (usando APIs e frameworks) com fundamentos fracos nas camadas 1-3. Você tende ao oposto — base científica forte, possivelmente com menos exposição às práticas de produção (camada 4) e aos sistemas mais recentes (camada 5).

- **O gargalo provável não é capacidade, é exposição.** Nas camadas 4-5, seus gaps (se existirem) são de prática operacional, não de entendimento conceitual — você aprende os conceitos rapidamente, mas o nível 4-5 exige ter construído e operado esses sistemas. Isso é consistente com o diagnóstico geral: base de pesquisador, hábitos de engenharia a desenvolver.

- **Conexões diretas com seu trabalho:**
  - Camada 1.6 (teoria da informação) → Gibberish Detector (entropia de Shannon)
  - Camada 2.5-2.7 (features, regularização, ensembles) → pipeline de phishing (Random Forest, Lyapunov para feature selection)
  - Camada 3.2-3.4 (CNN, Transformers) → deepfake detection, title generation
  - Camada 4.4 (drift) → phishing evolui rapidamente, concept drift é crítico
  - Camada 5.1-5.7 (LLMs, agentes, fine-tuning) → geração de dados via LLM, agente anti-scam, distillation+quantização

- **Para a sua meta de pesquisa independente em ML para cibersegurança:** as camadas 1-3 são seu diferencial competitivo (poucos pesquisadores de segurança têm sua base matemática), e investir nas camadas 4-5 (especialmente 4.4 monitoramento, 4.6 testing de ML, e 5.5-5.7 para sistemas generativos) é o que transformaria pesquisa em sistemas implantáveis — o caminho de "matemático que faz ML" para "pesquisador que constrói sistemas de ML confiáveis".

---

## Referências

| # | Fonte | Tipo | Uso |
|---|-------|------|-----|
| 1 | Dreyfus & Dreyfus (1980). *Five-Stage Model of Skill Acquisition.* UC Berkeley. | **PEER-REVIEWED** | Escala de progressão |
| 2 | Smith & Kendall (1963). *Retranslation of Expectations.* JAP, 47(2). DOI: 10.1037/h0047060 | **PEER-REVIEWED** | Âncoras comportamentais (BARS) |
| 3 | Kruger & Dunning (1999). *Unskilled and Unaware of It.* JPSP, 77(6). | **PEER-REVIEWED** | Viés de auto-avaliação |
| 4 | Bishop, C. M. (2006). *Pattern Recognition and Machine Learning.* Springer. | **CLÁSSICO** | Camadas 1-2 (fundamentos, ML probabilístico) |
| 5 | Hastie, Tibshirani & Friedman (2009). *The Elements of Statistical Learning* (2nd ed.). Springer. | **CLÁSSICO** | Camadas 1-2 (ML com rigor estatístico) |
| 6 | Goodfellow, Bengio & Courville (2016). *Deep Learning.* MIT Press. | **CLÁSSICO** | Camada 3 (deep learning) |
| 7 | Deisenroth, Faisal & Ong (2020). *Mathematics for Machine Learning.* Cambridge. | **CLÁSSICO** | Camada 1 (fundamentos matemáticos) |
| 8 | Vaswani et al. (2017). *Attention Is All You Need.* NeurIPS. arXiv: 1706.03762 | **PEER-REVIEWED** | Camada 3.4 (Transformers) |
| 9 | Brown et al. (2020). *Language Models are Few-Shot Learners.* NeurIPS. arXiv: 2005.14165 | **PEER-REVIEWED** | Camada 5.1 (LLMs, in-context learning) |
| 10 | Lewis et al. (2020). *Retrieval-Augmented Generation.* NeurIPS. arXiv: 2005.11401 | **PEER-REVIEWED** | Camada 5.3 (RAG) |
| 11 | Hu et al. (2021). *LoRA: Low-Rank Adaptation of LLMs.* arXiv: 2106.09685 | **PEER-REVIEWED** | Camada 5.7 (fine-tuning eficiente) |
| 12 | Sculley et al. (2015). *Hidden Technical Debt in ML Systems.* NeurIPS. | **PEER-REVIEWED** | Camada 4 (MLOps, dívida técnica) |
| 13 | Breck et al. (2017). *The ML Test Score.* IEEE Big Data. DOI: 10.1109/BigData.2017.8258038 | **PEER-REVIEWED** | Camada 4.6 (testing de ML) |
| 14 | Huyen, C. (2022). *Designing Machine Learning Systems.* O'Reilly. | **INDUSTRIAL** | Camada 4 (engenharia de ML) |

---

*Parte 2 de 3 das especialidades. **Parte 2 (Desenvolvedor de IA) COMPLETA**: 5 camadas, 33 competências, todas com progressão Dreyfus 0-5.*
*Concluídas: Parte 1 (Engenharia de Software, 4 sub-áreas) e Parte 2 (Desenvolvedor de IA). Próxima: Parte 3 (Data Scientist), depois as sínteses (Partes 4-7).*
*Escala ancorada em Dreyfus (1980) + BARS (Smith & Kendall, 1963). Auto-avaliação deve ser complementada por validação externa de pares seniores (Kruger & Dunning, 1999).*
*Revisão recomendada a cada 6 meses, registrando a evolução de nível e a nova evidência concreta.*
