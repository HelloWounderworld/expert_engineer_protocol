# Skill-Check de Engenharia de Software — Parte 1C: Middle-End / Integração
## Arquitetura Completa de Competências com Escala Dreyfus Ancorada

> *"The fundamental theorem of software engineering: we can solve any problem by introducing an extra level of indirection — except the problem of too many levels of indirection."*
> — Andrew Koenig (parafraseado)

---

## Como Este Documento Funciona

Este é o mapa de competências da sub-área **Middle-End / Camada de Integração** — a camada que conecta front-end, back-end e infraestrutura. É o terceiro documento da Parte 1 (após Front-End e Back-End).

**Diferença importante em relação ao Back-End:** o Back-End cobriu os *mecanismos* (como usar uma fila, como funciona um cache, o que é o teorema CAP). O Middle-End cobre a *arquitetura de integração* — como decompor um sistema em serviços, como definir os contratos entre eles, e como coordená-los. É a diferença entre "saber usar RabbitMQ" (Back-End) e "saber quando dois pedaços do sistema devem ser serviços separados e como eles devem conversar" (Middle-End).

Por ser um domínio mais focado, esta sub-área tem **7 camadas** (vs 10 do Front-End e Back-End). Cada camada mantém o formato: 4 competências com conceito, por que existe, profundidade, conexões, erro/sênior, e progressão Dreyfus completa (0-5) com teste de validação.

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
| **5** | Expert | Ensino, reconheço quando o padrão está errado |

---

## Visão Geral das 7 Camadas

```
TIER COORDENAÇÃO (como os serviços trabalham juntos)
  CAMADA 7 · Service Mesh e Preocupações Transversais
  CAMADA 6 · Orquestração vs Coreografia
  CAMADA 5 · Arquitetura Orientada a Eventos

TIER CONTRATO (como os serviços conversam)
  CAMADA 4 · Contratos, Versionamento e Compatibilidade
  CAMADA 3 · API Gateway, BFF e Composição
  CAMADA 2 · Estilos de Comunicação Inter-Serviços

TIER FRONTEIRA (onde começam e terminam os serviços)
  CAMADA 1 · Decomposição de Serviços e Domain-Driven Design
```

A lógica: tudo começa na **decomposição** (onde estão as fronteiras dos serviços) — a decisão mais difícil e mais cara de errar. Sobre ela se constroem os **contratos** (como os serviços conversam) e a **coordenação** (como trabalham juntos). Uma decomposição errada contamina tudo acima.

**Referências base de toda a arquitetura de integração:**
> **[CLÁSSICO]**
> Evans, E. (2003). *Domain-Driven Design: Tackling Complexity in the Heart of Software.* Addison-Wesley.
> — A referência para decomposição de domínio, bounded contexts e a linguagem ubíqua que fundamenta as fronteiras de serviço.

> **[CLÁSSICO]**
> Newman, S. (2021). *Building Microservices: Designing Fine-Grained Systems* (2nd ed.). O'Reilly.
> — A referência definitiva para arquitetura de microsserviços e integração.

> **[CLÁSSICO]**
> Hohpe, G., & Woolf, B. (2003). *Enterprise Integration Patterns.* Addison-Wesley.
> — O catálogo canônico de padrões de integração e mensageria.

---

# CAMADA 1 — Decomposição de Serviços e Domain-Driven Design

> *A fronteira. A decisão mais difícil e cara de toda arquitetura de integração: onde um serviço termina e o outro começa.*

---

## 1.1 Bounded Contexts e Fronteiras de Serviço

**Conceito + por que existe:** Um bounded context é uma fronteira explícita dentro da qual um modelo de domínio é consistente e tem significado único. Existe porque a decisão de onde dividir um sistema em serviços determina todo o resto — fronteiras erradas geram acoplamento, chamadas excessivas entre serviços, e mudanças que atravessam múltiplos serviços.

**Profundidade esperada:** Avançado · **Conexões:** → Decomposição (1.2), → Comunicação (Camada 2), → Modelo de componentes (Front-End 3.1)

**Erro de iniciante → Marca do sênior:** O iniciante decompõe por camada técnica (serviço de banco, serviço de UI) ou por entidade (serviço de usuário, serviço de pedido) sem analisar o domínio. O sênior decompõe por bounded context — agrupando o que muda junto e tem coesão de domínio, minimizando a comunicação entre serviços.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é bounded context | — |
| **1** | Ouvi falar de DDD, sem entender bounded contexts | Explico vagamente que "sistemas se dividem em partes" |
| **2** | Divido sistemas por entidades ou camadas técnicas | Já criei "serviço de usuário, serviço de produto" sem analisar |
| **3** | Identifico bounded contexts; decomponho por coesão de domínio | Decompus um sistema por contextos de negócio, não por entidades |
| **4** | Projeto fronteiras minimizando acoplamento entre serviços; uso context mapping | Desenhei fronteiras de serviço analisando o domínio e o acoplamento |
| **5** | Ensino DDD estratégico; reconheço fronteiras mal traçadas; domino context mapping e subdomínios | Estabeleci a arquitetura de decomposição de um sistema complexo |

---

## 1.2 Granularidade de Serviços (Monolito, Microsserviços, Modular)

**Conceito + por que existe:** A decisão sobre quão fino dividir o sistema — monolito (tudo junto), monolito modular (módulos com fronteiras internas), microsserviços (serviços independentes). Existe porque granularidade tem trade-offs profundos: microsserviços dão independência mas adicionam complexidade distribuída; o monolito é simples mas pode virar acoplado.

**Profundidade esperada:** Avançado · **Conexões:** → Bounded contexts (1.1), → Sistemas distribuídos (Back-End 8), → Complexidade (Seção 3 do README)

**Erro de iniciante → Marca do sênior:** O iniciante adota microsserviços por hype, herdando toda a complexidade distribuída sem necessidade ("distributed monolith"). O sênior entende que microsserviços são uma solução para problemas organizacionais e de escala específicos, e frequentemente começa com um monolito modular.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei a diferença entre monolito e microsserviços | — |
| **1** | Ouvi falar de microsserviços, sem entender os trade-offs | Explico que "microsserviços são serviços separados" |
| **2** | Acho que microsserviços são sempre melhores | Já quis usar microsserviços por serem "modernos" |
| **3** | Entendo os trade-offs; escolho a granularidade pelo contexto | Argumentei por monolito modular em vez de microsserviços |
| **4** | Projeto a granularidade pela necessidade real (escala, times); evito distributed monolith | Desenhei a estratégia de granularidade de um sistema justificada |
| **5** | Ensino granularidade de serviços; reconheço distributed monolith; domino a evolução monolito→serviços | Liderei a decisão arquitetural de granularidade de um produto |

---

## 1.3 Acoplamento e Coesão entre Serviços

**Conceito + por que existe:** Os princípios que medem a qualidade da decomposição — baixo acoplamento (serviços independentes) e alta coesão (cada serviço com responsabilidade única). Existe porque acoplamento e coesão são os indicadores fundamentais de uma boa arquitetura: serviços muito acoplados não dão independência; serviços sem coesão fazem coisas demais.

**Profundidade esperada:** Avançado · **Conexões:** → Bounded contexts (1.1), → Contratos (Camada 4), → Arquitetura (Seção 3)

**Erro de iniciante → Marca do sênior:** O iniciante cria serviços que compartilham banco de dados (acoplamento de dados) ou que precisam ser deployados juntos (acoplamento temporal). O sênior reconhece os tipos de acoplamento (dados, temporal, de implementação) e projeta para minimizá-los, mantendo cada serviço dono dos seus dados.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço acoplamento e coesão | — |
| **1** | Ouvi os termos, sem entender | Explico vagamente "serviços não devem depender muito" |
| **2** | Crio serviços acoplados sem perceber (banco compartilhado) | Já fiz dois serviços compartilharem o mesmo banco |
| **3** | Reconheço acoplamento; mantenho cada serviço dono dos seus dados | Separei bancos para desacoplar dois serviços |
| **4** | Projeto para baixo acoplamento; identifico os tipos de acoplamento; antecipo dependências | Desenhei serviços minimizando acoplamento de dados e temporal |
| **5** | Ensino acoplamento/coesão; reconheço arquiteturas acopladas; domino as métricas e padrões | Refatorei uma arquitetura acoplada em serviços independentes |

---

## 1.4 Estratégia de Dados Distribuídos (Database per Service)

**Conceito + por que existe:** O padrão de cada serviço ser dono exclusivo dos seus dados, sem acesso direto ao banco de outro serviço. Existe porque compartilhar banco entre serviços cria o acoplamento mais difícil de quebrar — qualquer mudança de schema afeta todos os serviços que acessam aquele banco, eliminando a independência.

**Profundidade esperada:** Avançado · **Conexões:** → Acoplamento (1.3), → Banco (Back-End 4), → Consistência distribuída (Camada 6)

**Erro de iniciante → Marca do sênior:** O iniciante deixa serviços acessarem o banco uns dos outros diretamente "para simplificar". O sênior mantém database-per-service, expõe dados via API, e resolve consultas que cruzam serviços com composição na API ou views materializadas — aceitando a complexidade em troca da independência.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é database-per-service | — |
| **1** | Ouvi falar, sem entender o porquê | Explico vagamente "cada serviço tem seu banco" |
| **2** | Deixo serviços acessarem o banco de outros | Já fiz um serviço ler a tabela de outro serviço |
| **3** | Mantenho database-per-service; exponho dados via API | Implementei serviços com bancos isolados e acesso via API |
| **4** | Projeto a estratégia de dados distribuídos; resolvo queries cross-service; aceito os trade-offs | Desenhei composição de dados de múltiplos serviços via API |
| **5** | Ensino estratégia de dados distribuídos; reconheço acoplamento de banco; domino CQRS e views materializadas | Estabeleci a arquitetura de dados distribuída de um produto |

---

# CAMADA 2 — Estilos de Comunicação Inter-Serviços

> *Como os serviços conversam. Síncrono ou assíncrono é a escolha que define a resiliência e o acoplamento temporal do sistema.*

---

## 2.1 Comunicação Síncrona vs Assíncrona

**Conceito + por que existe:** A escolha fundamental entre comunicação síncrona (o chamador espera a resposta) e assíncrona (o chamador continua, a resposta vem depois ou via evento). Existe porque essa escolha determina o acoplamento temporal: comunicação síncrona acopla a disponibilidade dos serviços (se B está fora, A falha); assíncrona desacopla mas adiciona complexidade.

**Profundidade esperada:** Avançado · **Conexões:** → Mensageria (Back-End 6), → Arquitetura de eventos (Camada 5), → Resiliência (Back-End 8.4)

**Erro de iniciante → Marca do sênior:** O iniciante usa chamadas síncronas (REST) para tudo, criando cadeias de dependência onde a falha de um serviço derruba todos. O sênior escolhe o estilo pelo acoplamento desejado — síncrono quando precisa de resposta imediata, assíncrono para desacoplar e resiliência.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei a diferença entre comunicação síncrona e assíncrona | — |
| **1** | Sei que existem, sem entender as implicações | Explico que "às vezes espera, às vezes não" |
| **2** | Uso REST síncrono para tudo | Já criei uma cadeia de chamadas síncronas entre serviços |
| **3** | Escolho síncrono vs assíncrono conscientemente | Usei mensageria para desacoplar dois serviços |
| **4** | Projeto a estratégia de comunicação pelo acoplamento temporal; antecipo falhas em cadeia | Desenhei a comunicação de um sistema escolhendo estilos por trade-off |
| **5** | Ensino estilos de comunicação; reconheço acoplamento temporal indevido; domino os padrões híbridos | Estabeleci a estratégia de comunicação inter-serviços de um produto |

---

## 2.2 Service Discovery e Roteamento

**Conceito + por que existe:** Como os serviços encontram uns aos outros dinamicamente em um ambiente onde instâncias sobem e descem (service registry, DNS, client-side vs server-side discovery). Existe porque, em sistemas distribuídos dinâmicos, endereços de serviço mudam constantemente, e hardcodar endereços é impossível.

**Profundidade esperada:** Intermediário · **Conexões:** → Comunicação (2.1), → Load balancing (Back-End 8.2), → Kubernetes (Infra)

**Erro de iniciante → Marca do sênior:** O iniciante hardcoda endereços de serviço ou IPs. O sênior usa service discovery (registry ou DNS), entende client-side vs server-side discovery, e projeta para instâncias dinâmicas.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é service discovery | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "serviços se encontram" |
| **2** | Hardcodo endereços ou uso config estática | Já hardcodei a URL de um serviço |
| **3** | Uso service discovery; entendo registry e DNS-based | Configurei descoberta de serviço num ambiente dinâmico |
| **4** | Projeto a estratégia de descoberta; escolho client vs server-side; integro com LB | Desenhei o roteamento e descoberta de um sistema de serviços |
| **5** | Ensino service discovery; reconheço configurações frágeis; domino os padrões e service mesh | Estabeleci a infraestrutura de descoberta de serviços de um produto |

---

## 2.3 Padrões de Integração (Enterprise Integration Patterns)

**Conceito + por que existe:** O catálogo de padrões para integrar sistemas via mensagens — message router, translator, aggregator, content-based router, etc. Existe porque a integração entre sistemas heterogêneos tem problemas recorrentes (rotear, transformar, agregar mensagens), e esses padrões são as soluções comprovadas.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Mensageria (Back-End 6), → Orquestração (Camada 6), → EIP (referência base)

**Erro de iniciante → Marca do sênior:** O iniciante reinventa lógica de integração ad-hoc para cada caso. O sênior reconhece o padrão de integração apropriado (Hohpe & Woolf), aplica a solução comprovada, e fala a linguagem comum desses padrões com o time.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço padrões de integração | — |
| **1** | Ouvi falar de EIP, sem conhecer os padrões | Nomeio o conceito de padrões de integração |
| **2** | Implemento integração ad-hoc sem reconhecer padrões | Já escrevi lógica de roteamento sem saber que era um padrão |
| **3** | Reconheço e aplico padrões comuns (router, translator, aggregator) | Implementei um content-based router conscientemente |
| **4** | Projeto integrações compondo padrões; escolho o padrão certo por problema | Desenhei uma integração complexa compondo múltiplos EIPs |
| **5** | Ensino EIP; reconheço integração ad-hoc reinventada; domino o catálogo completo | Estabeleci os padrões de integração de uma organização |

---

## 2.4 Resiliência de Comunicação (timeouts, retries, fallbacks na integração)

**Conceito + por que existe:** Aplicar os padrões de resiliência especificamente na comunicação entre serviços — timeouts em chamadas remotas, retries idempotentes, fallbacks quando um serviço está indisponível. Existe porque toda chamada remota pode falhar, e a integração entre serviços é onde as falhas parciais de sistemas distribuídos se manifestam.

**Profundidade esperada:** Avançado · **Conexões:** → Resiliência (Back-End 8.4), → Comunicação (2.1), → Tratamento de erros (Front-End 5.4)

**Erro de iniciante → Marca do sênior:** O iniciante faz chamadas entre serviços sem timeout, e uma lentidão em cascata trava o sistema. O sênior aplica timeout em toda chamada remota, retry idempotente com backoff, circuit breaker, e fallback gracioso — tratando a integração como inerentemente não-confiável.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não penso em resiliência de comunicação | — |
| **1** | Sei que chamadas podem falhar, sem proteger | Explico que "às vezes o outro serviço não responde" |
| **2** | Faço chamadas sem timeout nem retry | Já tive uma cascata de lentidão entre serviços |
| **3** | Aplico timeout e retry em chamadas remotas | Adicionei timeout e retry numa chamada entre serviços |
| **4** | Projeto a resiliência da integração; uso circuit breaker e fallback; antecipo cascatas | Desenhei a resiliência de comunicação de um fluxo entre serviços |
| **5** | Ensino resiliência de integração; reconheço pontos de cascata; domino bulkhead e degradação graciosa | Estabeleci os padrões de resiliência de integração de um produto |

---

# CAMADA 3 — API Gateway, BFF e Composição

> *A porta de entrada. Onde o mundo externo encontra o ecossistema de serviços internos.*

---

## 3.1 API Gateway e Edge Concerns

**Conceito + por que existe:** Um ponto de entrada único que roteia requisições para os serviços internos e centraliza preocupações transversais de borda — autenticação, rate limiting, roteamento, TLS termination. Existe porque expor dezenas de serviços diretamente ao cliente seria caótico e inseguro; o gateway dá um ponto único de controle e simplifica o cliente.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Autenticação (Back-End 5), → Rate limiting (Back-End 3.4), → Service mesh (Camada 7)

**Erro de iniciante → Marca do sênior:** O iniciante expõe serviços diretamente ou coloca lógica de negócio no gateway (tornando-o um gargalo monolítico). O sênior usa o gateway para preocupações de borda (auth, routing, rate limiting), mantém a lógica de negócio nos serviços, e evita o "gateway monolítico".

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é um API gateway | — |
| **1** | Ouvi falar, sem entender a função | Explico vagamente "ponto de entrada das APIs" |
| **2** | Sei que existe, sem configurá-lo | Nomeio um gateway (Kong, nginx) |
| **3** | Configuro um gateway para roteamento e auth | Configurei roteamento e autenticação num gateway |
| **4** | Projeto a estratégia de gateway; centralizo edge concerns sem lógica de negócio | Desenhei o gateway de um sistema com auth, rate limiting e roteamento |
| **5** | Ensino padrões de gateway; reconheço gateway monolítico; domino as estratégias de edge | Estabeleci a arquitetura de gateway de um produto |

---

## 3.2 Backend for Frontend (BFF)

**Conceito + por que existe:** Um backend dedicado para cada tipo de cliente (web, mobile, etc.), que agrega e adapta os dados dos serviços internos às necessidades específicas daquele cliente. Existe porque diferentes clientes têm necessidades de dados diferentes, e um BFF evita que o front-end faça muitas chamadas ou receba dados em excesso.

**Profundidade esperada:** Intermediário · **Conexões:** → Gateway (3.1), → Composição (3.3), → Data fetching (Front-End 5.3)

**Erro de iniciante → Marca do sênior:** O iniciante faz o front-end orquestrar múltiplas chamadas a serviços (lógica de agregação no cliente) ou usa uma API genérica que não serve bem nenhum cliente. O sênior cria BFFs que agregam e adaptam dados por tipo de cliente, simplificando o front-end.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço o padrão BFF | — |
| **1** | Ouvi falar, sem entender quando usar | Explico vagamente "backend para o front" |
| **2** | Faço o front orquestrar chamadas a serviços | Já fiz o front-end agregar dados de várias APIs |
| **3** | Implemento um BFF que agrega dados para um cliente | Construí um BFF que compõe dados de múltiplos serviços |
| **4** | Projeto a estratégia de BFF por tipo de cliente; balanceio agregação vs duplicação | Desenhei BFFs separados para web e mobile justificadamente |
| **5** | Ensino o padrão BFF; reconheço agregação mal colocada; domino os trade-offs | Estabeleci a estratégia de BFF de um produto multi-cliente |

---

## 3.3 Composição e Agregação de Serviços

**Conceito + por que existe:** As técnicas para combinar dados de múltiplos serviços em uma resposta única — agregação na API, composição de queries, GraphQL federation. Existe porque uma requisição do cliente frequentemente precisa de dados que vivem em múltiplos serviços, e alguém precisa compor esses dados.

**Profundidade esperada:** Avançado · **Conexões:** → BFF (3.2), → GraphQL (Back-End 3.2), → Database per service (1.4)

**Erro de iniciante → Marca do sênior:** O iniciante faz composição de forma ingênua (chamadas sequenciais que criam waterfalls) ou duplica dados sem estratégia. O sênior compõe de forma eficiente (chamadas paralelas), entende as opções (agregação, federation, CQRS), e escolhe pela necessidade.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei como compor dados de múltiplos serviços | — |
| **1** | Sei que dados vêm de vários serviços, sem saber compor | Explico que "às vezes precisa de vários serviços" |
| **2** | Faço chamadas sequenciais; crio waterfalls | Já compus dados com chamadas sequenciais lentas |
| **3** | Componho com chamadas paralelas; trato falhas parciais | Compus dados de serviços em paralelo |
| **4** | Projeto a estratégia de composição; escolho agregação vs federation vs CQRS | Desenhei a composição de dados de uma feature multi-serviço |
| **5** | Ensino composição; reconheço waterfalls e duplicação indevida; domino federation e CQRS | Estabeleci a estratégia de composição de dados de um produto |

---

## 3.4 Tradução e Anti-Corruption Layer

**Conceito + por que existe:** Uma camada que traduz entre o modelo de um sistema e o de outro, protegendo um domínio de ser "corrompido" pelo modelo de um sistema externo ou legado (Anti-Corruption Layer, do DDD). Existe porque integrar com sistemas externos ou legados, cujo modelo você não controla, pode poluir o seu domínio se você não isolar a tradução.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Bounded contexts (1.1), → Contratos (Camada 4), → Serialização (Back-End 2.4)

**Erro de iniciante → Marca do sênior:** O iniciante deixa o modelo de um sistema externo vazar para dentro do seu domínio. O sênior cria uma Anti-Corruption Layer que traduz entre os modelos, mantendo o domínio interno limpo e isolado das idiossincrasias do sistema externo.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço Anti-Corruption Layer | — |
| **1** | Ouvi falar, sem entender o propósito | Explico vagamente "traduzir entre sistemas" |
| **2** | Deixo o modelo externo vazar para o meu código | Já usei o modelo de uma API externa direto no domínio |
| **3** | Crio camada de tradução entre sistemas | Implementei uma camada que traduz dados de um sistema externo |
| **4** | Projeto Anti-Corruption Layers; protejo o domínio de modelos externos | Desenhei uma ACL para integrar com um sistema legado |
| **5** | Ensino ACL; reconheço vazamento de modelo externo; domino os padrões de integração de domínio | Estabeleci a estratégia de isolamento de domínio de um produto |

---

# CAMADA 4 — Contratos, Versionamento e Compatibilidade

> *O acordo entre serviços. Quebrar um contrato sem aviso quebra todos os consumidores que você não controla.*

---

## 4.1 Design de Contratos entre Serviços

**Conceito + por que existe:** Definir explicitamente a interface entre serviços — o que cada serviço promete (entradas, saídas, garantias). Existe porque, em sistemas distribuídos, o contrato é a fronteira de acoplamento: serviços se comunicam apenas via contratos, e um contrato bem desenhado permite que cada serviço evolua independentemente.

**Profundidade esperada:** Avançado · **Conexões:** → Acoplamento (1.3), → Versionamento (4.2), → Design de API (Back-End 3.1)

**Erro de iniciante → Marca do sênior:** O iniciante define contratos implícitos ou frouxos, gerando acoplamento acidental. O sênior projeta contratos explícitos, mínimos (expõem só o necessário) e estáveis, tratando o contrato como a interface pública que outros dependem.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não penso em contratos entre serviços | — |
| **1** | Sei que serviços têm interfaces, sem desenhá-las | Explico que "serviços têm APIs" |
| **2** | Defino contratos implícitos ou frouxos | Já mudei a resposta de um serviço quebrando consumidores |
| **3** | Defino contratos explícitos e mínimos | Projetei um contrato de serviço expondo só o necessário |
| **4** | Projeto contratos para evolução independente; minimizo acoplamento via contrato | Desenhei contratos que permitem serviços evoluírem isolados |
| **5** | Ensino design de contratos; reconheço contratos acoplados; domino as estratégias | Estabeleci os padrões de contrato de serviços de uma organização |

---

## 4.2 Versionamento e Compatibilidade (forward/backward)

**Conceito + por que existe:** As estratégias para evoluir contratos mantendo compatibilidade — compatibilidade para trás (consumidores antigos continuam funcionando) e para frente (consumidores novos lidam com produtores antigos). Existe porque, em sistemas distribuídos, você não pode atualizar todos os serviços simultaneamente; eles precisam coexistir em versões diferentes.

**Profundidade esperada:** Avançado · **Conexões:** → Contratos (4.1), → Serialização (Back-End 2.4), → Versionamento de API (Back-End 3.3)

**Erro de iniciante → Marca do sênior:** O iniciante faz mudanças quebradoras em contratos, exigindo deploy coordenado de todos os serviços. O sênior faz mudanças compatíveis para trás (adicionar campos opcionais, nunca remover), permitindo deploy independente e rollback seguro.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é compatibilidade de contrato | — |
| **1** | Ouvi falar, sem entender forward/backward | Explico vagamente "não quebrar quem usa" |
| **2** | Faço mudanças quebradoras sem perceber | Já exigi deploy coordenado por uma mudança de contrato |
| **3** | Faço mudanças compatíveis para trás; entendo as regras | Adicionei um campo opcional sem quebrar consumidores |
| **4** | Projeto evolução compatível em ambas as direções; permito deploy independente | Desenhei a evolução de um contrato com compat. forward e backward |
| **5** | Ensino compatibilidade; reconheço mudanças quebradoras; domino schema evolution distribuída | Estabeleci a política de evolução de contratos de um produto |

---

## 4.3 Contract Testing (Consumer-Driven Contracts)

**Conceito + por que existe:** Testes que verificam que um serviço respeita o contrato esperado por seus consumidores, sem precisar de testes de integração completos (Pact). Existe porque, em arquiteturas de microsserviços, testar a integração de todos os serviços juntos é caro e frágil; contract testing verifica a compatibilidade de forma isolada e rápida.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Contratos (4.1), → Testes (Guia de Testes Tipo 10), → CI/CD (Infra)

**Erro de iniciante → Marca do sênior:** O iniciante descobre quebras de contrato apenas em integração ou produção. O sênior usa consumer-driven contract testing, onde os consumidores definem suas expectativas e o produtor é testado contra elas no CI, detectando quebras antes do deploy.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço contract testing | — |
| **1** | Ouvi falar, sem entender | Nomeio o conceito ou a ferramenta (Pact) |
| **2** | Confio em testes de integração para pegar quebras | Já descobri uma quebra de contrato em produção |
| **3** | Implemento contract testing entre dois serviços | Configurei um contract test com Pact |
| **4** | Projeto a estratégia de contract testing; integro ao CI; uso consumer-driven contracts | Desenhei contract testing no pipeline entre serviços |
| **5** | Ensino contract testing; reconheço integração frágil; domino consumer-driven contracts em escala | Estabeleci a estratégia de contract testing de uma organização |

---

## 4.4 Schema Registry e Governança de Contratos

**Conceito + por que existe:** Um repositório central de schemas que governa a evolução dos contratos de dados (especialmente em mensageria — Confluent Schema Registry para Avro/Protobuf). Existe porque, quando muitos serviços trocam mensagens, é preciso um ponto central que valide compatibilidade de schema e evite que um produtor quebre os consumidores.

**Profundidade esperada:** Intermediário · **Conexões:** → Serialização (Back-End 2.4), → Mensageria (Back-End 6), → Versionamento (4.2)

**Erro de iniciante → Marca do sênior:** O iniciante evolui schemas de mensagens sem governança, quebrando consumidores silenciosamente. O sênior usa um schema registry que valida compatibilidade na publicação, garantindo que mudanças de schema não quebrem consumidores existentes.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço schema registry | — |
| **1** | Ouvi falar, sem entender o propósito | Nomeio o conceito |
| **2** | Evoluo schemas sem governança central | Já quebrei um consumidor com mudança de schema de mensagem |
| **3** | Uso schema registry; entendo validação de compatibilidade | Registrei e evoluí um schema com validação de compatibilidade |
| **4** | Projeto a governança de schemas; integro registry ao fluxo de dados | Desenhei a governança de schemas de um sistema de mensageria |
| **5** | Ensino governança de contratos; reconheço evolução sem governança; domino registry em escala | Estabeleci a governança de contratos de dados de uma organização |

---

# CAMADA 5 — Arquitetura Orientada a Eventos

> *Um paradigma diferente: serviços reagem a eventos em vez de chamarem uns aos outros. Desacoplamento máximo, complexidade própria.*

**Referência base:**
> **[CLÁSSICO]**
> Richardson, C. (2018). *Microservices Patterns.* Manning. — Cobre event-driven architecture, event sourcing, CQRS e sagas com profundidade prática.

---

## 5.1 Event-Driven Architecture (design)

**Conceito + por que existe:** Um estilo arquitetural onde serviços se comunicam publicando e reagindo a eventos (fatos que aconteceram), em vez de comandos diretos. Existe porque eventos desacoplam produtores de consumidores ao máximo — o produtor não sabe quem consome, permitindo adicionar novos consumidores sem mudar o produtor.

**Profundidade esperada:** Avançado · **Conexões:** → Comunicação assíncrona (2.1), → Mensageria (Back-End 6.3), → Coreografia (Camada 6)

**Erro de iniciante → Marca do sênior:** O iniciante usa eventos como comandos disfarçados (acoplando produtor e consumidor) ou cria uma teia de eventos impossível de rastrear. O sênior modela eventos como fatos de domínio, projeta o fluxo de eventos de forma rastreável, e entende quando eventos são apropriados vs chamadas diretas.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço arquitetura orientada a eventos | — |
| **1** | Ouvi falar, sem entender o paradigma | Explico vagamente "serviços mandam eventos" |
| **2** | Uso eventos como comandos diretos | Já publiquei um "evento" que era na verdade um comando |
| **3** | Modelo eventos como fatos de domínio; implemento fluxos de eventos | Construí uma feature com eventos de domínio bem modelados |
| **4** | Projeto a arquitetura de eventos; mantenho rastreabilidade; escolho eventos vs comandos | Desenhei o fluxo de eventos de um sistema mantendo rastreabilidade |
| **5** | Ensino EDA; reconheço eventos-comando e teias intratáveis; domino event modeling | Estabeleci a arquitetura orientada a eventos de um produto |

---

## 5.2 Event Sourcing

**Conceito + por que existe:** Um padrão onde o estado é derivado de uma sequência imutável de eventos (em vez de armazenar apenas o estado atual). Existe porque guardar todos os eventos dá uma trilha de auditoria completa, permite reconstruir qualquer estado passado, e habilita análises temporais — ao custo de complexidade significativa.

**Profundidade esperada:** Avançado · **Conexões:** → EDA (5.1), → CQRS (5.3), → Persistência (Back-End 4)

**Erro de iniciante → Marca do sênior:** O iniciante adota event sourcing por hype, herdando complexidade enorme (versionamento de eventos, replay, snapshots) sem necessidade. O sênior reconhece os casos onde event sourcing se justifica (auditoria, análise temporal), e entende seus custos antes de adotá-lo.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço event sourcing | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "guardar os eventos" |
| **2** | Acho que é só "guardar um histórico" | Confundo event sourcing com log de auditoria simples |
| **3** | Entendo o padrão; implemento um caso simples | Implementei event sourcing num agregado |
| **4** | Projeto sistemas com event sourcing; lido com replay, snapshots, versionamento | Desenhei um sistema event-sourced com snapshots e replay |
| **5** | Ensino event sourcing; reconheço adoção injustificada; domino os trade-offs e a complexidade | Estabeleci onde event sourcing se aplica num produto |

---

## 5.3 CQRS (Command Query Responsibility Segregation)

**Conceito + por que existe:** Separar o modelo de escrita (comandos) do modelo de leitura (queries), permitindo otimizar cada um independentemente. Existe porque leitura e escrita frequentemente têm necessidades opostas (escrita normalizada para consistência, leitura desnormalizada para performance), e separá-las permite otimizar ambas.

**Profundidade esperada:** Avançado · **Conexões:** → Event sourcing (5.2), → Composição (3.3), → Database per service (1.4)

**Erro de iniciante → Marca do sênior:** O iniciante aplica CQRS em todo lugar (complexidade desnecessária) ou não entende a separação. O sênior aplica CQRS onde leitura e escrita têm necessidades genuinamente diferentes, e entende que não precisa de event sourcing para usar CQRS.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço CQRS | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "separar leitura e escrita" |
| **2** | Confundo CQRS com ter dois bancos sem critério | Nomeio CQRS sem entender quando aplicar |
| **3** | Entendo a separação; implemento CQRS num caso apropriado | Implementei modelos de leitura e escrita separados |
| **4** | Projeto onde aplicar CQRS; otimizo leitura e escrita independentemente | Desenhei CQRS para uma feature com necessidades de leitura/escrita distintas |
| **5** | Ensino CQRS; reconheço aplicação desnecessária; domino a relação com event sourcing | Estabeleci onde CQRS se justifica num produto |

---

## 5.4 Outbox Pattern e Consistência de Eventos

**Conceito + por que existe:** Um padrão que garante que um evento seja publicado se e somente se a transação de banco correspondente foi confirmada (resolvendo o problema de dual write). Existe porque escrever no banco E publicar um evento são duas operações que podem falhar independentemente — sem o outbox, você pode confirmar a transação mas perder o evento, ou vice-versa.

**Profundidade esperada:** Avançado · **Conexões:** → Idempotência (Back-End 6.4), → Transações (Back-End 4.3), → EDA (5.1)

**Erro de iniciante → Marca do sênior:** O iniciante escreve no banco e publica o evento separadamente, criando inconsistência quando uma das operações falha (dual write problem). O sênior usa o outbox pattern (escreve o evento na mesma transação do banco, e um processo publica depois), garantindo consistência entre estado e eventos.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço o problema de dual write | — |
| **1** | Não sei que há risco em escrever no banco e publicar evento | Explico vagamente que "às vezes o evento se perde" |
| **2** | Escrevo no banco e publico evento separadamente | Já perdi um evento porque a publicação falhou após o commit |
| **3** | Conheço o outbox pattern; implemento um caso | Implementei o outbox pattern para garantir publicação |
| **4** | Projeto a consistência de eventos; uso outbox e CDC; antecipo dual write | Desenhei a estratégia de consistência entre estado e eventos |
| **5** | Ensino consistência de eventos; reconheço dual write; domino outbox, CDC e transactional messaging | Estabeleci os padrões de consistência de eventos de um produto |

---

# CAMADA 6 — Orquestração vs Coreografia

> *Como coordenar um fluxo de negócio que atravessa múltiplos serviços. Centralizar a coordenação ou distribuí-la?*

---

## 6.1 Orquestração (coordenação centralizada)

**Conceito + por que existe:** Um coordenador central (orquestrador) que dirige o fluxo, chamando cada serviço na ordem certa e tratando as respostas. Existe porque fluxos de negócio complexos que atravessam serviços precisam de coordenação, e a orquestração centraliza essa lógica em um lugar visível e rastreável.

**Profundidade esperada:** Avançado · **Conexões:** → Sagas (6.3), → Coreografia (6.2), → Comunicação (Camada 2)

**Erro de iniciante → Marca do sênior:** O iniciante espalha a lógica de coordenação por vários serviços (ninguém sabe o fluxo completo) ou cria um orquestrador que vira um monolito de lógica. O sênior usa orquestração quando o fluxo precisa de visibilidade central, mantendo o orquestrador focado em coordenação, não em lógica de negócio dos serviços.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é orquestração | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "alguém coordena os serviços" |
| **2** | Espalho coordenação sem perceber | Já tive um fluxo onde ninguém sabia a ordem completa |
| **3** | Implemento orquestração centralizada; entendo o padrão | Construí um orquestrador para um fluxo multi-serviço |
| **4** | Projeto orquestração; escolho onde centralizar; uso workflow engines | Desenhei um fluxo orquestrado com tratamento de falhas |
| **5** | Ensino orquestração; reconheço orquestrador-monolito; domino workflow engines | Estabeleci a estratégia de orquestração de um produto |

---

## 6.2 Coreografia (coordenação distribuída)

**Conceito + por que existe:** Cada serviço reage a eventos e decide sua própria ação, sem um coordenador central — o fluxo emerge das reações em cadeia. Existe porque a coreografia dá desacoplamento máximo (cada serviço é autônomo), evitando o ponto único de coordenação — ao custo de o fluxo ser implícito e mais difícil de rastrear.

**Profundidade esperada:** Avançado · **Conexões:** → EDA (5.1), → Orquestração (6.1), → Observabilidade (Back-End 9.3)

**Erro de iniciante → Marca do sênior:** O iniciante usa coreografia e perde a visibilidade do fluxo (ninguém entende o que acontece). O sênior escolhe entre orquestração e coreografia pelo trade-off (visibilidade vs autonomia), e quando usa coreografia, investe em observabilidade para tornar o fluxo rastreável.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é coreografia | — |
| **1** | Ouvi falar, sem entender a diferença para orquestração | Explico vagamente "serviços reagem sozinhos" |
| **2** | Uso coreografia e perco a visibilidade do fluxo | Já tive um fluxo coreografado impossível de rastrear |
| **3** | Implemento coreografia; entendo o trade-off com orquestração | Construí um fluxo coreografado com observabilidade |
| **4** | Escolho orquestração vs coreografia por trade-off; garanto rastreabilidade | Justifiquei coreografia vs orquestração para um fluxo |
| **5** | Ensino coordenação distribuída; reconheço fluxos intratáveis; domino os dois paradigmas | Estabeleci a estratégia de coordenação de um produto |

---

## 6.3 Sagas e Transações Distribuídas

**Conceito + por que existe:** Um padrão para manter consistência em transações que atravessam múltiplos serviços, usando uma sequência de transações locais com compensações em caso de falha (em vez de uma transação distribuída ACID). Existe porque transações ACID não funcionam entre serviços com bancos separados, e a saga é a forma de coordenar uma operação multi-serviço com consistência eventual.

**Profundidade esperada:** Avançado · **Conexões:** → Transações (Back-End 4.3), → Orquestração (6.1), → Idempotência (Back-End 6.4)

**Erro de iniciante → Marca do sênior:** O iniciante tenta usar transações distribuídas (two-phase commit) ingenuamente, ou não trata falhas parciais em operações multi-serviço (deixando o sistema inconsistente). O sênior usa sagas com transações compensatórias, projeta as compensações cuidadosamente, e aceita a consistência eventual.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço o padrão saga | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "transação entre serviços" |
| **2** | Tento transação distribuída ou ignoro falhas parciais | Já tive estado inconsistente após falha em fluxo multi-serviço |
| **3** | Implemento sagas com compensações; entendo o padrão | Construí uma saga com transações compensatórias |
| **4** | Projeto sagas (orquestradas ou coreografadas); desenho compensações robustas | Desenhei uma saga para uma operação distribuída crítica |
| **5** | Ensino sagas; reconheço tentativas de 2PC ingênuo; domino consistência distribuída | Estabeleci os padrões de transação distribuída de um produto |

---

## 6.4 Workflow Engines e Processos de Longa Duração

**Conceito + por que existe:** Ferramentas que gerenciam processos de negócio de longa duração e com estado (Temporal, Camunda, Step Functions), lidando com persistência de estado, retries, timeouts e compensações. Existe porque processos que duram horas ou dias (aprovações, onboarding) com muitos passos e falhas possíveis são difíceis de gerenciar com código ad-hoc; engines dão durabilidade e visibilidade.

**Profundidade esperada:** Intermediário · **Conexões:** → Orquestração (6.1), → Sagas (6.3), → Jobs (Back-End 6.1)

**Erro de iniciante → Marca do sênior:** O iniciante implementa processos longos com código ad-hoc e estado disperso (frágil, sem visibilidade). O sênior usa workflow engines para processos longos e críticos, ganhando durabilidade, retry automático, e visibilidade do estado do processo.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço workflow engines | — |
| **1** | Ouvi falar, sem saber quando usar | Nomeio uma engine (Temporal, Camunda) |
| **2** | Implemento processos longos com código ad-hoc | Já fiz um processo de múltiplos passos sem durabilidade |
| **3** | Uso uma workflow engine para um processo longo | Implementei um workflow durável numa engine |
| **4** | Projeto processos de longa duração; escolho engine vs código; desenho compensações | Desenhei um processo de negócio longo numa workflow engine |
| **5** | Ensino workflow engines; reconheço processos frágeis; domino os padrões de processo durável | Estabeleci a estratégia de processos de longa duração de um produto |

---

# CAMADA 7 — Service Mesh e Preocupações Transversais

> *A infraestrutura que resolve preocupações de comunicação de forma transparente, fora do código dos serviços.*

---

## 7.1 Service Mesh e Sidecar Pattern

**Conceito + por que existe:** Uma camada de infraestrutura (Istio, Linkerd) que intercepta toda comunicação entre serviços via proxies sidecar, provendo roteamento, resiliência, segurança e observabilidade sem mudar o código. Existe porque preocupações transversais (retry, mTLS, tracing) repetidas em cada serviço são dívida técnica; o mesh as resolve uma vez, transparentemente.

**Profundidade esperada:** Intermediário · **Conexões:** → Comunicação (Camada 2), → Resiliência (2.4), → Kubernetes (Infra)

**Erro de iniciante → Marca do sênior:** O iniciante reimplementa retry, mTLS e tracing em cada serviço, ou adota service mesh sem entender sua complexidade operacional. O sênior entende o que o mesh resolve (preocupações transversais de comunicação) e o custo operacional, decidindo se o trade-off compensa para a escala do sistema.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço service mesh | — |
| **1** | Ouvi falar, sem entender | Nomeio um mesh (Istio, Linkerd) |
| **2** | Reimplemento preocupações transversais em cada serviço | Já repeti lógica de retry/tracing em vários serviços |
| **3** | Entendo o que o mesh provê; configuro um caso básico | Configurei roteamento ou mTLS num service mesh |
| **4** | Projeto se/como usar mesh; avalio o custo operacional; configuro políticas | Avaliei e justifiquei adoção (ou não) de service mesh |
| **5** | Ensino service mesh; reconheço preocupações transversais reimplementadas; domino a operação | Estabeleci a estratégia de service mesh de uma plataforma |

---

## 7.2 Observabilidade Distribuída na Integração

**Conceito + por que existe:** Tornar visível o comportamento de fluxos que atravessam múltiplos serviços — correlação de logs, distributed tracing, e métricas de integração. Existe porque, em arquiteturas de integração, um problema raramente está em um serviço isolado; está na interação entre eles, e sem observabilidade distribuída isso é invisível.

**Profundidade esperada:** Avançado · **Conexões:** → Tracing (Back-End 9.3), → Coreografia (6.2), → Resiliência (2.4)

**Erro de iniciante → Marca do sênior:** O iniciante depura integração olhando cada serviço isoladamente, sem correlação. O sênior propaga contexto de correlação (trace IDs) por toda a cadeia de serviços, e usa tracing distribuído para ver o fluxo completo e identificar onde a integração falha.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não penso em observabilidade de fluxos distribuídos | — |
| **1** | Sei que dá para rastrear, sem saber como na integração | Explico vagamente "seguir a requisição entre serviços" |
| **2** | Depuro cada serviço isoladamente | Já depurei uma integração olhando logs separados |
| **3** | Propago trace IDs; correlaciono logs entre serviços | Implementei propagação de contexto entre serviços |
| **4** | Projeto a observabilidade da integração; instrumento o fluxo ponta a ponta | Desenhei a observabilidade de um fluxo multi-serviço |
| **5** | Ensino observabilidade distribuída; reconheço fluxos opacos; domino correlação em escala | Estabeleci a observabilidade de integração de um produto |

---

## 7.3 Segurança na Comunicação entre Serviços (mTLS, Zero Trust)

**Conceito + por que existe:** Proteger a comunicação interna entre serviços com autenticação mútua (mTLS) e o princípio de não confiar na rede interna (Zero Trust). Existe porque a suposição de que "a rede interna é confiável" é falsa — se um atacante entra na rede, comunicação interna sem proteção é livremente interceptável e falsificável.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Zero Trust (Guia de Segurança), → Service mesh (7.1), → Autenticação (Back-End 5)

**Erro de iniciante → Marca do sênior:** O iniciante deixa a comunicação interna sem criptografia nem autenticação ("é interno, é seguro"). O sênior aplica mTLS entre serviços, autentica serviço-a-serviço, e adota Zero Trust — tratando a rede interna como potencialmente hostil.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não penso em segurança interna entre serviços | — |
| **1** | Acho que comunicação interna é segura por ser interna | Explico que "dentro da rede é seguro" |
| **2** | Deixo comunicação interna sem proteção | Já fiz serviços se comunicarem sem TLS interno |
| **3** | Aplico TLS interno; entendo autenticação serviço-a-serviço | Configurei comunicação interna com TLS |
| **4** | Projeto segurança Zero Trust interna; uso mTLS; autentico serviços | Desenhei autenticação mútua entre serviços com mTLS |
| **5** | Ensino segurança de comunicação interna; reconheço confiança indevida na rede; domino Zero Trust | Estabeleci a arquitetura de segurança interna de um produto |

---

## 7.4 Multi-tenancy e Isolamento

**Conceito + por que existe:** As estratégias para servir múltiplos clientes (tenants) na mesma infraestrutura, com isolamento de dados e recursos entre eles. Existe porque produtos SaaS servem muitos clientes, e como você isola os dados e recursos de cada tenant (banco compartilhado vs isolado, isolamento de recursos) afeta segurança, custo e escala.

**Profundidade esperada:** Intermediário · **Conexões:** → Database per service (1.4), → Autorização (Back-End 5.4), → Segurança (7.3)

**Erro de iniciante → Marca do sênior:** O iniciante mistura dados de tenants sem isolamento robusto (risco de vazamento entre clientes) ou isola excessivamente (custo proibitivo). O sênior escolhe a estratégia de isolamento pelo trade-off (custo vs isolamento), garante que dados de um tenant nunca vazem para outro, e projeta para a escala de tenants esperada.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço multi-tenancy | — |
| **1** | Ouvi falar, sem entender as estratégias | Explico vagamente "vários clientes no mesmo sistema" |
| **2** | Misturo dados de tenants sem estratégia clara de isolamento | Não tenho certeza de que dados de tenants estão isolados |
| **3** | Implemento isolamento de tenants; entendo as estratégias | Implementei isolamento de dados por tenant |
| **4** | Projeto a estratégia de multi-tenancy; escolho o nível de isolamento por trade-off | Desenhei a arquitetura multi-tenant de uma aplicação |
| **5** | Ensino multi-tenancy; reconheço isolamento fraco ou caro demais; domino as estratégias em escala | Estabeleci a arquitetura multi-tenant de um produto SaaS |

---

# Planilha de Auto-Auditoria — Middle-End / Integração

Registre seu nível (0-5) em cada competência. **Regra:** não marque um nível sem passar no teste de validação. Anote a evidência concreta.

## Camada 1 — Decomposição de Serviços e DDD

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 1.1 Bounded Contexts e Fronteiras | ___ | |
| 1.2 Granularidade de Serviços | ___ | |
| 1.3 Acoplamento e Coesão | ___ | |
| 1.4 Estratégia de Dados Distribuídos | ___ | |

## Camada 2 — Estilos de Comunicação Inter-Serviços

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 2.1 Síncrono vs Assíncrono | ___ | |
| 2.2 Service Discovery e Roteamento | ___ | |
| 2.3 Padrões de Integração (EIP) | ___ | |
| 2.4 Resiliência de Comunicação | ___ | |

## Camada 3 — API Gateway, BFF e Composição

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 3.1 API Gateway e Edge Concerns | ___ | |
| 3.2 Backend for Frontend (BFF) | ___ | |
| 3.3 Composição e Agregação | ___ | |
| 3.4 Anti-Corruption Layer | ___ | |

## Camada 4 — Contratos, Versionamento e Compatibilidade

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 4.1 Design de Contratos | ___ | |
| 4.2 Versionamento e Compatibilidade | ___ | |
| 4.3 Contract Testing | ___ | |
| 4.4 Schema Registry e Governança | ___ | |

## Camada 5 — Arquitetura Orientada a Eventos

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 5.1 Event-Driven Architecture | ___ | |
| 5.2 Event Sourcing | ___ | |
| 5.3 CQRS | ___ | |
| 5.4 Outbox Pattern e Consistência | ___ | |

## Camada 6 — Orquestração vs Coreografia

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 6.1 Orquestração | ___ | |
| 6.2 Coreografia | ___ | |
| 6.3 Sagas e Transações Distribuídas | ___ | |
| 6.4 Workflow Engines | ___ | |

## Camada 7 — Service Mesh e Preocupações Transversais

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 7.1 Service Mesh e Sidecar | ___ | |
| 7.2 Observabilidade Distribuída | ___ | |
| 7.3 Segurança entre Serviços (mTLS) | ___ | |
| 7.4 Multi-tenancy e Isolamento | ___ | |

---

## Interpretação do Resultado

- **Especialista em Integração** significa **nível 4+ nas camadas 1-2** (decomposição e comunicação — a base de tudo) e **nível 3+ nas camadas 4-6** (contratos, eventos, coordenação). As camadas 3 e 7 (gateway, mesh) podem estar em nível 3, pois são mais dependentes de ferramentas específicas.

- **A Camada 1 (decomposição) é o divisor de águas.** Definir fronteiras de serviço corretamente é a habilidade mais rara e mais valiosa da integração — e a mais difícil de validar sem ter desenhado arquiteturas reais. É a competência que mais distingue o arquiteto do implementador.

- **Esta sub-área tem forte conexão com a Seção 3 do README de arquitetura.** Decomposição de serviços é fundamentalmente um problema topológico: onde traçar as fronteiras que minimizam o acoplamento (as "arestas" entre serviços) enquanto maximizam a coesão interna. Seu background matemático dá acesso direto a esse modo de pensar.

- **Para o seu perfil:** o Middle-End é provavelmente a sub-área onde você tem *menos exposição prática* (seu trabalho é mais ML/pipeline do que arquitetura de microsserviços), mas onde seu raciocínio estrutural mais se aplica. A lacuna aqui é de experiência, não de capacidade de raciocínio — você entenderá os conceitos rapidamente, mas o nível 4-5 exige ter desenhado e operado essas arquiteturas.

---

## Referências

| # | Fonte | Tipo | Uso |
|---|-------|------|-----|
| 1 | Dreyfus & Dreyfus (1980). *Five-Stage Model of Skill Acquisition.* UC Berkeley. | **PEER-REVIEWED** | Escala de progressão |
| 2 | Smith & Kendall (1963). *Retranslation of Expectations.* JAP, 47(2). DOI: 10.1037/h0047060 | **PEER-REVIEWED** | Âncoras comportamentais (BARS) |
| 3 | Kruger & Dunning (1999). *Unskilled and Unaware of It.* JPSP, 77(6). | **PEER-REVIEWED** | Viés de auto-avaliação |
| 4 | Evans, E. (2003). *Domain-Driven Design.* Addison-Wesley. | **CLÁSSICO** | Camada 1 (bounded contexts, decomposição) |
| 5 | Newman, S. (2021). *Building Microservices* (2nd ed.). O'Reilly. | **CLÁSSICO** | Toda a arquitetura de microsserviços |
| 6 | Hohpe, G., & Woolf, B. (2003). *Enterprise Integration Patterns.* Addison-Wesley. | **CLÁSSICO** | Camada 2.3 (padrões de integração) |
| 7 | Richardson, C. (2018). *Microservices Patterns.* Manning. | **CLÁSSICO** | Camadas 5-6 (eventos, sagas, CQRS) |
| 8 | Pact Foundation. *Consumer-Driven Contract Testing.* https://docs.pact.io/ | **INDUSTRIAL** | Camada 4.3 (contract testing) |
| 9 | Gilbert & Lynch (2002). *Brewer's Conjecture.* ACM SIGACT News, 33(2). | **PEER-REVIEWED** | Consistência distribuída (Camadas 5-6) |

---

*Parte 1C de 4 do Skill-Check de Engenharia de Software. Concluídas: Front-End, Back-End e Middle-End/Integração. Próxima e última sub-área: Infraestrutura / Cloud / DevOps.*
*Escala ancorada em Dreyfus (1980) + BARS (Smith & Kendall, 1963). Auto-avaliação deve ser complementada por validação externa (Kruger & Dunning, 1999).*
