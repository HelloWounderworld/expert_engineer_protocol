# Lista Completa de Tipos de Testes para Sênior/Especialista
## Com Referências, Taxonomia e Dívida Técnica Prevenida

---

## Aviso de Rigor Epistemológico

- **[PEER-REVIEWED]** — publicado com revisão por pares
- **[PADRÃO-ISO/IEEE]** — norma técnica internacional
- **[CLÁSSICO]** — obra fundacional amplamente aceita
- **[INDUSTRIAL]** — guia de empresa reconhecida, sem revisão formal
- **[DISPUTADO]** — amplamente citado, mas com evidência contestada

---

## Estrutura: Quatro Camadas Fundamentais

Antes da lista detalhada, é necessário entender a **taxonomia de camadas** que organiza todos os tipos de testes. Essa estrutura vem diretamente da norma internacional:

> **[PADRÃO-ISO/IEEE]**
> ISO/IEC/IEEE 29119-1:2022. *Software and Systems Engineering — Software Testing — Part 1: General Concepts.* (Substitui IEEE 829-2008.)
> — Define formalmente as camadas de teste, seus objetivos e relações. É a taxonomia canônica da área.

```
CAMADA 4 ──── Acceptance Testing (UAT)       ← O sistema resolve o problema certo?
CAMADA 3 ──── System Testing                 ← O sistema se comporta como especificado?
CAMADA 2 ──── Integration Testing            ← Os módulos funcionam juntos?
CAMADA 1 ──── Unit Testing                   ← Cada unidade faz o que promete?
```

As camadas superiores são mais lentas, mais caras de executar e cobrem mais território. As inferiores são mais rápidas, mais baratas e cobrem menos território. Um sênior sabe **quanto investir em cada camada** para cada tipo de sistema — e por que a maioria das equipes investe mal (excesso nas camadas superiores, déficit nas inferiores).

---

## GRUPO 1 — Testes de Estrutura (As Quatro Camadas Canônicas)

---

### 1. Unit Testing — Teste Unitário

**Definição precisa:** testa uma única unidade de código (função, método, classe) em *isolamento completo* de dependências externas. Dependências são substituídas por doubles (mocks, stubs, fakes).

**Referência fundacional:**
> **[CLÁSSICO]**
> Beck, K. (2002). *Test-Driven Development: By Example.* Addison-Wesley.
> — Popularizou o ciclo Red-Green-Refactor e estabeleceu testes unitários como prática central de desenvolvimento, não de QA.

> **[CLÁSSICO]**
> Feathers, M. (2004). *Working Effectively with Legacy Code.* Prentice Hall.
> — Define formalmente "unit test" em contraste com testes que acessam banco, rede ou sistema de arquivos. A distinção é operacional: se o teste roda em menos de um segundo sem dependências externas, é unitário.

**Dívida técnica prevenida:** bugs semânticos em lógica isolada que só seriam descobertos em produção ou em testes de integração caros. Refatoração sem segurança — sem testes unitários, qualquer mudança interna é uma aposta.

**Por que o sênior precisa dominar:** é a base de tudo. Sem cobertura unitária sólida, todas as outras camadas ficam frágeis. O sênior sabe o que isolar, o que não mockar (não mocke o que você possui), e quando um teste "unitário" está na verdade testando demais.

**Sinal de uso incorreto:** testes unitários que testam implementação interna em vez de comportamento — quebram a cada refatoração, sem indicar bugs reais.

---

### 2. Integration Testing — Teste de Integração

**Definição precisa:** testa a interação entre dois ou mais módulos, serviços ou componentes *reais* (sem mocks). O objetivo é detectar problemas que surgem nas interfaces e contratos entre partes.

**Referência:**
> **[PADRÃO-ISO/IEEE]**
> ISO/IEC/IEEE 29119-1:2022, op. cit. — Seção 5.1.3: "Integration test level."

> **[CLÁSSICO]**
> Meszaros, G. (2007). *xUnit Test Patterns: Refactoring Test Code.* Addison-Wesley.
> — Define a taxonomia completa de test doubles (mock, stub, fake, spy, dummy) e quando usar cada um. Referência definitiva para testes de integração bem estruturados.

**Dívida técnica prevenida:** bugs de interface que só aparecem quando módulos são combinados — formatos de dados incompatíveis, timeouts não tratados, contratos de API violados silenciosamente.

**Por que o sênior precisa dominar:** sabe onde colocar a fronteira entre testes unitários e de integração. Entende que testes de integração são mais lentos e frágeis por natureza — não devem ser escritos para tudo, apenas para as interfaces críticas.

---

### 3. System Testing — Teste de Sistema

**Definição precisa:** testa o sistema completo e integrado como uma caixa preta, verificando comportamento contra os requisitos especificados. Inclui testes funcionais e não-funcionais (performance, segurança).

**Referência:**
> **[PADRÃO-ISO/IEEE]**
> ISO/IEC/IEEE 29119-1:2022, op. cit. — Seção 5.1.4: "System test level."

**Dívida técnica prevenida:** comportamento emergente do sistema que não é visível em testes de camadas inferiores — falhas que só aparecem quando todos os componentes operam juntos sob condições realistas.

---

### 4. Acceptance Testing / UAT — Teste de Aceitação

**Definição precisa:** valida que o sistema satisfaz os critérios de aceitação do negócio e está pronto para entrega. Tipicamente executado pelo cliente ou representante do usuário.

**Referência:**
> **[PADRÃO-ISO/IEEE]**
> ISO/IEC/IEEE 29119-1:2022, op. cit. — Seção 5.1.5: "Acceptance test level."

> **[CLÁSSICO]**
> Gärtner, M. (2011). *ATDD by Example: A Practical Guide to Acceptance Test-Driven Development.* Addison-Wesley.

**Dívida técnica prevenida:** entregar o sistema certo errado — funcionalmente correto mas resolvendo o problema errado. É o teste mais próximo da definição de Brooks de complexidade essencial.

---

## GRUPO 2 — Técnicas de Teste (Abordagens Transversais a Todas as Camadas)

---

### 5. Regression Testing — Teste de Regressão

**Definição precisa:** re-executa testes existentes após uma mudança para garantir que comportamentos previamente corretos não foram quebrados. Não é um tipo de teste em si — é a *prática* de manter e re-executar a suite existente sistematicamente.

**Referência:**
> **[PEER-REVIEWED]**
> Rothermel, G., & Harrold, M. J. (1996). *Analyzing Regression Test Selection Techniques.* IEEE Transactions on Software Engineering, 22(8), 529–551.
> DOI: 10.1109/32.536955
> — Paper fundacional sobre seleção de testes de regressão. Introduziu o problema de *regression test selection* (RTS): como escolher o subconjunto mínimo de testes que cobre as mudanças feitas.

**Dívida técnica prevenida:** regressões — bugs que você já corrigiu voltando silenciosamente. Sem testes de regressão, cada correção de bug cria risco de quebrar algo que funcionava.

**Regra do sênior:** nunca corrija um bug sem primeiro escrever o teste que o reproduz. Isso transforma a correção em um teste de regressão permanente.

---

### 6. TDD — Test-Driven Development

**Definição precisa:** não é um tipo de teste — é uma *metodologia de desenvolvimento* em que os testes são escritos *antes* do código de produção. O ciclo é Red (escreve teste que falha) → Green (escreve código mínimo para passar) → Refactor (melhora o código mantendo testes verdes).

**Referência fundacional:**
> **[CLÁSSICO]**
> Beck, K. (2002). *Test-Driven Development: By Example.* Addison-Wesley.

> **[PEER-REVIEWED]**
> Erdogmus, H., Morisio, M., & Torchiano, M. (2005). *On the Effectiveness of the Test-First Approach to Programming.* IEEE Transactions on Software Engineering, 31(3), 226–237.
> DOI: 10.1109/TSE.2005.37
> — Um dos primeiros estudos controlados sobre TDD. Encontrou que desenvolvedores TDD escreveram mais testes e tiveram maior qualidade externa. A relação com qualidade de design interno é menos conclusiva.

**Nota honesta sobre evidência [DISPUTADO parcialmente]:** Uma meta-análise de Causevic, Sundmark & Punnekkat (2011) **[PEER-REVIEWED]** encontrou resultados mistos na literatura. Os benefícios mais consistentemente documentados são: melhor cobertura de testes, design mais modular (porque código difícil de testar é design ruim), e ciclos de feedback mais curtos. Os benefícios em produtividade são inconsistentes entre estudos.

**Dívida técnica prevenida:** design acoplado que dificulta testes futuros — código escrito sem TDD tende a ser mais difícil de testar porque não foi projetado com testabilidade em mente. TDD força o design a ser testável desde a concepção.

---

### 7. BDD — Behavior-Driven Development

**Definição precisa:** extensão do TDD onde os testes são escritos em linguagem natural estruturada (Given-When-Then), expressando comportamento do sistema do ponto de vista do usuário ou negócio.

**Referência:**
> **[INDUSTRIAL]**
> North, D. (2006). *Introducing BDD.* DanNorth.net.
> URL: https://dannorth.net/introducing-bdd/
> — Post original que definiu BDD como evolução do TDD focada em comunicação entre técnicos e não-técnicos.

> **[CLÁSSICO]**
> Cucumber Project. *The Gherkin Language Specification.*
> URL: https://cucumber.io/docs/gherkin/
> — Formaliza a sintaxe Given-When-Then como linguagem de especificação executável.

**Dívida técnica prevenida:** gap de comunicação entre requisitos de negócio e implementação técnica — testes BDD servem simultaneamente como documentação executável e especificação do sistema.

---

### 8. Property-Based Testing — Teste Baseado em Propriedades

**Definição precisa:** em vez de testar casos específicos (exemplo-baseado), define *propriedades* que devem valer para *qualquer* input válido. A ferramenta gera automaticamente centenas de casos de teste aleatórios e busca ativamente o menor input que viola a propriedade.

**Referência acadêmica fundamental:**
> **[PEER-REVIEWED]**
> Claessen, K., & Hughes, J. (2000). *QuickCheck: A Lightweight Tool for Random Testing of Haskell Programs.* ACM SIGPLAN Notices, 35(9), 268–279.
> DOI: 10.1145/357766.351266
> — Paper que introduziu property-based testing com QuickCheck. Altamente influente; a abordagem foi portada para quase todas as linguagens modernas.

> **[PEER-REVIEWED]**
> MacIver, D. R., Hatfield-Dodds, Z., et al. (2019). *Hypothesis: A new approach to property-based testing.* Journal of Open Source Software, 4(43), 1891.
> DOI: 10.21105/joss.01891
> — Hypothesis é a implementação de referência para Python. Paper documenta a abordagem e casos de bugs encontrados em bibliotecas científicas reais.

**Por que é poderoso:** testes exemplo-baseados testam o que o desenvolvedor *pensou* em testar. Property-based testing descobre os casos que o desenvolvedor *não pensou* em testar.

**Dívida técnica prevenida:** edge cases e comportamentos de fronteira que nunca seriam cobertos por testes manuais. Exemplos clássicos: overflow de inteiros, strings com caracteres especiais, listas vazias, valores negativos inesperados.

**Exemplo concreto para seu pipeline:**

```python
from hypothesis import given, strategies as st

@given(st.text())
def test_extractor_never_raises_on_any_string(url_candidate):
    """Propriedade: extract_features nunca deve levantar exceção,
    independente do input — mesmo com Unicode, strings vazias, etc."""
    result = extract_features(url_candidate)
    assert result is not None  # sempre retorna algo
    assert isinstance(result, dict)  # sempre retorna dict
```

---

### 9. Mutation Testing — Teste de Mutação

**Definição precisa:** avalia a *qualidade* dos testes, não do código. Introduz pequenas mutações sintáticas no código (inverte condicionais, troca operadores, remove linhas) e verifica se os testes existentes detectam essas mutações. Um mutante "sobrevivente" indica que os testes são fracos para aquela lógica.

**Referência:**
> **[PEER-REVIEWED]**
> Jia, Y., & Harman, M. (2011). *An Analysis and Survey of the Development of Mutation Testing.* IEEE Transactions on Software Engineering, 37(5), 649–678.
> DOI: 10.1109/TSE.2010.62
> — Survey definitivo de três décadas de pesquisa em mutation testing. 565 citações. Demonstra que a técnica é madura e aplicável industrialmente.

**Por que é fundamental para sêniores:** cobertura de código (code coverage) mede se uma linha foi *executada*, não se foi *testada significativamente*. É possível ter 100% de cobertura com testes que não detectam nenhum bug. Mutation testing mede se seus testes realmente validam o comportamento.

**Dívida técnica prevenida:** falsa sensação de segurança com alta cobertura de código — a suite de testes parece completa mas é incapaz de detectar bugs reais.

**Ferramentas:** `mutmut` (Python), `PIT` (Java), `Stryker` (JavaScript/TypeScript).

---

### 10. Contract Testing — Teste de Contrato

**Definição precisa:** verifica que a interface entre dois serviços (consumidor e provedor) respeita um contrato formal. Em arquiteturas de microsserviços, é a alternativa a testes de integração pesados — cada serviço testa contra o contrato sem precisar do outro serviço em execução.

**Referência:**
> **[INDUSTRIAL — Padrão da Indústria]**
> Pact Foundation. *Pact: Consumer-Driven Contract Testing.*
> URL: https://docs.pact.io/
> — A ferramenta de referência para contract testing. O padrão Consumer-Driven Contract foi formalizado pelo time da Pact Foundation e é adotado por Netflix, Google, Atlassian e outros.

> **[PEER-REVIEWED]**
> Camargo, V. V., et al. (2025). *Contract Testing with PACT: Ensuring Reliable API Interactions in Distributed Systems.* ResearchGate.

**Dívida técnica prevenida:** integration drift em microsserviços — serviços evoluem independentemente e quebram silenciosamente contratos com outros serviços. Sem contract testing, isso só é descoberto em testes de integração completos ou em produção.

---

## GRUPO 3 — Testes Não-Funcionais

---

### 11. Performance Testing / Load Testing — Teste de Performance e Carga

**Definição precisa:** verifica o comportamento do sistema sob carga esperada (load test), carga extrema (stress test), e sustentada por longos períodos (endurance test).

**Referência:**
> **[PADRÃO-ISO/IEEE]**
> ISO/IEC 25010:2023. *Systems and Software Quality Requirements and Evaluation (SQuaRE) — Product Quality Model.*
> — Define performance efficiency como uma das características de qualidade de software, incluindo: time behavior, resource utilization e capacity.

> **[INDUSTRIAL]**
> Beyer, B., Jones, C., Petoff, J., & Murphy, N. R. (Eds.) (2016). *Site Reliability Engineering.* O'Reilly.
> URL: https://sre.google/sre-book/
> — Capítulos sobre load testing, SLIs/SLOs e como definir performance budgets.

**Dívida técnica prevenida:** sistemas que funcionam com 10 usuários e colapso com 1000 — problemas descobertos em produção, tipicamente nos piores momentos possíveis.

**Ferramentas:** `locust` (Python), `k6`, `JMeter`, `Gatling`.

---

### 12. Smoke Testing — Teste de Fumaça

**Definição precisa:** conjunto mínimo de testes executados imediatamente após um build ou deploy para verificar que as funcionalidades críticas básicas funcionam — antes de executar a suite completa.

**Referência:**
> **[CLÁSSICO]**
> McConnell, S. (1996). *Rapid Development.* Microsoft Press.
> — Popularizou o termo "smoke test" em desenvolvimento de software, derivado da prática de engenharia elétrica de ligar um circuito e verificar se há fumaça antes de qualquer teste detalhado.

**Dívida técnica prevenida:** tempo desperdiçado executando suites completas de teste em builds claramente quebrados. Smoke tests falham rápido e barato.

---

### 13. Chaos Engineering — Engenharia do Caos

**Definição precisa:** disciplina de experimentação em produção para descobrir fraquezas sistêmicas antes que causem incidentes. Injeta falhas controladas (encerra serviços, corrompe rede, aumenta latência) para verificar que o sistema se comporta de forma resiliente.

**Referência:**
> **[INDUSTRIAL]**
> Basiri, A., Behnam, N., de Rooij, R., Hochstein, L., Kosewski, L., Reynolds, J., & Rosenthal, C. (2016). *Chaos Engineering.* IEEE Software, 33(3), 35–41.
> DOI: 10.1109/MS.2016.60
> — Paper dos engenheiros da Netflix que formalizou Chaos Engineering como disciplina. Descreve a origem do Chaos Monkey e os princípios da prática.

**Dívida técnica prevenida:** sistemas que funcionam apenas no happy path — fraquezas de resiliência que só aparecem quando componentes falham de formas inesperadas em produção.

---

## GRUPO 4 — Testes Específicos para ML/IA

Esta é a categoria mais crítica para o seu perfil e a menos coberta pela literatura de engenharia de software convencional.

**Referência base de todo este grupo:**
> **[PEER-REVIEWED]**
> Breck, E., Cai, S., Nielsen, E., Salib, M., & Sculley, D. (2017). *The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction.* IEEE Big Data.
> DOI: 10.1109/BigData.2017.8258038

---

### 14. Data Testing — Teste de Dados

**Definição precisa:** verifica que os dados de entrada satisfazem propriedades esperadas antes de serem usados para treino ou inferência. Inclui testes de schema, distribuição, valores ausentes, ranges válidos e relações entre features.

> **[PEER-REVIEWED]**
> Sculley et al. (2015), op. cit. — Seção "Data Testing Debt": "If data replaces code in ML systems, and code should be tested, then data should be tested too."

> **[INDUSTRIAL]**
> Great Expectations Project. *Data Validation for ML Pipelines.*
> URL: https://greatexpectations.io/
> — Framework de referência para data testing em Python.

**Dívida técnica prevenida:** garbage in, garbage out em escala — modelos treinados em dados corrompidos ou fora de distribuição que funcionam nos testes mas falham silenciosamente em produção.

**Exemplo:**

```python
# Great Expectations — teste de dados para pipeline de phishing
import great_expectations as ge

df = ge.from_pandas(features_df)
df.expect_column_values_to_be_between("entropy", 0.0, 8.0)
df.expect_column_values_to_not_be_null("domain_length")
df.expect_column_proportion_of_unique_values_to_be_between("tld", 0.001, 1.0)
```

---

### 15. Model Testing — Teste de Modelo

**Definição precisa:** além de métricas agregadas (AUC, F1), testa o comportamento do modelo em subconjuntos específicos, casos de fronteira, e invariâncias esperadas.

> **[PEER-REVIEWED]**
> Breck et al. (2017), op. cit. — Seção "Tests for ML Models": inclui testes de estabilidade de retreinamento, consistência de predição, e comportamento em slices de dados.

> **[PEER-REVIEWED]**
> Ribeiro, M. T., Wu, T., Guestrin, C., & Singh, S. (2020). *Beyond Accuracy: Behavioral Testing of NLP Models with CheckList.* ACL 2020.
> DOI: 10.18653/v1/2020.acl-main.442
> — Introduz o paradigma de *behavioral testing* para ML: testes de invariância (mudar o nome próprio não deve mudar o sentimento), testes de direção (adicionar negação deve inverter o sentimento), testes de perturbação mínima.

**Dívida técnica prevenida:** modelos que funcionam bem na média mas falham sistematicamente em subgrupos específicos — problema especialmente crítico em segurança e detecção de fraude.

---

### 16. Pipeline Testing — Teste de Pipeline ML

**Definição precisa:** testa o pipeline de ML end-to-end — desde a ingestão de dados até o output do modelo — como um sistema integrado. Inclui testes de reprodutibilidade de treino e testes de performance de inferência.

> **[PEER-REVIEWED]**
> Breck et al. (2017), op. cit. — Seção "Integration tests for ML": "A good integration test runs all the way from original data sources, through feature creation, to training, and to serving."

**Dívida técnica prevenida:** pipelines que funcionam em notebooks mas quebram no ambiente de produção — o problema mais comum em ciência de dados que tenta entrar em produção.

---

### 17. Distribution Drift Testing — Teste de Desvio de Distribuição

**Definição precisa:** monitora se a distribuição dos dados em produção está divergindo significativamente da distribuição de treino. Usa testes estatísticos (Kolmogorov-Smirnov, chi-quadrado, PSI) para detectar drift.

> **[PEER-REVIEWED]**
> Sculley et al. (2015), op. cit. — "Changes in the external world: The real world is a source of ongoing instability [...] Input distribution shift is perhaps the most common and insidious source of ML system failure."

**Dívida técnica prevenida:** degradação silenciosa de modelos em produção — o modo de falha mais comum e mais perigoso em sistemas ML de longa duração.

---

## GRUPO 5 — Testes Avançados

---

### 18. Fuzz Testing — Teste de Fuzzing

**Definição precisa:** alimenta o sistema com inputs inválidos, inesperados, ou aleatórios para descobrir comportamentos não tratados — crashes, exceções não capturadas, corrupção de estado, vulnerabilidades de segurança.

**Referência:**
> **[PEER-REVIEWED]**
> Miller, B. P., Fredriksen, L., & So, B. (1990). *An Empirical Study of the Reliability of UNIX Utilities.* Communications of the ACM, 33(12), 32–44.
> DOI: 10.1145/96267.96279
> — Paper que originou fuzzing como técnica sistemática. Os autores alimentaram utilitários Unix com input aleatório e descobriram falhas em 25–33% deles.

> **[PEER-REVIEWED]**
> MacIver, D. R., et al. (2019). *Hypothesis*, op. cit.
> — Hypothesis é simultaneamente um framework de property-based testing e um fuzzer estruturado para Python.

**Dívida técnica prevenida:** comportamentos não tratados em inputs de borda — especialmente relevante para parsers, extratores de features, e qualquer componente que processa dados externos não confiáveis (como URLs de phishing).

---

### 19. End-to-End Testing — Teste Ponta a Ponta

**Definição precisa:** simula o fluxo completo de um usuário real através do sistema, incluindo todas as integrações externas, sem mocks. O teste mais caro de escrever, mais lento de executar, e mais frágil de manter.

**Referência:**
> **[INDUSTRIAL]**
> Google Testing Blog. *Just Say No to More End-to-End Tests.*
> URL: https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html
> — Artigo de engenheiros do Google argumentando que E2E tests são frequentemente usados em excesso, com melhor cobertura obtida por combinação de testes unitários e de integração.

**Dívida técnica prevenida:** bugs que só aparecem no fluxo completo integrado — mas o sênior sabe que E2E tests são caros e frágeis, e portanto devem ser usados estrategicamente, não como cobertura principal.

---

## Síntese: A Pirâmide de Testes e Por Que a Maioria das Equipes Erra

A distribuição correta de investimento em testes foi formalizada como a **Test Pyramid** por Mike Cohn (2009) **[CLÁSSICO]** — e depois refinada por Martin Fowler:

> **[INDUSTRIAL]**
> Fowler, M. *TestPyramid.* Martin Fowler's Bliki.
> URL: https://martinfowler.com/bliki/TestPyramid.html

```
         /\
        /E2E\          ← Poucos, lentos, caros, frágeis
       /──────\
      /Integration\    ← Moderados, verificam interfaces
     /──────────────\
    /   Unit Tests   \ ← Muitos, rápidos, baratos, confiáveis
   /──────────────────\
```

A maioria das equipes inverte a pirâmide — poucos testes unitários e muitos E2E — criando suites lentas, frágeis e que dão pouco feedback sobre onde o bug está. Um sênior sabe construir e manter a pirâmide na proporção correta.

---

## Tabela de Referência Consolidada

| # | Tipo | Grupo | Referência Principal | Nível |
|---|------|-------|---------------------|-------|
| 1 | Unit Testing | Camada | Beck (2002); Feathers (2004) | CLÁSSICO |
| 2 | Integration Testing | Camada | ISO/IEC/IEEE 29119-1 (2022); Meszaros (2007) | PADRÃO + CLÁSSICO |
| 3 | System Testing | Camada | ISO/IEC/IEEE 29119-1 (2022) | PADRÃO |
| 4 | Acceptance Testing | Camada | ISO/IEC/IEEE 29119-1 (2022) | PADRÃO |
| 5 | Regression Testing | Técnica | Rothermel & Harrold (1996) — IEEE TSE | PEER-REVIEWED |
| 6 | TDD | Técnica | Beck (2002); Erdogmus et al. (2005) | CLÁSSICO + PEER-REVIEWED |
| 7 | BDD | Técnica | North (2006); Cucumber | INDUSTRIAL |
| 8 | Property-Based Testing | Técnica | Claessen & Hughes (2000) — ACM; MacIver (2019) | PEER-REVIEWED |
| 9 | Mutation Testing | Técnica | Jia & Harman (2011) — IEEE TSE | PEER-REVIEWED |
| 10 | Contract Testing | Técnica | Pact Foundation; Camargo et al. (2025) | INDUSTRIAL + PEER-REVIEWED |
| 11 | Performance/Load Testing | Não-funcional | ISO/IEC 25010:2023; SRE Book (2016) | PADRÃO + INDUSTRIAL |
| 12 | Smoke Testing | Não-funcional | McConnell (1996) | CLÁSSICO |
| 13 | Chaos Engineering | Não-funcional | Basiri et al. (2016) — IEEE Software | PEER-REVIEWED |
| 14 | Data Testing | ML/IA | Sculley et al. (2015) — NeurIPS | PEER-REVIEWED |
| 15 | Model Testing / Behavioral | ML/IA | Breck et al. (2017); Ribeiro et al. (2020) — ACL | PEER-REVIEWED |
| 16 | Pipeline Testing (ML) | ML/IA | Breck et al. (2017) — IEEE | PEER-REVIEWED |
| 17 | Distribution Drift Testing | ML/IA | Sculley et al. (2015) | PEER-REVIEWED |
| 18 | Fuzz Testing | Avançado | Miller et al. (1990) — CACM; MacIver (2019) | PEER-REVIEWED |
| 19 | End-to-End Testing | Avançado | Fowler (TestPyramid); Google Testing Blog (2015) | INDUSTRIAL |

---

Quer que eu aprofunde qualquer categoria específica — especialmente as do Grupo 4 (ML/IA) que são as mais relevantes para o seu pipeline atual?
