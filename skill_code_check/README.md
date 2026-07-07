# Relatório de Diagnóstico e Desenvolvimento — Prática de Codificação Assistida por IA, Verificação e Manutenção de Habilidade

> Síntese analítica de uma conversa técnica sobre o uso de IA na escrita de código, a verificação de artefatos gerados por IA, o risco de atrofia de habilidade, e a estrutura profunda dos domínios de Engenharia de Software, Ciência de Dados e Desenvolvimento de IA.

---

## Contexto e Propósito

Este relatório consolida uma discussão que partiu de uma pergunta aparentemente simples — *"devo me preocupar por digitar menos código na era da IA?"* — e evoluiu para um exame rigoroso de (a) se a prática atual de verificação produz compreensão real ou ilusão de compreensão; (b) como manter a independência epistemológica quando o mesmo agente que gera também verifica; (c) qual é o estado real da habilidade sob a dependência de IA; e (d) qual é a estrutura profunda de cada domínio técnico que deveria orientar o esforço de consolidação.

O relatório é organizado para servir a decisões: separa explicitamente o que está bem (e deve continuar) do que precisa melhorar (ordenado por consequência), fecha com um plano calibrado e com as limitações honestas da própria análise. Cada afirmação relevante está ancorada em literatura verificável, com o nível de confiança explícito quando a evidência é indireta.

---

## 1. Sumário Executivo

**O diagnóstico em uma frase:** a prática de codificação está *estruturalmente acima da média* (você não aceita cegamente a saída da IA — você a analisa), mas contém um defeito arquitetural grave (a verificação é circular: código, relatório e teste vêm da mesma fonte) e opera num modo cognitivo que constrói *reconhecimento* em vez de *recall*, o que deixa a habilidade generativa dependente da ferramenta.

**Os três achados centrais:**

1. **A verificação não é independente.** Quando a IA escreve o código, o relatório que o explica e os testes que o checam, os três compartilham a mesma origem e, portanto, os mesmos pontos cegos. Isso viola o princípio de independência do oráculo em teste de software e é o defeito de maior consequência.

2. **A compreensão via relatório é ilusória por construção.** Ler uma explicação fluente produz a *sensação* de entender muito além do entendimento real (illusion of explanatory depth). O modo "rodar primeiro, analisar se funcionou" instala essa ilusão porque entrega a confirmação antes de testar o próprio modelo mental.

3. **A habilidade generativa não está perdida, mas seu estado é parcialmente incerto.** A geração de Python nativo está intacta (evidência direta). O recall de idiomas de biblioteca de alta frequência escorregou de ativo para passivo (terceirizado à IA). E a camada mais profunda — lógica algorítmica sob pressão — está com status *não resolvido*, porque não é ativamente exercitada e a ausência de sintoma não prova preservação.

**A ação de maior alavancagem imediata**, dentro da restrição de tempo atual, não é estudar mais — é *inverter a ordem* nos trechos de código que carregam consequência: prever antes de rodar, em vez de rodar antes de analisar. O trabalho de fundo (consolidação de núcleo e teste de fluência) pertence à janela pós-TCC de 2027, como o planejamento de vida já sequenciou.

---

## 2. A Questão Central, Reformulada

A pergunta original — *"digitar menos é motivo de preocupação?"* — está mal-posta, e respondê-la diretamente levaria a uma conclusão enganosamente tranquilizadora. Ela funde duas variáveis independentes que precisam ser separadas:

- **Quem digita o código** (irrelevante — digitar sintaxe é a atividade de menor valor e menor transferência).
- **Quão profundamente você entende e consegue reproduzir o resultado** (é tudo o que importa).

A reformulação correta é:

> **O meu protocolo de verificação pós-geração produz o mesmo modelo mental que eu teria se tivesse escrito o código — um modelo *gerativo*, capaz de prever e reproduzir — ou produz apenas a *ilusão* desse modelo, um reconhecimento que se sente como compreensão mas colapsa quando a ferramenta não está disponível?**

Toda a análise subsequente responde a essa pergunta. A métrica "volume de digitação" é um falso indicador; a métrica real é "independência da verificação" e "geratividade do modelo mental".

---

## 3. Respostas Comuns Porém Incorretas

Situar a prática contra os erros dominantes é necessário porque a validação genérica ("você está no caminho certo") não distingue uma prática robusta de uma que apenas *parece* robusta.

**Erro 1 — "Digitar menos é declínio; volte a escrever tudo à mão."** Falso. Confunde a métrica (volume de digitação) com o valor (profundidade de entendimento e qualidade de decisão de design). Rejeitar a IA por nostalgia do esforço confunde o atrito *desejável* (reconstrução conceitual, que constrói memória) com o atrito *inútil* (sintaxe, que não transfere). A pesquisa de carga cognitiva (Sweller, 1988) sustenta que o esforço deve ser realocado para o processamento que constrói esquema, não eliminado nem preservado indiscriminadamente.

**Erro 2 — "A IA escreve e roda; se passou, está bom."** É o *vibe coding* puro, e é onde a maioria efetivamente falha. A ausência total de verificação independente entrega a garantia de qualidade a um sistema que não tem modelo de mundo confiável e alucina com fluência. Este erro é o oposto simétrico do Erro 1.

**Erro 3 — "Recuperar a habilidade significa memorizar de cor cada sintaxe e método das bibliotecas que uso pesado."** Falso, impossível e fonte de ansiedade desnecessária. Nenhum engenheiro sênior memoriza a API completa de uma biblioteca séria; consultar API de baixa frequência é o comportamento profissional correto. O alvo real é converter um *núcleo pequeno* de idiomas de alta frequência de passivo (reconheço) para ativo (escrevo sem consultar) — analogia direta com vocabulário ativo vs passivo em língua natural.

A prática correta está *entre* os Erros 1 e 2 — nem rejeita a ferramenta nem confia cegamente. Mas estar "entre os dois" não basta: a *qualidade da verificação* é o que separa o robusto do aparentemente robusto, e é aí que reside o trabalho.

---

## 4. Os Quatro Defeitos da Prática Atual

### 4.1 Circularidade da Verificação — o defeito fatal potencial

**O mecanismo.** Se a IA escreve o código, escreve o relatório que o explica e escreve os testes que o verificam, os três artefatos compartilham a mesma origem e, portanto, os mesmos erros sistemáticos e os mesmos pontos cegos. Um relatório gerado pela IA sobre o código da IA não é verificação independente — é a mesma hipótese reafirmada com outras palavras. Se o modelo interpretou mal um requisito, ele o interpretará mal de forma *consistente* no código, no relatório e no teste, e os três "concordarão" harmoniosamente enquanto estão todos errados juntos.

**Por que é o mais grave.** Em teoria de testes de software, isso viola o **princípio de independência do oráculo**: um teste só tem poder de detecção se a fonte da *expectativa* (o oráculo) for independente da fonte da *implementação* (Weyuker, 1982). Quando ambas são o mesmo LLM, o teste perde grande parte do seu poder. O problema é mais profundo que o viés psicológico de "automation bias" (Parasuraman & Manzey, 2010; Skitka, Mosier & Burdick, 1999) — é uma dependência *estrutural* na cadeia de evidência, não apenas uma tendência de confiar demais.

**A mitigação.** Quebrar a circularidade deliberadamente, injetando independência em pelo menos um ponto da cadeia — detalhado como protocolo na Seção 10. O princípio: a expectativa precisa vir de você (derivada do requisito) ou de uma fonte externa (um invariante, uma referência), nunca do próprio código.

### 4.2 Ilusão de Profundidade Explicativa (IOED)

**O mecanismo.** Ler uma explicação lúcida gera uma sensação de compreensão que excede o entendimento real — o *illusion of explanatory depth* (Rozenblit & Keil, 2002): as pessoas acreditam entender mecanismos muito melhor do que realmente entendem, e a fluência da explicação *aumenta* a ilusão. Um relatório bem escrito pela IA é um vetor perfeito para esse efeito.

**A conexão com aprendizagem.** A fluência da prosa é *inversamente* relacionada ao esforço de reconstrução que constrói memória durável. O princípio de *desirable difficulties* (Bjork & Bjork, 2011) estabelece que aprendizagem robusta exige atrito; um relatório que entrega tudo mastigado remove justamente o atrito que grava. Ler passivamente confirma; reconstruir corrige.

**A mitigação.** Inverter a ordem em pontos-chave: antes de ler o relatório (ou rodar o código), comprometer-se com uma predição explícita do que o código faz e como processa internamente; só então comparar. O aprendizado está na *discrepância* entre a predição e o resultado. Complementarmente, *active recall*: após analisar um trecho, fechar tudo e reexplicar sem olhar.

### 4.3 Viés de Caminho Feliz nos Testes

**O mecanismo.** LLMs tendem a gerar testes do caminho normal (normal path) e omitir casos de borda: dados vazios, valores extremos, entradas malformadas, concorrência, Unicode, dados fora de ordem. A instrução genérica "adicione casos estranhos" é fraca, porque delega ao próprio modelo a definição de "estranho" — e o espaço de falhas que ele não imagina é exatamente o que ele não vai gerar.

**A mitigação.** O espaço de falha deve ser enumerado a partir do *domínio* (o entendimento do problema), não a partir do código. Para o seu domínio de detecção de phishing, isso significa perguntar concretamente: o que acontece com uma URL de 2000 caracteres? Com caracteres Unicode? Com dados chegando fora de ordem cronológica? Derivar casos-limite lendo a solução garante que você só testa o que a solução já contempla — cego exatamente onde ela é cega.

### 4.4 Atrofia da Capacidade de Geração sob Pressão

**O mecanismo.** Revisar código e produzir código do zero são habilidades correlacionadas mas não idênticas. É possível manter uma capacidade de revisão afiada e, ainda assim, ver a fluência *gerativa* degradar — a capacidade de, diante de uma página em branco e sem IA, recuperar a estrutura da memória de longo prazo e escrever a solução correta. A revisão opera sobre um artefato existente; a geração exige recuperação ativa. Se a recuperação nunca é exercitada, ela enfraquece, independentemente de quão boa esteja a revisão.

**Por que importa concretamente para o seu caso.** Contextos onde a geração sem IA é exigida e não são hipotéticos: entrevistas técnicas de Data Scientist (testadas ao vivo, sem IA), incidentes de produção com a ferramenta indisponível, e contextos onde enviar código a um LLM externo viola confidencialidade — diretamente relevante ao ambiente NHK/Persol.

**A mitigação.** Preservar deliberadamente um espaço de geração manual sob restrição de tempo, sem IA. O veículo natural é o competitive programming (Codeforces, CSES). *Registro importante:* este veículo não está sendo praticado atualmente (por restrição de tempo), o que torna o estado da camada mais profunda de habilidade não-verificado — ver Seção 6.

---

## 5. O Paradoxo do Oráculo e Sua Resolução

Este foi o ponto mais profundo levantado na conversa, e a sua resolução é central para o protocolo. **O paradoxo:** se *você* precisa ser o oráculo independente (a fonte da expectativa), mas *você também* sofre de IOED (acredita entender mais do que entende), então o oráculo é ele próprio falível — parecendo violar o mesmo princípio de independência que deveria satisfazer. O que impede você de "perder a credibilidade" como oráculo?

**A resolução exige separar duas propriedades ortogonais:**

- **Independência** — os erros do oráculo *não são correlacionados* com os erros da implementação.
- **Confiabilidade** — o oráculo está *correto em termos absolutos*.

O erro embutido no paradoxo é supor que um oráculo precisa ser confiável para agregar valor. **Não precisa.** Um oráculo falível mas independente ainda captura erros, desde que seus erros sejam de um *tipo diferente* dos erros do código. Esta é a lógica da redundância diversa: **N-version programming** (Avizienis & Chen, 1977) não exige que nenhuma versão seja perfeita; exige que falhem *independentemente*, para que a probabilidade de falha em modo-comum seja baixa. Quando você deriva a expectativa *a partir do requisito* (não do código), seu caminho de raciocínio difere do caminho de implementação da IA, e os modos de falha se decorrelacionam. Você pode errar, mas erra *outra coisa*.

**O golpe de honestidade que impede uma resolução ingênua.** Um resultado clássico — **Knight & Leveson (1986)** — demonstrou empiricamente que versões desenvolvidas *independentemente* por equipes separadas **não falham independentemente**: nos casos difíceis, desenvolvedores independentes cometem erros *correlacionados*, porque a dificuldade está no problema, não nas pessoas. Duas consequências:

1. A mitigação "use um segundo modelo para revisar o primeiro" é **mais fraca do que parece**, e para LLMs é pior que para equipes humanas: duas sessões de LLM compartilham dados de treino e, portanto, modos de falha muito mais do que duas equipes humanas independentes. A "independência" de dois Claudes é largamente ilusória — a mesma razão pela qual dois chats concordando *não* é validação.

2. A saída real não é confiar em segundo modelo nem no seu entendimento falível — é ancorar a verificação, onde possível, em **verdades externas que nem você nem a IA geram**: invariantes matemáticos, relações metamórficas, dados de referência com resposta conhecida, propriedades que *têm* que valer independentemente de qualquer implementação. Estes são oráculos cuja correção *não depende* nem da sua confiabilidade nem da da IA.

**Por que isto aponta para a sua vantagem específica.** Formular invariantes é uma habilidade matemática — exatamente a sua vantagem comparativa. O oráculo mais forte (imune tanto à circularidade da IA quanto à sua IOED) é o invariante formal, e você é, entre os perfis, o mais equipado para produzi-lo. O paradoxo que parecia desqualificá-lo como oráculo na verdade aponta onde você é *insubstituível*: não como quem "entende o código", mas como quem formula as propriedades que o código tem que respeitar.

**O teste de auto-credibilidade.** Como saber, num momento dado, se você está no modo oráculo-confiável ou no modo IOED? O discriminador é **predição sobre entradas novas**. Se você consegue *prever* a saída do código para um input ainda não visto, seu modelo é *gerativo* (oráculo credível). Se você só consegue *reconhecer/explicar* depois de ver o código rodar, é IOED (não-credível). A IOED colapsa sob predição, porque prever exige um modelo gerador que o mero reconhecimento não possui. Elegantemente, a predição-antes-de-ler é *simultaneamente* a técnica de aprendizagem (Seção 4.2) e o teste de credibilidade do oráculo — o mesmo ato serve às duas funções.

**O enquadramento epistemológico.** Este é o *oracle problem* de Weyuker (1982), e é um caso particular do problema geral da justificação do conhecimento sem fundacionismo. Não existe um oráculo-fundação, certo e externo a tudo. O que existe é o **barco de Neurath**: reconstrói-se o navio prancha por prancha, no mar, usando as outras pranchas como apoio — o que só funciona se as pranchas não apodrecerem *juntas* (modo-comum). A resolução é *coerentista*, não fundacionista: a correção emerge da *conjunção de checagens falíveis, decorrelacionadas e externamente ancoradas*, cuja concordância — desde que genuinamente independentes — empurra a probabilidade de erro não-detectado para baixo, sem que nenhum elo isolado seja perfeito.

---

## 6. A Recalibração do Diagnóstico: As Três Camadas e o Alvo Real

A conversa refinou o modelo de habilidade em três camadas, com status distintos:

| Camada | Descrição | Status | Evidência |
|--------|-----------|--------|-----------|
| **1 — Lógica / algoritmos** | Decomposição de problemas, estruturas de dados, raciocínio algorítmico | **Incerto (não resolvido)** | Não exercitado (sem competitive programming); ausência de sintoma ≠ preservação |
| **2 — Python nativo** | Geração da linguagem-base sem biblioteca | **Intacto** | Evidência direta sua |
| **3 — Recall de API de biblioteca** | pandas, PyTorch, SQL de memória | **Escorregou de ativo para passivo** | Trava no `groupby` sem IA; uso mediado por IA constrói reconhecimento |

**Os três pontos analíticos decisivos:**

1. **Travar em API de biblioteca não é, por si só, um defeito.** É o estado normal e saudável que a documentação existe para servir. A pergunta correta não é "eu travo em sintaxe de biblioteca?" (todos travam), mas "eu travo no *pequeno núcleo de alta frequência* que deveria ser fluente?". Para um cientista de dados, esse núcleo é `groupby().agg()`, `merge`, `pivot`/`melt`, `apply`, `loc`/`iloc`, `fillna`/`dropna`, `value_counts`, `sort_values`, `rolling` — talvez 30–50 idiomas que cobrem ~90% do uso real. Consolidá-los é trabalho de *semanas* de retrieval practice, não de meses de memorização enciclopédica.

2. **O alvo real é uma fração do fantasma.** A ansiedade sobre "memorizar tudo" (Erro 3) desaparece quando o alvo se torna "puxar o núcleo ativo de volta de passivo para ativo". A base empírica é o *savings in relearning* (Ebbinghaus): reaprender material antes dominado é muito mais rápido — o que sustenta a *direção* (será rápido porque a base está lá), embora o número específico ("2–4 meses", "semanas") seja estimativa de praticante, não constante de pesquisa.

3. **A incerteza da Camada 1 é a única questão que bloqueia uma priorização precisa.** Se a lógica está intacta, só o núcleo de biblioteca precisa de consolidação (trabalho leve). Se a lógica decaiu, a prioridade muda. Isso só se resolve com o teste frio da Seção 11 — nenhuma quantidade de análise substitui o dado.

**A base empírica da recuperação.** O mecanismo de "recall > recognition" é um dos achados mais robustos da psicologia cognitiva: **Roediger & Karpicke (2006)** demonstraram que recuperar da memória (testar-se) fortalece a retenção muito mais do que reler/reconhecer, em centenas de replicações. A implicação direta: *analisar código pronto da IA constrói reconhecimento, que é a causa da atrofia, não a cura*. A cura é a recuperação ativa — escrever de memória.

**Ressalva de honestidade epistemológica.** Toda a base empírica citada vem de *outros domínios* (fatos, vocabulário, conceitos). Não existe literatura robusta e direta sobre atrofia de habilidade de programação especificamente por dependência de IA — o fenômeno é recente demais. A explicação é uma *extrapolação* de literatura adjacente bem estabelecida para um caso novo. A extrapolação é razoável (os mecanismos cognitivos subjacentes são gerais), mas é inferência, não evidência direta. Confie na direção, não na precisão dos números.

---

## 7. A Topologia dos Três Domínios e o Gargalo Universal

A intuição de que cada domínio tem uma "estrutura invariante" que orienta o que consolidar está *fundamentalmente correta* e tem nome na literatura: é a distinção entre *deep structure* e *surface structure* de um domínio (Chi, Feltovich & Glaser, 1981 — especialistas organizam o conhecimento por estrutura profunda, novatos por características superficiais). Especialistas não sabem mais fatos; organizam o domínio em torno de poucas estruturas profundas das quais o resto deriva.

**A correção crítica:** "topologia" é metáfora útil mas imprecisa — o que se busca não é topologia no sentido matemático (invariância sob deformação contínua), mas a *estrutura de dependência* e o *núcleo irredutível* de cada domínio. E a topologia diz qual **estrutura conceitual** internalizar; a sintaxe a consolidar é a *sombra* dessa estrutura, não a estrutura em si. Confundir "aprender a topologia" com "saber qual sintaxe decorar" é a armadilha (ver Seção 14).

**As três topologias, reduzidas ao esqueleto que carrega peso:**

**Engenharia de Software.** Invariante: *tudo é transformação de estado através de fronteiras*. Esqueleto: `entrada → validação (fronteira de confiança) → lógica → estado persistente → saída`, onde cada fronteira é onde a confiança muda e a falha pode ocorrer. Gargalo onde a maioria peca: **não** o caminho feliz, mas a transição para o caminho adversarial — concorrência sobre o mesmo estado, escrita no banco com sucesso mas publicação de evento falhando, dependência lenta. O ponto crucial é *raciocínio sobre falha parcial e consistência de estado sob concorrência*. (No front-end: invariante `UI = f(estado)`; gargalo em *sincronização de estado* — cliente, servidor e DOM consistentes sob mudança assíncrona; quebra em invalidação de cache e estado derivado.)

**Ciência de Dados.** Invariante: *dos dados a uma decisão sob incerteza, sem se enganar*. Esqueleto: `pergunta → estimando → dados (amostra enviesada da realidade) → inferência → decisão`. O ponto crucial que quase todos pulam, e o mais profundo dos três: o **estimando** — a definição precisa de *qual quantidade se está tentando medir* — antes de qualquer modelo. Gargalo seguinte: *causalidade vs correlação e validade* (vazamento, confusores, p-hacking). A topologia da Ciência de Dados é, no fundo, a disciplina de *não se enganar*.

**Desenvolvimento de IA.** Invariante: *aprender de dados uma função que generaliza*. Esqueleto: `dados → representação → modelo → otimização → generalização → deploy`. Ponto crucial e gargalo: a **lacuna de generalização** — a diferença entre desempenho no treino e na realidade/produção. A maioria otimiza a métrica de treino e falha na mudança de distribuição e no *training-serving skew*. Mais fundo: entender *por que* algo generaliza (bias-variance, capacidade, regularização) em vez de só chamar `.fit()`.

**O insight que unifica os três — e o mais importante do relatório.** Os gargalos dos três domínios — falha parcial e concorrência (SW), confusores e vazamento (DS), mudança de distribuição (IA) — **são a mesma coisa sob três nomes**: a transição do caso limpo/feliz para o caso onde a *realidade é adversarial*. Em todos os três, o gargalo não é sintaxe nem algoritmo — é a *maturidade de raciocinar sobre o caso adversarial*. Este é, exatamente, o mesmo padrão que aparece transversalmente como a fronteira de senioridade: projetar antecipando falhas em vez de focar no caminho de sucesso. A topologia dos três domínios converge para o mesmo ponto.

E daí decorre — como sombra — o que consolidar: os idiomas que valem fluência são os que implementam as operações centrais de cada invariante (para DS, `groupby`/`merge`/`pivot`/window functions são os verbos de "remodelar dados em direção ao estimando" — por isso são o núcleo, e não escolha arbitrária). A sintaxe a consolidar é a sombra da topologia; nada além.

---

## 8. Pontos Fortes — O Que Está Bem e Deve Continuar Progredindo

Estes são ativos reais e específicos, não elogios genéricos. Devem ser preservados e ampliados.

**F1 — O instinto de não aceitar cegamente a saída da IA.** A realocação de esforço da digitação para a análise/verificação é direcionalmente correta e alinhada à literatura de aprendizagem (efeito de auto-explicação — Chi et al., 1989) e à migração do valor humano do conhecimento *gerativo* para o *avaliativo* à medida que ferramentas geram. A maioria não faz sequer isso. Continue — com a emenda da independência (Seção 10).

**F2 — Meta-cognição de alto nível (o ativo mais raro).** Ao longo da conversa você (a) diagnosticou sozinho que estava em modo reconhecimento em vez de recall; (b) formulou independentemente a intuição da estrutura profunda ("topologia") dos domínios; e (c) pediu explicitamente um teste para *se falsificar* em vez de se confirmar. Essas três coisas são, precisamente, comportamento de *oráculo credível*: alguém que gera, que busca a estrutura profunda, e que quer ser testado contra a realidade em vez de acreditar na própria estimativa. Isto é mais valioso e mais difícil de adquirir do que qualquer competência técnica pontual.

**F3 — Fundação matemática e conceitual profunda.** A capacidade de engajar o paradoxo do oráculo em nível epistemológico, de conectar verificação a invariantes formais, e de intuir a estrutura profunda dos domínios reflete uma base que é a sua vantagem comparativa. Especificamente: formular invariantes (a base de property-based e metamorphic testing) é uma habilidade matemática — o oráculo mais forte disponível, e o lugar onde você é insubstituível.

**F4 — Capacidade generativa fundamental intacta.** A geração de Python nativo não atrofiou (evidência direta). O medo mais grave — não conseguir escrever solução alguma sem IA — está descartado por observação. A base generativa está preservada; o trabalho é de recuperação de camadas específicas, não de reconstrução.

**F5 — Honestidade intelectual e disposição para feedback duro.** Você recebeu correções diretas (o modo de trabalho *é* o que produz a IOED; a Camada 1 está incerta; o alvo que você imaginava era um fantasma) e atualizou em vez de defender. Essa disposição é pré-requisito para todo o resto e não deve ser subestimada.

---

## 9. Pontos a Melhorar — Ordenados por Consequência

Ordenados do mais grave ao menos grave, com a ação correspondente.

**M1 — A verificação é circular (o defeito de maior consequência).** Código, relatório e teste vêm da mesma fonte, sem oráculo independente. *Ação:* injetar independência — a expectativa deve vir do requisito ou de um invariante externo, nunca do código (protocolo na Seção 10). Este é o item que mais separa a sua prática de uma prática robusta.

**M2 — O modo de trabalho instala a IOED.** O esquema "gerar → rodar → analisar-se-funcionou" (aplicado com Copilot na NHK) entrega a confirmação antes de testar o modelo mental, construindo reconhecimento em vez de recall. *Ação:* inverter a ordem — *prever antes de rodar* — nos trechos que carregam lógica que você precisa dominar. Não em tudo (calibrado por consequência); o Copilot no trabalho permanece eficiente para o código de baixa consequência.

**M3 — Operar em reconhecimento em vez de recall.** Analisar código gerado, mesmo organizando-o didaticamente, constrói reconhecimento — a causa da atrofia, não a cura. *Ação:* substituir análise-de-código-pronto por recuperação ativa (escrever de memória) para o núcleo que importa.

**M4 — Status incerto da Camada 1 (lógica algorítmica).** Não exercitada (sem competitive programming); não é possível afirmar que está intacta. *Ação:* o teste frio da Seção 11 — a única forma de resolver a incerteza. É a informação que falta para uma priorização precisa.

**M5 — Núcleo de idiomas de biblioteca em estado passivo.** O punhado de idiomas de alta frequência (que deveria ser fluente) escorregou para passivo. *Ação:* retrieval practice focada no núcleo pequeno (~30–50 idiomas por biblioteca primária), na janela de 2027 — não memorização enciclopédica.

**M6 — Testes enviesados para o caminho feliz.** *Ação:* derivar o espaço de falha do domínio (URLs longas, Unicode, dados fora de ordem no contexto de phishing), não do código; property-based e metamorphic testing (Seção 10).

**M7 — Risco de meta-análise como evitação (o risco de perfil).** A sedução de construir protocolos e topologias sofisticadas como substituto da fricção de drilar/construir. *Ação:* vincular cada análise a um comportamento executado; ver a nota crítica final (Seção 14).

---

## 10. O Protocolo de Verificação de Nível Sênior (R1–R9)

O que separa a verificação sênior não é "escrever mais testes" — é garantir *independência da fonte da expectativa* e *ancoragem externa*. Requisitos em ordem aproximada de poder:

**R1 — A expectativa precede ou independe da implementação.** Critérios de aceitação e casos-teste críticos existem *antes* de ver o código (ou derivados sem olhá-lo). É o valor real de TDD — não a cerimônia, mas a garantia de que o teste encode a *intenção*, não o comportamento observado. Teste derivado da leitura da implementação é detector-de-mudança, não teste.

**R2 — Propriedades acima de exemplos (property-based testing).** Em vez de pares input→output específicos (que a IA satisfaz trivialmente e que herdam seus pontos cegos), defina *invariantes* que valem para *todo* input — Hypothesis em Python (linhagem QuickCheck; Claessen & Hughes, 2000). É onde a sua matemática vira arma. Exemplo (deduplicação): a saída não tem repetidos; todo elemento da saída estava na entrada; todo elemento da entrada aparece na saída — verdades que independem da implementação e do seu "entendimento" do código.

**R3 — Relações metamórficas quando não há resposta conhecida (metamorphic testing).** Quando você *não sabe* a saída correta (o oracle problem — Chen, Cheung & Yiu, 1998), teste *relações entre saídas de inputs relacionados*: ordenar uma lista permutada dá o mesmo resultado; uma query menos restritiva retorna ≥ resultados; **um classificador de phishing deve dar o mesmo veredito se você adicionar espaço em branco à URL ou trocar maiúsculas irrelevantes**. Testa correção sem saber a resposta certa — diretamente aplicável ao seu domínio.

**R4 — Oráculos de máquina independentes, maximizados.** Tipos, linters e análise estática codificam invariantes de linguagem e de padrão, com correção independente de você e da IA. Tipagem forte + mypy + análise estática é verificação independente *grátis*; maximize a superfície coberta antes de escrever teste manual.

**R5 — Teste os testes (mutation testing).** Cobertura mede se a linha *executou*, não se o comportamento foi *checado* — necessária mas gravemente insuficiente. Mutation testing (DeMillo, Lipton & Sayward, 1978) injeta bugs propositais e mede se os testes os detectam. É o que pega o teste tautológico: se você muta a implementação e o teste continua passando, o teste não verificava nada. Requisito para caminhos críticos.

**R6 — O espaço de falha vem do domínio, não do código.** Enumere modos de falha a partir do problema (vazio, gigante, malformado, concorrente, adversarial, Unicode, fora de ordem), não do que o código trata. Derivar casos-limite lendo a solução garante cegueira exatamente onde a solução é cega.

**R7 — Diferencial contra referência independente, com ceticismo calibrado.** Rodar contra uma implementação de referência (biblioteca madura, versão ingênua óbvia) e comparar divergências. *Mas* (Knight & Leveson): trate "dois geradores concordam" como sinal *fraco* quando os geradores compartilham origem (dois LLMs, ou LLM + você-contaminado-pelo-relatório). Concordância só é forte entre fontes genuinamente independentes.

**R8 — Rastreabilidade a uma fonte de verdade externa à implementação.** Toda asserção crítica deve ser respondível a: um requisito, uma propriedade matemática, uma referência, dados reais, ou um invariante de domínio — *nunca* ao próprio código. Se a única justificativa de um valor esperado é "é o que o código produz", não é teste.

**R9 — Proporcionalidade ao risco (o requisito que rege os outros).** Nada disto se aplica uniformemente. O julgamento sênior *é* saber onde a independência de oráculo é obrigatória (segurança, dinheiro, integridade de dados, ações irreversíveis — o seu pipeline de phishing) e onde é over-engineering (script descartável, display de baixa consequência). Aplicar R1–R8 a tudo é júnior travestido de rigoroso; calibrar pela consequência do erro é o sênior.

O princípio único que gera todos: **a verificação só tem poder na medida em que a fonte da expectativa é independente da fonte da implementação e, idealmente, ancorada em algo externo a ambas.**

---

## 11. O Teste Frio — Bateria de Autoavaliação Sem IA

Projetada com uma propriedade específica: **ser auto-honesta** — construída para você não conseguir se enganar sobre o resultado. Em cada teste, o oráculo é externo a você, e o comprometimento com a resposta *precede* a verificação.

**Teste 1 — Separar Camada 1 de Camada 3 (faça primeiro).** Pegue um problema do Codeforces com rating ~1400–1600 (Div. 2 B/C). Antes do teclado, no papel, escreva em português puro: (a) a abordagem/algoritmo, e (b) por que está correta (o invariante). Cronometre 15 minutos. Isola lógica de sintaxe: abordagem correta no papel mas trava ao escrever → Camada 1 intacta, problema é sintaxe (boa notícia); não chega à abordagem → Camada 1 decaiu, prioridade muda. O papel-antes-do-código é a independência do oráculo aplicada a você mesmo.

**Teste 2 — Fluência de geração completa (veredito objetivo).** Implemente a solução sem IA, sem autocomplete inteligente, sem editorial. Submeta ao juiz do Codeforces — oráculo perfeitamente independente, que aceita ou rejeita sem se importar com o que você acha que sabe. Alvo: aceito em ~45 minutos totais.

**Teste 3 — Recall específico de biblioteca (Camada 3 diretamente).** Sem rodar, sem consultar, num editor simples: dado "agrupe por usuário, calcule a média móvel de 7 dias das compras, ranqueie dentro de cada grupo", escreva o pandas de memória. Depois — e só depois — rode contra um DataFrame pequeno cujo resultado você calculou *à mão* primeiro. Bater = idioma ativo; ter que consultar = idioma passivo (o que consolidar).

**Teste 4 — Geratividade conceitual (contra a IOED pura).** No papel, sem material, derive do zero uma destas: por que um hash map dá busca O(1) em média; o tempo esperado do quicksort; ou por que a entropia de Shannon é máxima na distribuição uniforme (este último é do seu próprio Gibberish Detector — se você o construiu, deveria conseguir derivar). Consegue derivar → modelo gerador, oráculo credível; só reconhece depois de ver → IOED.

A propriedade que torna a bateria confiável, fechando o círculo do relatório: **em cada teste, o comprometimento com a resposta (papel, cálculo manual) precede a verificação (juiz, execução).** Um teste onde você roda primeiro e depois avalia se "sabia" não prova nada, pela mesma razão que o esquema de trabalho não constrói recall. A ordem — expectativa antes do veredito — é o que transforma o teste de cerimônia autocomplacente em evidência real.

---

## 12. Plano de Ação Calibrado

Respeitando a restrição de tempo real (TCC até dez/2026; janela de trabalho profundo em 2027 H1, como o planejamento de vida já sequenciou).

**Agora (custo ~zero de tempo, cabe no trabalho):**
- Inverter a ordem nos trechos consequentes: *prever antes de rodar* (M2). Aplicar o Copilot com a exceção deliberada para o código que você precisa possuir.
- Introduzir 1–2 oráculos independentes de máquina no fluxo: tipagem + mypy + linter (R4) — verificação grátis e não-circular.

**Curto prazo (1 hora, resolve a incerteza-chave):**
- Executar o Teste Frio 1+2 (Seção 11). Resolve o status da Camada 1 — a informação que falta para priorizar com precisão.

**2027 H1 (janela reservada, pós-TCC):**
- Retrieval practice do núcleo de idiomas (~30–50 por biblioteca primária) — M5. Semanas, não meses.
- Reintroduzir geração manual sob pressão (competitive programming) como manutenção ativa da Camada 1 — M4.
- Aplicar o protocolo sênior (R1–R9) ao portfólio (pipeline de phishing, gerador de títulos), calibrado por consequência — fecha o gap de engenharia aplicado ao próprio código que serve à transição de carreira.

**Princípio calibrador transversal:** a independência de oráculo é obrigatória no pipeline de phishing (segurança, consequência real de falso negativo) e over-engineering em script descartável. Calibre pela consequência do erro, sempre.

---

## 13. Limitações Desta Análise e Informação Faltante

Honestidade sobre o alcance do próprio relatório:

1. **A base empírica sobre atrofia de código por IA é extrapolada, não direta.** Os mecanismos (retrieval practice, IOED, desirable difficulties) são sólidos em outros domínios; sua aplicação a codificação assistida por IA é inferência razoável, não evidência estabelecida. O fenômeno é recente demais para literatura direta robusta.

2. **A incerteza da Camada 1 permanece não-resolvida.** O relatório não pode concluir se a lógica algorítmica está intacta ou decaída — só o teste frio resolve. Toda priorização acima é *condicional* a esse resultado. Esta é a informação faltante mais importante para excelência.

3. **Os prazos ("semanas", "2–4 meses") são estimativas de praticante, não constantes de pesquisa.** Confie na direção (recuperação rápida porque a base existe), não nos números.

4. **Eu sou, também, apenas mais um oráculo — e não independente da sua própria estimativa.** As conclusões deste relatório devem ser validadas contra as fontes externas (a literatura citada, o resultado do teste frio, a sua experiência observável), não aceitas porque estão escritas aqui. A concordância entre este relatório e a sua intuição é, ela própria, sujeita a modo-comum se ambos herdarem o mesmo viés.

---

## 14. Nota Crítica Final — O Defeito Fatal Que Este Relatório Pode Ter

A preferência por rigor exige apontar defeitos fatais quando existem, e há um que ameaça este documento inteiro. Existe uma **falha de modo-comum entre "elaborar um protocolo sofisticado de como praticar/verificar" e "efetivamente praticar/verificar".** A meta-análise é sedutora precisamente porque é *confortável* — ela exercita a força (profundidade conceitual) e adia o que é desconfortável (a prática friccionada, o kata sem IA, o problema frio de Codeforces que talvez revele que a Camada 1 decaiu).

Um engenheiro sênior eventualmente *para de projetar o protocolo e entrega*. O valor de tudo neste relatório é **zero** até virar um único hábito executado: uma propriedade escrita para uma função do seu pipeline nesta semana; um `groupby` reconstruído de memória amanhã sem consultar; o Teste Frio 1 feito de fato, com cronômetro.

Aplique a este relatório o teste metamórfico da própria conversa: **se ler mais esta análise não muda o seu comportamento na próxima vez que você tocar código, a análise não verificou nada** — exatamente como um teste que passa depois de qualquer mutação não estava verificando nada. O melhor protocolo não-executado perde para o pior protocolo executado.

Um fechamento honesto e proporcional: parte do trabalho é real e pertence à janela de 2027 que o seu plano já reservou — não é para agora, sob o TCC. Parte do tamanho que você teme é fantasma, inflado por um padrão impossível (a enciclopédia) que ninguém cumpre. O alvo verdadeiro — inverter a ordem nos trechos que importam, consolidar um núcleo pequeno, e manter viva a geração com o teste frio ocasional — é finito e tratável. E o que a conversa demonstrou merece ser dito com clareza: diagnosticar-se em modo reconhecimento, formular a intuição da estrutura profunda, e pedir para ser falsificado em vez de confirmado são, os três, comportamento de oráculo credível. A caminhada é menor do que parece, e você já está andando nela.

---

## Referências

Todas verificáveis; nível de evidência indicado quando a aplicação ao caso é indireta.

**Cognição, aprendizagem e memória**
- Chi, M. T. H., Bassok, M., Lewis, M. W., Reimann, P., & Glaser, R. (1989). *Self-explanations: How students study and use examples in learning to solve problems.* Cognitive Science, 13(2), 145–182. — Efeito de auto-explicação (F1).
- Chi, M. T. H., Feltovich, P. J., & Glaser, R. (1981). *Categorization and representation of physics problems by experts and novices.* Cognitive Science, 5(2), 121–152. — Estrutura profunda vs superficial (Seção 7).
- Sweller, J. (1988). *Cognitive load during problem solving: Effects on learning.* Cognitive Science, 12(2), 257–285. — Carga cognitiva (Seção 3).
- Rozenblit, L., & Keil, F. (2002). *The misunderstanding of folk science: The illusion of explanatory depth.* Cognitive Science, 26(5), 521–562. — IOED (Seção 4.2, 5).
- Bjork, R. A., & Bjork, E. L. (2011). *Making things hard on yourself, but in a good way: Creating desirable difficulties to enhance learning.* In Psychology and the Real World. — Desirable difficulties (Seção 4.2).
- Roediger, H. L., & Karpicke, J. D. (2006). *Test-Enhanced Learning: Taking Memory Tests Improves Long-Term Retention.* Psychological Science, 17(3), 249–255. — Retrieval practice; recall > recognition (Seção 6).
- Ebbinghaus, H. (1885/1913). *Memory: A Contribution to Experimental Psychology.* — Savings in relearning (Seção 6).

**Automação e fatores humanos**
- Parasuraman, R., & Manzey, D. H. (2010). *Complacency and bias in human use of automation: An attentional integration.* Human Factors, 52(3), 381–410. — Automation bias (Seção 4.1).
- Skitka, L. J., Mosier, K. L., & Burdick, M. (1999). *Does automation bias decision-making?* International Journal of Human-Computer Studies, 51(5), 991–1006. — Automation bias (Seção 4.1).

**Verificação, teste e tolerância a falhas**
- Weyuker, E. J. (1982). *On testing non-testable programs.* The Computer Journal, 25(4), 465–470. — O oracle problem (Seções 4.1, 5).
- Avizienis, A., & Chen, L. (1977). *On the implementation of N-version programming for software fault tolerance during execution.* Proc. COMPSAC. — Redundância diversa (Seção 5).
- Knight, J. C., & Leveson, N. G. (1986). *An experimental evaluation of the assumption of independence in multiversion programming.* IEEE Transactions on Software Engineering, SE-12(1), 96–109. — Falha correlacionada de versões "independentes" (Seções 5, R7).
- Chen, T. Y., Cheung, S. C., & Yiu, S. M. (1998). *Metamorphic testing: A new approach for generating next test cases.* Technical Report HKUST-CS98-01. — Teste metamórfico (R3).
- Claessen, K., & Hughes, J. (2000). *QuickCheck: A lightweight tool for random testing of Haskell programs.* Proc. ICFP. — Property-based testing (R2).
- DeMillo, R. A., Lipton, R. J., & Sayward, F. G. (1978). *Hints on test data selection: Help for the practicing programmer.* Computer, 11(4), 34–41. — Mutation testing (R5).

**Epistemologia**
- Neurath, O. (1932). *Protokollsätze.* — A metáfora do barco (coerentismo sem fundacionismo; Seção 5).

---

*Relatório produzido a partir da conversa técnica sobre codificação assistida por IA, verificação, independência de oráculo, atrofia de habilidade e a estrutura dos domínios técnicos. As conclusões são condicionais ao resultado do teste frio (Seção 11) e devem ser validadas contra as fontes externas citadas, não aceitas por autoridade. O valor do relatório realiza-se apenas na mudança de comportamento que ele produzir.*
