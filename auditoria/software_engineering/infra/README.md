# Skill-Check de Engenharia de Software — Parte 1D: Infraestrutura / Cloud / DevOps
## Arquitetura Completa de Competências com Escala Dreyfus Ancorada

> *"You build it, you run it."*
> — Werner Vogels, CTO Amazon (2006), sobre a responsabilidade de quem desenvolve também operar

---

## Como Este Documento Funciona

Este é o mapa de competências da sub-área **Infraestrutura / Cloud / DevOps** — a camada que leva o código da máquina do desenvolvedor até a produção e o mantém rodando de forma confiável. É o quarto e último documento da Parte 1 (após Front-End, Back-End e Middle-End).

**Diferença em relação às outras sub-áreas:** as três anteriores são sobre *construir* software. Esta é sobre *operar* software — empacotar, distribuir, escalar, monitorar e proteger sistemas em produção. É a disciplina que responde à pergunta: "o código funciona na minha máquina; como faço para funcionar de forma confiável para milhões de usuários?"

Mantém o formato: 10 camadas que se empilham, do substrato (sistema operacional) até a operação madura (confiabilidade e segurança), com 4 competências por camada. Cada competência tem conceito, por que existe, profundidade, conexões, erro/sênior, e progressão Dreyfus completa (0-5) com teste de validação.

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

> **Fundamentação verificada:** Dreyfus & Dreyfus (1980), UC Berkeley **[PEER-REVIEWED]**; Smith & Kendall (1963), JAP 47(2), DOI: 10.1037/h0047060 **[PEER-REVIEWED]**; Kruger & Dunning (1999), JPSP 77(6) **[PEER-REVIEWED]** — auto-avaliação requer validação externa.

---

## Visão Geral das 10 Camadas

```
TIER MATURIDADE (operação confiável e segura)
  CAMADA 10 · Segurança de Infraestrutura
  CAMADA  9 · Confiabilidade, Escalabilidade e Disponibilidade
  CAMADA  8 · Observabilidade de Infraestrutura

TIER AUTOMAÇÃO (entrega contínua)
  CAMADA  7 · CI/CD e Automação de Deploy
  CAMADA  6 · Infraestrutura como Código (IaC)
  CAMADA  5 · Cloud e Modelos de Serviço

TIER PLATAFORMA (onde o código roda)
  CAMADA  4 · Orquestração / Kubernetes
  CAMADA  3 · Containers

TIER SUBSTRATO (fundação)
  CAMADA  2 · Redes e Conectividade
  CAMADA  1 · Sistemas Operacionais / Linux
```

A lógica do empilhamento: tudo começa no **sistema operacional** (camada 1) — sem entender Linux, processos e permissões, as camadas superiores são mágica. Sobre ele vêm a **plataforma** (containers, orquestração), a **automação** (cloud, IaC, CI/CD) e a **maturidade** (observabilidade, confiabilidade, segurança). A régua de "especialista em DevOps" exige domínio do tier de automação e maturidade — não apenas saber rodar containers.

**Referências base de toda a disciplina:**
> **[INDUSTRIAL]**
> Kim, G., Humble, J., Debois, P., & Willis, J. (2016). *The DevOps Handbook.* IT Revolution.
> — A referência fundacional para a cultura e as práticas de DevOps.

> **[PEER-REVIEWED / INDUSTRIAL — Research-backed]**
> Forsgren, N., Humble, J., & Kim, G. (2018). *Accelerate: The Science of Lean Software and DevOps.* IT Revolution.
> — Baseado em pesquisa rigorosa com 23.000+ respondentes de 2.000+ organizações. Estabeleceu as quatro métricas DORA: Deployment Frequency, Lead Time for Changes, Time to Restore Service (MTTR), e Change Failure Rate. As duas primeiras medem velocidade; as duas últimas, estabilidade — e a pesquisa demonstrou que organizações de alta performance otimizam ambas simultaneamente, refutando o trade-off percebido entre velocidade e estabilidade.

> **[INDUSTRIAL]**
> Beyer, B., Jones, C., Petoff, J., & Murphy, N. R. (2016). *Site Reliability Engineering.* O'Reilly. https://sre.google/sre-book/
> — A referência definitiva para confiabilidade e operação em escala.

---

# CAMADA 1 — Sistemas Operacionais / Linux

> *O substrato de toda infraestrutura. Servidores rodam Linux. Quem não domina o SO trata tudo acima como mágica e fica perdido quando algo quebra.*

**Referência base:**
> **[CLÁSSICO]**
> Nemeth, E., Snyder, G., Hein, T., Whaley, B., & Mackin, D. (2017). *UNIX and Linux System Administration Handbook* (5th ed.). Addison-Wesley.
> — A referência abrangente para administração de sistemas Linux/UNIX.

---

## 1.1 Processos, Sinais e Gerenciamento de Recursos

**Conceito + por que existe:** Como o sistema operacional gerencia programas em execução — processos, threads, sinais, prioridades, e limites de recursos (CPU, memória, file descriptors). Existe porque entender como o SO executa e limita programas é a base para diagnosticar por que um serviço trava, consome recursos demais, ou não inicia.

**Profundidade esperada:** Avançado · **Conexões:** → Concorrência (Back-End 1.1), → Containers (Camada 3), → Observabilidade (Camada 8)

**Erro de iniciante → Marca do sênior:** O iniciante não sabe diagnosticar um processo que consome 100% de CPU ou que ficou zumbi. O sênior usa as ferramentas (`ps`, `top`, `htop`, `strace`, `lsof`) para inspecionar processos, entende sinais (SIGTERM vs SIGKILL), e diagnostica esgotamento de recursos.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é um processo no SO | — |
| **1** | Sei que programas "rodam", sem entender processos | Explico que "o programa está rodando" |
| **2** | Uso `ps`/`top` para ver processos; não diagnostico problemas | Listei processos com `top` |
| **3** | Inspeciono e gerencio processos; entendo sinais e prioridades | Diagnostiquei um processo consumindo CPU com `top`/`strace` |
| **4** | Projeto limites de recursos; antecipo esgotamento; uso ferramentas avançadas de diagnóstico | Resolvi um problema de file descriptors esgotados |
| **5** | Ensino gerenciamento de processos; reconheço problemas por inspeção; domino o scheduler e cgroups | Diagnostiquei um problema complexo de recursos em produção |

---

## 1.2 Sistema de Arquivos e Permissões

**Conceito + por que existe:** Como o Linux organiza e controla acesso a arquivos — a hierarquia de diretórios, permissões (usuário/grupo/outros, rwx), ownership, e montagem de volumes. Existe porque praticamente tudo no Linux é um arquivo, e problemas de permissão são uma das causas mais comuns de falhas em deploys e serviços.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Segurança (Camada 10), → Containers (Camada 3), → Menor privilégio (Back-End 10.4)

**Erro de iniciante → Marca do sênior:** O iniciante resolve qualquer problema de permissão com `chmod 777` (abrindo tudo). O sênior entende o modelo de permissões, concede o mínimo necessário, e diagnostica problemas de acesso corretamente.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço o sistema de arquivos Linux | — |
| **1** | Navego em diretórios, sem entender permissões | Uso `cd` e `ls` |
| **2** | Mudo permissões com `chmod`, frequentemente `777` | Já usei `chmod 777` para "resolver" um problema |
| **3** | Entendo o modelo de permissões; concedo acesso correto | Configurei permissões mínimas corretas para um serviço |
| **4** | Projeto a estratégia de permissões; uso ACLs e ownership corretamente; monto volumes | Desenhei a estrutura de permissões de uma aplicação multiusuário |
| **5** | Ensino permissões Linux; reconheço configurações inseguras; domino ACLs, SUID e o VFS | Auditei e corrigi permissões de um sistema de produção |

---

## 1.3 Shell, Scripting e Automação de Linha de Comando

**Conceito + por que existe:** O uso da shell (bash) para operar o sistema e automatizar tarefas — comandos, pipes, scripts, variáveis de ambiente. Existe porque a linha de comando é a interface primária de operação de servidores, e automatizar tarefas repetitivas via scripts é a essência da mentalidade DevOps.

**Profundidade esperada:** Intermediário · **Conexões:** → CI/CD (Camada 7), → IaC (Camada 6), → Automação geral

**Erro de iniciante → Marca do sênior:** O iniciante executa tarefas manualmente, repetidamente, e comete erros. O sênior automatiza tarefas repetitivas com scripts idempotentes e versionados, e domina a composição de comandos via pipes.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei usar a linha de comando | — |
| **1** | Executo comandos básicos copiando, sem entender | Rodei comandos seguindo um tutorial |
| **2** | Uso comandos comuns; não componho nem automatizo | Naveguei e manipulei arquivos via terminal |
| **3** | Componho comandos com pipes; escrevo scripts simples | Escrevi um script bash para automatizar uma tarefa |
| **4** | Automatizo operações complexas; scripts idempotentes e robustos; trato erros | Automatizei um processo operacional com script robusto |
| **5** | Ensino shell scripting; reconheço scripts frágeis; domino a shell a fundo | Estabeleci a biblioteca de automação operacional de um time |

---

## 1.4 Fundamentos de Sistema Operacional (memória, kernel, syscalls)

**Conceito + por que existe:** Os conceitos fundamentais do SO que sustentam tudo — gerenciamento de memória virtual, o papel do kernel, system calls, e a fronteira user space/kernel space. Existe porque problemas profundos de performance e estabilidade (OOM killer, swap, page faults) só são diagnosticáveis com entendimento do que o SO faz por baixo.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Memória (Back-End 1.2), → Containers (Camada 3), → Fundamentos computacionais (Eixo 1)

**Erro de iniciante → Marca do sênior:** O iniciante não entende por que o OOM killer matou seu processo ou por que o swap está degradando a performance. O sênior entende memória virtual, page cache, e o comportamento do kernel sob pressão de recursos.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que o sistema operacional faz | — |
| **1** | Sei que existe um SO, sem entender seu papel | Explico que "o SO gerencia o computador" |
| **2** | Conheço conceitos superficialmente; não diagnostico | Nomeio "kernel" e "memória" |
| **3** | Entendo memória virtual, kernel e syscalls; diagnostico problemas básicos | Diagnostiquei um problema de OOM ou swap |
| **4** | Projeto considerando o comportamento do SO; antecipo pressão de recursos | Ajustei parâmetros do kernel para um workload específico |
| **5** | Ensino fundamentos de SO; reconheço problemas por inspeção; domino o kernel Linux | Resolvi um problema profundo de kernel/memória em produção |

> *Conexão com seu diagnóstico (Eixo 1): esta competência é parte do gap de fundamentos computacionais. O comportamento do SO sob pressão de memória conecta diretamente ao gerenciamento de memória do seu runtime Python.*

---

# CAMADA 2 — Redes e Conectividade

> *Como os pacotes chegam ao seu serviço. A camada onde latência, timeouts e conectividade vivem — e onde muitos problemas de produção se escondem.*

---

## 2.1 Fundamentos de Rede (TCP/IP, DNS, roteamento)

**Conceito + por que existe:** Os protocolos e mecanismos que conectam sistemas — TCP/IP, DNS (resolução de nomes), roteamento, sub-redes, portas. Existe porque toda comunicação em infraestrutura depende de rede, e problemas de conectividade (DNS lento, rota errada, porta bloqueada) são onipresentes em produção.

**Profundidade esperada:** Avançado · **Conexões:** → TCP/IP (Back-End 2.2), → Load balancing (2.3), → Cloud networking (Camada 5)

**Erro de iniciante → Marca do sênior:** O iniciante não sabe diagnosticar "não consigo conectar no serviço" além de reiniciar. O sênior usa as ferramentas (`dig`, `nslookup`, `traceroute`, `netstat`, `tcpdump`) para diagnosticar onde a conexão falha na pilha de rede.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço fundamentos de rede | — |
| **1** | Sei que existe "a rede", sem entender as camadas | Explico que "os computadores se conectam pela rede" |
| **2** | Conheço IP e DNS superficialmente; não diagnostico | Sei que sites têm endereços IP |
| **3** | Entendo TCP/IP, DNS, portas; diagnostico conectividade | Diagnostiquei um problema de DNS com `dig` |
| **4** | Projeto topologias de rede; antecipo problemas; uso captura de pacotes | Desenhei a topologia de rede de uma aplicação |
| **5** | Ensino redes; reconheço problemas por inspeção; domino a pilha de rede a fundo | Diagnostiquei um problema complexo de rede em produção com `tcpdump` |

---

## 2.2 Firewalls, Segurança de Rede e Conectividade

**Conceito + por que existe:** Os controles que governam qual tráfego é permitido — firewalls, security groups, regras de entrada/saída, VPNs. Existe porque controlar o acesso de rede é uma camada fundamental de segurança (defesa em profundidade) e a causa de muitos problemas de "por que não consigo conectar".

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Segurança (Camada 10), → Cloud (Camada 5), → Superfície de ataque (Back-End 10.4)

**Erro de iniciante → Marca do sênior:** O iniciante abre todas as portas (`0.0.0.0/0`) para "fazer funcionar". O sênior aplica o menor privilégio na rede — abre apenas as portas necessárias, das origens necessárias — e entende as regras de firewall como parte da superfície de ataque.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é um firewall | — |
| **1** | Sei que firewalls "bloqueiam coisas", sem detalhes | Explico que "firewall protege a rede" |
| **2** | Abro portas para fazer funcionar, sem critério | Já abri tudo (`0.0.0.0/0`) para resolver |
| **3** | Configuro regras de firewall corretas; entendo entrada/saída | Configurei security groups com portas mínimas |
| **4** | Projeto a estratégia de segurança de rede; menor privilégio; segmentação | Desenhei a segmentação de rede de uma aplicação |
| **5** | Ensino segurança de rede; reconheço regras permissivas demais; domino as estratégias | Auditei e endureci a configuração de rede de um sistema |

---

## 2.3 Load Balancing e Distribuição de Tráfego

**Conceito + por que existe:** Distribuir requisições entre múltiplas instâncias de um serviço — algoritmos de balanceamento, health checks, e os tipos (L4 vs L7). Existe porque escalar horizontalmente exige distribuir carga, e o load balancer é o ponto de entrada que roteia tráfego e remove instâncias não-saudáveis.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Escalabilidade (Back-End 8.2), → Disponibilidade (Camada 9), → API Gateway (Middle-End 3.1)

**Erro de iniciante → Marca do sênior:** O iniciante usa um load balancer sem configurar health checks (tráfego vai para instâncias mortas). O sênior configura health checks corretos, entende a diferença L4/L7, e escolhe o algoritmo de balanceamento pelo perfil de carga.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é load balancing | — |
| **1** | Ouvi falar, sem saber como funciona | Explico que "distribui a carga" |
| **2** | Uso um load balancer gerenciado seguindo tutorial | Configurei um load balancer básico |
| **3** | Configuro load balancing com health checks; entendo L4 vs L7 | Configurei health checks que removem instâncias mortas |
| **4** | Projeto a estratégia de distribuição; escolho algoritmo; antecipo falhas | Desenhei o balanceamento de um serviço de alto tráfego |
| **5** | Ensino load balancing; reconheço configurações problemáticas; domino as estratégias | Estabeleci a arquitetura de distribuição de tráfego de um produto |

---

## 2.4 TLS, Certificados e Comunicação Segura

**Conceito + por que existe:** Como estabelecer comunicação criptografada — TLS, certificados, autoridades certificadoras, e gestão de certificados (renovação, automação). Existe porque toda comunicação deve ser criptografada (princípio Zero Trust), e a gestão de certificados (especialmente sua renovação) é uma fonte comum de incidentes ("o certificado expirou").

**Profundidade esperada:** Intermediário · **Conexões:** → Criptografia (Guia de Segurança), → mTLS (Middle-End 7.3), → HTTP (Back-End 2.1)

**Erro de iniciante → Marca do sênior:** O iniciante configura TLS manualmente e esquece de renovar (causa outage quando expira). O sênior automatiza a emissão e renovação de certificados (Let's Encrypt, cert-manager), e entende a cadeia de confiança.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é TLS/HTTPS | — |
| **1** | Sei que HTTPS é "seguro", sem entender como | Explico que "o cadeado significa seguro" |
| **2** | Configuro TLS seguindo tutorial; não gerencio renovação | Configurei HTTPS seguindo um guia |
| **3** | Configuro TLS corretamente; entendo certificados e cadeia de confiança | Configurei TLS com renovação automática (Let's Encrypt) |
| **4** | Projeto a estratégia de certificados; automatizo renovação; antecipo expiração | Desenhei a gestão automatizada de certificados de uma aplicação |
| **5** | Ensino TLS e PKI; reconheço configurações fracas; domino a criptografia aplicada | Estabeleci a infraestrutura de certificados de um produto |

---

# CAMADA 3 — Containers

> *A unidade moderna de empacotamento e deploy. Resolve o "funciona na minha máquina" empacotando código e dependências juntos.*

**Referência base:**
> **[INDUSTRIAL]**
> Docker Documentation. https://docs.docker.com/
> — A referência para containerização com Docker.

---

## 3.1 Conceitos de Containerização e Isolamento

**Conceito + por que existe:** O que é um container e como ele isola processos — namespaces, cgroups, e a diferença entre containers e máquinas virtuais. Existe porque containers resolvem o problema de consistência de ambiente (empacotando código + dependências) com isolamento leve, e entender o mecanismo é essencial para usá-los corretamente.

**Profundidade esperada:** Avançado · **Conexões:** → Processos (1.1), → Orquestração (Camada 4), → SO (1.4)

**Erro de iniciante → Marca do sênior:** O iniciante trata containers como máquinas virtuais leves sem entender o modelo. O sênior entende que containers compartilham o kernel do host, usam namespaces/cgroups para isolamento, e sabe as implicações disso para segurança e recursos.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é um container | — |
| **1** | Ouvi falar de Docker, sem entender o conceito | Explico que "container empacota a aplicação" |
| **2** | Rodo containers seguindo tutoriais; não entendo o isolamento | Rodei um container com `docker run` |
| **3** | Entendo namespaces/cgroups; uso containers corretamente | Expliquei a diferença entre container e VM |
| **4** | Projeto considerando o modelo de isolamento; antecipo implicações de recursos e segurança | Desenhei limites de recursos e isolamento de containers |
| **5** | Ensino containerização; reconheço uso inadequado; domino os internals (namespaces, cgroups, runtimes) | Diagnostiquei um problema profundo de isolamento de container |

---

## 3.2 Imagens, Dockerfiles e Build de Containers

**Conceito + por que existe:** Como criar imagens de container — Dockerfiles, camadas, multi-stage builds, e otimização de tamanho. Existe porque a imagem é o artefato de deploy, e construí-la corretamente (pequena, segura, cacheável) afeta velocidade de build, tamanho de transferência e superfície de ataque.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Containerização (3.1), → Supply chain (Guia de Segurança), → CI/CD (Camada 7)

**Erro de iniciante → Marca do sênior:** O iniciante cria imagens gigantes, rodando como root, com tudo incluído. O sênior usa imagens base mínimas, multi-stage builds, usuário não-root, e ordena as camadas para maximizar cache — reconhecendo a imagem como parte da superfície de ataque.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei criar uma imagem de container | — |
| **1** | Sei que existe Dockerfile, sem saber escrever | Explico que "Dockerfile define a imagem" |
| **2** | Escrevo Dockerfiles básicos; imagens grandes, rodando como root | Criei um Dockerfile seguindo um exemplo |
| **3** | Escrevo Dockerfiles eficientes; uso imagem mínima e usuário não-root | Otimizei uma imagem com multi-stage build |
| **4** | Projeto a estratégia de build; otimizo cache e tamanho; endureço segurança | Desenhei imagens mínimas e seguras para uma aplicação |
| **5** | Ensino build de imagens; reconheço Dockerfiles problemáticos; domino otimização e segurança | Estabeleci os padrões de imagem de container de um time |

---

## 3.3 Registries e Distribuição de Imagens

**Conceito + por que existe:** Onde imagens são armazenadas e distribuídas — registries (Docker Hub, ECR, GCR), tags, digests, e versionamento de imagens. Existe porque imagens precisam ser compartilhadas entre build e deploy, e gerenciar versões (tags imutáveis vs mutáveis) e proveniência é importante para reprodutibilidade e segurança.

**Profundidade esperada:** Intermediário · **Conexões:** → Imagens (3.2), → CI/CD (Camada 7), → Supply chain (Guia de Segurança)

**Erro de iniciante → Marca do sênior:** O iniciante usa a tag `latest` para tudo (deploy não-reprodutível). O sênior usa tags imutáveis ou digests para reprodutibilidade, entende a proveniência da imagem, e escaneia imagens por vulnerabilidades.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é um registry | — |
| **1** | Ouvi falar de Docker Hub, sem entender | Explico que "imagens ficam guardadas em algum lugar" |
| **2** | Faço push/pull de imagens; uso `latest` para tudo | Fiz push de uma imagem para um registry |
| **3** | Uso tags versionadas; entendo digests e reprodutibilidade | Usei tags imutáveis para deploy reprodutível |
| **4** | Projeto a estratégia de versionamento de imagens; escaneio vulnerabilidades | Desenhei a estratégia de tags e scan de imagens |
| **5** | Ensino distribuição de imagens; reconheço práticas não-reprodutíveis; domino proveniência e assinatura | Estabeleci a estratégia de registry e supply chain de um produto |

---

## 3.4 Orquestração Local e Composição (Docker Compose)

**Conceito + por que existe:** Definir e rodar aplicações multi-container localmente — Docker Compose, redes entre containers, volumes. Existe porque aplicações reais têm múltiplos serviços (app + banco + cache), e compô-los de forma declarativa facilita desenvolvimento e testes locais antes da orquestração em produção.

**Profundidade esperada:** Intermediário · **Conexões:** → Containerização (3.1), → Kubernetes (Camada 4), → Desenvolvimento local

**Erro de iniciante → Marca do sênior:** O iniciante roda cada container manualmente com comandos longos. O sênior define a aplicação completa de forma declarativa (Compose), versiona essa definição, e a usa para ambientes de desenvolvimento reproduzíveis.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei rodar múltiplos containers juntos | — |
| **1** | Ouvi falar de Docker Compose, sem usar | Explico que "dá para rodar vários containers" |
| **2** | Uso um `docker-compose.yml` existente | Subi uma aplicação com `docker compose up` |
| **3** | Escrevo Compose files; configuro redes e volumes | Escrevi um Compose para app + banco + cache |
| **4** | Projeto ambientes locais reproduzíveis; gerencio dependências entre serviços | Desenhei o ambiente de desenvolvimento de uma aplicação multi-serviço |
| **5** | Ensino composição local; reconheço configurações frágeis; domino as nuances | Estabeleci o ambiente de desenvolvimento containerizado de um time |

---

# CAMADA 4 — Orquestração / Kubernetes

> *Como rodar containers em escala, com auto-recuperação e distribuição. A plataforma dominante de operação de containers em produção.*

**Referência base:**
> **[INDUSTRIAL]**
> Kubernetes Documentation. https://kubernetes.io/docs/
> — A referência oficial para Kubernetes.

---

## 4.1 Conceitos Fundamentais (Pods, Deployments, Services)

**Conceito + por que existe:** As abstrações centrais do Kubernetes — pods (unidade de deploy), deployments (gerência de réplicas), services (descoberta e balanceamento), e o modelo declarativo. Existe porque orquestrar containers em escala manualmente é inviável, e o Kubernetes fornece um modelo declarativo onde você descreve o estado desejado e ele mantém esse estado.

**Profundidade esperada:** Avançado · **Conexões:** → Containers (Camada 3), → Escalabilidade (Camada 9), → Service discovery (Middle-End 2.2)

**Erro de iniciante → Marca do sênior:** O iniciante trata o Kubernetes imperativamente (comandos `kubectl` ad-hoc). O sênior usa o modelo declarativo (manifests versionados), entende o reconciliation loop (o controle que mantém o estado desejado), e raciocina em termos de estado, não de comandos.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é Kubernetes | — |
| **1** | Ouvi falar, sem entender o modelo | Explico que "Kubernetes roda containers" |
| **2** | Rodo comandos `kubectl` seguindo tutoriais | Fiz deploy seguindo um guia passo a passo |
| **3** | Escrevo manifests; entendo pods, deployments, services | Escrevi manifests para fazer deploy de uma aplicação |
| **4** | Projeto no modelo declarativo; entendo o reconciliation loop; raciocino por estado | Desenhei os recursos K8s de uma aplicação com auto-recuperação |
| **5** | Ensino Kubernetes; reconheço anti-padrões; domino a arquitetura (control plane, etcd, controllers) | Estabeleci a arquitetura Kubernetes de um produto |

---

## 4.2 Configuração, Secrets e Gestão de Estado

**Conceito + por que existe:** Como gerenciar configuração e dados sensíveis no Kubernetes — ConfigMaps, Secrets, volumes persistentes, e StatefulSets. Existe porque aplicações precisam de configuração e às vezes de estado persistente, e o Kubernetes (projetado para workloads stateless) tem mecanismos específicos para isso que precisam ser usados corretamente.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Secrets (Back-End 10.2), → Estado (Back-End 8.2), → Conceitos K8s (4.1)

**Erro de iniciante → Marca do sênior:** O iniciante coloca configuração e secrets hardcoded na imagem, ou usa Secrets do K8s achando que são criptografados (são apenas base64 por padrão). O sênior externaliza configuração via ConfigMaps, gerencia secrets adequadamente (com criptografia em repouso ou vault externo), e entende as limitações.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei gerenciar configuração no K8s | — |
| **1** | Sei que existe ConfigMap/Secret, sem usar | Nomeio ConfigMap ou Secret |
| **2** | Uso ConfigMaps/Secrets seguindo exemplos; acho que Secrets são criptografados | Criei um ConfigMap seguindo tutorial |
| **3** | Externalizo config; gerencio secrets; uso volumes persistentes | Externalizei configuração via ConfigMap e Secret |
| **4** | Projeto a estratégia de config e secrets; integro vault externo; gerencio estado | Desenhei a gestão de secrets com criptografia ou vault |
| **5** | Ensino gestão de config/estado; reconheço secrets mal protegidos; domino StatefulSets e CSI | Estabeleci a estratégia de configuração e estado de um produto K8s |

---

## 4.3 Networking e Service Mesh no Kubernetes

**Conceito + por que existe:** Como o tráfego flui dentro e para fora do cluster — services, ingress, network policies, e a integração com service mesh. Existe porque comunicação entre pods, exposição de serviços ao exterior, e controle de tráfego são fundamentais, e o modelo de rede do Kubernetes é específico e não-trivial.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Redes (Camada 2), → Service mesh (Middle-End 7.1), → Load balancing (2.3)

**Erro de iniciante → Marca do sênior:** O iniciante não entende como expor um serviço ou por que dois pods não se comunicam. O sênior entende o modelo de rede do K8s (cluster IP, ingress, network policies), expõe serviços corretamente, e usa network policies para segmentação.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei como funciona rede no K8s | — |
| **1** | Sei que pods se comunicam, sem entender como | Explico que "os pods conversam entre si" |
| **2** | Exponho serviços seguindo tutoriais | Expus um serviço com um exemplo de ingress |
| **3** | Configuro services e ingress; entendo o modelo de rede | Configurei ingress e roteamento para uma aplicação |
| **4** | Projeto a topologia de rede do cluster; uso network policies; integro service mesh | Desenhei a rede e segmentação de um cluster |
| **5** | Ensino networking K8s; reconheço configurações problemáticas; domino CNI e service mesh | Estabeleci a arquitetura de rede de um cluster de produção |

---

## 4.4 Escalabilidade, Recursos e Scheduling

**Conceito + por que existe:** Como o Kubernetes aloca recursos e escala — requests/limits, autoscaling (HPA, VPA, cluster autoscaler), e o scheduling de pods. Existe porque dimensionar recursos corretamente é essencial para estabilidade (sem requests/limits, pods competem e caem) e custo, e o autoscaling permite responder à demanda automaticamente.

**Profundidade esperada:** Avançado · **Conexões:** → Escalabilidade (Back-End 8.2), → Recursos (1.1), → Confiabilidade (Camada 9)

**Erro de iniciante → Marca do sênior:** O iniciante não define requests/limits (pods são mortos ou monopolizam recursos). O sênior dimensiona requests/limits corretamente, configura autoscaling baseado em métricas, e entende como o scheduler distribui pods.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei como o K8s gerencia recursos | — |
| **1** | Ouvi falar de requests/limits, sem usar | Explico vagamente que "dá para limitar recursos" |
| **2** | Defino recursos copiando valores, sem critério | Coloquei requests/limits seguindo um exemplo |
| **3** | Dimensiono requests/limits corretamente; configuro autoscaling | Configurei HPA baseado em CPU para um serviço |
| **4** | Projeto a estratégia de recursos e escala; ajusto scheduling; otimizo custo | Desenhei o autoscaling e dimensionamento de uma aplicação |
| **5** | Ensino gestão de recursos; reconheço dimensionamento ruim; domino o scheduler e autoscalers | Otimizei recursos e custo de um cluster de produção |

---

# CAMADA 5 — Cloud e Modelos de Serviço

> *A infraestrutura sob demanda que sustenta sistemas modernos. Onde a infraestrutura vira código e recurso elástico.*

**Referência base:**
> **[PADRÃO-NIST]**
> Mell, P., & Grance, T. (2011). *The NIST Definition of Cloud Computing.* NIST Special Publication 800-145.
> DOI: 10.6028/NIST.SP.800-145
> — A definição canônica de computação em nuvem: cinco características essenciais (on-demand self-service, broad network access, resource pooling, rapid elasticity, measured service) e os três modelos de serviço (IaaS, PaaS, SaaS).

---

## 5.1 Modelos de Serviço e Responsabilidade Compartilhada

**Conceito + por que existe:** Os modelos de serviço cloud (IaaS, PaaS, SaaS) e o modelo de responsabilidade compartilhada — o que o provedor gerencia vs o que você gerencia. Existe porque escolher o nível certo de abstração (gerenciar VMs vs usar serviços gerenciados) é uma decisão de trade-off fundamental, e entender quem é responsável por quê é crítico para segurança.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Segurança (Camada 10), → IaC (Camada 6), → NIST 800-145

**Erro de iniciante → Marca do sênior:** O iniciante assume que "está na cloud, então é seguro/gerenciado" sem entender suas responsabilidades. O sênior entende o modelo de responsabilidade compartilhada (o provedor protege a infraestrutura; você protege seus dados, configuração e acesso), e escolhe o modelo de serviço pelo trade-off.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço os modelos de cloud | — |
| **1** | Ouvi falar de IaaS/PaaS/SaaS, sem entender | Nomeio um dos modelos |
| **2** | Uso serviços cloud sem entender as fronteiras de responsabilidade | Usei uma VM ou serviço gerenciado |
| **3** | Entendo IaaS/PaaS/SaaS e responsabilidade compartilhada; escolho o nível | Escolhi entre VM e serviço gerenciado conscientemente |
| **4** | Projeto a estratégia de serviços; escolho por trade-off (controle vs gestão); aplico responsabilidade compartilhada | Desenhei a arquitetura cloud de uma aplicação por trade-offs |
| **5** | Ensino modelos de cloud; reconheço escolhas inadequadas; domino as implicações de cada modelo | Estabeleci a estratégia de cloud de uma organização |

---

## 5.2 Computação, Armazenamento e Banco Gerenciados

**Conceito + por que existe:** Os serviços fundamentais de cloud — computação (VMs, serverless, containers gerenciados), armazenamento (object storage, block storage), e bancos gerenciados. Existe porque esses são os blocos de construção de qualquer sistema na cloud, e escolher o serviço certo (e dimensioná-lo) afeta performance, custo e operação.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Banco (Back-End 4.4), → Escalabilidade (Camada 9), → Custo

**Erro de iniciante → Marca do sênior:** O iniciante usa o serviço que conhece sem comparar opções nem dimensionar (superprovisiona ou subprovisiona). O sênior escolhe o serviço pelo perfil de carga, dimensiona corretamente, e entende os trade-offs (serverless vs VM, object vs block storage).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço os serviços de cloud | — |
| **1** | Ouvi falar de VMs e storage na cloud, sem usar | Nomeio um serviço de cloud |
| **2** | Provisiono serviços seguindo tutoriais | Criei uma VM ou bucket seguindo guia |
| **3** | Escolho e configuro serviços adequados; dimensiono | Escolhi object storage vs block storage corretamente |
| **4** | Projeto a estratégia de serviços; escolho por trade-off; otimizo custo/performance | Desenhei a infraestrutura de computação e dados de uma aplicação |
| **5** | Ensino serviços de cloud; reconheço escolhas subótimas; domino o catálogo e os trade-offs | Estabeleci a arquitetura de serviços cloud de um produto |

---

## 5.3 Networking de Cloud (VPC, sub-redes, conectividade)

**Conceito + por que existe:** Como a rede é estruturada na cloud — VPCs (redes virtuais), sub-redes, gateways, peering, e conectividade híbrida. Existe porque isolar e conectar recursos corretamente é fundamental para segurança e arquitetura, e o modelo de rede cloud é uma camada que precisa ser projetada deliberadamente.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Redes (Camada 2), → Segurança (Camada 10), → K8s networking (4.3)

**Erro de iniciante → Marca do sênior:** O iniciante coloca tudo em rede pública ou usa a VPC padrão sem pensar. O sênior projeta a topologia de rede (sub-redes públicas/privadas, isolamento), coloca recursos sensíveis em sub-redes privadas, e controla a conectividade.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é uma VPC | — |
| **1** | Ouvi falar de VPC, sem entender | Explico vagamente "rede na cloud" |
| **2** | Uso a VPC padrão sem configurar | Subi recursos na rede padrão |
| **3** | Configuro VPC, sub-redes e roteamento; isolo recursos | Criei sub-redes públicas e privadas com isolamento |
| **4** | Projeto a topologia de rede cloud; segmento; planejo conectividade híbrida | Desenhei a topologia VPC de uma aplicação |
| **5** | Ensino networking cloud; reconheço topologias inseguras; domino a conectividade avançada | Estabeleci a arquitetura de rede cloud de um produto |

---

## 5.4 Custo, FinOps e Otimização de Recursos

**Conceito + por que existe:** Gerenciar e otimizar o custo da infraestrutura cloud — modelos de precificação, dimensionamento, e a disciplina de FinOps. Existe porque a cloud cobra por uso, e sem gestão de custo a conta cresce descontroladamente — dimensionar corretamente e escolher os modelos de preço certos (on-demand, reserved, spot) tem impacto financeiro direto.

**Profundidade esperada:** Intermediário · **Conexões:** → Recursos (4.4), → Computação (5.2), → Escalabilidade (Camada 9)

**Erro de iniciante → Marca do sênior:** O iniciante superprovisiona "por garantia" e ignora a conta. O sênior dimensiona pelo uso real, usa modelos de preço apropriados (spot para cargas tolerantes a falha, reserved para baseline), e monitora custo como uma métrica de primeira classe.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não penso em custo de cloud | — |
| **1** | Sei que a cloud custa, sem gerenciar | Explico que "a cloud cobra por uso" |
| **2** | Provisiono sem pensar em custo | Já superprovisionei recursos "por garantia" |
| **3** | Dimensiono pelo uso; entendo os modelos de preço | Reduzi custo dimensionando recursos corretamente |
| **4** | Projeto para custo-eficiência; uso spot/reserved estrategicamente; monitoro custo | Desenhei uma arquitetura otimizando custo com spot instances |
| **5** | Ensino FinOps; reconheço desperdício; domino as estratégias de otimização | Estabeleci a prática de gestão de custo de uma organização |

> *Conexão com seu perfil: esta competência conecta diretamente à sua estratégia de usar AWS Spot Instances para treino pesado de modelos — dimensionar e escolher o modelo de preço certo é exatamente o nível 4 desta competência.*

---

# CAMADA 6 — Infraestrutura como Código (IaC)

> *Tratar infraestrutura como software — versionada, revisável, reproduzível. A base da automação confiável e da mentalidade DevOps.*

**Referência base:**
> **[INDUSTRIAL]**
> Morris, K. (2020). *Infrastructure as Code: Dynamic Systems for the Cloud Age* (2nd ed.). O'Reilly.
> — A referência definitiva para os princípios e práticas de IaC.

---

## 6.1 Princípios de IaC e Infraestrutura Declarativa

**Conceito + por que existe:** Definir infraestrutura em código versionado e declarativo em vez de configuração manual — o que torna a infraestrutura reproduzível, revisável e auditável. Existe porque infraestrutura configurada manualmente é não-reproduzível, sujeita a drift (divergência do estado esperado) e impossível de auditar; IaC traz as práticas de engenharia de software para a infraestrutura.

**Profundidade esperada:** Avançado · **Conexões:** → Versionamento (Front-End/Back-End), → CI/CD (Camada 7), → Shell (1.3)

**Erro de iniciante → Marca do sênior:** O iniciante configura infraestrutura clicando no console (não-reproduzível, não-versionado). O sênior define tudo em código declarativo versionado, entende a diferença entre declarativo e imperativo, e trata mudanças de infraestrutura com revisão de código.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é IaC | — |
| **1** | Ouvi falar, sem entender o conceito | Explico que "infraestrutura vira código" |
| **2** | Configuro infraestrutura pelo console; ocasionalmente uso scripts | Configuro recursos clicando no console |
| **3** | Defino infraestrutura em código declarativo; versiono | Defini infraestrutura em código versionado |
| **4** | Projeto a estratégia de IaC; trato drift; revisão de mudanças como código | Desenhei a infraestrutura de uma aplicação inteiramente como código |
| **5** | Ensino IaC; reconheço configuração manual e drift; domino os princípios e padrões | Estabeleci a prática de IaC de uma organização |

---

## 6.2 Ferramentas de Provisionamento (Terraform e equivalentes)

**Conceito + por que existe:** As ferramentas que provisionam infraestrutura declarativamente — Terraform, Pulumi, CloudFormation — e seus conceitos (state, plan/apply, módulos). Existe porque provisionar infraestrutura cloud manualmente não escala, e essas ferramentas gerenciam o ciclo de vida dos recursos com um modelo declarativo e rastreamento de estado.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Princípios de IaC (6.1), → Cloud (Camada 5), → CI/CD (Camada 7)

**Erro de iniciante → Marca do sênior:** O iniciante roda `terraform apply` sem entender o state ou revisar o plan (mudanças destrutivas inesperadas). O sênior entende o state (e o protege), sempre revisa o plan antes de aplicar, e modulariza a infraestrutura para reúso.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço ferramentas de IaC | — |
| **1** | Ouvi falar de Terraform, sem usar | Nomeio uma ferramenta de IaC |
| **2** | Rodo `terraform apply` seguindo tutoriais; não entendo o state | Provisionei recursos seguindo um guia |
| **3** | Escrevo configurações; entendo state e plan/apply; reviso o plan | Provisionei infraestrutura revisando o plan antes |
| **4** | Projeto a estrutura de IaC; modularizo; protejo e gerencio o state remotamente | Desenhei módulos reutilizáveis de infraestrutura |
| **5** | Ensino ferramentas de IaC; reconheço configurações frágeis; domino state, módulos e padrões | Estabeleci a arquitetura de IaC de uma organização |

---

## 6.3 Gestão de Configuração e Provisionamento de Servidores

**Conceito + por que existe:** Configurar e manter o estado de servidores de forma automatizada — ferramentas como Ansible, e o conceito de configuração idempotente. Existe porque, além de provisionar recursos (Terraform), é preciso configurar o que roda dentro deles, e fazê-lo de forma idempotente e versionada evita o "configurei manualmente e esqueci o que fiz".

**Profundidade esperada:** Intermediário · **Conexões:** → IaC (6.1), → Shell (1.3), → Containers (Camada 3)

**Erro de iniciante → Marca do sênior:** O iniciante configura servidores via SSH manual, sem registro. O sênior usa gestão de configuração idempotente e versionada, de forma que qualquer servidor possa ser recriado a partir do código.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é gestão de configuração | — |
| **1** | Ouvi falar de Ansible, sem usar | Nomeio uma ferramenta de configuração |
| **2** | Configuro servidores via SSH manual | Configurei um servidor manualmente via SSH |
| **3** | Uso gestão de configuração idempotente; versiono | Automatizei a configuração de um servidor com Ansible |
| **4** | Projeto a estratégia de configuração; garanto idempotência e reprodutibilidade | Desenhei a configuração automatizada de uma frota de servidores |
| **5** | Ensino gestão de configuração; reconheço configuração manual; domino as ferramentas e padrões | Estabeleci a prática de gestão de configuração de um time |

---

## 6.4 Ambientes, Imutabilidade e GitOps

**Conceito + por que existe:** Gerenciar múltiplos ambientes (dev/staging/prod) de forma consistente, infraestrutura imutável (substituir em vez de modificar), e GitOps (Git como fonte de verdade do estado da infraestrutura). Existe porque inconsistência entre ambientes causa o "funciona em staging mas não em prod", e a imutabilidade + GitOps trazem reprodutibilidade e auditabilidade ao deploy de infraestrutura.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → IaC (6.1), → CI/CD (Camada 7), → Kubernetes (Camada 4)

**Erro de iniciante → Marca do sênior:** O iniciante modifica servidores em produção manualmente (configuration drift, ambientes divergentes). O sênior trata infraestrutura como imutável (recria em vez de modificar), mantém paridade entre ambientes, e usa GitOps onde o estado desejado vive no Git.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço esses conceitos | — |
| **1** | Ouvi falar de imutabilidade/GitOps, sem entender | Explico vagamente "não mexer no servidor direto" |
| **2** | Modifico ambientes manualmente; ambientes divergem | Já modifiquei produção manualmente |
| **3** | Mantenho paridade entre ambientes; pratico imutabilidade | Recriei infraestrutura em vez de modificá-la |
| **4** | Projeto a estratégia de ambientes; implemento GitOps; garanto paridade | Desenhei o fluxo GitOps de uma aplicação |
| **5** | Ensino imutabilidade e GitOps; reconheço drift; domino as práticas | Estabeleci a estratégia de ambientes e GitOps de uma organização |

---

# CAMADA 7 — CI/CD e Automação de Deploy

> *O pipeline que leva código a produção de forma automatizada e confiável. O coração operacional do DevOps.*

**Referências base:**
> **[CLÁSSICO]**
> Humble, J., & Farley, D. (2010). *Continuous Delivery: Reliable Software Releases through Build, Test, and Deployment Automation.* Addison-Wesley. (Jolt Award 2011)

> **[PEER-REVIEWED / Research-backed]**
> Forsgren, N., Humble, J., & Kim, G. (2018). *Accelerate.* IT Revolution. — As métricas DORA (Deployment Frequency, Lead Time, MTTR, Change Failure Rate) medem diretamente a maturidade desta camada.

---

## 7.1 Pipelines de CI (Integração Contínua)

**Conceito + por que existe:** Automação que integra, testa e valida cada mudança de código continuamente — build, testes, lint, análise estática a cada commit/PR. Existe porque integrar e validar manualmente não escala e depende de disciplina; a CI torna a qualidade estrutural ao rodar verificações automaticamente em cada mudança.

**Profundidade esperada:** Avançado · **Conexões:** → Testes (Front-End 9 / Back-End), → Análise estática (Guia de Segurança), → CD (7.2)

**Erro de iniciante → Marca do sênior:** O iniciante roda testes localmente (quando roda) e integra mudanças grandes esporadicamente. O sênior tem CI que roda em cada PR, bloqueia merge se algo falhar, e integra mudanças pequenas e frequentes — entendendo que "make your build self-testing" é princípio fundamental.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é CI | — |
| **1** | Ouvi falar, sem saber o que faz | Explico que "automatiza testes" |
| **2** | Sei que existe um pipeline, sem configurá-lo | Vi um pipeline de CI rodar |
| **3** | Configuro CI para rodar testes/lint/build; entendo os estágios | Configurei um pipeline que roda testes em cada PR |
| **4** | Projeto o pipeline de CI; quality gates; otimizo tempo de feedback | Desenhei um pipeline de CI com gates bloqueantes |
| **5** | Ensino CI; reconheço pipelines mal projetados; domino as práticas e otimização | Estabeleci a estratégia de CI de uma organização |

---

## 7.2 Pipelines de CD (Entrega/Deploy Contínuo)

**Conceito + por que existe:** Automação que leva código validado a produção — deploy automatizado, com validação e capacidade de rollback. Existe porque deploy manual é lento, propenso a erro e arriscado; o CD automatiza a entrega de forma que deploys sejam frequentes, pequenos e reversíveis — reduzindo o risco de cada deploy.

**Profundidade esperada:** Avançado · **Conexões:** → CI (7.1), → Estratégias de deploy (7.3), → IaC (Camada 6)

**Erro de iniciante → Marca do sênior:** O iniciante faz deploy manual, com medo, raramente. O sênior tem CD automatizado com validação, deploys pequenos e frequentes, e rollback automático — entendendo que deploys frequentes e pequenos são *menos* arriscados que deploys grandes e raros (contraintuitivo mas validado pela pesquisa DORA).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é CD | — |
| **1** | Ouvi falar, sem saber o que faz | Explico que "automatiza o deploy" |
| **2** | Faço deploy manual; não automatizo | Fiz deploy manualmente |
| **3** | Automatizo deploy com validação; implemento rollback | Configurei deploy automatizado com rollback |
| **4** | Projeto o pipeline de CD; deploys pequenos e frequentes; validação automatizada | Desenhei um pipeline de CD com validação e rollback automático |
| **5** | Ensino CD; reconheço processos de deploy arriscados; domino as práticas e métricas DORA | Estabeleci a estratégia de CD de uma organização |

---

## 7.3 Estratégias de Deploy (blue-green, canary, rolling)

**Conceito + por que existe:** As técnicas para fazer deploy minimizando risco e downtime — rolling update, blue-green (dois ambientes, troca instantânea), canary (liberar para um subconjunto antes de todos). Existem porque substituir uma versão por outra abruptamente é arriscado; essas estratégias permitem validar a nova versão com tráfego real antes de comprometer todos os usuários.

**Profundidade esperada:** Avançado · **Conexões:** → CD (7.2), → Disponibilidade (Camada 9), → Observabilidade (Camada 8)

**Erro de iniciante → Marca do sênior:** O iniciante substitui a versão antiga pela nova de uma vez (downtime e risco total). O sênior usa estratégias progressivas (canary, blue-green), monitora a nova versão com tráfego real, e tem rollback rápido se métricas degradarem.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço estratégias de deploy | — |
| **1** | Ouvi falar de blue-green/canary, sem entender | Nomeio uma estratégia de deploy |
| **2** | Substituo a versão diretamente; aceito downtime | Já fiz deploy com downtime substituindo tudo |
| **3** | Implemento rolling update; entendo blue-green e canary | Implementei rolling update sem downtime |
| **4** | Projeto a estratégia de deploy; uso canary com métricas; rollback automático por sintoma | Desenhei deploy canary com rollback baseado em métricas |
| **5** | Ensino estratégias de deploy; reconheço processos arriscados; domino deploys progressivos | Estabeleci a estratégia de deploy de baixo risco de um produto |

---

## 7.4 Automação de Pipeline e Quality Gates

**Conceito + por que existe:** A orquestração completa do pipeline com portões de qualidade automatizados — integração de testes, segurança (SAST/SCA), e aprovações que bloqueiam progressão se critérios não forem atendidos. Existe porque um pipeline só agrega valor se garante qualidade automaticamente; quality gates tornam impossível promover código que não passa nos critérios.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → CI (7.1), → Segurança no CI (Guia de Segurança), → Testes

**Erro de iniciante → Marca do sênior:** O iniciante tem um pipeline que roda mas não bloqueia nada (testes falham e o deploy continua). O sênior projeta quality gates que bloqueiam a progressão (cobertura mínima, zero vulnerabilidades críticas, testes passando), tornando a qualidade não-negociável.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que são quality gates | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "verificações no pipeline" |
| **2** | Tenho pipeline que roda mas não bloqueia | Meu pipeline roda testes mas não bloqueia merge |
| **3** | Configuro gates que bloqueiam; integro testes e segurança | Configurei o pipeline para bloquear em teste falho |
| **4** | Projeto a estratégia de gates; integro SAST/SCA; defino critérios de promoção | Desenhei quality gates com cobertura e segurança bloqueantes |
| **5** | Ensino quality gates; reconheço pipelines sem rigor; domino a integração completa | Estabeleci a estratégia de qualidade de pipeline de uma organização |

---

# CAMADA 8 — Observabilidade de Infraestrutura

> *Você não pode operar o que não pode ver. A diferença entre descobrir um problema em segundos ou descobri-lo pelos usuários reclamando.*

**Referência base:**
> **[INDUSTRIAL]**
> Beyer, B., et al. (2016). *Site Reliability Engineering.* O'Reilly. https://sre.google/sre-book/ — Capítulo 6 (Monitoring Distributed Systems) define os princípios de observabilidade.

---

## 8.1 Logs, Métricas e Traces (os três pilares)

**Conceito + por que existe:** Os três tipos fundamentais de telemetria — logs (eventos), métricas (valores agregados ao longo do tempo), e traces (caminho de uma requisição). Existe porque cada pilar responde a uma pergunta diferente (o que aconteceu / qual o estado de saúde / onde o tempo foi gasto), e juntos dão visibilidade completa do sistema.

**Profundidade esperada:** Avançado · **Conexões:** → Logging (Back-End 9.1), → Métricas (Back-End 9.2), → Tracing (Back-End 9.3)

**Erro de iniciante → Marca do sênior:** O iniciante só tem logs (e os lê manualmente quando algo quebra). O sênior instrumenta os três pilares, entende qual usar para cada pergunta, e os correlaciona (de uma métrica anômala para os traces e logs relevantes).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço os pilares de observabilidade | — |
| **1** | Sei que existem logs, sem os outros pilares | Explico que "logs mostram o que aconteceu" |
| **2** | Uso logs; não tenho métricas nem traces estruturados | Olhei logs quando algo quebrou |
| **3** | Instrumento os três pilares; sei qual usar para cada pergunta | Instrumentei logs, métricas e traces num serviço |
| **4** | Projeto a estratégia de observabilidade; correlaciono os pilares; instrumento o que importa | Desenhei a observabilidade de um sistema correlacionando os três pilares |
| **5** | Ensino observabilidade; reconheço telemetria inadequada; domino OpenTelemetry e a teoria | Estabeleci a estratégia de observabilidade de um produto |

---

## 8.2 Dashboards, Visualização e Análise

**Conceito + por que existe:** Transformar telemetria em visualizações acionáveis — dashboards (Grafana), agregação, e análise de tendências. Existe porque dados brutos de telemetria são inúteis sem visualização; dashboards bem projetados dão visibilidade imediata do estado de saúde e revelam tendências e anomalias.

**Profundidade esperada:** Intermediário · **Conexões:** → Pilares (8.1), → Métricas (Back-End 9.2), → SLO (Camada 9)

**Erro de iniciante → Marca do sênior:** O iniciante não tem dashboards ou os enche de gráficos sem foco. O sênior projeta dashboards focados nos sinais que importam (golden signals), organizados para diagnóstico rápido, e evita ruído visual.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é um dashboard de observabilidade | — |
| **1** | Ouvi falar de Grafana, sem usar | Nomeio uma ferramenta de dashboard |
| **2** | Olho dashboards prontos; não crio | Vi um dashboard existente |
| **3** | Crio dashboards com métricas relevantes | Construí um dashboard com os golden signals |
| **4** | Projeto dashboards para diagnóstico rápido; foco nos sinais que importam | Desenhei os dashboards operacionais de um serviço |
| **5** | Ensino visualização; reconheço dashboards ruidosos ou inúteis; domino as práticas | Estabeleci a estratégia de dashboards de um produto |

---

## 8.3 Alertas e Resposta a Incidentes

**Conceito + por que existe:** Notificar automaticamente quando algo requer atenção, e o processo de responder a incidentes — alertas acionáveis, on-call, e runbooks. Existe porque ninguém olha dashboards 24/7; alertas avisam proativamente, mas precisam ser acionáveis (alertar sobre sintomas que afetam usuários, não sobre cada flutuação) para evitar fadiga de alerta.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Métricas (Back-End 9.2), → SLO (Camada 9), → Resposta a incidentes (Guia de Segurança)

**Erro de iniciante → Marca do sênior:** O iniciante não tem alertas (descobre pelos usuários) ou tem alertas demais (fadiga, ignorados). O sênior configura alertas acionáveis baseados em sintomas (impacto ao usuário), com runbooks, e itera para reduzir ruído — entendendo que um alerta que não exige ação deve ser eliminado.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei configurar alertas | — |
| **1** | Sei que dá para alertar, sem saber como | Explico que "o sistema avisa quando dá problema" |
| **2** | Descubro problemas pelos usuários; sem alertas estruturados | Já soube de um problema pelos usuários |
| **3** | Configuro alertas; entendo acionabilidade | Configurei alertas baseados em sintomas |
| **4** | Projeto a estratégia de alertas; reduzo fadiga; crio runbooks | Desenhei alertas acionáveis com runbooks para um serviço |
| **5** | Ensino alertas e resposta a incidentes; reconheço fadiga de alerta; domino a prática SRE | Estabeleci a estratégia de alertas e on-call de uma organização |

---

## 8.4 Diagnóstico e Análise de Causa Raiz

**Conceito + por que existe:** A habilidade de investigar incidentes e encontrar a causa raiz — usar telemetria para diagnosticar, post-mortems sem culpa, e prevenção de recorrência. Existe porque resolver o sintoma sem a causa raiz garante recorrência; o diagnóstico sistemático e os post-mortems transformam incidentes em melhorias permanentes.

**Profundidade esperada:** Avançado · **Conexões:** → Observabilidade (toda a camada), → Raciocínio sobre falhas (Eixo 4), → SRE (Camada 9)

**Erro de iniciante → Marca do sênior:** O iniciante reinicia o serviço (resolve o sintoma) sem entender a causa. O sênior usa a telemetria para diagnóstico sistemático, conduz post-mortems sem culpa, e implementa prevenção — transformando cada incidente em aprendizado.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei diagnosticar problemas de produção | — |
| **1** | Reinicio e torço para resolver | Já resolvi reiniciando sem entender a causa |
| **2** | Investigo superficialmente; resolvo sintomas | Olhei logs mas não cheguei à causa raiz |
| **3** | Diagnostico com telemetria; encontro a causa raiz | Encontrei a causa raiz de um incidente com telemetria |
| **4** | Projeto a investigação; conduzo post-mortems; previno recorrência | Conduzi um post-mortem que gerou melhorias permanentes |
| **5** | Ensino análise de causa raiz; reconheço investigação superficial; domino a cultura blameless | Estabeleci a prática de post-mortem de uma organização |

> *Conexão com seu diagnóstico (Eixo 4): esta competência é a manifestação operacional do raciocínio sobre falhas. Diagnóstico de causa raiz é o oposto do happy-path thinking.*

---

# CAMADA 9 — Confiabilidade, Escalabilidade e Disponibilidade

> *As propriedades emergentes que definem um sistema de produção maduro. Onde a infraestrutura encontra os requisitos de negócio.*

**Referência base:**
> **[INDUSTRIAL]**
> Beyer, B., et al. (2016). *Site Reliability Engineering.* O'Reilly. — A referência definitiva para confiabilidade em escala.

---

## 9.1 Alta Disponibilidade e Tolerância a Falhas

**Conceito + por que existe:** Projetar sistemas que continuam funcionando apesar de falhas — redundância, eliminação de pontos únicos de falha (SPOF), e failover. Existe porque hardware e software falham inevitavelmente, e sistemas de produção precisam continuar disponíveis apesar dessas falhas — o que exige redundância deliberada.

**Profundidade esperada:** Avançado · **Conexões:** → Resiliência (Back-End 8.4), → Load balancing (2.3), → Disponibilidade

**Erro de iniciante → Marca do sênior:** O iniciante projeta sistemas com pontos únicos de falha (uma instância, uma zona). O sênior elimina SPOFs com redundância (múltiplas instâncias, múltiplas zonas de disponibilidade), projeta failover automático, e entende os níveis de disponibilidade (os "noves").

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é alta disponibilidade | — |
| **1** | Ouvi falar, sem entender | Explico que "o sistema deve ficar no ar" |
| **2** | Projeto com pontos únicos de falha sem perceber | Já tive um SPOF que causou outage |
| **3** | Elimino SPOFs com redundância; entendo failover | Projetei redundância em múltiplas zonas |
| **4** | Projeto a estratégia de disponibilidade; failover automático; defino os noves | Desenhei a arquitetura de alta disponibilidade de um sistema |
| **5** | Ensino alta disponibilidade; reconheço SPOFs por inspeção; domino as estratégias | Estabeleci a arquitetura de disponibilidade de um produto |

---

## 9.2 Escalabilidade e Elasticidade

**Conceito + por que existe:** A capacidade de o sistema crescer com a demanda — escala horizontal, autoscaling, e elasticidade (escalar para cima e para baixo automaticamente). Existe porque a demanda varia (picos, crescimento), e um sistema que não escala ou degrada nos picos ou desperdiça recursos no vale — a elasticidade ajusta a capacidade à demanda real.

**Profundidade esperada:** Avançado · **Conexões:** → Escalabilidade (Back-End 8.2), → Recursos K8s (4.4), → Custo (5.4)

**Erro de iniciante → Marca do sênior:** O iniciante provisiona capacidade fixa (cai no pico ou desperdiça no vale). O sênior projeta para escala horizontal com autoscaling baseado em demanda, e entende os gargalos que impedem a escala (estado, banco, dependências).

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é escalabilidade de infraestrutura | — |
| **1** | Ouvi falar, sem entender | Explico que "aguentar mais usuários" |
| **2** | Provisiono capacidade fixa; aumento manualmente | Aumentei recursos manualmente num pico |
| **3** | Configuro autoscaling; projeto para escala horizontal | Configurei autoscaling baseado em demanda |
| **4** | Projeto a estratégia de elasticidade; identifico gargalos de escala; otimizo | Desenhei a elasticidade de um sistema antecipando gargalos |
| **5** | Ensino escalabilidade; reconheço gargalos por inspeção; domino as estratégias em escala | Estabeleci a arquitetura de escalabilidade de um produto |

---

## 9.3 Backup, Disaster Recovery e Continuidade

**Conceito + por que existe:** As estratégias para recuperar dados e operação após desastres — backups, replicação geográfica, e planos de disaster recovery (RTO/RPO). Existe porque desastres acontecem (falha de hardware, erro humano, região inteira fora), e sem backups testados e plano de recuperação, um desastre pode significar perda permanente de dados ou negócio.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Replicação (Back-End 8.3), → Disponibilidade (9.1), → Continuidade de negócio

**Erro de iniciante → Marca do sênior:** O iniciante não tem backups ou os tem mas nunca testou a restauração (descobre que não funcionam no desastre). O sênior tem backups automatizados e *testados*, define RTO/RPO alinhados ao negócio, e tem plano de DR ensaiado.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não penso em backup e recuperação | — |
| **1** | Sei que backups existem, sem estratégia | Explico que "precisa fazer backup" |
| **2** | Tenho backups, mas nunca testei restauração | Tenho backups que nunca restaurei |
| **3** | Automatizo backups; testo restauração; entendo RTO/RPO | Testei a restauração de um backup com sucesso |
| **4** | Projeto a estratégia de DR; defino RTO/RPO; ensaio recuperação | Desenhei e ensaiei o plano de disaster recovery de um sistema |
| **5** | Ensino DR e continuidade; reconheço backups não-testados; domino as estratégias | Estabeleci a estratégia de continuidade de negócio de uma organização |

---

## 9.4 Capacity Planning e Performance em Escala

**Conceito + por que existe:** Antecipar e dimensionar a capacidade necessária — planejamento de capacidade, testes de carga, e identificação de gargalos sob escala. Existe porque crescer sem planejamento leva a degradação ou outage nos momentos de maior demanda (ironicamente, os mais importantes para o negócio), e testes de carga revelam os limites antes que os usuários os encontrem.

**Profundidade esperada:** Avançado · **Conexões:** → Profiling (Back-End 7.4), → Escalabilidade (9.2), → Performance

**Erro de iniciante → Marca do sênior:** O iniciante descobre os limites de capacidade quando o sistema cai em produção. O sênior faz testes de carga para conhecer os limites antecipadamente, planeja capacidade para o crescimento esperado, e identifica gargalos antes que se tornem incidentes.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é capacity planning | — |
| **1** | Ouvi falar de teste de carga, sem fazer | Explico vagamente "ver se aguenta carga" |
| **2** | Não testo carga; descubro limites em produção | Já descobri um limite quando o sistema caiu |
| **3** | Faço testes de carga; identifico limites; planejo capacidade | Fiz um teste de carga e encontrei o limite de um serviço |
| **4** | Projeto a estratégia de capacity planning; antecipo gargalos; planejo crescimento | Desenhei o planejamento de capacidade de um sistema em crescimento |
| **5** | Ensino capacity planning; reconheço falta de planejamento; domino modelagem de capacidade | Estabeleci a prática de capacity planning de uma organização |

---

# CAMADA 10 — Segurança de Infraestrutura

> *A defesa da fundação. Onde a infraestrutura encontra atacantes. (Complementa o Guia de Segurança nas camadas de infra.)*

**Referência base:**
> **[PADRÃO-NIST]**
> NIST SP 800-207 (2020). *Zero Trust Architecture.* DOI: 10.6028/NIST.SP.800-207 — o modelo de referência para segurança sem perímetro confiável.

---

## 10.1 Hardening e Configuração Segura

**Conceito + por que existe:** Endurecer sistemas removendo capacidades, serviços e configurações desnecessárias — seguindo benchmarks de configuração segura (CIS). Existe porque configurações padrão são frequentemente permissivas demais, e cada serviço, porta ou capacidade desnecessária é uma superfície de ataque evitável.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Superfície de ataque (Back-End 10.4), → Permissões (1.2), → Containers (3.2)

**Erro de iniciante → Marca do sênior:** O iniciante usa configurações padrão e deixa serviços desnecessários rodando. O sênior endurece sistemas seguindo benchmarks (CIS), remove o desnecessário, e trata a configuração segura como parte da redução da superfície de ataque.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é hardening | — |
| **1** | Ouvi falar, sem saber aplicar | Explico vagamente "deixar o sistema mais seguro" |
| **2** | Uso configurações padrão; não endureço | Subi um sistema com configuração padrão |
| **3** | Endureço sistemas; removo o desnecessário; sigo benchmarks | Apliquei CIS Benchmarks a um servidor |
| **4** | Projeto a estratégia de hardening; automatizo; reduzo superfície de ataque | Desenhei o hardening automatizado de uma frota |
| **5** | Ensino hardening; reconheço configurações inseguras; domino os benchmarks e práticas | Estabeleci os padrões de configuração segura de uma organização |

---

## 10.2 Gestão de Identidade e Acesso na Infraestrutura (IAM)

**Conceito + por que existe:** Controlar quem pode acessar e fazer o quê na infraestrutura — IAM cloud, roles, políticas, e o princípio do menor privilégio aplicado à infraestrutura. Existe porque acesso excessivo à infraestrutura é um vetor crítico (credenciais comprometidas com permissões amplas = comprometimento total), e o IAM granular limita o blast radius.

**Profundidade esperada:** Avançado · **Conexões:** → Autorização (Back-End 5.4), → Menor privilégio (Back-End 10.4), → Zero Trust

**Erro de iniciante → Marca do sênior:** O iniciante usa credenciais de administrador para tudo e compartilha acessos. O sênior aplica o menor privilégio (roles específicas, permissões mínimas), usa identidades gerenciadas em vez de credenciais estáticas, e audita acessos.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não sei o que é IAM de infraestrutura | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "controle de acesso na cloud" |
| **2** | Uso credenciais admin para tudo | Já usei uma conta admin para tarefas comuns |
| **3** | Aplico menor privilégio; uso roles específicas | Criei roles com permissões mínimas |
| **4** | Projeto a estratégia de IAM; uso identidades gerenciadas; audito acessos | Desenhei a estratégia de IAM de uma aplicação cloud |
| **5** | Ensino IAM; reconheço permissões excessivas; domino o modelo e Zero Trust | Estabeleci a arquitetura de IAM de uma organização |

---

## 10.3 Segurança de Containers e Kubernetes

**Conceito + por que existe:** Proteger a camada de containers e orquestração — imagens sem vulnerabilidades, containers sem privilégios excessivos, pod security, e RBAC do Kubernetes. Existe porque containers e Kubernetes introduzem superfícies de ataque específicas (imagens vulneráveis, containers privilegiados, RBAC mal configurado), e protegê-los exige conhecimento específico.

**Profundidade esperada:** Intermediário-Avançado · **Conexões:** → Containers (Camada 3), → Kubernetes (Camada 4), → Supply chain (Guia de Segurança)

**Erro de iniciante → Marca do sênior:** O iniciante roda containers privilegiados, com imagens não-escaneadas, e RBAC permissivo. O sênior escaneia imagens, roda containers sem privilégios e como não-root, configura pod security e RBAC mínimo, e entende a superfície de ataque específica de containers.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço segurança de containers | — |
| **1** | Sei que containers têm riscos, sem conhecê-los | Explico que "containers podem ser inseguros" |
| **2** | Rodo containers sem pensar em segurança | Já rodei um container privilegiado |
| **3** | Escaneio imagens; rodo sem privilégios; configuro RBAC | Configurei containers não-root e RBAC mínimo |
| **4** | Projeto a estratégia de segurança de containers; pod security; supply chain | Desenhei a segurança de containers de um cluster |
| **5** | Ensino segurança de containers/K8s; reconheço configurações inseguras; domino a superfície de ataque | Estabeleci os padrões de segurança de containers de uma organização |

---

## 10.4 Compliance, Auditoria e Postura de Segurança

**Conceito + por que existe:** Manter e demonstrar conformidade com padrões de segurança — auditoria, políticas, varredura contínua de configuração, e gestão de postura de segurança (CSPM). Existe porque segurança não é um estado pontual mas contínuo, e organizações precisam demonstrar conformidade (regulatória ou interna), detectar desvios de configuração, e manter visibilidade da postura de segurança.

**Profundidade esperada:** Intermediário · **Conexões:** → Hardening (10.1), → IAM (10.2), → Segurança geral (Guia de Segurança)

**Erro de iniciante → Marca do sênior:** O iniciante verifica segurança pontualmente (ou nunca) e não detecta desvios. O sênior implementa varredura contínua de configuração, auditoria automatizada, e mantém visibilidade da postura de segurança ao longo do tempo.

**Progressão Dreyfus:**

| Nível | O que significa para esta competência | Teste de validação |
|-------|----------------------------------------|--------------------|
| **0** | Não conheço compliance e auditoria de segurança | — |
| **1** | Ouvi falar, sem entender | Explico vagamente "seguir regras de segurança" |
| **2** | Verifico segurança pontualmente, sem continuidade | Fiz uma verificação de segurança manual uma vez |
| **3** | Implemento varredura de configuração; entendo auditoria | Configurei varredura de configuração de segurança |
| **4** | Projeto a estratégia de postura de segurança; auditoria contínua; CSPM | Desenhei a postura de segurança contínua de uma aplicação |
| **5** | Ensino compliance e postura; reconheço lacunas de auditoria; domino as práticas e ferramentas | Estabeleci a prática de gestão de postura de segurança de uma organização |

---

# Planilha de Auto-Auditoria — Infraestrutura / Cloud / DevOps

Registre seu nível (0-5) em cada competência. **Regra:** não marque um nível sem passar no teste de validação. Anote a evidência concreta.

## Camada 1 — Sistemas Operacionais / Linux

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 1.1 Processos, Sinais e Recursos | ___ | |
| 1.2 Sistema de Arquivos e Permissões | ___ | |
| 1.3 Shell, Scripting e Automação | ___ | |
| 1.4 Fundamentos de SO (memória, kernel) | ___ | |

## Camada 2 — Redes e Conectividade

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 2.1 Fundamentos de Rede (TCP/IP, DNS) | ___ | |
| 2.2 Firewalls e Segurança de Rede | ___ | |
| 2.3 Load Balancing | ___ | |
| 2.4 TLS e Certificados | ___ | |

## Camada 3 — Containers

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 3.1 Conceitos de Containerização | ___ | |
| 3.2 Imagens e Dockerfiles | ___ | |
| 3.3 Registries e Distribuição | ___ | |
| 3.4 Orquestração Local (Compose) | ___ | |

## Camada 4 — Orquestração / Kubernetes

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 4.1 Conceitos Fundamentais (Pods, etc.) | ___ | |
| 4.2 Configuração, Secrets e Estado | ___ | |
| 4.3 Networking e Service Mesh | ___ | |
| 4.4 Escalabilidade e Scheduling | ___ | |

## Camada 5 — Cloud e Modelos de Serviço

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 5.1 Modelos de Serviço e Responsabilidade | ___ | |
| 5.2 Computação, Storage e Banco Gerenciados | ___ | |
| 5.3 Networking de Cloud (VPC) | ___ | |
| 5.4 Custo, FinOps e Otimização | ___ | |

## Camada 6 — Infraestrutura como Código (IaC)

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 6.1 Princípios de IaC | ___ | |
| 6.2 Ferramentas de Provisionamento (Terraform) | ___ | |
| 6.3 Gestão de Configuração | ___ | |
| 6.4 Ambientes, Imutabilidade e GitOps | ___ | |

## Camada 7 — CI/CD e Automação de Deploy

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 7.1 Pipelines de CI | ___ | |
| 7.2 Pipelines de CD | ___ | |
| 7.3 Estratégias de Deploy (canary, etc.) | ___ | |
| 7.4 Automação de Pipeline e Quality Gates | ___ | |

## Camada 8 — Observabilidade de Infraestrutura

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 8.1 Logs, Métricas e Traces | ___ | |
| 8.2 Dashboards e Visualização | ___ | |
| 8.3 Alertas e Resposta a Incidentes | ___ | |
| 8.4 Diagnóstico e Causa Raiz | ___ | |

## Camada 9 — Confiabilidade, Escalabilidade e Disponibilidade

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 9.1 Alta Disponibilidade e Tolerância a Falhas | ___ | |
| 9.2 Escalabilidade e Elasticidade | ___ | |
| 9.3 Backup e Disaster Recovery | ___ | |
| 9.4 Capacity Planning | ___ | |

## Camada 10 — Segurança de Infraestrutura

| Competência | Nível (0-5) | Evidência concreta |
|-------------|-------------|--------------------|
| 10.1 Hardening e Configuração Segura | ___ | |
| 10.2 IAM de Infraestrutura | ___ | |
| 10.3 Segurança de Containers e K8s | ___ | |
| 10.4 Compliance e Postura de Segurança | ___ | |

---

## Interpretação do Resultado

- **Especialista em Infraestrutura/DevOps** significa **nível 4+ no tier de automação (camadas 5-7)** e **nível 4+ no tier de maturidade (camadas 8-9)** — porque é o domínio de automação (IaC, CI/CD) e operação madura (observabilidade, confiabilidade) que define o engenheiro de DevOps, não apenas saber rodar containers. As camadas 1-2 (substrato) devem estar em nível 3+ e a camada 10 (segurança) em nível 3+.

- **O tier de automação (5-7) é o divisor de águas.** Muita gente sabe rodar containers e fazer deploy manual (camadas 1-4), mas o que separa o sênior de DevOps é automatizar tudo de forma reproduzível (IaC) e operar com confiabilidade medida (DORA metrics, SLOs). A mentalidade "se é manual, automatize" é a marca da disciplina.

- **As métricas DORA são o termômetro objetivo desta sub-área.** Deployment Frequency, Lead Time, MTTR e Change Failure Rate (Forsgren et al., 2018) medem diretamente a maturidade da operação — e a pesquisa mostrou que velocidade e estabilidade não são trade-off, mas andam juntas em equipes de alta performance.

- **Para o seu perfil específico:** esta é provavelmente a sub-área onde você tem *exposição parcial mas não estruturada* — você opera em ambientes com produção (logo, toca infraestrutura) mas seu foco é ML/pipeline, não operação. As conexões mais fortes com seu diagnóstico: o gap de fundamentos computacionais (Eixo 1) aparece nas camadas 1-2; o gap de raciocínio sobre falhas (Eixo 4) aparece na camada 8 (diagnóstico) e 9 (confiabilidade); e o gap crítico de segurança (gestão de segredos) aparece na camada 10. A camada 5.4 (FinOps) conecta diretamente à sua estratégia de AWS Spot para treino de modelos.

- **Nota de contexto para ML:** muitas dessas competências têm um análogo direto em MLOps (a Parte 2 abordará isso). Containers, CI/CD, IaC e observabilidade são a base sobre a qual MLOps se constrói — dominar esta sub-área é pré-requisito para operar sistemas de ML em produção, que é exatamente o seu domínio profissional.

---

## Referências

| # | Fonte | Tipo | Uso |
|---|-------|------|-----|
| 1 | Dreyfus & Dreyfus (1980). *Five-Stage Model of Skill Acquisition.* UC Berkeley. | **PEER-REVIEWED** | Escala de progressão |
| 2 | Smith & Kendall (1963). *Retranslation of Expectations.* JAP, 47(2). DOI: 10.1037/h0047060 | **PEER-REVIEWED** | Âncoras comportamentais (BARS) |
| 3 | Kruger & Dunning (1999). *Unskilled and Unaware of It.* JPSP, 77(6). | **PEER-REVIEWED** | Viés de auto-avaliação |
| 4 | Kim, Humble, Debois & Willis (2016). *The DevOps Handbook.* IT Revolution. | **INDUSTRIAL** | Cultura e práticas DevOps (toda a disciplina) |
| 5 | Forsgren, Humble & Kim (2018). *Accelerate.* IT Revolution. | **PEER-REVIEWED / Research-backed** | Métricas DORA (camadas 7, 9) |
| 6 | Beyer et al. (2016). *Site Reliability Engineering.* O'Reilly. https://sre.google/sre-book/ | **INDUSTRIAL** | Observabilidade e confiabilidade (camadas 8, 9) |
| 7 | Morris, K. (2020). *Infrastructure as Code* (2nd ed.). O'Reilly. | **INDUSTRIAL** | IaC (camada 6) |
| 8 | Humble & Farley (2010). *Continuous Delivery.* Addison-Wesley. | **CLÁSSICO** | CI/CD (camada 7) |
| 9 | Mell & Grance (2011). *The NIST Definition of Cloud Computing.* NIST SP 800-145. DOI: 10.6028/NIST.SP.800-145 | **PADRÃO-NIST** | Modelos de cloud (camada 5) |
| 10 | NIST SP 800-207 (2020). *Zero Trust Architecture.* DOI: 10.6028/NIST.SP.800-207 | **PADRÃO-NIST** | Segurança de infra (camada 10) |
| 11 | Nemeth et al. (2017). *UNIX and Linux System Administration Handbook* (5th ed.). | **CLÁSSICO** | Linux/SO (camada 1) |
| 12 | Kubernetes Documentation. https://kubernetes.io/docs/ | **INDUSTRIAL** | Kubernetes (camada 4) |

---

*Parte 1D de 4 do Skill-Check de Engenharia de Software. **Parte 1 (Engenharia de Software) COMPLETA**: Front-End, Back-End, Middle-End/Integração e Infraestrutura/DevOps.*
*Próximas partes do projeto: Parte 2 (Desenvolvedor de IA), Parte 3 (Data Scientist), e as sínteses (Partes 4-7: matriz comparativa, arquitetura de maturidade, checklist consolidado, análise final).*
*Escala ancorada em Dreyfus (1980) + BARS (Smith & Kendall, 1963). Auto-avaliação deve ser complementada por validação externa de pares seniores (Kruger & Dunning, 1999).*
*Revisão recomendada a cada 6 meses, registrando a evolução de nível e a nova evidência concreta.*
