# Skill-Check de Engenharia de Software — Parte 1: Front-End
## Arquitetura Completa de Competências com Escala Dreyfus Ancorada

> *"The expert is no longer aware of features and rules; his understanding is tacit."*
> — Hubert & Stuart Dreyfus, *Mind Over Machine* (1986)

---

## Como Este Documento Funciona

Este é um mapa de competências para a sub-área **Front-End** da Engenharia de Software. Não é uma lista de tecnologias — é uma arquitetura de conhecimento organizada em 10 camadas que se empilham, do substrato da plataforma web até a entrega em produção.

Cada camada contém de 4 competências. Para cada competência, você encontra:

1. **Conceito + por que existe** — o que é e qual problema resolve
2. **Profundidade esperada** — Básico / Intermediário / Avançado
3. **Conexões** — com quais outras competências ela se comunica
4. **Erro de iniciante → Marca do sênior** — o contraste diagnóstico
5. **Progressão Dreyfus completa (0-5)** — o que cada nível significa especificamente para aquela competência, com o teste de validação (a evidência concreta que comprova o nível)

A última parte do documento traz uma **planilha de auto-auditoria** onde você registra seu nível em cada competência.

---

## A Escala: Fundamentação e Justificativa

A escala usada combina dois frameworks com pedigree acadêmico verificado.

### Framework 1 — Dreyfus Skill Acquisition Model

> **[PEER-REVIEWED]**
> Dreyfus, S. E., & Dreyfus, H. L. (1980). *A Five-Stage Model of the Mental Activities Involved in Directed Skill Acquisition.* Operations Research Center, University of California, Berkeley. ORC 80-2.
> URL: https://apps.dtic.mil/sti/tr/pdf/ADA084551.pdf
> — 1.433+ citações. Define a progressão Novice → Advanced Beginner → Competent → Proficient → Expert pela *natureza do processamento cognitivo*, não pelo volume de conhecimento.

### Framework 2 — Behaviorally Anchored Rating Scales (BARS)

> **[PEER-REVIEWED]**
> Smith, P. C., & Kendall, L. M. (1963). *Retranslation of Expectations: An Approach to the Construction of Unambiguous Anchors for Rating Scales.* Journal of Applied Psychology, 47(2), 149–155. DOI: 10.1037/h0047060
> — 854+ citações. Demonstrou que âncoras comportamentais concretas aumentam a confiabilidade entre avaliadores (inter-rater reliability) ao substituir categorias abstratas ("excelente", "bom") por descrições observáveis de comportamento.

### Por Que a Combinação Funciona

O problema da escala 0-5 numérica pura é que ela mede *confiança percebida* — exatamente o que o efeito Dunning-Kruger distorce:

> **[PEER-REVIEWED]**
> Kruger, J., & Dunning, D. (1999). *Unskilled and Unaware of It.* Journal of Personality and Social Psychology, 77(6), 1121–1134. DOI: 10.1037/0022-3514.77.6.1121
> — Performers no quartil inferior superestimaram dramaticamente suas habilidades (12º percentil real → 62º percentil autopercebido).

A solução BARS é forçar cada nível a ter uma **âncora comportamental + teste de validação**: você não responde "eu sei isto?" (subjetivo), você responde "eu consigo fazer *isto* especificamente, e tenho a evidência?" (verificável).

### Limites Honestos da Escala

- **BARS reduz, não elimina, o viés.** A literatura mostra que avaliações com BARS *às vezes* (não sempre) exibem menos viés de medição que escalas convencionais.
- **BARS foi validado para avaliação por terceiros**, não auto-avaliação. Por isso a recomendação permanece: pelo menos algumas competências devem ser validadas externamente por um par sênior.
- **O teste de validação é o que torna isto BARS de verdade.** Não marque nível 4 sem ter um artefato concreto (código, arquitetura, projeto real) que comprove.

### A Escala de 6 Níveis

| Nível | Dreyfus | Âncora Comportamental | Característica Cognitiva |
|-------|---------|----------------------|------------------------|
| **0** | Desconhecido | Não reconheço o conceito | Sem exposição |
| **1** | Novice | Explico o que é e quando se aplica, mas preciso de guia | Segue regras contexto-livre |
| **2** | Advanced Beginner | Uso com documentação aberta; funciona, mas não diagnostico falhas | Reconhece aspectos por experiência |
| **3** | Competent | Implemento sozinho sem consulta constante; depuro quando quebra | Planeja deliberadamente |
| **4** | Proficient | Projeto antecipando trade-offs e modos de falha | Percepção holística |
| **5** | Expert | Ensino, reconheço quando o padrão está errado, contribuo com o estado da arte | Intuição fluida |

---

## Visão Geral das 10 Camadas

```
TIER PRODUÇÃO (qualidade de produção)
  CAMADA 10 · Build, Tooling & Deploy
  CAMADA  9 · Qualidade & Testes
  CAMADA  8 · Segurança no Cliente
  CAMADA  7 · UX & Acessibilidade
  CAMADA  6 · Performance

TIER CONSTRUÇÃO (construção do app)
  CAMADA  5 · Comunicação Cliente-Servidor
  CAMADA  4 · Gerenciamento de Estado
  CAMADA  3 · Arquitetura de Componentes

TIER SUBSTRATO (fundação da plataforma)
  CAMADA  2 · Linguagem & Runtime (JS/TS)
  CAMADA  1 · Plataforma Web
```

A lógica do empilhamento: cada camada se apoia nas inferiores. Quem não domina o substrato (camadas 1-2) constrói sobre abstrações que não entende — e quando o framework "vaza", fica perdido. A régua de "especialista em Front-End" exige competência distribuída por todas as camadas, não profundidade em apenas uma.

**Referência canônica de toda a plataforma web:**
> **[INDUSTRIAL — Referência Definitiva]**
> MDN Web Docs (Mozilla Developer Network).
> URL: https://developer.mozilla.org/
> — A documentação de referência definitiva para HTML, CSS, JavaScript e APIs da plataforma web. Mantida pela Mozilla com revisão da comunidade e dos implementadores de browsers.

---

# CAMADA 1 — Plataforma Web

> *O substrato. Quem não domina isto constrói sobre abstrações que não entende.*

---

## 1.1 Modelo de Renderização do Browser (Critical Rendering Path)

**Conceito + por que existe:** A sequência pela qual o browser transforma HTML/CSS/JS em pixels — parse do HTML → DOM, parse do CSS → CSSOM, combinação → render tree → layout → paint → composite. Existe porque entender *onde* o tempo é gasto nessa pipeline separa "meu site está lento" de "sei exatamente qual etapa otimizar".

**Profundidade esperada:** Avançado · **Conexões:** → Performance (6.1), → DOM (1.4), → CSS (1.3)

**Erro de iniciante → Marca do sênior:** O iniciante trata o browser como caixa-preta que "renderiza HTML". O sênior sabe que layout e paint são etapas distintas, que `transform`/`opacity` pulam o layout (compositor-only), e usa isso para animações de 60fps.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei como o browser transforma código em pixels | — |
| **1** | Sei que existe um processo de renderização, mas não suas etapas | Explico que o browser "lê HTML e CSS e desenha" |
| **2** | Conheço DOM e CSSOM de nome; sigo dicas de performance sem entender o porquê | Apliquei `will-change` ou lazy loading seguindo um tutorial |
| **3** | Entendo as etapas (layout, paint, composite) e depuro com DevTools Performance | Usei o painel Performance para identificar um paint custoso |
| **4** | Projeto interações antecipando reflow/repaint; escolho propriedades CSS compositor-only deliberadamente | Otimizei uma animação para rodar fora da main thread e medi o ganho |
| **5** | Ensino o pipeline; reconheço layout thrashing por inspeção; conheço diferenças entre engines (Blink/WebKit/Gecko) | Resolvi um jank de produção sem profiler, só pela leitura do código |

---

## 1.2 HTML Semântico e Estrutura de Documento

**Conceito + por que existe:** Usar elementos HTML pelo seu *significado* (`<nav>`, `<article>`, `<button>`), não pela aparência. Existe porque o HTML é a camada de acessibilidade e SEO — leitores de tela, crawlers e tecnologias assistivas dependem da semântica, não do CSS.

**Profundidade esperada:** Intermediário · **Conexões:** → Acessibilidade (7.1), → SEO, → DOM (1.4)

**Erro de iniciante → Marca do sênior:** O iniciante usa `<div onclick>` para tudo. O sênior usa `<button>` porque já vem com foco de teclado, role ARIA e ativação por Enter/Space — e sabe que recriar isso com div exige 5+ atributos manuais.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é HTML semântico | — |
| **1** | Sei que existem tags além de `<div>`, mas uso `<div>` para quase tudo | Nomeio 3 tags semânticas |
| **2** | Uso tags semânticas quando lembro, sem método consistente | Estruturei uma página com `<header>`, `<main>`, `<footer>` |
| **3** | Estruturo documentos semanticamente por padrão; entendo landmarks | Construí um formulário com `<label>`, `<fieldset>` corretos |
| **4** | Projeto a estrutura do documento pensando em navegação por teclado e leitor de tela *antes* do CSS | Desenhei a hierarquia de headings (h1-h6) para navegação assistiva |
| **5** | Ensino semântica; conheço a árvore de acessibilidade gerada; reconheço quando ARIA é necessário vs quando HTML nativo basta | Auditei e corrigi a semântica de uma aplicação inteira |

---

## 1.3 CSS: Modelo de Caixa, Layout, Cascata e Especificidade

**Conceito + por que existe:** Como o CSS calcula tamanho (box model), posiciona elementos (flexbox, grid) e resolve conflitos entre regras (cascata + especificidade). Existe porque CSS é declarativo e seu modelo de resolução de conflitos é não-óbvio — a maioria dos "bugs de CSS" são especificidade mal compreendida.

**Profundidade esperada:** Avançado · **Conexões:** → Rendering (1.1), → Responsividade (7.2), → Performance (6.1)

**Erro de iniciante → Marca do sênior:** O iniciante combate especificidade com `!important` e acumula dívida. O sênior projeta uma arquitetura de CSS (BEM, CSS Modules, utility-first) onde a especificidade é plana e previsível por design.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei escrever CSS | — |
| **1** | Aplico estilos básicos copiando exemplos; não entendo por que alguns não funcionam | Mudei cor e tamanho de fonte de um elemento |
| **2** | Uso flexbox/grid seguindo guias; resolvo conflitos por tentativa e erro com `!important` | Centralizei elementos com flexbox |
| **3** | Entendo box model, cascata e especificidade; escolho flexbox vs grid pelo problema | Construí um layout responsivo de duas colunas sem hacks |
| **4** | Projeto arquitetura de CSS escalável; resolvo qualquer bug de `z-index` (stacking contexts) e `margin collapse` | Defini uma convenção de CSS (BEM/Modules) para um projeto |
| **5** | Ensino o modelo de cascata; conheço cálculo de especificidade de cor; otimizo CSS para performance de render | Refatorei um CSS legado caótico em sistema previsível |

---

## 1.4 DOM e Manipulação

**Conceito + por que existe:** O DOM é a representação em árvore do documento que o JavaScript manipula. Existe porque é a ponte entre conteúdo estático (HTML) e interatividade (JS) — e manipulá-lo é caro, com implicações de performance diretas.

**Profundidade esperada:** Intermediário · **Conexões:** → Frameworks (Camada 3), → Rendering (1.1), → Event loop (2.2)

**Erro de iniciante → Marca do sênior:** O iniciante manipula o DOM dentro de loops, causando múltiplos reflows. O sênior entende por que frameworks usam Virtual DOM ou compilação reativa — porque batch de mudanças é o gargalo que eles resolvem.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é o DOM | — |
| **1** | Sei que JS "mexe na página", mas não conheço a API | Explico que o DOM é a página vista pelo código |
| **2** | Uso `querySelector` e `addEventListener` seguindo exemplos | Adicionei um event listener a um botão |
| **3** | Manipulo o DOM com fluência; entendo event delegation e bubbling | Implementei delegação de eventos para lista dinâmica |
| **4** | Projeto manipulação eficiente (batch, DocumentFragment); sei quando o custo do DOM justifica memoização | Otimizei renderização de lista grande evitando reflows |
| **5** | Ensino o modelo; entendo profundamente o suficiente para saber *quando não precisa* de framework | Construí UI complexa em vanilla JS por decisão arquitetural justificada |

---

# CAMADA 2 — Linguagem & Runtime (JavaScript / TypeScript)

> *A linguagem que dá vida ao front. O modelo de execução assíncrona é onde a maioria dos bugs sutis nasce.*

---

## 2.1 JavaScript Core: Closures, Prototypes, `this`, Coerção

**Conceito + por que existe:** Os mecanismos fundamentais da linguagem — escopo léxico e closures, herança via protótipos, binding dinâmico de `this`, coerção de tipos. Existem porque JavaScript tem decisões de design idiossincráticas que, mal compreendidas, produzem bugs que "não fazem sentido".

**Profundidade esperada:** Avançado · **Conexões:** → Frameworks (Camada 3), → Estado (Camada 4), → TypeScript (2.3)

**Erro de iniciante → Marca do sênior:** O iniciante é surpreendido por `this` sendo `undefined` num callback. O sênior entende arrow functions (capturam `this` lexicamente) vs funções regulares, e nunca é pego de surpresa.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não programo em JavaScript | — |
| **1** | Escrevo funções básicas; não conheço closures nem protótipos | Declaro variáveis e funções simples |
| **2** | Uso a linguagem, mas sou surpreendido por `this`, hoisting e coerção | Já escrevi código que quebrou por `this` indefinido |
| **3** | Entendo closures, protótipos e `this`; depuro esses problemas sozinho | Expliquei por que um callback perdeu o contexto e corrigi |
| **4** | Uso closures deliberadamente (encapsulamento, memoização); domino a cadeia de protótipos | Implementei memoização ou módulo privado com closures |
| **5** | Ensino os mecanismos; conheço os casos extremos de coerção; entendo o spec (ECMAScript) | Resolvi um bug sutil que dependia de entender a spec de coerção |

---

## 2.2 Event Loop e Assincronia (Promises, async/await, microtasks)

**Conceito + por que existe:** O modelo de concorrência single-threaded do JavaScript — call stack, task queue, microtask queue, e como Promises e async/await são agendados. Existe porque JS é single-threaded mas precisa lidar com I/O assíncrono sem bloquear a UI.

**Profundidade esperada:** Avançado · **Conexões:** → Comunicação Cliente-Servidor (Camada 5), → Performance (Camada 6), → JS Core (2.1)

**Erro de iniciante → Marca do sênior:** O iniciante trata `async/await` como mágica e não entende por que um `await` num loop serializa requisições que poderiam ser paralelas. O sênior sabe quando usar `Promise.all` (paralelo), `Promise.allSettled` (paralelo tolerante a falhas), ou sequência deliberada.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é assincronia em JS | — |
| **1** | Sei que JS é single-threaded e que existe "algo" chamado event loop | Explico que JS faz uma coisa de cada vez |
| **2** | Uso async/await e Promises, mas não prevejo ordem de execução nem evito bloqueio | Já usei `.then()` ou `await` copiando exemplos |
| **3** | Uso `Promise.all` vs sequência conscientemente; depuro problemas de assincronia | Paralelizei requisições que estavam serializadas num loop |
| **4** | Projeto fluxos async evitando bloqueio de UI e race conditions; entendo macrotask vs microtask | Resolvi uma race condition de produção por design de fluxo |
| **5** | Prevejo a ordem exata de execução de código misto (setTimeout + Promise + síncrono); ensino o modelo | Expliquei corretamente a ordem de saída de um código adversarial |

> *Conexão com seu diagnóstico: esta competência é o análogo no front do GIL do Python (Eixo 1). O modelo mental de concorrência single-threaded transfere diretamente.*

---

## 2.3 TypeScript e Tipagem Estática

**Conceito + por que existe:** Um superset do JavaScript que adiciona tipos verificados em compilação. Existe porque JS não tem tipos, e em sistemas grandes a ausência de tipos transforma refatoração em adivinhação — TypeScript move classes de erro de runtime para build time.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → JS Core (2.1), → Análise estática, → Contratos de API (Camada 5)

**Erro de iniciante → Marca do sênior:** O iniciante usa `any` para silenciar o compilador. O sênior usa tipos como ferramenta de design — generics, utility types, discriminated unions — para tornar estados inválidos *impossíveis de representar*.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço TypeScript | — |
| **1** | Sei que adiciona tipos ao JS, mas não sei usá-los | Explico que TS "adiciona tipos" |
| **2** | Anoto tipos básicos; uso `any` quando o compilador reclama | Adicionei tipos a uma função simples |
| **3** | Tipo funções e objetos corretamente; uso interfaces e generics básicos | Tipei uma API com interfaces sem usar `any` |
| **4** | Modelo o domínio com tipos; uso generics, utility types e discriminated unions para impedir estados inválidos | Modelei estados de UI de forma que estado inválido não compila |
| **5** | Ensino design por tipos; conheço o sistema de tipos profundamente (conditional/mapped types); entendo a correspondência tipos-proposições | Construí tipos avançados que codificam invariantes de domínio |

> *Conexão com seu background: tipos são, formalmente, proposições (correspondência de Curry-Howard). Sua formação matemática dá acesso direto a este nível de raciocínio.*

---

## 2.4 Módulos e Sistema de Imports

**Conceito + por que existe:** Como o código é dividido em unidades reutilizáveis (ES Modules, tree-shaking, dynamic imports). Existe porque apps modernas têm milhares de arquivos, e como eles se conectam afeta o tamanho do bundle e a performance de carregamento.

**Profundidade esperada:** Intermediário · **Conexões:** → Build/Tooling (Camada 10), → Performance (6.2)

**Erro de iniciante → Marca do sênior:** O iniciante importa bibliotecas inteiras (`import _ from 'lodash'`) sem perceber o custo. O sênior entende tree-shaking e usa dynamic imports para code splitting.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que são módulos | — |
| **1** | Sei que existe `import`/`export`, mas não os detalhes | Importo uma função de outro arquivo |
| **2** | Uso imports/exports; não penso no impacto no bundle | Organizei código em múltiplos arquivos |
| **3** | Entendo named vs default exports, tree-shaking; importo seletivamente | Reduzi o bundle importando apenas o necessário de uma lib |
| **4** | Projeto a estrutura de módulos pensando em quais pedaços carregam juntos; uso dynamic imports estrategicamente | Implementei code splitting por rota com dynamic imports |
| **5** | Ensino arquitetura de módulos; entendo a diferença entre ESM/CJS e suas implicações de bundling | Diagnostiquei e resolvi problema de bundle por interop ESM/CJS |

---

# CAMADA 3 — Arquitetura de Componentes

> *Onde o front moderno realmente vive. A diferença entre componentes que escalam e componentes que viram espaguete.*

---

## 3.1 Modelo de Componentes e Composição

**Conceito + por que existe:** Construir UIs a partir de unidades isoladas e reutilizáveis que se compõem. Existe porque UIs complexas precisam ser decompostas em partes gerenciáveis — e a *forma* da decomposição determina se o código é manutenível.

**Profundidade esperada:** Avançado · **Conexões:** → Estado (Camada 4), → Arquitetura de sistemas (conceito geral)

**Erro de iniciante → Marca do sênior:** O iniciante cria componentes gigantes ou decompõe por aparência visual. O sênior decompõe por *responsabilidade* e *fronteira de mudança* — componentes que mudam juntos ficam juntos (princípio de coesão, análogo à decomposição arquitetural).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é um componente | — |
| **1** | Sei que UIs são feitas de componentes, mas não sei decompor | Explico que componente é "um pedaço reutilizável de UI" |
| **2** | Crio componentes, mas eles tendem a ser grandes e acoplados | Construí um componente que renderiza dados |
| **3** | Decomponho por responsabilidade; uso props e composição com children | Quebrei uma tela em componentes coesos e reutilizáveis |
| **4** | Projeto hierarquias com composição (render props, slots) vs configuração; separo apresentação de lógica | Desenhei uma biblioteca de componentes com API de composição |
| **5** | Ensino design de componentes; reconheço quando uma abstração está errada; defino padrões para o time | Estabeleci o design system / padrões de composição de um produto |

---

## 3.2 Ciclo de Vida e Renderização

**Conceito + por que existe:** Quando e por que um componente re-renderiza, e os pontos de intervenção (montagem, atualização, desmontagem). Existe porque re-renders desnecessários são a causa mais comum de problemas de performance em apps de componentes.

**Profundidade esperada:** Avançado · **Conexões:** → Performance (6.3), → Reatividade (3.3), → Estado (Camada 4)

**Erro de iniciante → Marca do sênior:** O iniciante não entende por que seu componente re-renderiza e adiciona otimizações aleatórias. O sênior sabe exatamente o que dispara um re-render e otimiza cirurgicamente.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é ciclo de vida de componente | — |
| **1** | Sei que componentes "atualizam", mas não quando nem por quê | Explico que a UI muda quando os dados mudam |
| **2** | Uso hooks de efeito copiando padrões; sofro com loops e efeitos errados | Já tive um `useEffect` em loop infinito |
| **3** | Entendo o que dispara re-render (estado/props/pai); gerencio efeitos corretamente | Corrigi um array de dependências de efeito problemático |
| **4** | Prevejo a cascata de re-renders; coloco fronteiras de memoização no lugar certo | Otimizei re-renders de uma árvore com memoização cirúrgica |
| **5** | Ensino o modelo de renderização; reconheço anti-padrões de efeito; entendo o reconciliador | Diagnostiquei problema de performance de render sem profiler |

---

## 3.3 Reatividade e Fluxo de Dados Unidirecional

**Conceito + por que existe:** O princípio de que dados fluem em uma direção (estado → UI) e mudanças de UI disparam atualizações de estado de forma controlada. Existe porque o fluxo bidirecional descontrolado torna o comportamento do sistema impossível de raciocinar.

**Profundidade esperada:** Avançado · **Conexões:** → Estado (Camada 4), → Modelo de componentes (3.1)

**Erro de iniciante → Marca do sênior:** O iniciante luta contra o fluxo unidirecional tentando mutar props ou sincronizar estados duplicados. O sênior abraça o fluxo unidirecional e mantém uma única fonte de verdade.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço o conceito de fluxo de dados | — |
| **1** | Sei que "dados descem, eventos sobem" de ouvir falar | Repito o princípio sem aplicá-lo |
| **2** | Sigo o padrão quando o framework força, mas duplico estado | Já tive estados duplicados que dessincronizaram |
| **3** | Mantenho single source of truth; entendo por que mutar props é errado | Refatorei estado duplicado para uma única fonte |
| **4** | Reconheço quando um bug de estado é problema de *topologia de fluxo* — estado no lugar errado da árvore — e resolvo movendo o estado | Resolvi um bug "subindo" o estado ao ancestral comum correto |
| **5** | Ensino fluxo unidirecional; projeto a topologia de dados de aplicações inteiras | Defini a arquitetura de fluxo de dados de um produto complexo |

> *Conexão direta com o argumento topológico: estado no lugar errado da árvore é um problema topológico, não de sincronização. A solução é mover o estado, não adicionar sincronização.*

---

## 3.4 Lógica Reutilizável (Hooks / Composables)

**Conceito + por que existe:** Mecanismos para extrair e reutilizar lógica com estado entre componentes (React Hooks, Vue Composables). Existem porque lógica de UI (fetch, subscrição, formulários) se repete, e duplicá-la é dívida técnica.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Modelo de componentes (3.1), → Estado (Camada 4)

**Erro de iniciante → Marca do sênior:** O iniciante copia-cola lógica entre componentes ou cria hooks com dependências mal gerenciadas. O sênior extrai abstrações no nível certo e entende as regras que governam hooks.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que são hooks/composables | — |
| **1** | Sei que existem hooks, mas só uso os built-in básicos | Usei `useState` seguindo um tutorial |
| **2** | Uso hooks built-in; não extraio lógica customizada | Usei `useState` e `useEffect` num componente |
| **3** | Crio hooks customizados para reutilizar lógica; entendo as regras dos hooks | Extraí lógica de fetch para um hook reutilizável |
| **4** | Projeto hooks com API limpa que encapsula complexidade; sei quando *não* abstrair | Desenhei um hook que encapsula lógica complexa de forma elegante |
| **5** | Ensino design de hooks; reconheço abstração prematura; defino padrões de composição de lógica | Estabeleci a biblioteca de hooks compartilhados de um time |

---

# CAMADA 4 — Gerenciamento de Estado

> *O sistema nervoso do app. Onde mora a complexidade de aplicações reais.*

---

## 4.1 Estado Local vs Global

**Conceito + por que existe:** A decisão de onde cada pedaço de estado deve viver — local ao componente, elevado a um ancestral, ou global à aplicação. Existe porque colocar estado no lugar errado é a origem de bugs de sincronização e re-renders desnecessários.

**Profundidade esperada:** Avançado · **Conexões:** → Reatividade (3.3), → Ciclo de vida (3.2)

**Erro de iniciante → Marca do sênior:** O iniciante coloca tudo em estado global "por garantia" ou duplica estado local. O sênior segue o princípio de colocar o estado no nível mais baixo possível que ainda serve a todos que precisam dele.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei a diferença entre estado local e global | — |
| **1** | Sei que existe estado, mas não onde colocá-lo | Explico que "estado é dado que muda" |
| **2** | Uso estado local; recorro a global sem critério claro | Já coloquei tudo em estado global por conveniência |
| **3** | Decido local vs global por necessidade real de compartilhamento | Elevei estado ao ancestral comum quando dois componentes precisaram dele |
| **4** | Projeto a topologia de estado da aplicação; minimizo escopo de cada pedaço | Desenhei a estratégia de estado de uma feature complexa |
| **5** | Ensino colocação de estado; reconheço quando estado mal colocado é a raiz de um bug | Refatorei a arquitetura de estado de uma aplicação inteira |

---

## 4.2 Padrões de Gerenciamento de Estado (Flux, atomic, signals)

**Conceito + por que existe:** Os modelos arquiteturais para gerenciar estado complexo — Flux/Redux (store centralizado + ações), atomic (Recoil/Jotai), signals (reatividade fina). Existem porque diferentes aplicações têm diferentes perfis de complexidade de estado, e cada padrão tem trade-offs distintos.

**Profundidade esperada:** Avançado · **Conexões:** → Reatividade (3.3), → Estado local/global (4.1)

**Erro de iniciante → Marca do sênior:** O iniciante adota Redux para tudo (overkill) ou evita qualquer padrão (caos). O sênior escolhe o padrão pelo perfil de complexidade real do app, e sabe quando estado local basta.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço padrões de gerenciamento de estado | — |
| **1** | Ouvi falar de Redux/Context, mas não sei como funcionam | Nomeio uma biblioteca de estado |
| **2** | Uso uma biblioteca de estado seguindo boilerplate | Implementei um store seguindo a documentação |
| **3** | Implemento gerenciamento de estado corretamente; entendo o fluxo de ações/reducers | Construí uma feature com store centralizado funcionando |
| **4** | Escolho o padrão pelo trade-off (centralizado vs atomic vs signals); justifico a decisão | Escolhi e justifiquei o padrão de estado para um projeto |
| **5** | Ensino os trade-offs entre padrões; reconheço quando um padrão foi mal aplicado; conheço a teoria (Flux, CQRS) | Migrei um app de um padrão de estado para outro com ganho mensurável |

---

## 4.3 Estado de Servidor vs Estado de Cliente

**Conceito + por que existe:** A distinção entre estado que pertence ao servidor (dados remotos, cacheados localmente) e estado puramente do cliente (UI, formulários). Existe porque tratá-los igual é um erro categórico — estado de servidor precisa de cache, invalidação, refetch e sincronização que estado de cliente não precisa.

**Profundidade esperada:** Avançado · **Conexões:** → Comunicação Cliente-Servidor (Camada 5), → Cache (4.4)

**Erro de iniciante → Marca do sênior:** O iniciante coloca dados de servidor no mesmo store global do estado de UI e reinventa cache manualmente. O sênior usa ferramentas de server-state (React Query, SWR) que resolvem cache/invalidação/refetch, e separa as duas categorias.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei que há distinção entre os dois tipos de estado | — |
| **1** | Trato todo dado como igual, sem distinção | Coloco dados de API no mesmo lugar que estado de UI |
| **2** | Faço fetch e guardo em estado, gerenciando loading manualmente | Já gerenciei loading/error manualmente para cada requisição |
| **3** | Uso ferramentas de server-state (React Query/SWR); entendo cache básico | Implementei fetch com cache usando React Query |
| **4** | Projeto a estratégia de cache/invalidação; separo claramente server-state de client-state | Desenhei a estratégia de sincronização de dados de uma feature |
| **5** | Ensino a distinção; reconheço quando estado de servidor foi mal gerenciado; otimizo estratégias de cache | Estabeleci a arquitetura de dados remota de um produto |

---

## 4.4 Sincronização, Cache e Invalidação

**Conceito + por que existe:** As estratégias para manter dados locais consistentes com a fonte remota — quando refazer fetch, quando invalidar cache, como lidar com updates otimistas. Existe porque "there are only two hard things in CS: cache invalidation and naming things" — manter cache consistente é genuinamente difícil.

**Profundidade esperada:** Avançado · **Conexões:** → Estado de servidor (4.3), → Comunicação (Camada 5)

**Erro de iniciante → Marca do sênior:** O iniciante nunca invalida cache (dados ficam stale) ou invalida tudo sempre (perde o benefício do cache). O sênior projeta estratégias de invalidação granulares e usa updates otimistas com rollback.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é invalidação de cache | — |
| **1** | Sei que cache "guarda dados", mas não como gerenciar | Explico o que é cache de forma geral |
| **2** | Uso cache da ferramenta sem entender invalidação; dados às vezes ficam stale | Já tive dados desatualizados na tela |
| **3** | Invalido cache após mutations; entendo staleness e refetch | Implementei invalidação após uma mutation |
| **4** | Projeto estratégias de invalidação granulares; uso updates otimistas com rollback | Desenhei optimistic updates com tratamento de falha |
| **5** | Ensino estratégias de cache; reconheço bugs de consistência; conheço a teoria de cache distribuído | Resolvi um problema complexo de consistência de cache em produção |

---

# CAMADA 5 — Comunicação Cliente-Servidor

> *A fronteira entre o front e o resto do mundo. Onde o sistema encontra a rede — e suas falhas.*

---

## 5.1 HTTP e o Protocolo da Web

**Conceito + por que existe:** O protocolo que governa toda comunicação na web — métodos, status codes, headers, cookies, cache, CORS. Existe porque toda interação cliente-servidor passa por HTTP, e não entendê-lo torna a depuração de problemas de rede uma adivinhação.

**Profundidade esperada:** Avançado · **Conexões:** → REST/GraphQL (5.2), → Segurança (Camada 8), → Performance (Camada 6)

**Erro de iniciante → Marca do sênior:** O iniciante não entende por que uma requisição falha com CORS e tenta "consertar" no front. O sênior entende que CORS é uma política do browser aplicada via headers do servidor, e sabe exatamente onde está o problema.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é HTTP | — |
| **1** | Sei que HTTP "busca dados do servidor", sem detalhes | Explico que o navegador "pede dados" |
| **2** | Faço requisições; reconheço status 200/404/500 mas não os nuances | Já fiz um fetch e li o status code |
| **3** | Entendo métodos, status codes, headers; depuro requisições no Network tab | Diagnostiquei um erro de API pelo status e headers |
| **4** | Domino CORS, cache HTTP, cookies, auth headers; projeto a camada de comunicação | Resolvi um problema de CORS entendendo a origem real |
| **5** | Ensino o protocolo; conheço HTTP/2, HTTP/3, e suas implicações de performance | Otimizei carregamento explorando características do protocolo |

---

## 5.2 REST, GraphQL e Estilos de API

**Conceito + por que existe:** Os estilos arquiteturais de API — REST (recursos + verbos HTTP), GraphQL (query declarativa), RPC. Existem porque diferentes necessidades de dados têm diferentes perfis ótimos: REST é simples e cacheável; GraphQL resolve over/under-fetching; cada um tem trade-offs.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → HTTP (5.1), → Data fetching (5.3), → TypeScript (2.3)

**Erro de iniciante → Marca do sênior:** O iniciante trata toda API como "endpoints que retornam JSON" sem entender o estilo. O sênior reconhece o estilo, suas garantias (idempotência em REST) e seus trade-offs (complexidade do GraphQL vs flexibilidade).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço estilos de API | — |
| **1** | Sei que APIs "retornam dados", sem distinguir estilos | Nomeio REST ou GraphQL |
| **2** | Consumo APIs REST seguindo a documentação | Consumi um endpoint REST com fetch |
| **3** | Entendo REST (recursos, verbos, idempotência) e consumo GraphQL | Consumi uma API GraphQL com queries |
| **4** | Escolho o estilo pelo trade-off; projeto contratos de API com o backend | Defini o contrato de uma API com a equipe de backend |
| **5** | Ensino design de API; reconheço APIs mal projetadas; conheço REST maturity (Richardson), federação GraphQL | Projetei a estratégia de API de um produto |

---

## 5.3 Data Fetching e Mutations

**Conceito + por que existe:** Os padrões para buscar e modificar dados remotos — quando buscar, como lidar com waterfalls, prefetching, paginação, mutations. Existe porque a forma como você orquestra requisições determina a performance percebida e a complexidade do código.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Estado de servidor (4.3), → Event loop (2.2), → Performance (Camada 6)

**Erro de iniciante → Marca do sênior:** O iniciante cria request waterfalls (requisições sequenciais que poderiam ser paralelas) sem perceber. O sênior identifica waterfalls, paraleliza o que pode, e usa prefetching para antecipar necessidades.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei buscar dados de uma API | — |
| **1** | Sei que dados vêm de requisições, sem saber orquestrar | Explico que o app "busca dados do servidor" |
| **2** | Faço fetch básico; crio waterfalls sem perceber | Já busquei dados em sequência que poderiam ser paralelos |
| **3** | Orquestro fetch corretamente; implemento paginação e mutations | Implementei paginação e mutations funcionais |
| **4** | Identifico e elimino waterfalls; uso prefetching; projeto a estratégia de carregamento | Otimizei o carregamento de uma tela eliminando waterfalls |
| **5** | Ensino padrões de fetching; reconheço anti-padrões; domino streaming/suspense | Desenhei a arquitetura de data fetching de um produto |

---

## 5.4 Tratamento de Erros e Estados de Carregamento

**Conceito + por que existe:** As estratégias para lidar com os estados não-felizes da comunicação — loading, erro, vazio, retry, timeout. Existe porque o "happy path" é a parte fácil; a robustez de uma aplicação está em como ela se comporta quando a rede falha.

**Profundidade esperada:** Avançado · **Conexões:** → Raciocínio sobre falhas (Eixo 4 do diagnóstico), → UX (Camada 7)

**Erro de iniciante → Marca do sênior:** O iniciante só implementa o caminho de sucesso e o app quebra ou trava quando a rede falha. O sênior trata loading, erro, vazio e retry como estados de primeira classe, com feedback claro ao usuário.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não penso em estados de erro | — |
| **1** | Sei que requisições podem falhar, mas não trato | Explico que "às vezes dá erro" |
| **2** | Trato erro com um alert genérico; loading inconsistente | Adicionei um spinner de loading |
| **3** | Trato loading/erro/vazio consistentemente; implemento retry | Construí estados de loading, erro e vazio para uma tela |
| **4** | Projeto a estratégia de resiliência (timeout, retry com backoff, error boundaries); antecipo modos de falha | Desenhei o tratamento de falhas de rede de uma feature crítica |
| **5** | Ensino design de resiliência no cliente; reconheço happy-path thinking; defino padrões de erro do time | Estabeleci a estratégia de tratamento de erros de um produto |

> *Conexão direta com o Eixo 4 do seu diagnóstico (raciocínio sobre falhas). Esta competência é a manifestação no front do "pensar em falha primeiro".*

---

# CAMADA 6 — Performance

> *A diferença entre um app que parece rápido e um que frustra. Frequentemente invisível até medir.*

---

## 6.1 Critical Rendering Path e Otimização de Carregamento

**Conceito + por que existe:** As técnicas para acelerar o carregamento inicial — minimizar recursos bloqueantes, otimizar a ordem de carga, reduzir o tempo até o conteúdo aparecer. Existe porque o carregamento inicial é a primeira impressão, e usuários abandonam páginas lentas.

**Profundidade esperada:** Avançado · **Conexões:** → Rendering (1.1), → Módulos (2.4), → Web Vitals (6.4)

**Erro de iniciante → Marca do sênior:** O iniciante carrega tudo de uma vez e não percebe recursos bloqueantes. O sênior entende o critical rendering path, defere o não-essencial, e prioriza o conteúdo above-the-fold.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não penso em performance de carregamento | — |
| **1** | Sei que sites podem ser lentos, mas não por quê | Explico que "carregar muita coisa deixa lento" |
| **2** | Aplico dicas (minificar, comprimir) seguindo recomendações | Habilitei minificação seguindo um guia |
| **3** | Identifico recursos bloqueantes; defiro/async scripts; otimizo carregamento crítico | Otimizei o carregamento removendo bloqueios de render |
| **4** | Projeto a estratégia de carregamento (critical CSS, preload, resource hints); priorizo o caminho crítico | Desenhei a estratégia de loading de uma aplicação |
| **5** | Ensino otimização de CRP; reconheço gargalos por inspeção; conheço técnicas avançadas (streaming SSR) | Reduzi drasticamente o tempo de carregamento de um produto em produção |

---

## 6.2 Code Splitting e Lazy Loading

**Conceito + por que existe:** Dividir o código em pedaços carregados sob demanda, em vez de um bundle monolítico. Existe porque carregar todo o JavaScript da aplicação no início é desperdício — o usuário só precisa do código da tela atual.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Módulos (2.4), → Build (Camada 10), → CRP (6.1)

**Erro de iniciante → Marca do sênior:** O iniciante entrega um bundle único gigante. O sênior divide por rota e por componente pesado, carregando sob demanda — e sabe medir o impacto no bundle.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é code splitting | — |
| **1** | Sei que existe, mas não como aplicar | Explico que "carrega só o necessário" |
| **2** | Sei que o bundler faz splitting, sem controlá-lo | Sei que existe um bundle gerado |
| **3** | Implemento lazy loading por rota; uso dynamic imports | Implementei lazy loading de rotas |
| **4** | Projeto a estratégia de splitting (por rota, por componente pesado); meço o impacto no bundle | Reduzi o bundle inicial com splitting estratégico medido |
| **5** | Ensino estratégias de splitting; reconheço oportunidades por análise de bundle; otimizo chunks | Desenhei a estratégia de carregamento de código de um produto |

---

## 6.3 Otimização de Re-render e Memoização

**Conceito + por que existe:** As técnicas para evitar trabalho de renderização desnecessário — memoização de componentes, valores e callbacks. Existe porque re-renders desnecessários são a causa mais comum de UIs lentas em apps de componentes.

**Profundidade esperada:** Avançado · **Conexões:** → Ciclo de vida (3.2), → Reatividade (3.3)

**Erro de iniciante → Marca do sênior:** O iniciante memoiza tudo "por garantia" (o que pode piorar a performance) ou não memoiza nada. O sênior identifica os re-renders custosos reais e memoiza cirurgicamente, medindo antes e depois.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é memoização | — |
| **1** | Ouvi falar de `memo`/`useMemo`, sem saber quando usar | Nomeio uma API de memoização |
| **2** | Aplico memoização copiando padrões, sem medir | Adicionei `useMemo` seguindo um exemplo |
| **3** | Memoizo quando identifico re-render custoso; entendo igualdade referencial | Corrigi um re-render custoso com memoização |
| **4** | Identifico os gargalos reais com profiler; memoizo cirurgicamente; meço o ganho | Otimizei uma árvore de componentes com profiling antes/depois |
| **5** | Ensino quando memoizar (e quando não); reconheço memoização contraproducente; entendo o custo da própria memoização | Estabeleci diretrizes de otimização de render para um time |

---

## 6.4 Core Web Vitals e Medição

**Conceito + por que existe:** As métricas padronizadas de experiência do usuário — LCP (carregamento), INP (interatividade), CLS (estabilidade visual) — e as ferramentas para medi-las. Existe porque "rápido" é subjetivo até ser medido, e o Google usa essas métricas como fator de ranking.

> **[INDUSTRIAL]**
> Google. *Web Vitals.* web.dev.
> URL: https://web.dev/articles/vitals
> — Define os Core Web Vitals (LCP, INP, CLS) como o padrão da indústria para medir experiência de carregamento, interatividade e estabilidade visual.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → CRP (6.1), → todas as competências de performance

**Erro de iniciante → Marca do sênior:** O iniciante otimiza por intuição sem medir. O sênior mede com dados reais (field data, não só lab), prioriza pela métrica que mais impacta o usuário, e valida cada otimização.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço métricas de performance | — |
| **1** | Ouvi falar de Core Web Vitals, sem saber o que medem | Nomeio uma métrica (ex: LCP) |
| **2** | Rodo Lighthouse e leio a nota, sem agir sistematicamente | Gerei um relatório Lighthouse |
| **3** | Entendo LCP/INP/CLS; uso DevTools e Lighthouse para diagnosticar | Diagnostiquei um problema de CLS e corrigi |
| **4** | Meço com field data; priorizo otimizações pela métrica de maior impacto; valido cada mudança | Estabeleci medição contínua e melhorei uma métrica com dados |
| **5** | Ensino medição de performance; reconheço a diferença lab vs field; defino orçamentos de performance | Implementei performance budgets e monitoramento de um produto |

---

# CAMADA 7 — UX & Acessibilidade

> *A diferença entre um app que funciona para alguns e um que funciona para todos.*

---

## 7.1 Acessibilidade (ARIA, WCAG, navegação por teclado)

**Conceito + por que existe:** Tornar a aplicação utilizável por pessoas com deficiências — leitores de tela, navegação por teclado, contraste, ARIA. Existe porque a web é para todos, é frequentemente uma exigência legal, e acessibilidade melhora a usabilidade para todos os usuários.

> **[PADRÃO-W3C]**
> W3C Web Accessibility Initiative. *Web Content Accessibility Guidelines (WCAG) 2.2.* W3C Recommendation, 5 de outubro de 2023.
> URL: https://www.w3.org/TR/WCAG22/
> — O padrão internacional de acessibilidade. Organizado em 4 princípios (Perceivable, Operable, Understandable, Robust — POUR), 13 diretrizes e critérios de sucesso em três níveis de conformidade: A (mínimo), AA (padrão da indústria e referência da maioria das leis), AAA (mais rigoroso). A maioria das legislações de acessibilidade referencia o nível AA.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → HTML semântico (1.2), → UX (7.3)

**Erro de iniciante → Marca do sênior:** O iniciante ignora acessibilidade ou joga atributos ARIA aleatoriamente (frequentemente piorando). O sênior usa HTML semântico nativo primeiro, ARIA apenas quando necessário, e testa com leitor de tela e navegação por teclado.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é acessibilidade web | — |
| **1** | Sei que existe, mas não como implementar | Explico que "sites devem funcionar para pessoas com deficiência" |
| **2** | Adiciono `alt` em imagens; conheço acessibilidade superficialmente | Adicionei texto alternativo a imagens |
| **3** | Implemento navegação por teclado, contraste e ARIA básico corretamente | Tornei um componente navegável por teclado |
| **4** | Projeto para acessibilidade desde o início; testo com leitor de tela; viso WCAG AA | Auditei e adequei uma feature ao WCAG AA |
| **5** | Ensino acessibilidade; reconheço ARIA mal usado; conheço a árvore de acessibilidade e tecnologias assistivas | Estabeleci a estratégia de acessibilidade de um produto |

---

## 7.2 Responsividade e Design Adaptativo

**Conceito + por que existe:** Fazer a interface funcionar em qualquer tamanho de tela — de celulares a monitores grandes. Existe porque os usuários acessam de dispositivos com viewports radicalmente diferentes, e um layout fixo quebra na maioria deles.

**Profundidade esperada:** Intermediário · **Conexões:** → CSS (1.3), → Performance (Camada 6), → UX (7.3)

**Erro de iniciante → Marca do sênior:** O iniciante desenha para uma tela e adiciona breakpoints como remendo. O sênior pensa mobile-first, usa unidades fluidas e layouts intrinsecamente responsivos (grid, flexbox), e testa em dispositivos reais.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é design responsivo | — |
| **1** | Sei que sites devem funcionar no celular, sem saber como | Explico que "tem que funcionar no mobile" |
| **2** | Adiciono media queries seguindo exemplos | Adicionei um breakpoint para mobile |
| **3** | Construo layouts responsivos com flexbox/grid e media queries | Construí uma página que funciona de mobile a desktop |
| **4** | Projeto mobile-first com unidades fluidas; uso container queries; testo em dispositivos reais | Desenhei um sistema de layout responsivo para uma aplicação |
| **5** | Ensino design responsivo; reconheço anti-padrões; domino técnicas modernas (container queries, fluid type) | Estabeleci a estratégia responsiva de um design system |

---

## 7.3 Padrões de Interação e Feedback

**Conceito + por que existe:** Os padrões que tornam a interface compreensível e agradável — feedback de ações, estados de transição, affordances, prevenção de erros. Existe porque uma interface que não comunica o que está acontecendo confunde e frustra o usuário.

**Profundidade esperada:** Intermediário · **Conexões:** → Tratamento de erros (5.4), → Acessibilidade (7.1)

**Erro de iniciante → Marca do sênior:** O iniciante constrói interfaces que não dão feedback (o usuário não sabe se o clique funcionou). O sênior projeta feedback claro para cada ação, estados de transição suaves, e previne erros antes que aconteçam.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não penso em padrões de interação | — |
| **1** | Sei que UX importa, sem saber aplicar | Explico que "a interface deve ser fácil de usar" |
| **2** | Adiciono feedback básico (hover, loading) quando lembro | Adicionei estado de hover a um botão |
| **3** | Implemento feedback consistente para ações; estados de transição claros | Construí feedback de sucesso/erro para um formulário |
| **4** | Projeto a experiência de interação completa; previno erros; antecipo confusão do usuário | Desenhei o fluxo de interação de uma feature complexa |
| **5** | Ensino padrões de interação; reconheço fricção de UX; conheço heurísticas (Nielsen) e psicologia de UX | Estabeleci os padrões de interação de um produto |

---

## 7.4 Internacionalização (i18n) e Localização

**Conceito + por que existe:** Preparar a aplicação para múltiplos idiomas, formatos de data/número, e direções de texto (RTL). Existe porque produtos globais precisam servir usuários de diferentes locales, e retrofitar i18n depois é muito mais caro do que projetar desde o início.

**Profundidade esperada:** Básico-Intermediário · **Conexões:** → Acessibilidade (7.1), → Arquitetura de componentes (Camada 3)

**Erro de iniciante → Marca do sênior:** O iniciante hardcoda strings e formatos no código. O sênior externaliza strings, usa APIs de formatação locale-aware (Intl), e projeta o layout para acomodar idiomas com comprimentos e direções diferentes.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é i18n | — |
| **1** | Sei que apps podem ter vários idiomas, sem saber como | Explico que "o app pode estar em vários idiomas" |
| **2** | Sei que existem bibliotecas de i18n, sem usá-las estruturadamente | Nomeio uma biblioteca de i18n |
| **3** | Externalizo strings; uso uma biblioteca de i18n; formato datas/números com Intl | Implementei troca de idioma numa aplicação |
| **4** | Projeto a arquitetura de i18n desde o início; lido com pluralização, RTL e layout adaptativo | Desenhei a estratégia de internacionalização de um produto |
| **5** | Ensino i18n; reconheço problemas de localização; conheço as nuances culturais e técnicas (CLDR, ICU) | Estabeleci a infraestrutura de localização de um produto global |

---

# CAMADA 8 — Segurança no Cliente

> *A fronteira de confiança. Onde o código encontra inputs hostis e dados sensíveis.*

**Referência base de toda esta camada:**
> **[INDUSTRIAL-OWASP]**
> OWASP Foundation. *OWASP Top Ten 2021.*
> URL: https://owasp.org/Top10/
> — O documento de conscientização de segurança de aplicações mais adotado globalmente, baseado em dados de 500.000+ aplicações.

---

## 8.1 XSS e Sanitização

**Conceito + por que existe:** Cross-Site Scripting (XSS) é a injeção de scripts maliciosos via input não sanitizado. Sanitização é a defesa. Existe porque renderizar input do usuário sem tratamento permite que um atacante execute código arbitrário no browser de outras vítimas.

**Profundidade esperada:** Avançado · **Conexões:** → DOM (1.4), → Validação de input (segurança geral)

**Erro de iniciante → Marca do sênior:** O iniciante insere HTML do usuário diretamente (`innerHTML`/`dangerouslySetInnerHTML`) sem sanitizar. O sênior nunca confia em input, usa as proteções nativas do framework, e sanitiza com bibliotecas confiáveis (DOMPurify) quando precisa renderizar HTML.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é XSS | — |
| **1** | Ouvi falar de XSS, sem entender o mecanismo | Explico que "scripts maliciosos são um risco" |
| **2** | Sei que não devo confiar em input, sem saber as defesas | Evito `innerHTML` por recomendação |
| **3** | Entendo o vetor XSS; uso as proteções do framework; sanitizo HTML | Sanitizei input antes de renderizar com DOMPurify |
| **4** | Projeto defesa em profundidade contra XSS; reconheço vetores sutis (DOM-based, stored, reflected) | Auditei uma feature contra os três tipos de XSS |
| **5** | Ensino prevenção de XSS; reconheço bypasses de sanitização; conheço a superfície de ataque completa | Estabeleci as defesas contra injeção de um produto |

---

## 8.2 Content Security Policy (CSP)

**Conceito + por que existe:** Um header HTTP que instrui o browser sobre quais fontes de conteúdo são confiáveis, mitigando XSS e injeção. Existe porque é uma camada de defesa em profundidade — mesmo que um XSS passe pela sanitização, a CSP pode impedir sua execução.

**Profundidade esperada:** Intermediário · **Conexões:** → XSS (8.1), → HTTP (5.1), → defesa em profundidade

**Erro de iniciante → Marca do sênior:** O iniciante nunca configurou CSP ou usa uma política tão permissiva que não protege (`unsafe-inline`). O sênior projeta uma CSP restritiva com nonces/hashes, e a trata como camada complementar à sanitização.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é CSP | — |
| **1** | Ouvi falar de CSP, sem saber o que faz | Explico que "controla o que pode carregar" |
| **2** | Sei que CSP existe, sem configurá-la | Reconheço o header CSP |
| **3** | Configuro uma CSP básica; entendo as diretivas principais | Implementei uma CSP funcional |
| **4** | Projeto CSP restritiva com nonces/hashes; trato como defesa em profundidade | Desenhei a CSP de uma aplicação evitando `unsafe-inline` |
| **5** | Ensino CSP; reconheço políticas fracas; conheço bypasses e CSP Level 3 | Estabeleci a política de segurança de conteúdo de um produto |

---

## 8.3 CSRF e Proteção de Requisições

**Conceito + por que existe:** Cross-Site Request Forgery (CSRF) explora a sessão autenticada do usuário para fazer requisições não-intencionais. As defesas incluem tokens CSRF e SameSite cookies. Existe porque, sem proteção, um site malicioso pode disparar ações em nome do usuário autenticado em outro site.

**Profundidade esperada:** Intermediário · **Conexões:** → HTTP/cookies (5.1), → Autenticação (8.4)

**Erro de iniciante → Marca do sênior:** O iniciante não sabe o que é CSRF e não implementa proteção. O sênior entende o vetor, usa SameSite cookies e tokens CSRF, e sabe quando cada defesa se aplica.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é CSRF | — |
| **1** | Ouvi falar de CSRF, sem entender o mecanismo | Explico que "é um tipo de ataque" |
| **2** | Sei que existe proteção CSRF, sem saber implementar | Reconheço um token CSRF |
| **3** | Entendo o vetor; uso SameSite cookies e tokens CSRF | Implementei proteção CSRF numa aplicação |
| **4** | Projeto a estratégia de proteção; entendo a interação com CORS e autenticação | Desenhei a defesa CSRF de uma feature com cookies de sessão |
| **5** | Ensino prevenção de CSRF; reconheço configurações vulneráveis; conheço os trade-offs de cada defesa | Estabeleci a estratégia de proteção de requisições de um produto |

---

## 8.4 Gestão de Tokens e Autenticação no Cliente

**Conceito + por que existe:** Como armazenar e usar credenciais de autenticação no cliente de forma segura — onde guardar tokens (cookies httpOnly vs localStorage), como renová-los, como protegê-los. Existe porque tokens mal armazenados são um vetor direto de comprometimento de conta.

**Profundidade esperada:** Avançado · **Conexões:** → XSS (8.1), → CSRF (8.3), → HTTP (5.1)

**Erro de iniciante → Marca do sênior:** O iniciante guarda tokens em localStorage (acessível por XSS) sem pensar nas implicações. O sênior entende os trade-offs (httpOnly cookie protege de XSS mas exige proteção CSRF; localStorage é vulnerável a XSS), e escolhe conscientemente.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei como autenticação funciona no cliente | — |
| **1** | Sei que existe "login com token", sem detalhes | Explico que "o app guarda um token de login" |
| **2** | Guardo tokens onde for mais fácil (localStorage), sem pensar em segurança | Já guardei um token em localStorage |
| **3** | Entendo as opções de armazenamento; uso cookies httpOnly quando apropriado | Implementei autenticação com cookies httpOnly |
| **4** | Projeto o fluxo de autenticação considerando trade-offs (XSS vs CSRF); implemento refresh seguro | Desenhei o fluxo de auth de uma aplicação com refresh tokens |
| **5** | Ensino segurança de autenticação no cliente; reconheço armazenamento inseguro; conheço OAuth/OIDC a fundo | Estabeleci a arquitetura de autenticação de um produto |

---

# CAMADA 9 — Qualidade & Testes

> *A rede de segurança que permite mudar código sem medo. (Detalhada em profundidade no Guia de Testes.)*

---

## 9.1 Testes Unitários de Componentes

**Conceito + por que existe:** Testar componentes isoladamente, verificando que renderizam e se comportam corretamente dado um conjunto de props/estado. Existe porque componentes são as unidades do front, e testá-los isoladamente detecta regressões cedo e barato.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Modelo de componentes (3.1), → Guia de Testes (toda a Camada 9)

**Erro de iniciante → Marca do sênior:** O iniciante testa detalhes de implementação (que quebram a cada refatoração) ou não testa nada. O sênior testa comportamento observável do ponto de vista do usuário (Testing Library philosophy), tornando os testes resilientes a refatoração.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei testar componentes | — |
| **1** | Sei que devo testar, sem saber como | Explico que "testes verificam se funciona" |
| **2** | Escrevo testes seguindo exemplos; testo implementação | Já escrevi um teste de componente copiando um exemplo |
| **3** | Testo comportamento observável; uso Testing Library corretamente | Testei interações de um componente do ponto de vista do usuário |
| **4** | Projeto a estratégia de teste do componente; sei o que vale testar e o que não | Defini o que testar numa feature, evitando testes frágeis |
| **5** | Ensino testes de componente; reconheço testes frágeis; defino padrões de teste do time | Estabeleci a estratégia de testes de front de um produto |

---

## 9.2 Testes de Integração

**Conceito + por que existe:** Testar múltiplos componentes e a comunicação com APIs (mockadas) funcionando juntos. Existe porque bugs frequentemente surgem nas interfaces entre componentes, não dentro deles — e testes de integração capturam isso.

**Profundidade esperada:** Intermediário · **Conexões:** → Testes unitários (9.1), → Comunicação (Camada 5)

**Erro de iniciante → Marca do sênior:** O iniciante só testa unidades isoladas ou pula direto para E2E. O sênior usa testes de integração para verificar fluxos de múltiplos componentes com APIs mockadas (MSW), no ponto certo da pirâmide de testes.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é teste de integração | — |
| **1** | Sei que existe, sem saber a diferença para unitário | Explico vagamente que "testa partes juntas" |
| **2** | Escrevo algo entre unitário e integração sem método | Testei dois componentes juntos uma vez |
| **3** | Testo fluxos de múltiplos componentes; mocko APIs (MSW) | Testei um fluxo de formulário com API mockada |
| **4** | Projeto a estratégia de integração; escolho a fronteira certa entre unit e integração | Defini o nível de teste de integração de uma feature |
| **5** | Ensino testes de integração; reconheço cobertura mal distribuída; equilibro a pirâmide | Estabeleci a estratégia de integração de testes de um produto |

---

## 9.3 Testes End-to-End (E2E)

**Conceito + por que existe:** Testar a aplicação completa simulando o usuário real através de um browser automatizado (Playwright, Cypress). Existe porque alguns fluxos críticos só podem ser validados de ponta a ponta — mas E2E é caro e frágil, então deve ser usado estrategicamente.

**Profundidade esperada:** Intermediário · **Conexões:** → Guia de Testes (Tipo 19), → CI/CD (10.3)

**Erro de iniciante → Marca do sênior:** O iniciante testa tudo com E2E (suíte lenta e frágil) ou não tem nenhum. O sênior reserva E2E para os fluxos críticos de negócio, mantém a suíte enxuta, e entende a pirâmide de testes.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é teste E2E | — |
| **1** | Ouvi falar, sem saber o que faz | Explico que "testa o app inteiro" |
| **2** | Escrevo um teste E2E seguindo a documentação | Escrevi um teste E2E básico |
| **3** | Implemento E2E para fluxos importantes; lido com esperas e seletores | Testei o fluxo de login end-to-end |
| **4** | Projeto a estratégia de E2E; reservo para fluxos críticos; mantenho a suíte estável | Defini quais fluxos merecem E2E numa aplicação |
| **5** | Ensino E2E estratégico; reconheço suítes infladas e frágeis; equilibro a pirâmide | Estabeleci a estratégia de E2E de um produto |

---

## 9.4 Testes de Acessibilidade e Regressão Visual

**Conceito + por que existe:** Testes automatizados que verificam conformidade de acessibilidade (axe) e detectam mudanças visuais não-intencionais (snapshot visual). Existem porque acessibilidade e aparência regridem silenciosamente, e testes manuais não escalam.

**Profundidade esperada:** Básico-Intermediário · **Conexões:** → Acessibilidade (7.1), → CI/CD (10.3)

**Erro de iniciante → Marca do sênior:** O iniciante nunca automatiza verificação de acessibilidade ou regressão visual. O sênior integra testes de acessibilidade (axe) ao CI e usa regressão visual para componentes críticos do design system.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei que dá para automatizar esses testes | — |
| **1** | Sei que existem, sem saber usar | Nomeio uma ferramenta (ex: axe) |
| **2** | Rodo uma verificação de acessibilidade manualmente | Rodei o axe DevTools uma vez |
| **3** | Integro testes de acessibilidade automatizados; uso snapshot visual | Adicionei verificação axe a alguns testes |
| **4** | Projeto a estratégia de testes de a11y e visual no CI; escolho o que cobrir | Integrei testes de acessibilidade ao pipeline de CI |
| **5** | Ensino automação de a11y/visual; reconheço lacunas de cobertura; define a estratégia do time | Estabeleci testes de acessibilidade e visual de um design system |

---

# CAMADA 10 — Build, Tooling & Deploy

> *Como o código sai da sua máquina e chega ao usuário. A ponte para produção.*

---

## 10.1 Bundlers e Build Tools

**Conceito + por que existe:** As ferramentas que transformam o código-fonte (módulos, TS, JSX) em assets otimizados para o browser (Vite, webpack, esbuild). Existem porque o código que escrevemos não roda diretamente no browser — precisa ser transpilado, empacotado e otimizado.

**Profundidade esperada:** Intermediário · **Conexões:** → Módulos (2.4), → Performance (Camada 6)

**Erro de iniciante → Marca do sênior:** O iniciante trata o bundler como caixa-preta e não sabe configurá-lo quando algo quebra. O sênior entende o que o bundler faz (transpilação, bundling, tree-shaking, code splitting) e configura-o conscientemente.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é um bundler | — |
| **1** | Sei que "algo" transforma meu código, sem saber o quê | Explico que "tem uma ferramenta de build" |
| **2** | Uso um template/CLI sem configurar o build | Rodei `npm run build` sem entender o que faz |
| **3** | Configuro o bundler para necessidades comuns; entendo transpilação e bundling | Configurei aliases ou variáveis de ambiente no build |
| **4** | Projeto a configuração de build; otimizo para performance; resolvo problemas complexos | Diagnostiquei e resolvi um problema complexo de build |
| **5** | Ensino build tooling; reconheço configurações subótimas; conheço o ecossistema a fundo | Estabeleci a infraestrutura de build de um produto |

---

## 10.2 Linting, Formatting e Análise Estática

**Conceito + por que existe:** Ferramentas que detectam problemas e padronizam código automaticamente (ESLint, Prettier, type checking). Existem porque consistência e detecção precoce de bugs não devem depender da disciplina individual — devem ser automáticas.

**Profundidade esperada:** Intermediário · **Conexões:** → TypeScript (2.3), → CI/CD (10.3), → Guia de Segurança (análise estática)

**Erro de iniciante → Marca do sênior:** O iniciante nunca usou linters (ou os ignora). O sênior configura linting com regras de qualidade e segurança, formatação automática, e integra ao pre-commit e CI para que nada passe sem verificação.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é um linter | — |
| **1** | Ouvi falar de ESLint/Prettier, sem usar | Nomeio uma ferramenta de linting |
| **2** | Uso linting que veio no template, sem configurar | O editor mostra avisos de lint que às vezes ignoro |
| **3** | Configuro ESLint e Prettier; corrijo os avisos; entendo as regras | Configurei regras de lint para um projeto |
| **4** | Projeto a configuração de qualidade; integro ao pre-commit e CI; adiciono regras de segurança | Integrei linting + formatação ao pipeline bloqueante |
| **5** | Ensino análise estática; reconheço configurações fracas; escrevo regras customizadas | Estabeleci a estratégia de qualidade de código de um time |

> *Conexão com seu diagnóstico: esta é uma das competências do Eixo 3 (Craft) identificadas como gap — "nunca usei linters". É um alvo prioritário e de baixo custo de implementação.*

---

## 10.3 CI/CD para Front-End

**Conceito + por que existe:** Automação que roda testes, lint e build a cada mudança, e faz deploy automaticamente quando tudo passa. Existe porque verificações manuais não escalam e dependem de disciplina — CI/CD torna a qualidade estrutural, não opcional.

> **[INDUSTRIAL]**
> Fowler, M., & Foemmel, M. (2006). *Continuous Integration.* martinfowler.com.
> URL: https://martinfowler.com/articles/continuousIntegration.html
> — Define os princípios de CI, incluindo "make your build self-testing".

**Profundidade esperada:** Intermediário · **Conexões:** → Testes (Camada 9), → Guia de Testes/Automação, → Deploy (10.4)

**Erro de iniciante → Marca do sênior:** O iniciante faz deploy manual e roda testes localmente (quando roda). O sênior tem um pipeline que bloqueia merge se testes/lint falharem e faz deploy automatizado com validação.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é CI/CD | — |
| **1** | Ouvi falar, sem saber o que faz | Explico que "automatiza testes e deploy" |
| **2** | Sei que existe um pipeline, sem configurá-lo | Vi um workflow de CI rodar |
| **3** | Configuro CI para rodar testes/lint/build; entendo os estágios | Configurei um workflow que roda testes em cada PR |
| **4** | Projeto o pipeline com quality gates; integro deploy automatizado com validação | Desenhei um pipeline que bloqueia merge e faz deploy |
| **5** | Ensino CI/CD; reconheço pipelines mal projetados; otimizo feedback e confiabilidade | Estabeleci a estratégia de CI/CD de um produto |

---

## 10.4 Deploy, Hosting e Entrega (CDN, Edge)

**Conceito + por que existe:** Como a aplicação é servida ao usuário — hosting estático, CDN, edge computing, estratégias de cache de assets. Existe porque *onde* e *como* os assets são servidos afeta diretamente a performance de carregamento global e a disponibilidade.

**Profundidade esperada:** Básico-Intermediário · **Conexões:** → Performance (Camada 6), → HTTP/cache (5.1)

**Erro de iniciante → Marca do sênior:** O iniciante faz deploy num servidor único sem CDN nem estratégia de cache. O sênior usa CDN para distribuição global, configura cache de assets com hashing, e entende edge computing para latência mínima.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei como uma aplicação chega à produção | — |
| **1** | Sei que "sobe para um servidor", sem detalhes | Explico que "o site fica hospedado em algum lugar" |
| **2** | Faço deploy seguindo um tutorial de uma plataforma | Fiz deploy numa plataforma (Vercel/Netlify) seguindo guia |
| **3** | Configuro deploy estático com CDN; entendo cache de assets | Configurei deploy com CDN e cache de assets |
| **4** | Projeto a estratégia de entrega (CDN, edge, cache headers, imutabilidade); otimizo latência global | Desenhei a estratégia de hosting e cache de uma aplicação |
| **5** | Ensino estratégias de entrega; reconheço configurações subótimas; domino edge computing | Estabeleci a infraestrutura de entrega de um produto global |

---

# Planilha de Auto-Auditoria — Front-End

Registre seu nível atual (0-5) em cada competência. **Regra:** não marque um nível sem passar no teste de validação correspondente. Use a coluna "Evidência" para anotar o artefato concreto que comprova seu nível (projeto, código, decisão).

## Camada 1 — Plataforma Web

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 1.1 Critical Rendering Path | ___ | |
| 1.2 HTML Semântico | ___ | |
| 1.3 CSS (box model, cascata, layout) | ___ | |
| 1.4 DOM e Manipulação | ___ | |

## Camada 2 — Linguagem & Runtime

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 2.1 JavaScript Core | ___ | |
| 2.2 Event Loop e Assincronia | ___ | |
| 2.3 TypeScript | ___ | |
| 2.4 Módulos e Imports | ___ | |

## Camada 3 — Arquitetura de Componentes

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 3.1 Modelo de Componentes | ___ | |
| 3.2 Ciclo de Vida e Renderização | ___ | |
| 3.3 Reatividade e Fluxo Unidirecional | ___ | |
| 3.4 Lógica Reutilizável (Hooks) | ___ | |

## Camada 4 — Gerenciamento de Estado

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 4.1 Estado Local vs Global | ___ | |
| 4.2 Padrões de Estado | ___ | |
| 4.3 Estado Servidor vs Cliente | ___ | |
| 4.4 Sincronização, Cache e Invalidação | ___ | |

## Camada 5 — Comunicação Cliente-Servidor

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 5.1 HTTP | ___ | |
| 5.2 REST, GraphQL e Estilos de API | ___ | |
| 5.3 Data Fetching e Mutations | ___ | |
| 5.4 Tratamento de Erros e Loading | ___ | |

## Camada 6 — Performance

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 6.1 Critical Rendering Path / Carregamento | ___ | |
| 6.2 Code Splitting e Lazy Loading | ___ | |
| 6.3 Otimização de Re-render | ___ | |
| 6.4 Core Web Vitals e Medição | ___ | |

## Camada 7 — UX & Acessibilidade

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 7.1 Acessibilidade (WCAG/ARIA) | ___ | |
| 7.2 Responsividade | ___ | |
| 7.3 Padrões de Interação | ___ | |
| 7.4 Internacionalização (i18n) | ___ | |

## Camada 8 — Segurança no Cliente

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 8.1 XSS e Sanitização | ___ | |
| 8.2 Content Security Policy | ___ | |
| 8.3 CSRF | ___ | |
| 8.4 Gestão de Tokens e Autenticação | ___ | |

## Camada 9 — Qualidade & Testes

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 9.1 Testes Unitários de Componentes | ___ | |
| 9.2 Testes de Integração | ___ | |
| 9.3 Testes E2E | ___ | |
| 9.4 Testes de Acessibilidade e Visual | ___ | |

## Camada 10 — Build, Tooling & Deploy

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 10.1 Bundlers e Build Tools | ___ | |
| 10.2 Linting e Análise Estática | ___ | |
| 10.3 CI/CD para Front-End | ___ | |
| 10.4 Deploy, Hosting e Entrega | ___ | |

---

## Interpretação do Resultado

Após preencher, calcule a média por camada e observe o **perfil de distribuição**:

- **Especialista em Front-End** não significa nível 5 em tudo — significa **nível 4+ consistente nas camadas 1-5** (substrato e construção) e **nível 3+ nas camadas 6-10** (produção), sem nenhuma camada abaixo de 2.

- **O gargalo é a camada mais fraca, não a média.** Um perfil com média 4 mas uma camada em nível 1 tem um ponto cego que compromete a alegação de especialista. Uma corrente é tão forte quanto seu elo mais fraco.

- **Camadas 1-2 (substrato) são pré-requisito.** Gaps aqui contaminam todas as outras — não é possível ser nível 4 em Performance (Camada 6) sem nível 4 em Plataforma Web (Camada 1), porque otimização de rendering depende de entender o rendering.

- **Honestidade na evidência é tudo.** Um nível 4 sem artefato concreto na coluna "Evidência" é, na verdade, um nível 2-3 com viés de auto-avaliação (Kruger & Dunning, 1999). Trate cada nível não-evidenciado como uma hipótese a validar.

---

## Referências

| # | Fonte | Tipo | Uso |
|---|-------|------|-----|
| 1 | Dreyfus, S. E., & Dreyfus, H. L. (1980). *A Five-Stage Model of Skill Acquisition.* UC Berkeley. | **PEER-REVIEWED** | Escala de progressão de expertise |
| 2 | Smith, P. C., & Kendall, L. M. (1963). *Retranslation of Expectations.* Journal of Applied Psychology, 47(2). DOI: 10.1037/h0047060 | **PEER-REVIEWED** | Âncoras comportamentais (BARS) |
| 3 | Kruger, J., & Dunning, D. (1999). *Unskilled and Unaware of It.* JPSP, 77(6). DOI: 10.1037/0022-3514.77.6.1121 | **PEER-REVIEWED** | Viés de auto-avaliação; validação externa |
| 4 | MDN Web Docs (Mozilla). https://developer.mozilla.org/ | **INDUSTRIAL** | Referência definitiva da plataforma web |
| 5 | W3C WAI. *WCAG 2.2.* W3C Recommendation, 2023. https://www.w3.org/TR/WCAG22/ | **PADRÃO-W3C** | Acessibilidade (Camada 7.1) |
| 6 | OWASP Foundation. *OWASP Top Ten 2021.* https://owasp.org/Top10/ | **INDUSTRIAL-OWASP** | Segurança no cliente (Camada 8) |
| 7 | Google. *Web Vitals.* https://web.dev/articles/vitals | **INDUSTRIAL** | Métricas de performance (Camada 6.4) |
| 8 | Fowler, M., & Foemmel, M. (2006). *Continuous Integration.* | **INDUSTRIAL** | CI/CD (Camada 10.3) |

---

*Parte 1 de 3 do Skill-Check de Engenharia de Software. Próximas sub-áreas: Back-End, Middle-End/Integração, Infraestrutura/DevOps.*
*Escala ancorada em Dreyfus (1980) + BARS (Smith & Kendall, 1963). Auto-avaliação deve ser complementada por validação externa de pares seniores (Kruger & Dunning, 1999).*
*Revisão recomendada a cada 6 meses, registrando a evolução de nível e a nova evidência concreta.*
