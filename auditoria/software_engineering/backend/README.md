# Skill-Check de Engenharia de Software — Parte 1B: Back-End
## Arquitetura Completa de Competências com Escala Dreyfus Ancorada

> *"The limits of my language mean the limits of my world."*
> — Ludwig Wittgenstein (parafraseado para sistemas: os limites da sua arquitetura são os limites da sua escalabilidade)

---

## Como Este Documento Funciona

Este é o mapa de competências da sub-área **Back-End** da Engenharia de Software — o segundo da Parte 1 (a primeira foi Front-End). Mantém a mesma metodologia: 10 camadas que se empilham, do substrato de runtime até a operação em produção, com 4 competências por camada.

Para cada competência você encontra:

1. **Conceito + por que existe** — o que é e qual problema resolve
2. **Profundidade esperada** — Básico / Intermediário / Avançado
3. **Conexões** — com quais outras competências ela se comunica
4. **Erro de iniciante → Marca do sênior** — o contraste diagnóstico
5. **Progressão Dreyfus completa (0-5)** — o que cada nível significa especificamente, com o teste de validação (a evidência concreta que comprova o nível)

A escala é a mesma da Parte 1 (Front-End), fundamentada em Dreyfus (1980) + BARS (Smith & Kendall, 1963), com a ressalva de Kruger & Dunning (1999) sobre o viés de auto-avaliação. A planilha de auto-auditoria está no fim.

---

## A Escala de 6 Níveis (referência rápida)

| Nível | Dreyfus | Âncora Comportamental |
|-------|---------|----------------------|
| **0** | Desconhecido | Não reconheço o conceito |
| **1** | Novice | Explico o que é, mas preciso de guia para usar |
| **2** | Advanced Beginner | Uso com documentação aberta; não diagnostico falhas |
| **3** | Competent | Implemento sozinho; depuro quando quebra |
| **4** | Proficient | Projeto antecipando trade-offs e modos de falha |
| **5** | Expert | Ensino, reconheço quando o padrão está errado, contribuo com o estado da arte |

> **Fundamentação da escala (verificada):**
> Dreyfus, S. E., & Dreyfus, H. L. (1980). *A Five-Stage Model of the Mental Activities Involved in Directed Skill Acquisition.* UC Berkeley. ORC 80-2. **[PEER-REVIEWED]**
> Smith, P. C., & Kendall, L. M. (1963). *Retranslation of Expectations.* Journal of Applied Psychology, 47(2), 149–155. DOI: 10.1037/h0047060 **[PEER-REVIEWED]**
> Kruger, J., & Dunning, D. (1999). *Unskilled and Unaware of It.* JPSP, 77(6). DOI: 10.1037/0022-3514.77.6.1121 **[PEER-REVIEWED]** — auto-avaliação requer validação externa.

---

## Visão Geral das 10 Camadas

```
TIER PRODUÇÃO (operação e defesa)
  CAMADA 10 · Segurança de Backend
  CAMADA  9 · Observabilidade e Confiabilidade

TIER ESCALA (sistemas que crescem)
  CAMADA  8 · Sistemas Distribuídos e Escalabilidade
  CAMADA  7 · Cache e Otimização de Performance
  CAMADA  6 · Processamento Assíncrono, Filas e Mensageria

TIER CONSTRUÇÃO (o serviço)
  CAMADA  5 · Autenticação e Autorização
  CAMADA  4 · Persistência e Bancos de Dados
  CAMADA  3 · Arquitetura de APIs

TIER SUBSTRATO (fundação)
  CAMADA  2 · Protocolos e Comunicação de Rede
  CAMADA  1 · Fundamentos de Runtime e Concorrência
```

A lógica do empilhamento é a mesma do Front-End: cada camada se apoia nas inferiores. A diferença de natureza é que o Back-End é onde os **modos de falha de sistemas distribuídos** vivem — a régua de "especialista em Back-End" exige domínio do tier de escala (camadas 6-8) e de produção (9-10), não apenas a construção de APIs.

**Referências base de toda a arquitetura de Back-End:**
> **[CLÁSSICO — Referência Definitiva]**
> Kleppmann, M. (2017). *Designing Data-Intensive Applications.* O'Reilly.
> — A referência definitiva para sistemas de dados, distribuição, consistência e confiabilidade. Cobre as camadas 4, 6, 7 e 8 deste documento com profundidade rara.

> **[CLÁSSICO]**
> Bryant, R. E., & O'Hallaron, D. R. (2015). *Computer Systems: A Programmer's Perspective* (3rd ed.). Pearson.
> — Fundamentos de sistemas que sustentam a Camada 1 (processos, memória, I/O, concorrência).

---

# CAMADA 1 — Fundamentos de Runtime e Concorrência

> *O substrato do servidor. Onde o código encontra o sistema operacional, a CPU e a memória. Quem não domina isto não entende por que seu serviço trava sob carga.*

---

## 1.1 Modelo de Processo, Threads e Concorrência

**Conceito + por que existe:** Como o sistema operacional e o runtime executam código concorrentemente — processos, threads, e os modelos de concorrência (thread-per-request, event loop, async). Existe porque servidores precisam atender múltiplas requisições simultâneas, e o modelo escolhido determina os limites de escala e os modos de falha.

**Profundidade esperada:** Avançado · **Conexões:** → I/O (1.3), → Escalabilidade (Camada 8), → Event loop (Front-End 2.2)

**Erro de iniciante → Marca do sênior:** O iniciante trata concorrência como caixa-preta e é surpreendido por race conditions e deadlocks. O sênior entende o modelo de concorrência do seu runtime (threads, GIL, event loop) e projeta para evitar contenção e estados compartilhados problemáticos.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que são processos e threads | — |
| **1** | Sei que existem threads, mas não como funcionam | Explico que "o servidor atende vários ao mesmo tempo" |
| **2** | Uso concorrência via framework; sou surpreendido por race conditions | Já tive um bug intermitente que não soube explicar |
| **3** | Entendo threads vs processos; identifico e corrijo race conditions e deadlocks | Diagnostiquei e corrigi uma race condition com locks |
| **4** | Projeto para o modelo de concorrência do runtime; minimizo estado compartilhado; antecipo contenção | Desenhei um serviço evitando contenção sob carga concorrente |
| **5** | Ensino modelos de concorrência; reconheço anti-padrões; domino primitivas (mutex, semáforo, atomics) e suas implicações | Otimizei um sistema com alta contenção repensando o modelo de concorrência |

> *Conexão com seu diagnóstico (Eixo 1): este é o núcleo do gap de fundamentos computacionais. O modelo de concorrência do servidor é o análogo, em escala, da questão GIL + async/threadpool do seu pipeline.*

---

## 1.2 Gerenciamento de Memória e Garbage Collection

**Conceito + por que existe:** Como o runtime aloca, usa e libera memória — stack vs heap, garbage collection, memory leaks. Existe porque serviços de longa duração que vazam memória degradam e caem, e entender o GC é essencial para diagnosticar problemas de memória em produção.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Runtime (1.4), → Performance (Camada 7), → Observabilidade (Camada 9)

**Erro de iniciante → Marca do sênior:** O iniciante não pensa em memória até o serviço cair com OOM (out of memory). O sênior entende o modelo de memória do runtime, reconhece padrões de leak (referências retidas, closures, caches sem limite), e usa profiling de memória.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei como a memória é gerenciada | — |
| **1** | Sei que existe "memória", mas não stack vs heap nem GC | Explico que "o programa usa memória" |
| **2** | Sei que o GC limpa memória; não diagnostico leaks | Já vi um serviço cair por falta de memória sem saber a causa |
| **3** | Entendo stack/heap e GC; identifico leaks comuns | Diagnostiquei um memory leak com um profiler |
| **4** | Projeto para uso eficiente de memória; antecipo leaks (caches sem limite, listeners); ajusto o GC | Resolvi um problema de OOM ajustando estrutura de dados e GC |
| **5** | Ensino gerenciamento de memória; reconheço padrões de leak por inspeção; conheço os algoritmos de GC | Otimizei o perfil de memória de um sistema de produção |

---

## 1.3 I/O: Blocking vs Non-blocking, Event Loop vs Thread Pool

**Conceito + por que existe:** Os modelos de tratamento de operações de entrada/saída — bloqueante (uma thread espera) vs não-bloqueante (a thread continua), e as arquiteturas que os usam (event loop, thread pool). Existe porque I/O (rede, disco, banco) é a operação mais lenta de um servidor, e como você a gerencia determina quantas requisições simultâneas o sistema suporta.

**Profundidade esperada:** Avançado · **Conexões:** → Concorrência (1.1), → Banco de dados (Camada 4), → Escalabilidade (Camada 8)

**Erro de iniciante → Marca do sênior:** O iniciante faz operações bloqueantes na thread errada, esgotando o pool e travando o servidor. O sênior entende quando usar I/O bloqueante vs não-bloqueante, e projeta para não bloquear o event loop ou esgotar o thread pool.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei a diferença entre I/O bloqueante e não-bloqueante | — |
| **1** | Ouvi falar de async I/O, sem entender o modelo | Explico que "async não trava" |
| **2** | Uso async seguindo padrões; bloqueio o event loop sem perceber | Já travei um servidor com operação síncrona pesada |
| **3** | Entendo blocking vs non-blocking; sei quando usar cada um | Movi uma operação bloqueante para um worker apropriado |
| **4** | Projeto a arquitetura de I/O do serviço; evito esgotar pools; dimensiono recursos | Desenhei o tratamento de I/O de um serviço de alta concorrência |
| **5** | Ensino modelos de I/O; reconheço bloqueios sutis; conheço epoll/kqueue e a base do event loop | Otimizei o throughput de I/O de um sistema repensando o modelo |

---

## 1.4 Modelo de Execução da Linguagem/Runtime

**Conceito + por que existe:** As características específicas do runtime usado (JVM, Node.js, Go runtime, CPython com GIL, etc.) — como ele agenda, otimiza e executa código. Existe porque cada runtime tem trade-offs distintos de concorrência, performance e modelo de memória que afetam diretamente as decisões de arquitetura.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Concorrência (1.1), → Memória (1.2)

**Erro de iniciante → Marca do sênior:** O iniciante escreve código sem considerar as características do runtime (ex: CPU-bound em Node, ou ignorar o GIL em Python). O sênior conhece os trade-offs do seu runtime e projeta de acordo — ou escolhe o runtime certo para o perfil de carga.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei como meu runtime executa código | — |
| **1** | Uso a linguagem sem conhecer o runtime | Escrevo código que funciona localmente |
| **2** | Conheço o runtime superficialmente; sou surpreendido por seu comportamento | Já tive um problema de performance que não esperava |
| **3** | Entendo as características do runtime; escrevo código alinhado a elas | Evitei CPU-bound no event loop / contornei o GIL conscientemente |
| **4** | Projeto considerando os trade-offs do runtime; escolho o runtime pelo perfil de carga | Justifiquei a escolha de runtime para um serviço por suas características |
| **5** | Ensino o modelo do runtime; reconheço código mal alinhado; conheço a VM/interpretador a fundo | Otimizei um serviço explorando características internas do runtime |

> *Conexão com seu background: o GIL do CPython, que aparece no seu pipeline de phishing, é exatamente esta competência. Entender por que o GIL serializa threads CPU-bound mas não afeta I/O-bound é o nível 4 desta competência.*

---

# CAMADA 2 — Protocolos e Comunicação de Rede

> *Como serviços conversam entre si e com o mundo. A rede é onde a latência e as falhas parciais vivem.*

---

## 2.1 HTTP a Fundo (métodos, status, headers, HTTP/2, HTTP/3)

**Conceito + por que existe:** O protocolo de aplicação dominante da web — semântica de métodos, status codes, headers, e as evoluções (HTTP/1.1 → HTTP/2 multiplexação → HTTP/3 sobre QUIC). Existe porque é a espinha dorsal da comunicação web, e dominar sua semântica é essencial para projetar APIs corretas e depurar problemas de rede.

**Profundidade esperada:** Avançado · **Conexões:** → APIs (Camada 3), → Cache (Camada 7), → HTTP (Front-End 5.1)

**Erro de iniciante → Marca do sênior:** O iniciante usa métodos e status codes incorretamente (POST para tudo, 200 para erros). O sênior usa a semântica HTTP corretamente (idempotência de PUT/DELETE, status codes precisos, cache headers) e entende as implicações de performance de HTTP/2 e HTTP/3.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço o protocolo HTTP | — |
| **1** | Sei que HTTP transporta requisições, sem detalhes | Explico que "o cliente faz requisições HTTP" |
| **2** | Uso GET/POST e status comuns; uso incorretamente os nuances | Já usei POST para uma operação que deveria ser GET |
| **3** | Uso métodos e status corretamente; entendo headers e cache HTTP | Projetei endpoints com métodos e status semânticos |
| **4** | Domino a semântica completa (idempotência, content negotiation); exploro HTTP/2 multiplexação | Otimizei comunicação usando características de HTTP/2 |
| **5** | Ensino o protocolo; reconheço uso incorreto; conheço HTTP/3, QUIC e suas implicações | Projetei a estratégia de protocolo de um sistema de alto tráfego |

---

## 2.2 TCP/IP e o Modelo de Rede

**Conceito + por que existe:** Os protocolos fundamentais sobre os quais tudo roda — TCP (confiável, ordenado), UDP (rápido, sem garantias), IP, DNS, TLS. Existe porque problemas de rede (latência, timeouts, conexões esgotadas) são frequentemente diagnosticáveis apenas com entendimento das camadas abaixo do HTTP.

**Profundidade esperada:** Intermediário · **Conexões:** → HTTP (2.1), → Segurança (Camada 10), → Sistemas distribuídos (Camada 8)

**Erro de iniciante → Marca do sênior:** O iniciante trata a rede como confiável e instantânea. O sênior entende que a rede falha, tem latência variável, e que connection pooling, timeouts e keep-alive são decisões importantes — sabe que "a rede é não-confiável" é uma das falácias da computação distribuída.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço TCP/IP | — |
| **1** | Sei que existe "a internet", sem entender as camadas | Explico que "os dados viajam pela rede" |
| **2** | Sei que TCP é confiável, sem entender as implicações | Reconheço que existem TCP e UDP |
| **3** | Entendo TCP vs UDP, DNS, TLS handshake; configuro timeouts e pools | Configurei connection pooling e timeouts adequados |
| **4** | Projeto considerando características da rede; dimensiono pools; antecipo falhas parciais | Diagnostiquei um problema de esgotamento de conexões |
| **5** | Ensino o modelo de rede; reconheço problemas de rede por inspeção; conheço TCP tuning | Resolvi um problema complexo de latência na camada de rede |

---

## 2.3 Protocolos de RPC e Streaming (gRPC, WebSockets, SSE)

**Conceito + por que existe:** Os protocolos além do request-response tradicional — RPC para comunicação entre serviços (gRPC), e comunicação bidirecional/streaming (WebSockets, Server-Sent Events). Existem porque nem toda comunicação se encaixa no modelo request-response: comunicação entre microsserviços e atualizações em tempo real têm necessidades diferentes.

**Profundidade esperada:** Intermediário · **Conexões:** → Serialização (2.4), → Mensageria (Camada 6), → Microsserviços (Camada 8)

**Erro de iniciante → Marca do sênior:** O iniciante usa REST/polling para tudo, inclusive casos que pedem streaming. O sênior escolhe o protocolo pelo padrão de comunicação — gRPC para RPC interno de baixa latência, WebSockets para bidirecional, SSE para server-push unidirecional.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço protocolos além de HTTP request-response | — |
| **1** | Ouvi falar de WebSockets/gRPC, sem saber quando usar | Nomeio um protocolo de streaming |
| **2** | Usei WebSockets ou gRPC seguindo um tutorial | Implementei um chat com WebSocket seguindo guia |
| **3** | Implemento o protocolo certo para o caso; entendo os trade-offs básicos | Escolhi e implementei SSE vs WebSocket conscientemente |
| **4** | Projeto a estratégia de comunicação; escolho gRPC/WS/SSE pelo padrão de uso | Desenhei a comunicação entre serviços usando gRPC justificadamente |
| **5** | Ensino protocolos de comunicação; reconheço escolhas subótimas; domino streaming bidirecional e backpressure | Projetei a arquitetura de comunicação em tempo real de um produto |

---

## 2.4 Serialização e Formatos de Dados (JSON, Protobuf, schemas)

**Conceito + por que existe:** Como dados estruturados são convertidos para transmissão e de volta — formatos (JSON, Protocol Buffers, Avro), schemas, e evolução de schema. Existe porque toda comunicação entre sistemas requer serialização, e a escolha afeta performance, tamanho, e a capacidade de evoluir contratos sem quebrar.

**Profundidade esperada:** Intermediário · **Conexões:** → RPC (2.3), → APIs (Camada 3), → Versionamento (3.3)

**Erro de iniciante → Marca do sênior:** O iniciante usa JSON para tudo sem pensar em schema ou evolução. O sênior escolhe o formato pelo trade-off (JSON legível vs Protobuf compacto e tipado), e projeta schemas que podem evoluir com compatibilidade para frente e para trás.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é serialização | — |
| **1** | Sei que dados viram JSON, sem entender o conceito geral | Explico que "os dados viram texto para enviar" |
| **2** | Uso JSON; não penso em schema nem evolução | Serializei dados para JSON numa API |
| **3** | Entendo formatos e schemas; uso Protobuf/Avro quando apropriado | Defini um schema Protobuf para comunicação entre serviços |
| **4** | Projeto schemas evolutivos (compat. para frente/trás); escolho formato pelo trade-off | Desenhei evolução de schema sem quebrar consumidores existentes |
| **5** | Ensino serialização e schema evolution; reconheço schemas frágeis; domino schema registry | Estabeleci a estratégia de contratos de dados de um sistema distribuído |

---

# CAMADA 3 — Arquitetura de APIs

> *A interface pública do serviço. O contrato que outros sistemas dependem — e que é caro mudar depois.*

**Referência fundacional de design de API:**
> **[PEER-REVIEWED — Tese de Doutorado]**
> Fielding, R. T. (2000). *Architectural Styles and the Design of Network-based Software Architectures.* PhD Dissertation, University of California, Irvine.
> URL: https://ics.uci.edu/~fielding/pubs/dissertation/top.htm
> — A tese que definiu formalmente o estilo arquitetural REST. Leitura fundacional para entender por que REST é como é, não apenas como usá-lo.

---

## 3.1 Design de API REST (recursos, verbos, idempotência, HATEOAS)

**Conceito + por que existe:** O estilo arquitetural REST aplicado ao design de APIs — modelagem de recursos, uso semântico de verbos HTTP, idempotência, e os níveis de maturidade (Richardson). Existe porque APIs bem projetadas são intuitivas, cacheáveis e evolutivas, enquanto APIs mal projetadas se tornam dívida técnica que todos os consumidores carregam.

**Profundidade esperada:** Avançado · **Conexões:** → HTTP (2.1), → Versionamento (3.3), → REST (Front-End 5.2)

**Erro de iniciante → Marca do sênior:** O iniciante cria APIs RPC-disfarçadas-de-REST (`/getUser`, `/createOrder` como POST). O sênior modela recursos corretamente, usa verbos semanticamente, garante idempotência onde necessário, e projeta para evolução.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é REST | — |
| **1** | Sei que REST é "um jeito de fazer API", sem os princípios | Explico que "API REST retorna JSON" |
| **2** | Crio endpoints; misturo REST com RPC sem perceber | Já criei `/getUser` como endpoint |
| **3** | Modelo recursos corretamente; uso verbos e status semânticos; garanto idempotência | Projetei uma API REST com recursos e verbos corretos |
| **4** | Projeto contratos evolutivos; entendo os trade-offs de REST; aplico maturidade Richardson | Desenhei uma API pública pensando em evolução e consumidores |
| **5** | Ensino design de API; reconheço APIs mal modeladas; conheço a tese de Fielding e HATEOAS | Estabeleci os padrões de design de API de uma organização |

---

## 3.2 GraphQL e APIs Declarativas

**Conceito + por que existe:** Um estilo de API onde o cliente especifica exatamente os dados que precisa via query declarativa, resolvendo over-fetching e under-fetching do REST. Existe porque clientes com necessidades de dados variadas (especialmente mobile e front-ends complexos) sofrem com a rigidez dos endpoints REST.

**Profundidade esperada:** Intermediário · **Conexões:** → REST (3.1), → N+1 (7.3), → GraphQL (Front-End 5.2)

**Erro de iniciante → Marca do sênior:** O iniciante adota GraphQL sem entender seus custos (complexidade, problema N+1, cache mais difícil). O sênior escolhe GraphQL pelo trade-off real, resolve N+1 com dataloaders, e entende quando REST seria mais simples.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço GraphQL | — |
| **1** | Ouvi falar, sem saber como funciona | Explico que "o cliente pede os campos que quer" |
| **2** | Consumi ou criei um schema GraphQL seguindo tutorial | Defini um resolver simples |
| **3** | Implemento APIs GraphQL; entendo schema, resolvers, queries/mutations | Construí uma API GraphQL funcional com resolvers |
| **4** | Projeto schemas GraphQL; resolvo N+1 com dataloaders; escolho GraphQL vs REST por trade-off | Resolvi o problema N+1 numa API GraphQL com batching |
| **5** | Ensino GraphQL; reconheço schemas mal projetados; domino federação e performance | Estabeleci a arquitetura GraphQL (federada) de um produto |

---

## 3.3 Versionamento e Evolução de Contratos

**Conceito + por que existe:** As estratégias para evoluir uma API sem quebrar consumidores existentes — versionamento (URL, header), deprecação, compatibilidade para trás. Existe porque uma API publicada é um contrato com terceiros, e mudá-la sem cuidado quebra integrações que você não controla.

**Profundidade esperada:** Avançado · **Conexões:** → Design de API (3.1), → Serialização (2.4), → Contratos (Middle-End)

**Erro de iniciante → Marca do sênior:** O iniciante muda a API livremente e quebra consumidores. O sênior projeta para evolução desde o início, mantém compatibilidade para trás, versiona conscientemente, e tem processo de deprecação.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não penso em versionamento de API | — |
| **1** | Sei que APIs "têm versões", sem saber gerenciar | Explico que "existe v1, v2 de API" |
| **2** | Adiciono `/v2` quando preciso mudar, sem estratégia | Já criei uma v2 quebrando a v1 |
| **3** | Versiono conscientemente; mantenho compatibilidade para trás em mudanças | Adicionei um campo sem quebrar consumidores existentes |
| **4** | Projeto a estratégia de evolução; planejo deprecação; comunico mudanças | Desenhei o ciclo de vida e deprecação de uma API pública |
| **5** | Ensino evolução de contratos; reconheço mudanças quebradoras; domino estratégias de versionamento | Estabeleci a política de versionamento de API de uma organização |

---

## 3.4 Validação, Paginação e Rate Limiting

**Conceito + por que existe:** Os mecanismos transversais que tornam uma API robusta — validação de input, paginação de grandes resultados, e rate limiting contra abuso. Existem porque APIs recebem input não-confiável, retornam volumes que precisam ser paginados, e precisam se proteger contra consumo excessivo.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Segurança (Camada 10), → Performance (Camada 7), → OWASP API Top 10

**Erro de iniciante → Marca do sênior:** O iniciante confia no input, retorna listas ilimitadas, e não tem rate limiting. O sênior valida todo input na fronteira, pagina por padrão, e implementa rate limiting — reconhecendo que "Unrestricted Resource Consumption" é o item #4 do OWASP API Security Top 10.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não penso em validação, paginação ou rate limiting | — |
| **1** | Sei que devo validar input, sem método | Explico que "tem que validar os dados" |
| **2** | Valido alguns campos; retorno listas sem paginação | Já retornei uma lista ilimitada de uma API |
| **3** | Valido input sistematicamente; pagino resultados; entendo rate limiting | Implementei paginação e validação numa API |
| **4** | Projeto a estratégia de robustez; rate limiting por cliente; validação de schema | Desenhei rate limiting e validação de schema de uma API pública |
| **5** | Ensino robustez de API; reconheço APIs vulneráveis a abuso; domino estratégias de throttling | Estabeleci os padrões de proteção de API de uma organização |

---

# CAMADA 4 — Persistência e Bancos de Dados

> *Onde o estado do sistema realmente vive. A camada mais difícil de mudar e a mais cara de errar.*

**Referência base:**
> **[CLÁSSICO]**
> Kleppmann, M. (2017). *Designing Data-Intensive Applications.* O'Reilly. — Capítulos 2-7 cobrem modelagem, storage engines, transações e replicação com profundidade definitiva.

---

## 4.1 Modelagem de Dados e Normalização

**Conceito + por que existe:** Como estruturar dados em tabelas/coleções — normalização (eliminar redundância), desnormalização (otimizar leitura), e modelagem de relacionamentos. Existe porque a estrutura dos dados é a decisão mais duradoura de um sistema, e modelagem ruim gera anomalias, inconsistência e queries impossíveis.

**Profundidade esperada:** Avançado · **Conexões:** → SQL (4.2), → Transações (4.3), → Escolha de banco (4.4)

**Erro de iniciante → Marca do sênior:** O iniciante modela dados como espelho da UI ou sem pensar em relacionamentos. O sênior modela pelo domínio e pelos padrões de acesso, sabe quando normalizar (consistência) e quando desnormalizar (performance de leitura).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei modelar dados | — |
| **1** | Sei que dados ficam em tabelas, sem entender modelagem | Crio uma tabela com colunas |
| **2** | Crio tabelas; não penso em normalização nem relacionamentos | Já tive dados duplicados que dessincronizaram |
| **3** | Modelo com normalização; defino relacionamentos e chaves corretamente | Modelei um schema normalizado com chaves estrangeiras |
| **4** | Projeto pelo domínio e padrões de acesso; decido normalizar vs desnormalizar por trade-off | Desenhei um schema otimizando para os padrões de query reais |
| **5** | Ensino modelagem; reconheço schemas problemáticos; domino formas normais e modelagem dimensional | Estabeleci a arquitetura de dados de um sistema complexo |

---

## 4.2 SQL e Query Optimization (índices, planos de execução)

**Conceito + por que existe:** A linguagem de consulta e como otimizá-la — escrever queries eficientes, usar índices corretamente, ler planos de execução. Existe porque queries mal otimizadas são a causa mais comum de lentidão em sistemas com banco de dados, e índices são a ferramenta principal de otimização.

**Profundidade esperada:** Avançado · **Conexões:** → Modelagem (4.1), → Performance (Camada 7), → N+1 (7.3)

**Erro de iniciante → Marca do sênior:** O iniciante escreve queries que funcionam mas fazem full table scans, sem índices. O sênior entende planos de execução, cria índices estratégicos, e reconhece queries problemáticas (N+1, falta de índice) antes que cheguem à produção.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei escrever SQL | — |
| **1** | Escrevo SELECT básico; não conheço JOINs nem índices | Faço uma query simples de uma tabela |
| **2** | Escrevo queries com JOINs; não penso em performance | Já escrevi uma query lenta sem saber por quê |
| **3** | Escrevo queries eficientes; crio índices; leio planos de execução básicos | Otimizei uma query lenta adicionando um índice |
| **4** | Projeto a estratégia de indexação; analiso planos de execução; antecipo queries problemáticas | Diagnostiquei e otimizei uma query complexa via plano de execução |
| **5** | Ensino otimização de queries; reconheço problemas por inspeção; domino o query planner | Otimizei a camada de dados de um sistema de produção em escala |

---

## 4.3 Transações, ACID e Concorrência (isolation levels, locks)

**Conceito + por que existe:** As garantias de consistência em operações concorrentes — propriedades ACID, níveis de isolamento, locks, e os fenômenos de concorrência (dirty reads, phantom reads). Existe porque múltiplas operações simultâneas sobre os mesmos dados podem corromper o estado, e transações são o mecanismo que garante consistência.

**Profundidade esperada:** Avançado · **Conexões:** → Modelagem (4.1), → Sistemas distribuídos (Camada 8), → Concorrência (1.1)

**Erro de iniciante → Marca do sênior:** O iniciante não usa transações ou não entende isolation levels, gerando race conditions de dados. O sênior usa transações corretamente, escolhe o isolation level pelo trade-off (consistência vs performance), e reconhece os fenômenos de concorrência.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que são transações | — |
| **1** | Ouvi falar de transações, sem entender ACID | Explico que "transação agrupa operações" |
| **2** | Uso transações básicas; não entendo isolation levels | Envolvi operações numa transação seguindo exemplo |
| **3** | Uso transações corretamente; entendo ACID e isolation levels básicos | Resolvi uma race condition de dados com transação/lock |
| **4** | Escolho isolation level por trade-off; antecipo fenômenos de concorrência; uso locks otimistas/pessimistas | Desenhei o controle de concorrência de uma operação crítica |
| **5** | Ensino transações e isolamento; reconheço bugs de concorrência sutis; domino MVCC e a teoria | Resolvi um problema complexo de concorrência de dados em produção |

---

## 4.4 NoSQL e Escolha de Banco (document, key-value, wide-column, graph)

**Conceito + por que existe:** Os modelos de banco não-relacionais — documento (MongoDB), key-value (Redis), wide-column (Cassandra), graph (Neo4j) — e quando usar cada um vs SQL relacional. Existe porque diferentes perfis de dados e acesso têm diferentes bancos ótimos, e usar o tipo errado gera complexidade e limitações desnecessárias.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Modelagem (4.1), → CAP (8.1), → Cache (7.2)

**Erro de iniciante → Marca do sênior:** O iniciante usa o banco que conhece para tudo, ou adota NoSQL por hype sem entender os trade-offs. O sênior escolhe o banco pelo perfil de dados e acesso, entende os trade-offs (consistência, flexibilidade de schema, padrões de query), e sabe quando SQL relacional é a escolha certa.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei que existem tipos diferentes de banco | — |
| **1** | Ouvi falar de SQL e NoSQL, sem saber a diferença | Nomeio um banco NoSQL |
| **2** | Uso um banco específico; não sei quando usar outros | Usei MongoDB ou Postgres seguindo o que conhecia |
| **3** | Entendo os modelos de banco; escolho pelo caso de uso básico | Escolhi key-value para cache e relacional para dados transacionais |
| **4** | Projeto a estratégia de persistência; escolho o banco pelo trade-off; uso polyglot persistence | Justifiquei a escolha de banco para diferentes partes de um sistema |
| **5** | Ensino escolha de banco; reconheço escolhas inadequadas; domino os trade-offs de cada modelo | Estabeleci a estratégia de persistência poliglota de um produto |

---

# CAMADA 5 — Autenticação e Autorização

> *Quem é você (autenticação) e o que você pode fazer (autorização). A fronteira de confiança do sistema.*

**Referências base:**
> **[PADRÃO-NIST]**
> NIST SP 800-63B (2017). *Digital Identity Guidelines: Authentication and Lifecycle Management.* DOI: 10.6028/NIST.SP.800-63b

> **[PADRÃO-IETF]**
> Hardt, D. (2012). *RFC 6749: The OAuth 2.0 Authorization Framework.* IETF.
> URL: https://datatracker.ietf.org/doc/html/rfc6749

---

## 5.1 Fundamentos de Identidade e Autenticação

**Conceito + por que existe:** Os mecanismos para verificar identidade — senhas (e seu armazenamento correto), MFA, fatores de autenticação. Existe porque verificar quem está fazendo uma requisição é a base de toda segurança, e fazê-lo incorretamente (senhas em texto plano, sem MFA) é um vetor direto de comprometimento.

**Profundidade esperada:** Avançado · **Conexões:** → Tokens (5.2), → Segurança (Camada 10), → Auth (Front-End 8.4)

**Erro de iniciante → Marca do sênior:** O iniciante armazena senhas com hash rápido (MD5/SHA) ou texto plano. O sênior usa funções de derivação lentas (argon2id, bcrypt), implementa MFA, e segue as diretrizes do NIST SP 800-63B — reconhecendo que "Broken Authentication" é o #2 do OWASP API Security Top 10 desde 2019.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei como autenticação funciona | — |
| **1** | Sei que existe login com senha, sem os detalhes de segurança | Explico que "o usuário faz login com senha" |
| **2** | Implemento login; armazeno senhas sem saber o método correto | Já armazenei senha com hash simples (SHA/MD5) |
| **3** | Armazeno senhas corretamente (bcrypt/argon2id); implemento autenticação segura | Implementei login com bcrypt e validação correta |
| **4** | Projeto o fluxo de autenticação; implemento MFA; sigo NIST 800-63B | Desenhei o sistema de autenticação de uma aplicação com MFA |
| **5** | Ensino segurança de autenticação; reconheço implementações inseguras; domino os padrões e ataques | Estabeleci a arquitetura de identidade de um produto |

---

## 5.2 Sessões, Tokens e JWT

**Conceito + por que existe:** Como manter o estado de autenticação entre requisições — sessões com estado no servidor vs tokens stateless (JWT), e os trade-offs de cada um. Existe porque HTTP é stateless, e o sistema precisa lembrar que um usuário está autenticado sem reautenticar a cada requisição.

**Profundidade esperada:** Avançado · **Conexões:** → Autenticação (5.1), → OAuth (5.3), → Tokens (Front-End 8.4)

**Erro de iniciante → Marca do sênior:** O iniciante usa JWT sem entender suas limitações (não-revogável, payload exposto) ou armazena tokens inseguramente. O sênior entende o trade-off sessão (stateful, revogável) vs JWT (stateless, escalável mas difícil de revogar), e implementa refresh tokens com rotação.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei como o estado de login é mantido | — |
| **1** | Ouvi falar de sessões e tokens, sem entender | Explico que "o sistema lembra que você logou" |
| **2** | Uso JWT ou sessões seguindo um tutorial | Implementei login com JWT copiando exemplo |
| **3** | Implemento sessões ou JWT corretamente; entendo a diferença | Implementei autenticação com refresh tokens |
| **4** | Escolho sessão vs JWT por trade-off; implemento rotação de tokens e revogação | Desenhei a estratégia de tokens considerando revogação e escala |
| **5** | Ensino gestão de sessão/token; reconheço implementações vulneráveis; domino os trade-offs e ataques (replay) | Estabeleci a arquitetura de sessão/token de um sistema distribuído |

---

## 5.3 OAuth 2.0 e OpenID Connect

**Conceito + por que existe:** Os protocolos padrão para autorização delegada (OAuth 2.0 — "login com Google") e autenticação federada (OIDC). Existem porque permitir que usuários se autentiquem via provedores externos, e que aplicações acessem recursos em nome do usuário, requer protocolos padronizados e seguros.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Tokens (5.2), → Autorização (5.4)

**Erro de iniciante → Marca do sênior:** O iniciante implementa OAuth incorretamente (confunde os flows, expõe secrets) ou reinventa autenticação federada. O sênior entende os flows do OAuth (authorization code, PKCE), escolhe o correto, e segue o RFC — reconhecendo o princípio "don't reinvent the wheel, always use standards".

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço OAuth | — |
| **1** | Sei que existe "login com Google", sem entender o protocolo | Explico que "dá para logar com outra conta" |
| **2** | Integrei OAuth via biblioteca seguindo tutorial | Implementei "login com Google" seguindo guia |
| **3** | Implemento OAuth corretamente; entendo os flows principais | Implementei o authorization code flow com PKCE |
| **4** | Projeto a integração; escolho o flow correto; entendo OIDC vs OAuth | Desenhei a estratégia de autenticação federada de uma aplicação |
| **5** | Ensino OAuth/OIDC; reconheço implementações inseguras; domino os flows e ataques | Estabeleci a arquitetura de identidade federada de um produto |

---

## 5.4 Autorização (RBAC, ABAC, controle de acesso)

**Conceito + por que existe:** Os modelos para decidir o que um usuário autenticado pode fazer — RBAC (baseado em papéis), ABAC (baseado em atributos), e a verificação de permissões em cada operação. Existe porque autenticar (quem é) não basta; é preciso autorizar (o que pode fazer), e fazê-lo incorretamente é o vetor #1 do OWASP API Security Top 10 (Broken Object Level Authorization).

**Profundidade esperada:** Avançado · **Conexões:** → Autenticação (5.1), → Segurança (Camada 10), → OWASP API Top 10

**Erro de iniciante → Marca do sênior:** O iniciante assume que autenticado = autorizado, ou verifica permissão no front mas não no servidor. O sênior verifica autorização no servidor em cada operação sobre cada objeto — reconhecendo que BOLA (acesso a objeto de outro usuário trocando o ID) está em ~40% dos ataques a APIs.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei a diferença entre autenticação e autorização | — |
| **1** | Sei que existem permissões, sem saber implementar | Explico que "nem todo usuário pode tudo" |
| **2** | Implemento checagens de permissão pontuais, sem sistema | Já assumi que autenticado = autorizado |
| **3** | Implemento RBAC; verifico autorização no servidor em cada operação | Implementei controle de acesso por papéis no backend |
| **4** | Projeto o modelo de autorização (RBAC/ABAC); verifico object-level authorization | Desenhei autorização verificando acesso a cada objeto (anti-BOLA) |
| **5** | Ensino autorização; reconheço BOLA e falhas de controle de acesso; domino os modelos | Estabeleci a arquitetura de autorização de um produto |

---

# CAMADA 6 — Processamento Assíncrono, Filas e Mensageria

> *Como o sistema faz trabalho fora do ciclo request-response. A base de sistemas resilientes e escaláveis.*

---

## 6.1 Jobs Assíncronos e Background Processing

**Conceito + por que existe:** Executar trabalho fora do ciclo request-response — tarefas demoradas (envio de email, processamento de imagem, geração de relatório) processadas em background. Existe porque algumas operações são lentas demais para bloquear a resposta ao usuário, e devem ser desacopladas para não degradar a experiência.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Filas (6.2), → Concorrência (1.1), → Data fetching (Front-End 5.3)

**Erro de iniciante → Marca do sênior:** O iniciante faz trabalho pesado de forma síncrona, fazendo o usuário esperar (ou causando timeout). O sênior desacopla trabalho pesado em jobs assíncronos, com feedback de progresso e tratamento de falha.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é processamento assíncrono | — |
| **1** | Sei que dá para fazer trabalho "depois", sem saber como | Explico que "algumas tarefas rodam em segundo plano" |
| **2** | Uso uma fila de jobs seguindo tutorial; não trato falhas | Implementei um job assíncrono seguindo exemplo |
| **3** | Implemento background jobs corretamente; trato retry e falha | Movi envio de email para um job assíncrono com retry |
| **4** | Projeto a arquitetura de processamento assíncrono; dimensiono workers; antecipo falhas | Desenhei o processamento em background de uma operação pesada |
| **5** | Ensino processamento assíncrono; reconheço trabalho mal desacoplado; domino padrões de worker | Estabeleci a arquitetura de jobs de um sistema em escala |

---

## 6.2 Filas e Brokers de Mensagem (RabbitMQ, SQS, Kafka)

**Conceito + por que existe:** A infraestrutura que transporta mensagens entre componentes de forma desacoplada e confiável — filas (RabbitMQ, SQS) e logs de eventos (Kafka). Existe porque acoplar serviços diretamente os torna frágeis; um broker desacopla produtores de consumidores, absorvendo picos e tolerando falhas.

**Profundidade esperada:** Avançado · **Conexões:** → Jobs (6.1), → Padrões de mensageria (6.3), → Sistemas distribuídos (Camada 8)

**Erro de iniciante → Marca do sênior:** O iniciante usa uma fila como caixa-preta sem entender as garantias. O sênior entende os trade-offs entre brokers (fila vs log, at-least-once vs at-most-once), escolhe o certo, e projeta para as garantias de entrega que precisa.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é uma fila de mensagens | — |
| **1** | Ouvi falar de RabbitMQ/Kafka, sem saber o que fazem | Nomeio um broker de mensagens |
| **2** | Uso uma fila seguindo tutorial; não entendo as garantias | Publiquei e consumi mensagens seguindo exemplo |
| **3** | Implemento produção/consumo corretamente; entendo ack e garantias básicas | Implementei um consumer com acknowledgment correto |
| **4** | Escolho o broker por trade-off; projeto para garantias de entrega; dimensiono | Escolhi Kafka vs RabbitMQ justificadamente para um caso |
| **5** | Ensino mensageria; reconheço uso inadequado; domino as garantias e internals (partições, offsets) | Estabeleci a arquitetura de mensageria de um sistema distribuído |

---

## 6.3 Padrões de Mensageria (pub/sub, event-driven, sagas)

**Conceito + por que existe:** Os padrões arquiteturais construídos sobre mensageria — publish/subscribe, arquitetura orientada a eventos, e sagas (transações distribuídas). Existem porque sistemas distribuídos precisam coordenar trabalho entre serviços sem acoplamento forte, e esses padrões resolvem comunicação e consistência distribuída.

**Profundidade esperada:** Avançado · **Conexões:** → Filas (6.2), → Sistemas distribuídos (Camada 8), → Arquitetura orientada a eventos (Middle-End)

**Erro de iniciante → Marca do sênior:** O iniciante implementa comunicação ponto-a-ponto acoplada, ou tenta transações distribuídas com two-phase commit ingênuo. O sênior usa pub/sub para desacoplamento, eventos para comunicação assíncrona, e sagas para consistência eventual em transações distribuídas.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço padrões de mensageria | — |
| **1** | Ouvi falar de pub/sub e eventos, sem entender | Explico que "serviços mandam eventos" |
| **2** | Implementei pub/sub seguindo tutorial | Publiquei eventos para múltiplos consumidores |
| **3** | Implemento arquitetura orientada a eventos; entendo os padrões | Construí uma feature com comunicação por eventos |
| **4** | Projeto a arquitetura de eventos; uso sagas para consistência distribuída | Desenhei uma saga para uma transação entre serviços |
| **5** | Ensino padrões de mensageria; reconheço acoplamento indevido; domino event sourcing e CQRS | Estabeleci a arquitetura orientada a eventos de um produto |

---

## 6.4 Garantias de Entrega e Idempotência

**Conceito + por que existe:** Como garantir que mensagens sejam processadas corretamente apesar de falhas — at-least-once vs exactly-once, e idempotência (processar a mesma mensagem duas vezes sem efeito colateral duplicado). Existe porque sistemas distribuídos falham, mensagens são reentregues, e sem idempotência uma reentrega causa efeitos duplicados (cobrança dupla, email duplicado).

**Profundidade esperada:** Avançado · **Conexões:** → Filas (6.2), → Transações (4.3), → Resiliência (Camada 8)

**Erro de iniciante → Marca do sênior:** O iniciante assume que mensagens são entregues exatamente uma vez e não trata duplicatas. O sênior entende que entrega confiável é at-least-once (logo, duplicatas acontecem), e projeta consumers idempotentes com chaves de deduplicação.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é idempotência | — |
| **1** | Ouvi falar, sem entender o problema | Explico vagamente que "não pode processar duas vezes" |
| **2** | Assumo entrega única; não trato duplicatas | Já tive um efeito duplicado por reprocessamento |
| **3** | Implemento consumers idempotentes; uso chaves de deduplicação | Tornei um consumer idempotente com chave de deduplicação |
| **4** | Projeto para garantias de entrega; antecipo reentrega; desenho idempotência end-to-end | Desenhei idempotência para uma operação de pagamento |
| **5** | Ensino garantias de entrega; reconheço código não-idempotente; domino exactly-once semantics | Estabeleci os padrões de idempotência de um sistema crítico |

---

# CAMADA 7 — Cache e Otimização de Performance

> *A diferença entre um sistema que aguenta carga e um que cai. Frequentemente a primeira otimização e a mais impactante.*

---

## 7.1 Estratégias de Cache (cache-aside, write-through, TTL)

**Conceito + por que existe:** Os padrões de cache — cache-aside (busca no cache, senão no banco), write-through (escreve em ambos), e políticas de expiração (TTL, LRU). Existe porque acessar dados frequentes repetidamente do banco é caro, e o cache reduz latência e carga drasticamente — mas introduz o problema de consistência.

**Profundidade esperada:** Avançado · **Conexões:** → Cache distribuído (7.2), → Invalidação (Front-End 4.4), → Banco (Camada 4)

**Erro de iniciante → Marca do sênior:** O iniciante adiciona cache sem estratégia de invalidação (dados ficam stale) ou não cacheia o que deveria. O sênior escolhe a estratégia pelo padrão de leitura/escrita, define TTLs conscientes, e tem estratégia de invalidação.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é cache | — |
| **1** | Sei que cache "deixa mais rápido", sem saber como | Explico que "cache guarda dados para acesso rápido" |
| **2** | Adiciono cache sem estratégia de invalidação | Já tive dados desatualizados por cache |
| **3** | Implemento cache-aside com TTL; invalido após escritas | Implementei cache com invalidação após mutation |
| **4** | Escolho a estratégia por padrão de acesso; projeto invalidação; defino TTLs conscientes | Desenhei a estratégia de cache de uma feature de alto tráfego |
| **5** | Ensino estratégias de cache; reconheço problemas de consistência; domino os trade-offs | Estabeleci a arquitetura de cache de um sistema em escala |

---

## 7.2 Cache Distribuído (Redis, Memcached)

**Conceito + por que existe:** Cache compartilhado entre múltiplas instâncias do serviço — Redis, Memcached. Existe porque, quando o serviço roda em múltiplas instâncias (escala horizontal), cada uma com cache local geraria inconsistência; um cache distribuído dá uma fonte única e rápida compartilhada.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Estratégias de cache (7.1), → Escalabilidade (Camada 8), → NoSQL (4.4)

**Erro de iniciante → Marca do sênior:** O iniciante usa Redis apenas como cache simples, ignorando suas estruturas de dados e usos (locks distribuídos, rate limiting, pub/sub). O sênior entende as capacidades do Redis, usa a estrutura de dados certa, e projeta para falha do cache (cache stampede, fallback).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é cache distribuído | — |
| **1** | Ouvi falar de Redis, sem saber usar | Nomeio o Redis como ferramenta de cache |
| **2** | Uso Redis como cache key-value simples | Cacheei dados no Redis seguindo tutorial |
| **3** | Uso as estruturas do Redis adequadamente; implemento cache distribuído | Usei estruturas do Redis (hash, sorted set) apropriadamente |
| **4** | Projeto para falha de cache (stampede, fallback); uso Redis para locks/rate limiting | Resolvi cache stampede e usei Redis além de cache simples |
| **5** | Ensino cache distribuído; reconheço uso subótimo; domino Redis internals e padrões avançados | Estabeleci a arquitetura de cache distribuído de um produto |

---

## 7.3 Otimização de Queries e o Problema N+1

**Conceito + por que existe:** Identificar e eliminar o anti-padrão N+1 (uma query para a lista + N queries para cada item) e outras ineficiências de acesso a dados. Existe porque o N+1 é o problema de performance mais comum em aplicações com ORM, transformando uma operação que deveria ser uma query em centenas.

**Profundidade esperada:** Avançado · **Conexões:** → SQL (4.2), → GraphQL (3.2), → Performance geral

**Erro de iniciante → Marca do sênior:** O iniciante usa ORM ingenuamente e gera N+1 sem perceber (o código parece limpo, mas faz 500 queries). O sênior reconhece N+1 por inspeção, usa eager loading / dataloaders, e monitora o número de queries por requisição.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é o problema N+1 | — |
| **1** | Ouvi falar, sem entender | Explico vagamente que "muitas queries são ruins" |
| **2** | Gero N+1 sem perceber; não monitoro queries | Já tive uma listagem lenta por N+1 sem saber |
| **3** | Reconheço N+1; uso eager loading para resolver | Resolvi um N+1 com eager loading / JOIN |
| **4** | Antecipo N+1; projeto acesso a dados eficiente; uso dataloaders | Desenhei o acesso a dados de uma feature evitando N+1 |
| **5** | Ensino otimização de acesso; reconheço anti-padrões por inspeção; domino estratégias de batching | Estabeleci padrões de acesso a dados eficiente de um time |

---

## 7.4 Profiling e Identificação de Gargalos

**Conceito + por que existe:** As técnicas e ferramentas para medir onde o tempo e os recursos são gastos — profiling de CPU, memória, queries, e APM. Existe porque otimizar sem medir é adivinhação; o gargalo real é frequentemente diferente do que a intuição sugere, e profiling revela onde investir esforço.

**Profundidade esperada:** Avançado · **Conexões:** → Todas as competências de performance, → Observabilidade (Camada 9), → Web Vitals (Front-End 6.4)

**Erro de iniciante → Marca do sênior:** O iniciante otimiza por intuição, frequentemente o lugar errado. O sênior mede primeiro com profiling, identifica o gargalo real (regra de Amdahl: otimizar o que domina o tempo), e valida o ganho após a otimização.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é profiling | — |
| **1** | Sei que dá para medir performance, sem saber como | Explico que "dá para ver o que está lento" |
| **2** | Adiciono logs de tempo manualmente; não uso profiler | Medi tempo com prints/logs |
| **3** | Uso profilers; identifico gargalos com dados | Usei um profiler para encontrar a função mais lenta |
| **4** | Projeto a estratégia de medição; identifico o gargalo dominante; valido otimizações | Otimizei um sistema medindo antes/depois com profiling |
| **5** | Ensino profiling; reconheço otimização prematura; domino as ferramentas e a regra de Amdahl | Estabeleci a prática de otimização baseada em dados de um time |

> *Conexão com seu diagnóstico (Eixo 1): sua "intuição de performance" declarada precisa desta competência como validação. Profiling é o que transforma intuição em conhecimento verificado.*

---

# CAMADA 8 — Sistemas Distribuídos e Escalabilidade

> *Onde o Back-End encontra sua maior complexidade. Falhas parciais, consistência e o teorema CAP. A fronteira do especialista.*

**Referência base:**
> **[PEER-REVIEWED]**
> Gilbert, S., & Lynch, N. (2002). *Brewer's Conjecture and the Feasibility of Consistent, Available, Partition-Tolerant Web Services.* ACM SIGACT News, 33(2), 51–59. DOI: 10.1145/564585.564601 — prova formal do teorema CAP.

> **[CLÁSSICO]**
> Kleppmann, M. (2017). *Designing Data-Intensive Applications.* O'Reilly. — Parte II (capítulos 5-9) é a referência definitiva para sistemas distribuídos.

---

## 8.1 Teorema CAP e Consistência

**Conceito + por que existe:** O teorema que prova que um sistema distribuído não pode garantir simultaneamente Consistência, Disponibilidade e tolerância a Partição — você escolhe dois sob partição. Existe porque é a restrição fundamental de sistemas distribuídos, e entendê-la é pré-requisito para qualquer decisão de arquitetura distribuída.

**Profundidade esperada:** Avançado · **Conexões:** → Replicação (8.3), → Transações (4.3), → CAP (Seção 3 do README de arquitetura)

**Erro de iniciante → Marca do sênior:** O iniciante assume que sistemas distribuídos podem ser sempre consistentes e disponíveis. O sênior entende o teorema CAP, escolhe conscientemente entre CP e AP pelo requisito do domínio, e entende os modelos de consistência (forte, eventual, causal).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço o teorema CAP | — |
| **1** | Ouvi falar de CAP, sem entender | Cito as três letras de CAP |
| **2** | Sei que existe um trade-off, sem aplicá-lo | Explico vagamente "consistência vs disponibilidade" |
| **3** | Entendo CAP; entendo consistência forte vs eventual | Expliquei por que um sistema escolheu eventual consistency |
| **4** | Aplico CAP em decisões de arquitetura; escolho CP/AP pelo domínio | Justifiquei uma escolha de consistência por requisito de negócio |
| **5** | Ensino CAP e consistência; reconheço escolhas inadequadas; domino PACELC e modelos de consistência | Projetei a estratégia de consistência de um sistema distribuído |

> *Conexão com seu background matemático: o teorema CAP (Gilbert & Lynch, 2002) é um invariante arquitetural com prova formal — exatamente o tipo de conhecimento que sua formação permite dominar profundamente.*

---

## 8.2 Escalabilidade Horizontal e Load Balancing

**Conceito + por que existe:** Escalar adicionando mais instâncias (horizontal) em vez de máquinas maiores (vertical), e distribuir carga entre elas (load balancing). Existe porque a escala vertical tem limite físico e custo crescente, enquanto a horizontal é a base de sistemas que atendem milhões — mas exige que o serviço seja stateless.

**Profundidade esperada:** Avançado · **Conexões:** → Estado (sessões 5.2), → Replicação (8.3), → Cache distribuído (7.2)

**Erro de iniciante → Marca do sênior:** O iniciante mantém estado nas instâncias (sessão em memória local), impedindo escala horizontal. O sênior projeta serviços stateless, externaliza estado (cache/banco compartilhado), e entende as estratégias de load balancing.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei a diferença entre escala horizontal e vertical | — |
| **1** | Ouvi falar de escalar, sem saber como | Explico que "dá para colocar mais servidores" |
| **2** | Sei que existe load balancer, sem entender stateless | Já mantive sessão em memória local sem perceber o problema |
| **3** | Projeto serviços stateless; entendo load balancing | Tornei um serviço stateless externalizando a sessão |
| **4** | Projeto a estratégia de escala horizontal; escolho algoritmo de balanceamento; antecipo gargalos | Desenhei a arquitetura de escala horizontal de um serviço |
| **5** | Ensino escalabilidade; reconheço estado mal colocado; domino auto-scaling e estratégias de LB | Estabeleci a estratégia de escalabilidade de um produto |

---

## 8.3 Replicação e Sharding de Dados

**Conceito + por que existe:** As técnicas para escalar a camada de dados — replicação (cópias para disponibilidade e leitura) e sharding (particionar dados entre nós para escala de escrita). Existe porque um único banco tem limite de capacidade, e essas técnicas distribuem dados — mas introduzem complexidade de consistência e roteamento.

**Profundidade esperada:** Avançado · **Conexões:** → CAP (8.1), → Banco (Camada 4), → Escalabilidade (8.2)

**Erro de iniciante → Marca do sênior:** O iniciante não considera replicação até o banco ser gargalo, ou faz sharding com chave errada (hotspots). O sênior entende replicação (síncrona vs assíncrona, lag), escolhe a chave de sharding cuidadosamente, e antecipa os problemas de distribuição.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço replicação e sharding | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "copiar e dividir dados" |
| **2** | Sei que existem, sem saber as implicações | Nomeio replicação ou sharding |
| **3** | Entendo replicação (leader-follower) e sharding; configuro réplicas de leitura | Configurei réplicas de leitura para um banco |
| **4** | Projeto a estratégia de distribuição; escolho a chave de sharding; antecipo lag e hotspots | Desenhei o particionamento de dados de um sistema em escala |
| **5** | Ensino distribuição de dados; reconheço chaves de sharding ruins; domino consensus e replicação | Estabeleci a arquitetura de dados distribuída de um produto |

---

## 8.4 Padrões de Resiliência (circuit breaker, retry, bulkhead)

**Conceito + por que existe:** Os padrões que mantêm um sistema funcionando apesar de falhas de dependências — circuit breaker (parar de chamar um serviço que está falhando), retry com backoff, timeout, bulkhead (isolar falhas). Existem porque em sistemas distribuídos as dependências falham, e sem esses padrões uma falha em cascata derruba o sistema inteiro.

**Profundidade esperada:** Avançado · **Conexões:** → Sistemas distribuídos (toda a camada), → Tratamento de erros (Front-End 5.4), → SRE (Camada 9)

**Erro de iniciante → Marca do sênior:** O iniciante chama dependências sem timeout nem retry, e uma falha trava ou derruba o sistema (cascading failure). O sênior implementa circuit breakers, retry com backoff exponencial e jitter, timeouts, e bulkheads para conter falhas.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço padrões de resiliência | — |
| **1** | Sei que sistemas podem falhar, sem saber os padrões | Explico que "tem que tratar falha" |
| **2** | Adiciono try/catch; não uso timeout nem retry estruturado | Já tive uma falha em cascata sem proteção |
| **3** | Implemento retry com backoff e timeout; entendo circuit breaker | Implementei retry com backoff exponencial |
| **4** | Projeto a estratégia de resiliência; uso circuit breaker e bulkhead; antecipo falhas em cascata | Desenhei a resiliência de um serviço com circuit breaker |
| **5** | Ensino padrões de resiliência; reconheço pontos de falha em cascata; domino chaos engineering | Estabeleci a estratégia de resiliência de um sistema distribuído |

> *Conexão com seu diagnóstico (Eixo 4): esta camada é a manifestação, em escala distribuída, do "raciocínio sobre falhas" identificado como gap. É o coração do que separa o pleno do sênior.*

---

# CAMADA 9 — Observabilidade e Confiabilidade

> *Você não pode operar o que não pode ver. A diferença entre descobrir um problema em segundos ou em dias.*

**Referência base:**
> **[INDUSTRIAL]**
> Beyer, B., Jones, C., Petoff, J., & Murphy, N. R. (Eds.) (2016). *Site Reliability Engineering.* O'Reilly.
> URL: https://sre.google/sre-book/
> — A referência definitiva para confiabilidade, SLIs/SLOs, e operação de sistemas em escala.

---

## 9.1 Logging Estruturado

**Conceito + por que existe:** Registrar eventos do sistema de forma estruturada (JSON) e pesquisável, com contexto suficiente para diagnóstico — sem expor dados sensíveis. Existe porque, quando algo dá errado em produção, os logs são frequentemente a única forma de reconstruir o que aconteceu.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Segurança (Camada 10), → Tracing (9.3), → Logging (Guia de Segurança)

**Erro de iniciante → Marca do sênior:** O iniciante loga strings não-estruturadas (ou nada), e frequentemente vaza dados sensíveis nos logs. O sênior usa logging estruturado com níveis apropriados, contexto correlacionável (request ID), e nunca loga segredos ou PII.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei a importância de logs | — |
| **1** | Uso prints/console para debug, sem estratégia | Adiciono prints quando algo dá errado |
| **2** | Logo strings; não estruturo nem penso em dados sensíveis | Já loguei dados que não deveria |
| **3** | Uso logging estruturado com níveis; correlaciono com request ID | Implementei logs estruturados em JSON com request ID |
| **4** | Projeto a estratégia de logging; balanceio verbosidade vs custo; protejo dados sensíveis | Desenhei a estratégia de logs de um serviço sem vazar PII |
| **5** | Ensino logging; reconheço logs inúteis ou perigosos; domino agregação e correlação | Estabeleci a estratégia de observabilidade de logs de um produto |

---

## 9.2 Métricas e Monitoramento

**Conceito + por que existe:** Coletar e visualizar métricas quantitativas do sistema (latência, throughput, taxa de erro, uso de recursos) e alertar sobre anomalias. Existe porque logs mostram eventos individuais, mas métricas mostram tendências e o estado de saúde agregado — e alertas avisam antes que usuários percebam.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Logging (9.1), → SLO (9.4), → Performance (Camada 7)

**Erro de iniciante → Marca do sênior:** O iniciante não tem métricas e descobre problemas pelos usuários reclamando. O sênior instrumenta métricas-chave (os "quatro sinais de ouro": latência, tráfego, erros, saturação), cria dashboards, e configura alertas acionáveis.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que são métricas de sistema | — |
| **1** | Sei que dá para monitorar, sem saber o quê | Explico que "dá para ver se o sistema está bem" |
| **2** | Olho métricas básicas da plataforma; não instrumento as minhas | Vi CPU/memória num painel da cloud |
| **3** | Instrumento métricas-chave; crio dashboards; configuro alertas | Instrumentei latência e taxa de erro de um serviço |
| **4** | Projeto a estratégia de monitoramento; uso os golden signals; alertas acionáveis | Desenhei o monitoramento de um serviço com alertas baseados em sintomas |
| **5** | Ensino monitoramento; reconheço métricas e alertas ruins; domino RED/USE e cardinality | Estabeleci a estratégia de métricas de um produto |

---

## 9.3 Distributed Tracing

**Conceito + por que existe:** Rastrear uma requisição através de múltiplos serviços, vendo o caminho completo e onde o tempo foi gasto (OpenTelemetry, Jaeger). Existe porque em arquiteturas distribuídas uma requisição passa por muitos serviços, e sem tracing é impossível saber qual serviço causou a lentidão ou o erro.

**Profundidade esperada:** Intermediário · **Conexões:** → Logging (9.1), → Microsserviços (Middle-End), → Resiliência (8.4)

**Erro de iniciante → Marca do sênior:** O iniciante depura sistemas distribuídos olhando logs de cada serviço isoladamente. O sênior usa distributed tracing com trace IDs propagados, vendo a requisição inteira de ponta a ponta e identificando o serviço problemático rapidamente.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é distributed tracing | — |
| **1** | Ouvi falar, sem saber o que faz | Explico que "dá para seguir a requisição" |
| **2** | Sei que existe, sem usar | Nomeio uma ferramenta (Jaeger/OpenTelemetry) |
| **3** | Implemento tracing; propago trace IDs; leio traces | Instrumentei tracing num serviço e segui uma requisição |
| **4** | Projeto a estratégia de tracing; instrumento spans significativos; correlaciono com logs/métricas | Desenhei o tracing de um fluxo distribuído ponta a ponta |
| **5** | Ensino tracing; reconheço instrumentação inadequada; domino OpenTelemetry e sampling | Estabeleci a estratégia de tracing de um sistema de microsserviços |

---

## 9.4 SLIs, SLOs e Confiabilidade (SRE)

**Conceito + por que existe:** A disciplina de definir e medir confiabilidade de forma quantitativa — SLIs (indicadores), SLOs (objetivos), e error budgets. Existe porque "confiável" é subjetivo até ser medido; SLOs dão um alvo numérico que equilibra confiabilidade com velocidade de desenvolvimento (error budget).

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Métricas (9.2), → Resiliência (8.4), → SRE (referência base)

**Erro de iniciante → Marca do sênior:** O iniciante não tem metas de confiabilidade definidas, ou busca 100% (impossível e contraproducente). O sênior define SLIs/SLOs alinhados ao negócio, usa error budgets para equilibrar confiabilidade vs features, e entende que confiabilidade tem custo crescente.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço SLI/SLO | — |
| **1** | Ouvi falar de SLA, sem entender SLI/SLO | Explico vagamente "garantia de uptime" |
| **2** | Sei que existem metas de confiabilidade, sem defini-las | Nomeio o conceito de SLA |
| **3** | Defino SLIs e SLOs básicos; meço confiabilidade | Defini um SLO de disponibilidade e o medi |
| **4** | Projeto a estratégia de confiabilidade; uso error budgets; alinho SLOs ao negócio | Desenhei SLOs e error budget de um serviço |
| **5** | Ensino SRE; reconheço metas inadequadas; domino a filosofia de error budget e toil | Estabeleci a prática de confiabilidade (SRE) de uma organização |

---

# CAMADA 10 — Segurança de Backend

> *A fronteira de defesa. Onde o sistema encontra atacantes ativos. (Aprofundada no Guia de Segurança.)*

**Referência base:**
> **[INDUSTRIAL-OWASP]**
> OWASP API Security Top 10 (2023 edition).
> URL: https://owasp.org/API-Security/editions/2023/en/0x11-t10/
> — Os dez riscos de segurança mais críticos específicos de APIs. BOLA (Broken Object Level Authorization) é o #1 desde 2019, presente em ~40% dos ataques a APIs.

---

## 10.1 Validação de Input e Prevenção de Injeção

**Conceito + por que existe:** Tratar todo input externo como não-confiável — validar, sanitizar, e usar queries parametrizadas para prevenir injeção (SQL injection, command injection). Existe porque input não validado usado em queries ou comandos permite que atacantes executem código arbitrário — uma das classes de vulnerabilidade mais antigas e ainda mais comuns.

**Profundidade esperada:** Avançado · **Conexões:** → APIs (Camada 3), → Banco (Camada 4), → OWASP, → Validação de input (Guia de Segurança)

**Erro de iniciante → Marca do sênior:** O iniciante concatena input em queries SQL (`"SELECT * WHERE id=" + userInput`), criando SQL injection. O sênior usa exclusivamente queries parametrizadas/prepared statements, valida input contra schema, e trata toda fronteira de confiança.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é injeção | — |
| **1** | Ouvi falar de SQL injection, sem entender o mecanismo | Explico que "input malicioso é perigoso" |
| **2** | Sei que não devo confiar em input, mas já concatenei em query | Já construí uma query com concatenação de string |
| **3** | Uso queries parametrizadas sempre; valido input | Usei prepared statements e validação de schema |
| **4** | Projeto defesa em profundidade contra injeção; valido em todas as fronteiras | Auditei uma aplicação contra vetores de injeção |
| **5** | Ensino prevenção de injeção; reconheço código vulnerável por inspeção; domino os vetores | Estabeleci os padrões de validação e prevenção de injeção de um time |

---

## 10.2 Gestão de Segredos e Criptografia

**Conceito + por que existe:** Como armazenar e usar credenciais, chaves e dados sensíveis de forma segura — gestão de segredos (vault), criptografia em trânsito (TLS) e em repouso. Existe porque segredos hardcoded ou dados sensíveis em texto plano são vetores diretos de comprometimento, e a exposição de credenciais é a causa mais evitável de breaches.

**Profundidade esperada:** Avançado · **Conexões:** → Autenticação (Camada 5), → Gestão de segredos (Guia de Segurança)

**Erro de iniciante → Marca do sênior:** O iniciante hardcoda credenciais no código e as comita no Git. O sênior usa gestão de segredos (variáveis de ambiente no mínimo, vault idealmente), nunca comita segredos, criptografa dados sensíveis, e rotaciona credenciais.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não penso em gestão de segredos | — |
| **1** | Sei que não devo expor senhas, sem método | Explico que "senhas não podem vazar" |
| **2** | Uso variáveis de ambiente às vezes; já hardcodei segredos | Já comitei uma credencial no código |
| **3** | Externalizo segredos via env; criptografo dados sensíveis; uso TLS | Movi segredos para variáveis de ambiente e .gitignore |
| **4** | Projeto a gestão de segredos (vault, rotação); criptografo em repouso e trânsito | Desenhei a gestão de segredos de uma aplicação com vault |
| **5** | Ensino gestão de segredos; reconheço exposições; domino criptografia aplicada e key management | Estabeleci a arquitetura de segredos de um produto |

> *Conexão com seu diagnóstico de segurança: este é o gap crítico identificado (credenciais às vezes hardcoded + acesso a produção). É a Prioridade 1 do seu plano de ação.*

---

## 10.3 Segurança de APIs (OWASP API Top 10)

**Conceito + por que existe:** Os riscos de segurança específicos de APIs e suas defesas — BOLA, broken authentication, excessive data exposure, e os demais do OWASP API Security Top 10. Existe porque APIs têm uma superfície de ataque distinta de aplicações web tradicionais, e os vetores mais comuns (autorização em nível de objeto) são específicos de APIs.

**Profundidade esperada:** Avançado · **Conexões:** → Autorização (5.4), → Validação (10.1), → Rate limiting (3.4)

**Erro de iniciante → Marca do sênior:** O iniciante expõe endpoints sem verificar autorização em nível de objeto (BOLA) e retorna dados em excesso. O sênior verifica autorização para cada objeto, retorna apenas os campos necessários, e conhece e mitiga os dez riscos do OWASP API Security Top 10.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço riscos de segurança de API | — |
| **1** | Sei que APIs têm riscos, sem conhecê-los | Explico que "APIs podem ser atacadas" |
| **2** | Implemento APIs sem pensar nos vetores específicos | Já expus um endpoint sem checar acesso ao objeto |
| **3** | Conheço os principais riscos; verifico autorização de objeto; limito exposição de dados | Implementei verificação anti-BOLA num endpoint |
| **4** | Projeto APIs seguras por design; mitigo o OWASP API Top 10; faço threat modeling | Auditei uma API contra o OWASP API Security Top 10 |
| **5** | Ensino segurança de API; reconheço os vetores por inspeção; domino o cenário de ameaças | Estabeleci os padrões de segurança de API de uma organização |

---

## 10.4 Princípio do Menor Privilégio e Superfície de Ataque

**Conceito + por que existe:** Conceder a cada componente, serviço e credencial apenas o acesso mínimo necessário, e minimizar os pontos de entrada exploráveis. Existe porque, quando um componente é comprometido, o princípio do menor privilégio limita o dano (blast radius), e reduzir a superfície de ataque reduz as oportunidades de exploração.

**Profundidade esperada:** Avançado · **Conexões:** → Autorização (5.4), → Zero Trust (Guia de Segurança), → Infra/DevOps

**Erro de iniciante → Marca do sênior:** O iniciante dá permissões amplas "por conveniência" (banco com superusuário, serviço com acesso total). O sênior aplica o menor privilégio em cada nível (credenciais de banco com escopo mínimo, serviços isolados), e minimiza a superfície de ataque fechando o que não é necessário.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço o princípio do menor privilégio | — |
| **1** | Ouvi falar, sem aplicar | Explico que "dar só o acesso necessário" |
| **2** | Dou permissões amplas por conveniência | Já usei um superusuário de banco na aplicação |
| **3** | Aplico menor privilégio em credenciais e acessos | Criei um usuário de banco com permissões mínimas |
| **4** | Projeto para menor privilégio e superfície mínima; isolo componentes | Desenhei o acesso de um sistema seguindo menor privilégio |
| **5** | Ensino menor privilégio; reconheço permissões excessivas; domino Zero Trust e isolamento | Estabeleci a arquitetura de acesso mínimo de um produto |

> *Conexão topológica: a superfície de ataque é uma propriedade topológica do sistema (conjunto de pontos de entrada). Reduzi-la é uma operação topológica — conecta diretamente ao argumento da Seção 3 do README de arquitetura.*

---

# Planilha de Auto-Auditoria — Back-End

Registre seu nível (0-5) em cada competência. **Regra:** não marque um nível sem passar no teste de validação. Anote a evidência concreta.

## Camada 1 — Fundamentos de Runtime e Concorrência

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 1.1 Processo, Threads e Concorrência | ___ | |
| 1.2 Memória e Garbage Collection | ___ | |
| 1.3 I/O: Blocking vs Non-blocking | ___ | |
| 1.4 Modelo de Execução do Runtime | ___ | |

## Camada 2 — Protocolos e Comunicação de Rede

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 2.1 HTTP a Fundo | ___ | |
| 2.2 TCP/IP e Modelo de Rede | ___ | |
| 2.3 RPC e Streaming (gRPC, WS, SSE) | ___ | |
| 2.4 Serialização e Formatos | ___ | |

## Camada 3 — Arquitetura de APIs

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 3.1 Design de API REST | ___ | |
| 3.2 GraphQL | ___ | |
| 3.3 Versionamento e Evolução | ___ | |
| 3.4 Validação, Paginação, Rate Limiting | ___ | |

## Camada 4 — Persistência e Bancos de Dados

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 4.1 Modelagem de Dados | ___ | |
| 4.2 SQL e Query Optimization | ___ | |
| 4.3 Transações, ACID, Concorrência | ___ | |
| 4.4 NoSQL e Escolha de Banco | ___ | |

## Camada 5 — Autenticação e Autorização

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 5.1 Identidade e Autenticação | ___ | |
| 5.2 Sessões, Tokens e JWT | ___ | |
| 5.3 OAuth 2.0 e OpenID Connect | ___ | |
| 5.4 Autorização (RBAC/ABAC) | ___ | |

## Camada 6 — Processamento Assíncrono e Mensageria

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 6.1 Jobs Assíncronos | ___ | |
| 6.2 Filas e Brokers | ___ | |
| 6.3 Padrões de Mensageria | ___ | |
| 6.4 Garantias de Entrega e Idempotência | ___ | |

## Camada 7 — Cache e Otimização de Performance

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 7.1 Estratégias de Cache | ___ | |
| 7.2 Cache Distribuído (Redis) | ___ | |
| 7.3 Otimização de Queries e N+1 | ___ | |
| 7.4 Profiling e Gargalos | ___ | |

## Camada 8 — Sistemas Distribuídos e Escalabilidade

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 8.1 Teorema CAP e Consistência | ___ | |
| 8.2 Escalabilidade Horizontal e LB | ___ | |
| 8.3 Replicação e Sharding | ___ | |
| 8.4 Padrões de Resiliência | ___ | |

## Camada 9 — Observabilidade e Confiabilidade

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 9.1 Logging Estruturado | ___ | |
| 9.2 Métricas e Monitoramento | ___ | |
| 9.3 Distributed Tracing | ___ | |
| 9.4 SLIs, SLOs e Confiabilidade | ___ | |

## Camada 10 — Segurança de Backend

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 10.1 Validação de Input e Injeção | ___ | |
| 10.2 Gestão de Segredos e Criptografia | ___ | |
| 10.3 Segurança de APIs (OWASP) | ___ | |
| 10.4 Menor Privilégio e Superfície de Ataque | ___ | |

---

## Interpretação do Resultado

Após preencher, observe o **perfil de distribuição** com os mesmos critérios do Front-End, ajustados para o Back-End:

- **Especialista em Back-End** significa **nível 4+ consistente nas camadas 1-5** (substrato, construção e dados) e **nível 4+ no tier de escala (camadas 6-8)** — porque é justamente o domínio de sistemas distribuídos que separa o sênior de Back-End do desenvolvedor de APIs CRUD. As camadas 9-10 (produção/segurança) devem estar em nível 3+.

- **O tier de escala (6-8) é o divisor de águas.** Muitos desenvolvedores constroem APIs competentes (camadas 1-5) mas nunca operaram sistemas distribuídos reais. A régua de especialista exige domínio de filas, cache distribuído, CAP, replicação e resiliência.

- **Camadas 1-2 são pré-requisito absoluto.** Não é possível ser nível 4 em Sistemas Distribuídos (Camada 8) sem nível 4 em Concorrência e Rede (camadas 1-2) — distribuição é concorrência e rede levadas à escala.

- **Para o seu perfil específico:** suas conexões mais fortes prováveis estão onde a matemática encontra sistemas — o teorema CAP (8.1) como invariante formal, e o raciocínio sobre concorrência (1.1). Seus gaps prováveis, consistentes com o diagnóstico, estão em segurança (10.2 — gestão de segredos) e nas práticas de produção (camada 9 — observabilidade), que dependem de exposição operacional mais do que de fundamentos teóricos.

---

## Referências

| # | Fonte | Tipo | Uso |
|---|-------|------|-----|
| 1 | Dreyfus & Dreyfus (1980). *Five-Stage Model of Skill Acquisition.* UC Berkeley. | **PEER-REVIEWED** | Escala de progressão |
| 2 | Smith & Kendall (1963). *Retranslation of Expectations.* JAP, 47(2). DOI: 10.1037/h0047060 | **PEER-REVIEWED** | Âncoras comportamentais (BARS) |
| 3 | Kruger & Dunning (1999). *Unskilled and Unaware of It.* JPSP, 77(6). | **PEER-REVIEWED** | Viés de auto-avaliação |
| 4 | Kleppmann, M. (2017). *Designing Data-Intensive Applications.* O'Reilly. | **CLÁSSICO** | Camadas 4, 6, 7, 8 (dados e distribuição) |
| 5 | Bryant & O'Hallaron (2015). *Computer Systems: A Programmer's Perspective* (3rd ed.). | **CLÁSSICO** | Camada 1 (runtime, concorrência) |
| 6 | Fielding, R. T. (2000). *Architectural Styles.* PhD Dissertation, UC Irvine. | **PEER-REVIEWED** | Camada 3 (REST) |
| 7 | Gilbert & Lynch (2002). *Brewer's Conjecture.* ACM SIGACT News, 33(2). DOI: 10.1145/564585.564601 | **PEER-REVIEWED** | Camada 8.1 (CAP) |
| 8 | NIST SP 800-63B (2017). *Digital Identity Guidelines.* DOI: 10.6028/NIST.SP.800-63b | **PADRÃO-NIST** | Camada 5 (autenticação) |
| 9 | Hardt, D. (2012). *RFC 6749: OAuth 2.0.* IETF. | **PADRÃO-IETF** | Camada 5.3 (OAuth) |
| 10 | Beyer et al. (2016). *Site Reliability Engineering.* O'Reilly. https://sre.google/sre-book/ | **INDUSTRIAL** | Camada 9 (observabilidade, SRE) |
| 11 | OWASP API Security Top 10 (2023). https://owasp.org/API-Security/ | **INDUSTRIAL-OWASP** | Camada 10 (segurança de API) |

---

*Parte 1B de 3 do Skill-Check de Engenharia de Software. Concluídas: Front-End e Back-End. Próximas sub-áreas: Middle-End/Integração e Infraestrutura/DevOps.*
*Escala ancorada em Dreyfus (1980) + BARS (Smith & Kendall, 1963). Auto-avaliação deve ser complementada por validação externa de pares seniores (Kruger & Dunning, 1999).*
*Revisão recomendada a cada 6 meses, registrando a evolução de nível e a nova evidência concreta.*
