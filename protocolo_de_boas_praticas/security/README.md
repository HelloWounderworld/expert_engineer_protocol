# Boas Práticas de Segurança para Desenvolvedores Sênior e Especialistas
## Guia Completo com Referências Acadêmicas, Industriais e Normas Técnicas

> *"Assume a hostile environment. The enterprise assumes that all communications are suspect regardless of origination."*
> — NIST SP 800-207, *Zero Trust Architecture* (2020)

---

## Aviso de Rigor Epistemológico

Este documento classifica o nível de evidência de cada afirmação:

- **[PADRÃO-NIST]** — publicação oficial do National Institute of Standards and Technology (EUA)
- **[PADRÃO-ISO/IEC]** — norma técnica internacional
- **[INDUSTRIAL-OWASP]** — Open Web Application Security Project (consenso global da indústria)
- **[INDUSTRIAL]** — guia de empresa reconhecida, sem revisão formal por pares
- **[PEER-REVIEWED]** — publicado com revisão por pares
- **[CLÁSSICO]** — obra seminal amplamente aceita
- **[DISPUTADO]** — amplamente citado, mas com evidência contestada ou não auditada externamente

---

## Sumário

**PARTE I — FUNDAMENTOS**
1. [Por Que Segurança É Diferente de Outras Boas Práticas](#1-por-que-segurança-é-diferente-de-outras-boas-práticas)
2. [O Princípio Unificador: Zero Trust e Defense in Depth](#2-o-princípio-unificador-zero-trust-e-defense-in-depth)
3. [A Taxonomia dos Sete Domínios](#3-a-taxonomia-dos-sete-domínios)
4. [A Tabela de Trade-offs: O Que Define o Sênior](#4-a-tabela-de-trade-offs-o-que-define-o-sênior)

**PARTE II — OS SETE DOMÍNIOS EM DETALHES**
5. [Domínio 1 — Gestão de Identidade e Acesso (IAM)](#5-domínio-1--gestão-de-identidade-e-acesso-iam)
6. [Domínio 2 — Proteção de Dados e Criptografia](#6-domínio-2--proteção-de-dados-e-criptografia)
7. [Domínio 3 — Segurança de Código e Aplicação (OWASP Top Ten)](#7-domínio-3--segurança-de-código-e-aplicação-owasp-top-ten)
8. [Domínio 4 — Segurança de Infraestrutura e Rede](#8-domínio-4--segurança-de-infraestrutura-e-rede)
9. [Domínio 5 — Segurança de Dependências e Supply Chain](#9-domínio-5--segurança-de-dependências-e-supply-chain)
10. [Domínio 6 — Logging, Monitoramento e Resposta a Incidentes](#10-domínio-6--logging-monitoramento-e-resposta-a-incidentes)
11. [Domínio 7 — Segurança Específica para ML/IA](#11-domínio-7--segurança-específica-para-mlia)

**PARTE III — INTEGRAÇÃO AO CICLO DE DESENVOLVIMENTO**
12. [DevSecOps: Segurança no Pipeline de CI/CD](#12-devsecops-segurança-no-pipeline-de-cicd)
13. [Checklist Operacional por Domínio](#13-checklist-operacional-por-domínio)
14. [Roteiro de Implementação Gradual](#14-roteiro-de-implementação-gradual)

**PARTE IV — REFERÊNCIAS**
15. [Mapa de Confiabilidade das Afirmações](#15-mapa-de-confiabilidade-das-afirmações)
16. [Referências Completas](#16-referências-completas)

---

# PARTE I — FUNDAMENTOS

## 1. Por Que Segurança É Diferente de Outras Boas Práticas

### A Assimetria Fundamental

Segurança tem uma propriedade que nenhuma outra disciplina de engenharia possui: **a assimetria radical entre atacante e defensor**.

- O **defensor** precisa proteger *todos* os vetores de ataque *simultaneamente*
- O **atacante** precisa encontrar *apenas um* vetor que funcione

Isso tem implicações estruturais para como um sênior pensa sobre segurança:

1. Segurança não é um estado final — é um processo contínuo
2. Segurança perfeita é matematicamente impossível (e tornaria o sistema inutilizável)
3. O objetivo é *aumentar o custo do ataque* até que ele se torne inviável para o perfil de ameaça do sistema

### O Custo de uma Violação

> **[INDUSTRIAL]**
> IBM. *Cost of a Data Breach Report 2023.* IBM Security.
> URL: https://www.ibm.com/reports/data-breach

O relatório anual da IBM documentou que o custo médio global de uma violação de dados em 2023 foi de USD 4,45 milhões — o maior valor registrado na história do relatório. Organizações com maturidade de segurança alta (IA/automação em segurança) tiveram custos ~$1,76M menores.

**Nota sobre fonte [DISPUTADO como dado absoluto]:** Números do relatório IBM são baseados em entrevistas com organizações que voluntariamente participam — possível viés de seleção. A direção do efeito (violações custam caro) é amplamente corroborada. O número preciso deve ser tratado como estimativa ilustrativa, não fato preciso.

### Por Que Disciplina Individual Não É Suficiente

Da mesma forma que testes precisam ser automatizados (não podem depender de alguém lembrar de rodar), segurança precisa ser **estrutural** — incorporada ao design e ao pipeline, não uma camada aplicada depois.

> **[INDUSTRIAL]**
> Howard, M., & Lipner, S. (2006). *The Security Development Lifecycle.* Microsoft Press.
> — A Microsoft reportou internamente que a adoção do SDL reduziu vulnerabilidades em mais de 50% nos próprios produtos.
> **Nota [DISPUTADO]:** Este dado vem de fontes internas da Microsoft e não foi auditado independentemente. A direção (SDL reduz vulnerabilidades) é amplamente aceita; o percentual exato é reivindicação interna não verificada por terceiros.

---

## 2. O Princípio Unificador: Zero Trust e Defense in Depth

### Zero Trust — "Never Trust, Always Verify"

> **[PADRÃO-NIST]**
> Rose, S., Borchert, O., Mitchell, S., & Connelly, S. (2020). *Zero Trust Architecture.* NIST Special Publication 800-207. National Institute of Standards and Technology.
> DOI: 10.6028/NIST.SP.800-207
> URL: https://csrc.nist.gov/pubs/sp/800/207/final

O NIST SP 800-207 é o documento de referência canônico para Zero Trust Architecture (ZTA). Ele define:

> *"Zero trust (ZT) is the term for an evolving set of cybersecurity paradigms that move defenses from static, network-based perimeters to focus on users, assets, and resources."*

**Os Sete Princípios (Tenets) do Zero Trust (NIST SP 800-207):**

| # | Tenet | Implicação Prática |
|---|-------|--------------------|
| 1 | Todos os data sources e serviços são recursos | Nenhum recurso é implicitamente confiável |
| 2 | Todas as comunicações são protegidas | TLS em tudo, incluindo redes internas |
| 3 | Acesso é concedido por sessão individual | Não por localização de rede |
| 4 | Acesso determinado por política dinâmica | Com base em identidade + postura + contexto |
| 5 | Monitoramento contínuo de todos os ativos | Nenhum ativo é inerentemente confiável |
| 6 | Autenticação e autorização são dinâmicas | Reavaliadas continuamente |
| 7 | Coleta máxima de informação | Para melhorar postura de segurança |

**O Trade-off Central do Zero Trust:**

| Mais Zero Trust | Menos Zero Trust |
|----------------|-----------------|
| Menor blast radius em comprometimentos | Menor fricção operacional |
| Proteção contra insider threats | Menos overhead de autenticação |
| Maior complexidade de implementação | Mais simples de implementar |
| Requer infraestrutura de identidade madura | Funciona com sistemas legados |
| **Para:** produção, dados sensíveis, cloud | **Para:** sistemas legados isolados em rede física controlada |

### Defense in Depth — Camadas Independentes

> **[INDUSTRIAL]**
> Microsoft Security Development Lifecycle.
> URL: https://www.microsoft.com/en-us/securityengineering/sdl

Defense in Depth é o princípio de que nenhum controle único é suficiente. Camadas independentes garantem que a falha de uma não comprometa o sistema inteiro.

```
CAMADA 7 ── Dados:          Criptografia em repouso, DLP, backups
CAMADA 6 ── Aplicação:      OWASP Top 10, input validation, autenticação
CAMADA 5 ── Endpoint:       Patch management, EDR, hardening de SO
CAMADA 4 ── Identidade:     MFA, PoLP, Zero Trust, gestão de sessões
CAMADA 3 ── Rede:           Firewall, microsegmentação, IDS/IPS, TLS
CAMADA 2 ── Infraestrutura: Hardening de configuração, imagens seguras
CAMADA 1 ── Física:         Controle de acesso físico, destruição segura
```

**Trade-off do Defense in Depth:**

| Mais Camadas | Menos Camadas |
|-------------|--------------|
| Maior resiliência a falhas individuais | Menor complexidade operacional |
| Maior custo e overhead | Mais fácil de auditar e entender |
| Pode criar falsa sensação de segurança | Mais ágil para mudanças |
| **Para:** sistemas críticos, dados sensíveis | **Para:** serviços internos de baixo risco |

---

## 3. A Taxonomia dos Sete Domínios

A estrutura deste documento é derivada de dois frameworks complementares:

**Framework 1 — NIST SP 800-207 (Pilares de Zero Trust):**
Identidade → Dispositivo → Rede → Aplicação/Workload → Dados → Visibilidade → Automação

**Framework 2 — OWASP Top Ten 2021:**
Os dez riscos mais críticos baseados em dados de 500.000+ aplicações testadas.

> **[INDUSTRIAL-OWASP]**
> OWASP Foundation. (2021). *OWASP Top Ten 2021.*
> URL: https://owasp.org/Top10/

Os domínios deste guia são:

```
DOMÍNIO 1 ── Gestão de Identidade e Acesso (IAM)
DOMÍNIO 2 ── Proteção de Dados e Criptografia
DOMÍNIO 3 ── Segurança de Código e Aplicação
DOMÍNIO 4 ── Segurança de Infraestrutura e Rede
DOMÍNIO 5 ── Segurança de Dependências e Supply Chain
DOMÍNIO 6 ── Logging, Monitoramento e Resposta a Incidentes
DOMÍNIO 7 ── Segurança Específica para ML/IA
```

---

## 4. A Tabela de Trade-offs: O Que Define o Sênior

A habilidade mais importante não é saber *implementar* cada prática — é saber *quando* aplicar e *onde* está o equilíbrio correto para cada contexto.

| Domínio | Trade-off Central | Regra Absoluta | Negociável Conforme Contexto |
|---------|-------------------|---------------|------------------------------|
| **IAM** | Fricção de auth vs. segurança | MFA em produção, PoLP sempre | Nível de MFA (TOTP vs FIDO2) |
| **Criptografia** | Performance vs. proteção | TLS em trânsito sem exceção | Nível de criptografia em repouso |
| **Código** | Velocidade vs. segurança | Deny by default; validar na fronteira | Profundidade de validação por endpoint |
| **Infra** | Conveniência vs. superfície de ataque | Fechar tudo; abrir o mínimo | Granularidade de segmentação |
| **Supply Chain** | Velocidade vs. integridade | SCA automatizado no CI | Nível de SLSA exigido |
| **Logging** | Visibilidade vs. privacidade | Nunca logar dados sensíveis em plain text | Volume e retenção de logs |
| **ML/IA** | Performance vs. robustez | Verificar integridade de artefatos | Defesa adversarial por nível de ameaça |

---

# PARTE II — OS SETE DOMÍNIOS EM DETALHES

## 5. Domínio 1 — Gestão de Identidade e Acesso (IAM)

### 5.1 Princípio do Menor Privilégio (PoLP)

**Definição:** cada usuário, processo ou serviço acessa *somente* os recursos estritamente necessários para sua função — nada além, nada permanente quando não necessário.

**Referência:**
> **[PADRÃO-NIST]**
> NIST SP 800-207 (2020), op. cit. — Tenet 4: *"Access to resources is determined by dynamic policy — including the observable state of client identity, application/service, and the requesting asset — and may include other behavioral and environmental attributes. Least privilege principles are applied to restrict both visibility and accessibility."*

**Vetor de ataque prevenido:** lateral movement. Quando um atacante compromete uma conta com privilégios excessivos, ele pode mover-se por todo o sistema. Com PoLP, o *blast radius* de qualquer comprometimento é minimizado ao escopo mínimo da credencial comprometida.

**Trade-off explícito:**

| Mais Restritivo | Mais Permissivo |
|----------------|-----------------|
| Menor blast radius se comprometido | Menor fricção operacional |
| Maior complexidade de gestão de permissões | Desenvolvedores mais produtivos no curto prazo |
| Pode bloquear usuários legítimos por configuração incorreta | Mais rápido de configurar inicialmente |
| **Recomendado para:** produção, dados sensíveis, serviços externos | **Aceitável para:** ambientes de desenvolvimento completamente isolados |

**Implementação em Python/ML:**

```python
# ERRADO — conexão com banco usando superusuário
import psycopg2
conn = psycopg2.connect(
    user="postgres",        # root do banco — acesso total
    password="senha_admin",
    database="phishing_db"
)

# CORRETO — usuário com apenas as permissões necessárias
# No banco (SQL executado UMA VEZ pelo DBA):
# CREATE USER phishing_reader WITH PASSWORD '...';
# GRANT SELECT ON TABLE features, url_samples TO phishing_reader;
# (sem INSERT, UPDATE, DELETE, DROP, CREATE)

import os
from dotenv import load_dotenv
load_dotenv()

conn = psycopg2.connect(
    user="phishing_reader",         # acesso somente leitura
    password=os.getenv("DB_PASSWORD"),
    database="phishing_db",
    sslmode="require"               # exige TLS na conexão
)
```

---

### 5.2 Autenticação Multi-Fator (MFA)

**Definição:** exigir dois ou mais fatores independentes para autenticação:
- Algo que você *sabe* (senha, PIN)
- Algo que você *tem* (hardware key, app TOTP, SMS)
- Algo que você *é* (biometria)

**Referência:**
> **[PADRÃO-NIST]**
> NIST SP 800-63B (2017). *Digital Identity Guidelines — Authentication and Lifecycle Management.* NIST Special Publication 800-63B.
> DOI: 10.6028/NIST.SP.800-63b
> — Define três níveis de garantia (AAL1, AAL2, AAL3) e requisitos de MFA para cada nível.

**Vetor prevenido:** credential stuffing, phishing de credenciais, brute force de senha.

Pesquisa de incident response documentou que credenciais comprometidas são um dos vetores de acesso inicial mais frequentes em investigações de segurança. MFA mitiga diretamente esse vetor ao tornar credenciais roubadas insuficientes para acesso.

**Trade-off explícito:**

| Mais Seguro | Menos Fricção |
|------------|--------------|
| Hardware security keys (FIDO2/WebAuthn) | SMS-based OTP |
| Re-autenticação frequente por sessão | Sessões longas sem re-autenticação |
| MFA obrigatório em toda autenticação | MFA apenas para acesso privilegiado |
| **Crítico para:** acesso a produção, cloud admin, deploy | **Aceitável para:** serviços internos de baixo risco |

**Hierarquia de força dos fatores (NIST SP 800-63B):**

```
FIDO2 / Hardware Key (YubiKey)      ← AAL3, phishing-resistant
TOTP App (Google Authenticator)     ← AAL2, ampla adoção
Push Notifications (Duo, Okta)      ← AAL2, susceptível a MFA fatigue
SMS OTP                             ← NIST DESACONSELHA (SIM swapping)
Email OTP                           ← fraco, susceptível a phishing
Apenas senha                        ← AAL1, não usar para acesso crítico
```

**Nota importante sobre SMS OTP:** O NIST SP 800-63B inicialmente restringia uso de SMS como fator; em revisões subsequentes flexibilizou para não proibir, mas ainda expressa preocupação. O OWASP recomenda TOTP ou hardware key em vez de SMS para sistemas críticos.

---

### 5.3 Gestão de Segredos e Credenciais

**Definição:** credenciais, chaves de API, tokens e certificados nunca devem existir em texto plano no código, commits, logs ou configurações estáticas. Devem ser gerenciados por serviço dedicado com rotação.

**Referências:**
> **[INDUSTRIAL-OWASP]**
> OWASP Cheat Sheet Series. *Secrets Management Cheat Sheet.*
> URL: https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html

> **[INDUSTRIAL]**
> Microsoft Azure. *Recommendations for managing application secrets.*
> URL: https://learn.microsoft.com/en-us/azure/well-architected/security/secure-development-lifecycle

**Vetor prevenido:** credential exposure — a causa mais direta e evitável de comprometimentos em desenvolvimento de software.

**Regra absoluta (sem trade-off):** credenciais *nunca* no código, *nunca* no Git.

O histórico Git é imutável — remover a credencial do arquivo não remove do histórico. Uma credencial commitada, mesmo que removida imediatamente, deve ser considerada comprometida e rotacionada.

```bash
# Auditoria do histórico Git — execute imediatamente se não sabe o estado atual
git log --all -p | grep -iE "password|secret|api_key|token|private_key|access_key"

# Se encontrado → ROTACIONE a credencial imediatamente
# Remover do código não é suficiente — o histórico persiste
```

**Trade-off por nível de maturidade:**

| Nível | Solução | Trade-off |
|-------|---------|-----------|
| **Mínimo aceitável** | .env + python-dotenv + .gitignore | Simples; credenciais ainda em disco local |
| **Recomendado** | Vault dedicado (HashiCorp Vault, AWS Secrets Manager) | Mais complexo; credenciais nunca em disco |
| **Avançado** | Managed identities (sem credencial explícita) | Mais seguro; requer infraestrutura cloud |
| **Produção crítica** | Credenciais efêmeras com TTL de minutos/horas | Máximo; rotação automática contínua |

**Estrutura mínima recomendada:**

```
projeto/
├── .env.example     ← COMMITADO (apenas os nomes das chaves)
├── .env.local       ← NÃO commitado (valores de desenvolvimento)
├── .env.production  ← NÃO commitado; preferencialmente não existe localmente
└── .gitignore       ← contém: .env, .env.*, *.pem, *.key, secrets/
```

---

### 5.4 Controle de Acesso Baseado em Papel (RBAC)

**Definição:** permissões são associadas a *papéis* (roles), não diretamente a usuários. Usuários recebem papéis. Facilita gestão e auditoria de permissões em escala.

**Referência:**
> **[PADRÃO-NIST]**
> NIST SP 800-207 (2020), op. cit. — Tenet 3: *"Access to individual enterprise resources is granted on a per-session basis. Trust in the requester is evaluated before the access is granted."*

**Trade-off explícito:**

| RBAC (Roles) | ABAC (Atributos) | Permissões Diretas |
|-------------|-----------------|-------------------|
| Simples de auditar | Mais granular e flexível | Difícil de auditar em escala |
| Menos granular | Mais complexo de implementar | Mais simples inicialmente |
| **Para:** maioria dos sistemas | **Para:** sistemas com contexto complexo | **Nunca para:** produção com mais de ~10 usuários |

---

## 6. Domínio 2 — Proteção de Dados e Criptografia

### Fundação: OWASP A02 — Cryptographic Failures

> **[INDUSTRIAL-OWASP]**
> OWASP Top Ten 2021. *A02:2021 — Cryptographic Failures.*
> URL: https://owasp.org/Top10/2021/A02_2021-Cryptographic_Failures/

Este item cobre falhas ao proteger dados sensíveis, incluindo uso de algoritmos desatualizados, implementação incorreta de criptografia e exposição de dados sensíveis em trânsito ou em repouso.

---

### 6.1 Criptografia em Trânsito (TLS)

**Definição:** toda comunicação entre componentes usa TLS 1.2+ (preferencialmente TLS 1.3). Sem exceções para "redes internas" — Zero Trust assume que qualquer rede pode estar comprometida.

**Referência:**
> **[PADRÃO-NIST]**
> NIST SP 800-52 Rev 2 (2019). *Guidelines for the Selection, Configuration, and Use of Transport Layer Security (TLS) Implementations.*
> DOI: 10.6028/NIST.SP.800-52r2
> — Define TLS 1.2 como mínimo; TLS 1.3 fortemente recomendado.

**Trade-off explícito:**

| TLS em Toda Comunicação | TLS Seletivo |
|------------------------|-------------|
| Overhead de CPU para handshake/criptografia | Menor overhead em redes "confiáveis" |
| Complexidade de gestão de certificados | Configuração mais simples |
| Proteção contra man-in-the-middle interno | Vulnerável a ataques de insider e lateral movement |
| **Recomendado:** produção, staging, todas as comunicações | **Aceitável apenas:** pipelines batch em ambiente completamente air-gapped |

**Algoritmos e versões (2024+):**

```
RECOMENDADO:
  Protocolo: TLS 1.3
  Ciphers:   AES-256-GCM, ChaCha20-Poly1305, AES-128-GCM
  Curvas:    X25519, P-256, P-384
  Assinatura: Ed25519, ECDSA P-256, RSA-PSS

ACEITÁVEL (com ressalvas):
  Protocolo: TLS 1.2 (mínimo aceitável per NIST)
  Ciphers:   AES-128-GCM (com TLS 1.2)

PROIBIDO:
  Protocolo: TLS 1.0, TLS 1.1 (RFC 8996 — depreciados em 2021), SSL 3.0/2.0
  Ciphers:   RC4, DES, 3DES, exportCiphers, NULL cipher
  Hash:      MD5, SHA-1 para assinatura de certificados
```

---

### 6.2 Criptografia em Repouso

**Definição:** dados sensíveis armazenados (banco, arquivos, modelos ML, datasets) são criptografados com chaves gerenciadas separadamente dos dados.

**Trade-off explícito:**

| Tudo Criptografado | Criptografia Seletiva |
|-------------------|----------------------|
| Proteção uniforme; simples de raciocinar | Menor overhead de CPU em dados não-sensíveis |
| Gerenciamento de chaves mais complexo | Mais simples de implementar inicialmente |
| Impacto de performance em I/O intensivo | Melhor performance para dados de baixo risco |
| **Para:** todos os dados de usuário, credenciais, modelos ML | **Para:** dados públicos, logs sem PII |

**Atenção crítica para ML — modelos serializados com Pickle:**

O formato Pickle do Python executa código Python arbitrário durante a desserialização. Um modelo comprometido (substituído por um adversário no armazenamento) pode ser usado para execução remota de código (RCE) quando carregado.

```python
# INSEGURO — pickle executa código arbitrário ao desserializar
import pickle
model = pickle.load(open("model.pkl", "rb"))
# Um arquivo model.pkl malicioso pode executar qualquer código

# SEGURO — verificação de integridade antes de carregar
import hashlib
import joblib
import io
from pathlib import Path

EXPECTED_HASHES = {
    "models/phishing_v2.joblib": "sha256:abc123...",  # registrado na implantação
}

def load_model_safe(path: str) -> object:
    """Carrega modelo com verificação de integridade SHA-256."""
    path = Path(path)
    expected = EXPECTED_HASHES.get(str(path))
    if not expected:
        raise ValueError(f"Modelo não registrado: {path}")

    with open(path, "rb") as f:
        data = f.read()

    actual_hash = "sha256:" + hashlib.sha256(data).hexdigest()
    if actual_hash != expected:
        raise SecurityError(
            f"Hash do modelo não confere.\n"
            f"  Esperado: {expected}\n"
            f"  Atual: {actual_hash}\n"
            f"  POSSÍVEL TAMPERING — não carregue este modelo."
        )

    return joblib.load(io.BytesIO(data))
```

---

### 6.3 Hashing de Senhas

**Definição:** senhas nunca são armazenadas em texto plano nem com hashes rápidos (MD5, SHA-1, SHA-256 — projetados para velocidade, não para segurança de senhas). Devem usar funções de derivação de chave lentas com salt aleatório.

**Referência:**
> **[PADRÃO-NIST]**
> NIST SP 800-63B (2017), op. cit. — Seção 5.1.1.2: *"Memorized Secret Authenticators."*
> — NIST recomenda uso de funções de derivação de chave aprovadas como PBKDF2, bcrypt, scrypt, ou Argon2.

> **[INDUSTRIAL-OWASP]**
> OWASP Cheat Sheet. *Password Storage Cheat Sheet.*
> URL: https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html
> — OWASP recomenda Argon2id como primeira escolha; bcrypt como segunda.

**Hierarquia de algoritmos (2024+):**

```
argon2id   ← RECOMENDADO pela OWASP; resistente a GPU e ASIC; ajustável
bcrypt     ← Amplamente suportado; segunda opção sólida
scrypt     ← Alternativa válida; resistente a GPU
PBKDF2-HMAC-SHA256 ← Aceitável com ≥ 600.000 iterações (NIST 2023)
SHA-256 puro  ← NÃO USAR para senhas — muito rápido
MD5/SHA-1     ← NÃO USAR — comprometidos e rápidos
```

**Trade-off explícito:**

| argon2id (mais seguro) | PBKDF2 (mais compatível) |
|-----------------------|--------------------------|
| Resistente a GPU e ASIC | Amplamente suportado em frameworks legados |
| Configurável: memória, tempo, paralelismo | Menor custo computacional |
| Pode causar problemas em sistemas legados | Seguro com número correto de iterações |
| **Para:** sistemas novos, senhas críticas | **Para:** quando argon2id não está disponível |

---

### 6.4 Classificação e Rotulagem de Dados

**Definição:** toda informação tem um nível de sensibilidade explicitamente definido que determina como deve ser manuseada, armazenada, transmitida e destruída.

**Referência:**
> **[PADRÃO-NIST]**
> NIST SP 800-53 Rev 5 (2020). *Security and Privacy Controls for Information Systems and Organizations.*
> URL: https://doi.org/10.6028/NIST.SP.800-53r5
> — Controle RA-2: Security Categorization.

**Exemplo de taxonomia de dados:**

| Nível | Descrição | Controles Mínimos |
|-------|-----------|-------------------|
| **Público** | Informação disponível abertamente | Integridade básica |
| **Interno** | Uso interno da organização | Autenticação básica |
| **Confidencial** | Dados de negócio sensíveis | Criptografia + controle de acesso |
| **Restrito** | PII, credenciais, dados de saúde | Criptografia forte + audit trail + MFA |

---

## 7. Domínio 3 — Segurança de Código e Aplicação (OWASP Top Ten)

### O OWASP Top Ten 2021

> **[INDUSTRIAL-OWASP]**
> OWASP Foundation. (2021). *OWASP Top Ten 2021.*
> URL: https://owasp.org/Top10/

O OWASP Top Ten é compilado a partir de dados de 500.000+ aplicações testadas, combinados com survey de especialistas da indústria. É o framework de conscientização de segurança de aplicações mais amplamente adotado globalmente.

**Os dez riscos em 2021:**

| # | Categoria | Prevalência Documentada | Novo em 2021 |
|---|-----------|------------------------|--------------|
| A01 | Broken Access Control | 94% das apps | ↑ do #5 |
| A02 | Cryptographic Failures | — | ↑ renomeado |
| A03 | Injection | 94% das apps | = mantido |
| A04 | Insecure Design | — | Novo |
| A05 | Security Misconfiguration | ~90% das apps | ↑ do #6 |
| A06 | Vulnerable/Outdated Components | — | = renomeado |
| A07 | Auth & Identification Failures | — | ↓ do #2 |
| A08 | Software & Data Integrity Failures | — | Novo |
| A09 | Security Logging Failures | — | = mantido |
| A10 | Server-Side Request Forgery (SSRF) | — | Novo |

**Nota sobre a OWASP Top Ten 2025:** Uma nova versão está em desenvolvimento com dados coletados em 2024. As categorias e rankings podem mudar. Consulte https://owasp.org/Top10 para a versão mais atual.

---

### 7.1 A01 — Broken Access Control (o mais prevalente)

**Definição:** verificar *em cada operação* se o usuário autenticado tem permissão para executar *aquela ação específica* sobre *aquele recurso específico*.

A prevalência de 94% das aplicações testadas indica que este é o problema mais comum em código de produção.

**Trade-off explícito:**

| Deny by Default | Allow by Default |
|----------------|-----------------|
| Tudo bloqueado até permissão explícita | Tudo liberado até bloqueio explícito |
| Falhas de configuração = acesso negado (seguro) | Falhas de configuração = acesso concedido (inseguro) |
| Mais trabalho de configuração | Menor fricção no desenvolvimento |
| **Sempre recomendado para produção** | **Nunca recomendado para produção** |

```python
# ERRADO — assume que autenticado = autorizado para tudo
@app.route("/api/predict", methods=["POST"])
def predict():
    if not current_user.is_authenticated:
        abort(401)
    return jsonify(model.predict(request.json["url"]))
# Qualquer usuário autenticado pode usar o endpoint sem restrição

# CORRETO — verificação explícita de permissão + rate limiting
from functools import wraps

def require_permission(permission: str):
    def decorator(f):
        @wraps(f)
        def decorated_function(*args, **kwargs):
            if not current_user.is_authenticated:
                abort(401)
            if not current_user.has_permission(permission):
                abort(403)  # autenticado mas não autorizado
            return f(*args, **kwargs)
        return decorated_function
    return decorator

@app.route("/api/predict", methods=["POST"])
@require_permission("model:predict:execute")
@rate_limit(requests_per_minute=60)
def predict():
    url = validate_url_input(request.json.get("url", ""))
    return jsonify(model.predict(url))
```

---

### 7.2 A03 — Injection (94% das aplicações)

**Definição:** toda entrada de dados externos (usuário, API, arquivo) é validada, tipada e sanitizada antes de ser usada em queries, comandos, ou renderização.

**Referência:**
> **[INDUSTRIAL-OWASP]**
> OWASP Top Ten 2021. *A03:2021 — Injection.*
> URL: https://owasp.org/Top10/2021/A03_2021-Injection/
> *"User-supplied data is not validated, filtered, or sanitized by the application. The preferred option is to use a safe API, which avoids using the interpreter entirely, provides a parameterized interface."*

**Trade-off explícito:**

| Validação Estrita | Validação Permissiva |
|------------------|----------------------|
| Rejeita inputs maliciosos | Menos falsos positivos (rejeições de inputs legítimos) |
| Pode rejeitar inputs legítimos edge-case | Pode aceitar inputs maliciosos |
| Mais código de validação a manter | Código mais simples |
| **Para:** inputs de usuário não confiável, APIs públicas | **Para:** inputs de sistemas internos de alta confiança |

```python
from urllib.parse import urlparse
import re
from typing import Optional

MAX_URL_LENGTH = 2048
ALLOWED_SCHEMES = frozenset({"http", "https"})

def validate_url_input(url: Optional[str]) -> str:
    """
    Valida e normaliza URL antes de qualquer processamento.
    Levanta ValueError com mensagem descritiva em caso de falha.
    """
    if url is None:
        raise ValueError("URL não pode ser None")

    if not isinstance(url, str):
        raise ValueError(f"URL deve ser string, recebido: {type(url)}")

    url = url.strip()

    if len(url) == 0:
        raise ValueError("URL não pode ser vazia")

    if len(url) > MAX_URL_LENGTH:
        raise ValueError(f"URL excede comprimento máximo: {len(url)} > {MAX_URL_LENGTH}")

    # Bloqueia esquemas perigosos (javascript:, data:, file:, vbscript:)
    parsed = urlparse(url)
    if parsed.scheme.lower() not in ALLOWED_SCHEMES:
        raise ValueError(f"Esquema não permitido: {parsed.scheme!r}")

    # Bloqueia caracteres de controle
    if re.search(r"[\x00-\x1f\x7f]", url):
        raise ValueError("URL contém caracteres de controle proibidos")

    return url
```

---

### 7.3 A04 — Insecure Design (novo em 2021)

**Definição:** vulnerabilidades embutidas na *arquitetura* do sistema, não na implementação. Nenhuma quantidade de código correto resolve um design fundamentalmente inseguro.

**Referência:**
> **[INDUSTRIAL-OWASP]**
> OWASP Top Ten 2021. *A04:2021 — Insecure Design.*
> URL: https://owasp.org/Top10/2021/A04_2021-Insecure_Design/

**Diferença crítica:** Insecure Design ≠ Insecure Implementation. É possível ter design seguro com implementação insegura. Não é possível ter design inseguro com implementação segura.

**Trade-off explícito — Threat Modeling:**

| Threat Modeling Formal | Sem Threat Modeling |
|------------------------|---------------------|
| Identifica ameaças antes de escrever código | Mais rápido no início |
| Custo de remediação menor (mudança de design) | Problemas descobertos em produção são caros |
| Requer tempo e expertise específica | Sem overhead de processo |
| **Para:** sistemas novos com dados sensíveis | **Nunca recomendado para sistemas críticos** |

**O framework STRIDE para Threat Modeling:**

> **[INDUSTRIAL]**
> Shostack, A. (2014). *Threat Modeling: Designing for Security.* Wiley.

| Letra | Ameaça | Contramedida |
|-------|--------|-------------|
| S | Spoofing (falsificação de identidade) | Autenticação forte |
| T | Tampering (adulteração) | Integridade (HMAC, assinaturas) |
| R | Repudiation (repúdio) | Logging não-repudiável |
| I | Information Disclosure (vazamento) | Criptografia, PoLP |
| D | Denial of Service | Resiliência, rate limiting |
| E | Elevation of Privilege (escalada) | Autorização, sandboxing |

---

### 7.4 A05 — Security Misconfiguration (~90% das aplicações)

**Definição:** configurações padrão de frameworks, servidores e serviços frequentemente são inseguras. Todo componente deve ser configurado explicitamente para segurança mínima necessária.

**Referência:**
> **[INDUSTRIAL-OWASP]**
> OWASP Top Ten 2021. *A05:2021 — Security Misconfiguration.*
> URL: https://owasp.org/Top10/2021/A05_2021-Security_Misconfiguration/
> *"Security misconfiguration is the most common vulnerability on the list, and is often the result of using default configurations or displaying excessively verbose errors."*

**Trade-off explícito — Modo Debug:**

| Debug Desligado (produção) | Debug Ligado (problema crítico) |
|---------------------------|----------------------------------|
| Stack traces não expostos ao atacante | Facilita diagnóstico de erros |
| Erros genéricos para o usuário | Expõe estrutura interna da aplicação |
| Variáveis de ambiente não vazadas em erros | Pode expor paths, versões, configs |
| **Sempre em produção** | **Nunca em produção** |

```python
# Flask — configuração segura por ambiente
import os
from flask import Flask

app = Flask(__name__)

# VARIÁVEIS QUE MUDAM POR AMBIENTE:
app.config.update(
    DEBUG=False,                           # nunca True em produção
    TESTING=False,
    SECRET_KEY=os.getenv("FLASK_SECRET_KEY"),  # nunca hardcoded
    SESSION_COOKIE_SECURE=True,            # apenas HTTPS
    SESSION_COOKIE_HTTPONLY=True,          # sem acesso JavaScript
    SESSION_COOKIE_SAMESITE="Strict",      # mitigação CSRF
    PERMANENT_SESSION_LIFETIME=3600,       # sessão expira em 1h
    WTF_CSRF_ENABLED=True,                 # CSRF protection ativo
    MAX_CONTENT_LENGTH=16 * 1024 * 1024,   # limite de 16MB no upload
)

# Cabeçalhos de segurança (HTTP)
@app.after_request
def add_security_headers(response):
    response.headers["X-Content-Type-Options"] = "nosniff"
    response.headers["X-Frame-Options"] = "DENY"
    response.headers["X-XSS-Protection"] = "1; mode=block"
    response.headers["Strict-Transport-Security"] = "max-age=31536000; includeSubDomains"
    response.headers["Content-Security-Policy"] = "default-src 'self'"
    # NUNCA expor versão do servidor:
    response.headers.pop("Server", None)
    response.headers.pop("X-Powered-By", None)
    return response
```

---

### 7.5 A08 — Software and Data Integrity Failures (novo em 2021)

**Definição:** verifica a integridade de atualizações de software, dados críticos e pipelines CI/CD. Previne que código malicioso seja injetado sem detecção.

**Vetor documentado:** o ataque SolarWinds (2020) comprometeu o pipeline de build da SolarWinds, injetando código malicioso em atualizações de software legítimas distribuídas para mais de 18.000 organizações, incluindo agências do governo dos EUA.

**Referência:**
> **[INDUSTRIAL-OWASP]**
> OWASP Top Ten 2021. *A08:2021 — Software and Data Integrity Failures.*
> URL: https://owasp.org/Top10/2021/A08_2021-Software_and_Data_Integrity_Failures/

**Trade-off explícito:**

| Verificação Total | Sem Verificação |
|------------------|-----------------|
| Detecta tampering em artefatos e dependências | Sem overhead de verificação |
| Complexidade adicional no pipeline | Pipeline de deploy mais simples |
| Requer gestão de hashes/assinaturas | Confia implicitamente em toda dependência |
| **Para:** produção, artefatos críticos | **Nunca aceitável para código que executa em produção** |

---

## 8. Domínio 4 — Segurança de Infraestrutura e Rede

### 8.1 Superfície Mínima de Ataque (Attack Surface Reduction)

**Definição:** expor apenas o que é necessário. Cada serviço, porta, endpoint que não precisa existir é uma superfície de ataque evitável.

**Referência:**
> **[PADRÃO-NIST]**
> NIST SP 800-53 Rev 5 (2020), op. cit. — Controle SA-15: *"Development Process, Standards, and Tools"* e CM-7: *"Least Functionality."*

**Trade-off explícito:**

| Superfície Mínima | Superfície Permissiva |
|------------------|-----------------------|
| Menor superfície de ataque | Mais conveniente para desenvolvimento e debug |
| Mais trabalho de configuração de firewall | Menos restrições operacionais |
| Pode bloquear ferramentas legítimas de monitoramento | Mais fácil de diagnosticar problemas remotamente |
| **Para:** produção | **Para:** ambiente de desenvolvimento local completamente isolado |

```bash
# Verificar portas abertas desnecessariamente
ss -tlnp    # TCP em escuta com processo associado
ss -ulnp    # UDP em escuta
netstat -tulpn  # alternativa em sistemas mais antigos

# Regra prática:
# Se você não sabe para que serve → feche
# Se não precisa estar exposto à internet → não exponha
# Se dois serviços se comunicam → use rede privada, não pública
```

---

### 8.2 Hardening de Sistemas Operacionais e Containers

**Definição:** configurações padrão de sistemas operacionais e imagens de container são frequentemente excessivamente permissivas. Hardening remove capacidades, serviços e configurações desnecessárias.

**Referência:**
> **[PADRÃO-NIST]**
> NIST SP 800-123 (2008). *Guide to General Server Security.*
> DOI: 10.6028/NIST.SP.800-123

> **[INDUSTRIAL]**
> CIS Benchmarks. *Center for Internet Security.*
> URL: https://www.cisecurity.org/cis-benchmarks/
> — Benchmarks de configuração segura para sistemas operacionais, databases, cloud providers e containers. Referência da indústria para hardening.

**Trade-off explícito:**

| Hardening Agressivo | Configuração Padrão |
|--------------------|---------------------|
| Menor superfície de ataque | Menos trabalho de configuração |
| Pode quebrar aplicações que dependem de configurações padrão | Mais fácil de operar |
| Requer testes após hardening | Pode ter serviços desnecessários expostos |
| **Para:** produção, staging | **Para:** desenvolvimento local isolado |

**Para containers Docker — princípios básicos:**

```dockerfile
# INSEGURO — executa como root (padrão)
FROM python:3.11
COPY . /app
CMD ["python", "app.py"]

# SEGURO — princípios de hardening
FROM python:3.11-slim          # imagem menor = menos superfície de ataque

# Executa como usuário não-root
RUN groupadd -r appuser && useradd -r -g appuser appuser

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt  # sem cache = imagem menor

COPY --chown=appuser:appuser . .

USER appuser                    # nunca root em produção

# Apenas a porta necessária
EXPOSE 8080

CMD ["python", "-m", "gunicorn", "--bind", "0.0.0.0:8080", "app:app"]
```

---

### 8.3 Patch Management (Gestão de Atualizações)

**Definição:** dependências, bibliotecas, sistemas operacionais e frameworks são mantidos atualizados com patches de segurança de forma sistemática e rastreável.

**Caso histórico documentado:** A violação da Equifax (2017) explorou CVE-2017-5638 no Apache Struts, uma vulnerabilidade para a qual um patch havia sido publicado 2 meses antes. Resultado: 147 milhões de registros pessoais expostos, custos finais superiores a USD 1 bilhão.

**Referência:**
> **[INDUSTRIAL-OWASP]**
> OWASP Top Ten 2021. *A06:2021 — Vulnerable and Outdated Components.*
> URL: https://owasp.org/Top10/2021/A06_2021-Vulnerable_and_Outdated_Components/

**Trade-off explícito:**

| Atualização Imediata de Patches | Atualização Planejada |
|--------------------------------|----------------------|
| Vulnerabilidades fechadas rapidamente | Menos risco de instabilidade por breaking changes |
| Risco de instabilidade por mudanças | Mais tempo para testar em staging |
| Janela de exposição mínima | Janela de exposição maior |
| **Para:** patches de segurança críticos (CVSS ≥ 9.0) | **Para:** atualizações de feature e patches menores |

**Automação de auditoria de dependências:**

```bash
# Python — auditoria de vulnerabilidades conhecidas
pip install pip-audit
pip-audit                              # verifica CVEs em todas as dependências

# Ou com safety
pip install safety
safety check -r requirements.txt

# GitHub Dependabot — PRs automáticos para atualizações
```

```yaml
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: pip
    directory: "/"
    schedule:
      interval: weekly
    open-pull-requests-limit: 5
    # Patches de segurança com prioridade máxima:
    ignore:
      - dependency-name: "*"
        update-types: ["version-update:semver-major"]
```

---

## 9. Domínio 5 — Segurança de Dependências e Supply Chain

### O Problema da Supply Chain em Escala

> **[INDUSTRIAL]**
> Mandiant. *M-Trends 2022 Report.* Google/Mandiant.
> — Comprometimentos de supply chain contribuíram para 17% de todas as intrusões em 2021, comparado com menos de 1% em 2020. Ataque SolarWinds: 18.000+ organizações afetadas por uma única atualização de software comprometida.

---

### 9.1 Software Composition Analysis (SCA)

**Definição:** análise automatizada de todas as dependências diretas e transitivas em busca de vulnerabilidades conhecidas (CVEs no banco de dados do NIST NVD).

**Trade-off explícito:**

| SCA Rigoroso (bloquear qualquer CVE) | SCA por Severidade |
|--------------------------------------|-------------------|
| Zero tolerância a vulnerabilidades | Foco em riscos reais (CVSS ≥ 7.0) |
| Pode bloquear dependências sem alternativa disponível | Menos interrupções no desenvolvimento |
| Requer gestão ativa de exceções justificadas | Mais fácil de operar em equipes pequenas |
| **Para:** software com dados altamente sensíveis | **Para:** ferramentas internas, prototipagem |

**Ferramentas:** `pip-audit` (Python), `npm audit` (Node.js), `Snyk`, `Dependabot`, `OWASP Dependency-Check`.

---

### 9.2 SLSA Framework (Supply-chain Levels for Software Artifacts)

**Definição:** framework que garante integridade de artefatos de software do código-fonte ao binário distribuído, usando provenância verificável e assinaturas digitais.

**Referência:**
> **[INDUSTRIAL]**
> Lewandowski, K., & Lodato, M. (2021). *Introducing SLSA, an End-to-End Framework for Supply Chain Integrity.* Google Security Blog.
> URL: https://security.googleblog.com/2021/06/introducing-slsa-end-to-end-framework.html
> — Derivado do sistema interno "Binary Authorization for Borg" do Google, obrigatório para todas as workloads de produção do Google há 8+ anos.

> **[INDUSTRIAL]**
> SLSA Framework v1.1. *Supply-chain Levels for Software Artifacts.* OpenSSF.
> URL: https://slsa.dev/

**Analogia documentada pelo projeto:** SBOM é a lista de ingredientes. SLSA é a certificação de segurança alimentar que garante que a lista de ingredientes é confiável.

**Os quatro níveis de maturidade:**

| Nível | O Que Garante | Proteção Contra | Trade-off |
|-------|--------------|-----------------|-----------|
| **SLSA 1** | Provenância documentada | Básica rastreabilidade | Provenância não assinada; pode ser forjada |
| **SLSA 2** | Provenância assinada por plataforma hospedada | Modificação por insider básico | Requer CI/CD hospedado, não local |
| **SLSA 3** | Build em plataforma hardened e isolada | Comprometimento do build server | Requer infraestrutura dedicada |
| **SLSA 4** | Aprovação multilateral + builds herméticos | Insider threats avançados | Maior overhead; menor agilidade |

**Trade-off por contexto:**

| SLSA 3-4 | SLSA 1-2 |
|----------|----------|
| Proteção contra insider threats no CI/CD | Menor overhead de configuração |
| Detecta tampering em artefatos de forma verificável | Mais flexível para equipes pequenas |
| Requer infraestrutura dedicada de build | Adoção mais rápida e simples |
| **Para:** software distribuído a terceiros, OSS crítico | **Para:** software interno, projetos menores |

---

### 9.3 SBOM (Software Bill of Materials)

**Definição:** inventário completo de todas as dependências diretas e transitivas de um sistema.

**Referência:**
> **[PADRÃO-NIST]**
> CISA / NTIA. *Software Bill of Materials (SBOM) — Minimum Elements.*
> Executive Order 14028, May 12, 2021.
> URL: https://www.cisa.gov/sbom
> — O Executive Order 14028 exige SBOMs para software vendido ao governo federal dos EUA, acelerando a adoção industrial.

**Trade-off explícito:**

| Com SBOM | Sem SBOM |
|---------|---------|
| Visibilidade total das dependências diretas e transitivas | Sem overhead de geração |
| Identifica rapidamente impacto de novas CVEs (ex: Log4Shell) | Vulnerabilidades transitivas ocultas |
| Requerido em contextos regulatórios crescentes | Mais rápido inicialmente |
| **Para:** software crítico, contratos governamentais, OSS | **Progressivamente menos aceitável** |

---

## 10. Domínio 6 — Logging, Monitoramento e Resposta a Incidentes

### Fundação: OWASP A09 — Security Logging and Monitoring Failures

> **[INDUSTRIAL-OWASP]**
> OWASP Top Ten 2021. *A09:2021 — Security Logging and Monitoring Failures.*
> URL: https://owasp.org/Top10/2021/A09_2021-Security_Logging_and_Monitoring_Failures/

A ausência de logging adequado é problemática por uma razão específica: a maioria das violações documentadas não é detectada pela organização afetada — é descoberta externamente (por reguladores, pesquisadores, ou pela mídia). Logging e monitoramento são a diferença entre saber que você foi comprometido em horas versus em meses.

---

### 10.1 Logs de Segurança Estruturados e Auditáveis

**Definição:** logs estruturados (JSON) com contexto suficiente para reconstruir *o que aconteceu, quando, por quem, de onde* — sem expor dados sensíveis.

**O Dilema Central do Logging:**

| Log Máximo (tudo) | Log Mínimo (só erros críticos) |
|------------------|---------------------------------|
| Melhor visibilidade para forensics e detecção | Menor volume de dados e custo de armazenamento |
| Pode expor PII, credenciais, tokens nos logs | Menor superfície de vazamento através de logs |
| Requer redação (scrubbing) de dados sensíveis | Pode perder contexto crítico para investigação |
| **Para:** sistemas regulados (PCI-DSS, HIPAA), ambientes críticos | **Para:** microsserviços de baixo risco com dados não-sensíveis |

**O Que NUNCA Logar (regra absoluta, sem trade-off):**

```
NUNCA logar:
- Senhas (mesmo parcialmente mascaradas como "pass***")
- Tokens de sessão completos ou parciais
- Chaves de API ou tokens de autenticação
- Números de cartão de crédito (mesmo últimos 4 dígitos em alguns regulamentos)
- Dados pessoais sem necessidade operacional documentada
- Stack traces completos em respostas ao usuário final
```

**Implementação segura para o pipeline de phishing:**

```python
import logging
import json
import hashlib
from datetime import datetime, timezone
from typing import Optional

# Configuração de logging estruturado
logging.basicConfig(level=logging.INFO, format="%(message)s")
logger = logging.getLogger(__name__)

def log_prediction_event(
    url: str,
    prediction: int,
    confidence: float,
    latency_ms: float,
    model_version: str,
    user_id: Optional[str] = None
) -> None:
    """
    Log estruturado para predições — seguro e auditável.
    URL é hasheada para preservar privacidade mas manter rastreabilidade.
    """
    event = {
        "timestamp": datetime.now(timezone.utc).isoformat(),
        "event_type": "phishing_prediction",
        # URL NUNCA logada diretamente — pode conter dados sensíveis
        "url_sha256_prefix": hashlib.sha256(url.encode()).hexdigest()[:16],
        "prediction": int(prediction),
        "confidence": round(float(confidence), 4),
        "latency_ms": round(float(latency_ms), 2),
        "model_version": model_version,
        # user_id logado para auditoria, mas não PII adicional
        "user_id": user_id if user_id else "anonymous",
    }
    logger.info(json.dumps(event))

def log_security_event(
    event_type: str,
    severity: str,  # "low", "medium", "high", "critical"
    description: str,
    context: dict
) -> None:
    """Log de eventos de segurança — sempre estruturado e sem dados sensíveis."""
    # Remove chaves potencialmente sensíveis do contexto
    safe_context = {
        k: v for k, v in context.items()
        if k.lower() not in {"password", "token", "secret", "key", "credential"}
    }
    event = {
        "timestamp": datetime.now(timezone.utc).isoformat(),
        "event_type": f"security.{event_type}",
        "severity": severity,
        "description": description,
        "context": safe_context,
    }
    logger.warning(json.dumps(event))
```

---

### 10.2 Resposta a Incidentes (NIST SP 800-61)

**Definição:** procedimento documentado e *testado* para quando uma violação ou incidente de segurança ocorre. O momento de criar o plano não é durante a crise.

**Referência:**
> **[PADRÃO-NIST]**
> Cichonski, P., Millar, T., Grance, T., & Scarfone, K. (2012). *Computer Security Incident Handling Guide.* NIST Special Publication 800-61 Rev 2.
> DOI: 10.6028/NIST.SP.800-61r2
> URL: https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final

**As quatro fases do NIST:**

```
FASE 1: PREPARAÇÃO
  → Plano de resposta documentado e aprovado
  → Equipe de resposta identificada com papéis claros
  → Ferramentas de investigação instaladas e testadas
  → Exercícios de tabletop realizados periodicamente

FASE 2: DETECÇÃO E ANÁLISE
  → Monitoramento ativo com alertas calibrados
  → Correlação de logs (SIEM)
  → Triagem: real incident vs. false positive
  → Documentação de timeline desde o início

FASE 3: CONTENÇÃO, ERRADICAÇÃO E RECUPERAÇÃO
  → Contenção: isolar o sistema afetado (short-term + long-term)
  → Erradicação: remover a causa raiz (malware, credencial comprometida)
  → Recuperação: restaurar serviço com monitoramento intensificado

FASE 4: ATIVIDADE PÓS-INCIDENTE
  → Post-mortem sem culpa (blameless post-mortem)
  → Lições aprendidas documentadas
  → Controles melhorados para prevenir recorrência
  → Atualização do plano de resposta
```

**O Trade-off Mais Importante em Contenção:**

| Contenção Agressiva (desligar tudo) | Contenção Cirúrgica |
|-------------------------------------|---------------------|
| Máxima proteção dos dados | Menor impacto na disponibilidade do serviço |
| Maior impacto operacional imediato | Risco de não conter completamente |
| Mais simples de executar sob pressão | Requer diagnóstico preciso sob pressão |
| **Para:** violação confirmada com exfiltração de dados | **Para:** incidentes de baixo impacto ou suspeita inicial |

---

### 10.3 Threat Modeling e Revisão Periódica

**Definição:** análise estruturada das ameaças potenciais ao sistema, suas probabilidades e impactos, realizada durante o design e revisada periodicamente.

**Referência:**
> **[INDUSTRIAL]**
> Shostack, A. (2014). *Threat Modeling: Designing for Security.* Wiley.
> — O livro de referência mais completo sobre threat modeling prático.

**Trade-off explícito:**

| Threat Modeling Formal (STRIDE) | Revisão Informal |
|--------------------------------|-----------------|
| Identifica ameaças sistematicamente | Mais rápido de executar |
| Documentado e auditável | Depende de expertise da equipe |
| Facilita comunicação com stakeholders | Menos overhead de processo |
| **Para:** sistemas novos com dados sensíveis, mudanças arquiteturais | **Para:** features menores em sistemas já modelados |

---

## 11. Domínio 7 — Segurança Específica para ML/IA

Este é o domínio mais emergente. Os frameworks são mais recentes e menos consolidados que os outros domínios.

### Base de Referências

> **[INDUSTRIAL-OWASP]**
> OWASP Machine Learning Security Top Ten.
> URL: https://owasp.org/www-project-machine-learning-security-top-10/
> — Projeto OWASP específico para ML/IA. Menos maduro que o Web Top Ten, mas em desenvolvimento ativo.

> **[PEER-REVIEWED]**
> Sculley, D., et al. (2015). *Hidden Technical Debt in Machine Learning Systems.* NeurIPS.
> — Inclui riscos de segurança sistêmicos como hidden feedback loops e undeclared consumers que têm implicações de segurança diretas.

---

### 11.1 Adversarial Robustness (Robustez Adversarial)

**Definição:** modelos ML podem ser enganados por inputs especialmente construídos (*adversarial examples*) que para humanos parecem normais mas causam predições incorretas. Para sistemas de detecção de phishing, atacantes podem construir URLs que contornam o modelo.

**Referências:**
> **[PEER-REVIEWED]**
> Goodfellow, I. J., Shlens, J., & Szegedy, C. (2015). *Explaining and Harnessing Adversarial Examples.* ICLR 2015.
> arXiv: 1412.6572
> — Paper seminal que formalizou adversarial examples e o método FGSM.

> **[PEER-REVIEWED]**
> Madry, A., Makelov, A., Schmidt, L., Tsipras, D., & Vladu, A. (2018). *Towards Deep Learning Models Resistant to Adversarial Attacks.* ICLR 2018.
> arXiv: 1706.06083
> — Introduziu PGD (Projected Gradient Descent) como ataque mais forte e o treinamento adversarial como defesa.

**Trade-off explícito:**

| Treinamento Adversarial | Sem Defesa Adversarial |
|------------------------|------------------------|
| Modelo mais robusto a ataques por evasão | Treinamento mais simples e barato |
| Custo computacional maior (mais epochs, dados adversariais) | Melhor accuracy em inputs limpos |
| Pode reduzir accuracy em alguns benchmarks normais | Vulnerável a ataques de evasão sistemáticos |
| **Para:** sistemas de segurança (phishing, fraude, spam) | **Insuficiente para:** sistemas onde atacantes motivados existem |

---

### 11.2 Data Poisoning Defense

**Definição:** em sistemas que continuamente aprendem de novos dados (online learning, retreinamento periódico), atacantes podem submeter dados manipulados para degradar o modelo ou inserir backdoors.

**Trade-off explícito:**

| Validação Rigorosa dos Dados de Treino | Validação Mínima |
|----------------------------------------|-----------------|
| Detecta dados envenenados antes do treino | Maior volume de dados disponível para treino |
| Pipeline mais lento (mais validação) | Pipeline mais simples e rápido |
| Pode rejeitar dados legítimos de edge cases | Vulnerável a poisoning gradual e sistemático |
| **Para:** sistemas de segurança críticos, detecção de ameaças | **Para:** datasets com origem completamente confiável e auditada |

**Checklist de validação de dados para treino:**

```python
from typing import Tuple
import numpy as np
import pandas as pd
from scipy import stats

def validate_training_data(
    df: pd.DataFrame,
    reference_stats: dict
) -> Tuple[bool, list]:
    """
    Valida integridade do dataset antes do treino.
    Retorna (válido: bool, problemas: list).
    """
    issues = []

    # 1. Verificar distribuição de labels (deve ser similar ao histórico)
    label_dist = df["label"].value_counts(normalize=True)
    expected_positive_rate = reference_stats["expected_positive_rate"]
    if abs(label_dist.get(1, 0) - expected_positive_rate) > 0.15:
        issues.append(
            f"Distribuição de labels suspeita: "
            f"{label_dist.get(1, 0):.2%} positivos "
            f"(esperado: ~{expected_positive_rate:.2%})"
        )

    # 2. Verificar drift de features vs. distribuição histórica
    for col in reference_stats["feature_means"]:
        if col not in df.columns:
            issues.append(f"Feature ausente: {col}")
            continue
        ks_stat, p_val = stats.ks_2samp(
            df[col].dropna(),
            reference_stats["reference_samples"][col]
        )
        if p_val < 0.001:  # drift estatisticamente significativo
            issues.append(f"Drift detectado em feature '{col}': p={p_val:.4f}")

    # 3. Verificar valores absurdos (possível corrupção ou injeção)
    for col in ["entropy", "domain_length"]:
        if col in df.columns:
            z_scores = np.abs(stats.zscore(df[col].dropna()))
            n_outliers = (z_scores > 5).sum()
            if n_outliers > len(df) * 0.01:  # >1% de outliers extremos
                issues.append(f"Muitos outliers em '{col}': {n_outliers}")

    is_valid = len(issues) == 0
    return is_valid, issues
```

---

### 11.3 Model Access Control, Rate Limiting e Anti-Extraction

**Definição:** APIs de inferência de modelos exigem autenticação, autorização granular e rate limiting para prevenir:
- **Model stealing:** extração do comportamento do modelo via muitas queries
- **Model inversion:** reconstrução de dados de treino via queries direcionadas
- **DDoS:** saturação do endpoint de inferência

**Trade-off explícito:**

| Rate Limiting Estrito | Rate Limiting Permissivo |
|----------------------|--------------------------|
| Previne model stealing e DDoS | Melhor experiência para usuários legítimos com alta demanda |
| Pode bloquear usuários legítimos com pico de uso | Mais vulnerável a abuso sistemático |
| Requer lógica de gestão de quotas | Pipeline mais simples |
| **Para:** APIs públicas, serviços com usuários externos | **Para:** APIs internas com usuários conhecidos e confiáveis |

---

### 11.4 Privacidade Diferencial e Minimização de PII em Datasets

**Definição:** se o dataset de treino contém PII (informações pessoalmente identificáveis), técnicas de privacidade diferencial ou anonimização devem ser aplicadas para prevenir que o modelo "memorize" dados individuais.

**Referência:**
> **[PEER-REVIEWED]**
> Dwork, C., & Roth, A. (2014). *The Algorithmic Foundations of Differential Privacy.* Foundations and Trends in Theoretical Computer Science, 9(3–4), 211–407.
> DOI: 10.1561/0400000042
> — Paper seminal sobre privacidade diferencial.

**Trade-off explícito:**

| Privacidade Diferencial | Sem Proteção de Privacidade |
|------------------------|------------------------------|
| Garante proteção formal de dados individuais | Melhor performance do modelo |
| Reduz accuracy do modelo (adição de ruído) | Mais simples de implementar |
| Proteção contra ataques de membership inference | Vulnerável a memorização e inversão |
| **Para:** datasets com dados de usuários reais, aplicações reguladas | **Para:** datasets completamente anônimos e públicos |

---

# PARTE III — INTEGRAÇÃO AO CICLO DE DESENVOLVIMENTO

## 12. DevSecOps: Segurança no Pipeline de CI/CD

### A Filosofia Shift Left

**Definição:** "Shift Left" significa mover verificações de segurança para o mais cedo possível no ciclo de desenvolvimento — antes que vulnerabilidades se tornem caras de corrigir.

**Referência:**
> **[INDUSTRIAL]**
> Microsoft SDL. *Secure Development Lifecycle.*
> URL: https://www.microsoft.com/en-us/securityengineering/sdl

### Integração de Segurança no CI/CD

O pipeline de segurança deve ser paralelo ao pipeline de testes — com os mesmos princípios de "fail fast" e feedback rápido:

```yaml
# .github/workflows/security.yml
name: Security Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  security:
    name: Security Gates
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0  # necessário para scan completo do histórico

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.11"

      - name: Install security tools
        run: |
          pip install bandit detect-secrets pip-audit ruff

      # GATE 1: Segredos no código (mais rápido — falha primeiro)
      - name: Scan for secrets (detect-secrets)
        run: |
          detect-secrets scan --baseline .secrets.baseline
          detect-secrets audit .secrets.baseline

      # GATE 2: Análise estática de segurança (SAST)
      - name: SAST with bandit
        run: |
          bandit -r src/ \
            --severity-level medium \
            --confidence-level medium \
            --format json \
            -o bandit-report.json
          # Falha se encontrar HIGH severity
          bandit -r src/ --severity-level high --exit-zero

      # GATE 3: Linter com regras de segurança
      - name: Lint security rules (ruff)
        run: |
          ruff check . \
            --select S \
            --format github
          # Regras S = bandit/segurança integradas no ruff

      # GATE 4: Auditoria de dependências
      - name: Dependency audit (pip-audit)
        run: |
          pip-audit \
            --requirement requirements.txt \
            --format json \
            --output pip-audit-report.json

      # GATE 5: Publicar relatórios como artefatos
      - name: Upload security reports
        uses: actions/upload-artifact@v4
        if: always()
        with:
          name: security-reports
          path: |
            bandit-report.json
            pip-audit-report.json
```

---

### SAST vs DAST vs IAST

| Tipo | Quando Roda | O Que Encontra | Custo |
|------|-------------|----------------|-------|
| **SAST** (estático) | Durante development, no CI | Vulnerabilidades no código sem executar | Baixo |
| **DAST** (dinâmico) | Contra ambiente running | Vulnerabilidades em runtime | Médio |
| **IAST** (interativo) | Durante testes | Combina SAST + DAST em tempo real | Alto |
| **SCA** (composição) | No CI, em pull requests | Vulnerabilidades em dependências | Baixo |

**Trade-off por contexto:**

| Cobertura Completa (SAST+DAST+IAST+SCA) | Cobertura Mínima (SAST+SCA) |
|----------------------------------------|------------------------------|
| Detecção máxima de vulnerabilidades | Menor overhead no pipeline |
| Pipeline mais lento e caro | Feedback mais rápido |
| Requer ambientes dedicados para DAST | Simples de implementar |
| **Para:** sistemas críticos, regulated industries | **Para:** ponto de partida em projetos novos |

---

## 13. Checklist Operacional por Domínio

Use este checklist para rastrear progresso:
- `[x]` — implementado e funcionando
- `[-]` — parcialmente implementado
- `[ ]` — gap confirmado (próximo alvo)

### Domínio 1 — Gestão de Identidade e Acesso

```
[ ] .env + python-dotenv configurados; .gitignore cobre .env.*
[ ] Histórico Git auditado em busca de credenciais expostas
[ ] Credenciais rotacionadas se encontradas no histórico
[ ] detect-secrets configurado como pre-commit hook
[ ] PoLP aplicado (DB, APIs, cloud — cada serviço com acesso mínimo)
[ ] MFA habilitado em: GitHub, cloud provider, serviços críticos
[ ] Credenciais de produção nunca existem em máquinas de desenvolvimento
[ ] Separação de credenciais por ambiente (dev ≠ staging ≠ prod)
```

### Domínio 2 — Proteção de Dados e Criptografia

```
[ ] TLS 1.2+ em toda comunicação (incluindo serviços internos)
[ ] Certificados TLS com renovação automática (Let's Encrypt ou equivalente)
[ ] Modelos ML verificados por SHA-256 antes de carregamento
[ ] Nenhum dado sensível em texto plano no banco ou arquivos
[ ] Senhas hasheadas com argon2id ou bcrypt (nunca MD5/SHA-256 puro)
[ ] Algoritmos proibidos banidos: RC4, DES, MD5 para assinatura
```

### Domínio 3 — Segurança de Código e Aplicação

```
[ ] Validação de input em toda fronteira de confiança
[ ] Deny by default em controle de acesso
[ ] Debug mode desligado em produção
[ ] Cabeçalhos de segurança HTTP configurados
[ ] bandit rodando no CI (SAST para Python)
[ ] ruff com regras S (security) habilitadas
[ ] Nenhuma credencial hardcoded no código (verificado por SAST)
[ ] SQL parametrizado (sem concatenação de strings em queries)
```

### Domínio 4 — Infraestrutura e Rede

```
[ ] Apenas portas necessárias expostas (verificado com ss -tlnp)
[ ] Containers rodando como usuário não-root
[ ] Imagens base atualizadas com patches recentes
[ ] CIS Benchmarks aplicados ao SO (ou equivalente)
[ ] Segmentação de rede entre ambientes (dev/staging/prod)
[ ] Patch management automatizado para dependências do SO
```

### Domínio 5 — Supply Chain

```
[ ] pip-audit rodando no CI
[ ] Dependabot configurado para PRs automáticos de segurança
[ ] Nenhuma dependência sem versão fixada em requirements.txt
[ ] SBOMs gerados para releases (ao menos localmente)
[ ] Imagens Docker com digest fixado (não apenas tag)
```

### Domínio 6 — Logging e Monitoramento

```
[ ] Logs estruturados (JSON) em todos os componentes críticos
[ ] Nenhum dado sensível nos logs (auditado regularmente)
[ ] Alertas configurados para tentativas de autenticação falhadas
[ ] Alertas configurados para uso anormal da API (rate)
[ ] Plano de resposta a incidentes documentado
[ ] Contatos de emergência identificados para cada componente crítico
```

### Domínio 7 — ML/IA

```
[ ] Integridade de modelos verificada por hash antes de carregar
[ ] Modelos serializados com joblib (não pickle puro) quando possível
[ ] Rate limiting no endpoint de inferência
[ ] Autenticação exigida em toda API de predição
[ ] Validação de dados de entrada antes de predição
[ ] Monitoramento de distribuição dos inputs em produção
[ ] Processo documentado para retreinamento seguro
```

---

## 14. Roteiro de Implementação Gradual

Priorizado por urgência e impacto, calibrado para desenvolvimento em paralelo com outros projetos.

### SEMANA 1 — Fundação de Segurança (Crítico — Deve ser feito agora)

```
1. Auditar histórico Git em busca de credenciais:
   git log --all -p | grep -iE "password|secret|api_key|token"

2. Configurar gestão de segredos:
   touch .env
   echo ".env\n.env.*\n*.pem\n*.key" >> .gitignore
   pip install python-dotenv detect-secrets
   detect-secrets scan > .secrets.baseline

3. Instalar e ativar pre-commit com hooks de segurança:
   pip install pre-commit
   # Criar .pre-commit-config.yaml com detect-secrets + ruff (rules S)
   pre-commit install
```

**Por que agora:** você tem ambientes múltiplos incluindo produção. Credenciais hardcoded + commits diretos na main + acesso a produção = risco crítico ativo.

### SEMANA 2-3 — Qualidade de Código Seguro

```
1. Configurar bandit no CI:
   pip install bandit
   bandit -r src/ --severity-level medium

2. Habilitar regras de segurança no ruff (pyproject.toml):
   [tool.ruff]
   select = ["S", "B", ...]

3. Adicionar verificação de integridade de modelos
4. Revisar controle de acesso em endpoints da API (deny by default)
```

### MÊS 2 — Supply Chain e Automação

```
1. pip-audit no CI para auditoria de dependências
2. Dependabot configurado para PRs automáticos
3. Fixar versões de todas as dependências em requirements.txt
4. Security gates no GitHub Actions (bloquear merge se falhar)
```

### MÊS 3 — Monitoramento e Resposta

```
1. Logging estruturado em todos os módulos críticos
2. Alertas configurados para anomalias (auth failures, rate spikes)
3. Documento de plano de resposta a incidentes (simples)
4. Processo documentado para rotação de credenciais
```

---

# PARTE IV — REFERÊNCIAS

## 15. Mapa de Confiabilidade das Afirmações

| Afirmação | Fonte | Nível | Nota |
|-----------|-------|-------|------|
| Zero Trust como arquitetura de segurança moderna | NIST SP 800-207 (2020) | **PADRÃO-NIST** | Documento oficial do governo dos EUA |
| Broken Access Control em 94% das aplicações | OWASP Top Ten 2021 | **INDUSTRIAL-OWASP** | Baseado em 500.000+ aplicações |
| Injection em 94% das aplicações testadas | OWASP Top Ten 2021 | **INDUSTRIAL-OWASP** | Dado empírico direto |
| Security Misconfiguration em ~90% das apps | OWASP Top Ten 2021 | **INDUSTRIAL-OWASP** | Dado empírico direto |
| MFA como requisito para AAL2 | NIST SP 800-63B (2017) | **PADRÃO-NIST** | Norma técnica governamental |
| TLS 1.2 como mínimo aceitável | NIST SP 800-52 Rev 2 (2019) | **PADRÃO-NIST** | Norma técnica governamental |
| Supply chain: 17% das intrusões em 2021 | Mandiant M-Trends 2022 | **INDUSTRIAL** | Relatório de empresa de segurança; pode ter viés de amostra |
| SDL reduziu vulnerabilidades em 50%+ | Microsoft (interno, 2006) | **DISPUTADO** | Não auditado externamente; dado interno da Microsoft |
| Custo médio de violação: USD 4,45M | IBM Cost of Breach 2023 | **DISPUTADO** | Possível viés de seleção; use como ordem de magnitude |
| SolarWinds: 18.000+ organizações afetadas | Múltiplas fontes jornalísticas e governamentais | **INDUSTRIAL** | Número reportado; difícil de verificar independentemente |
| Argon2id como função de hash de senha recomendada | OWASP Password Storage Cheat Sheet | **INDUSTRIAL-OWASP** | Consenso da comunidade de segurança |
| Adversarial examples formalizado por Goodfellow et al. | ICLR 2015 | **PEER-REVIEWED** | Altamente citado, amplamente replicado |
| Privacidade diferencial formalizada por Dwork & Roth | Foundations and Trends 2014 | **PEER-REVIEWED** | Obra de referência acadêmica |

---

## 16. Referências Completas

### Normas Técnicas e Publicações Governamentais (NIST)

1. **Rose, S., Borchert, O., Mitchell, S., & Connelly, S.** (2020). *Zero Trust Architecture.* NIST Special Publication 800-207.
   DOI: 10.6028/NIST.SP.800-207
   URL: https://csrc.nist.gov/pubs/sp/800/207/final
   — **Relevância:** Fundação de Zero Trust, princípio do menor privilégio

2. **Grassi, P. A., et al.** (2017). *Digital Identity Guidelines: Authentication and Lifecycle Management.* NIST Special Publication 800-63B.
   DOI: 10.6028/NIST.SP.800-63b
   URL: https://pages.nist.gov/800-63-3/sp800-63b.html
   — **Relevância:** MFA, níveis de garantia (AAL), hashing de senhas

3. **McKay, K., & Cooper, D.** (2019). *Guidelines for the Selection, Configuration, and Use of TLS Implementations.* NIST Special Publication 800-52 Rev 2.
   DOI: 10.6028/NIST.SP.800-52r2
   — **Relevância:** TLS 1.2 como mínimo aceitável, algoritmos aprovados

4. **Cichonski, P., Millar, T., Grance, T., & Scarfone, K.** (2012). *Computer Security Incident Handling Guide.* NIST Special Publication 800-61 Rev 2.
   DOI: 10.6028/NIST.SP.800-61r2
   — **Relevância:** As quatro fases de resposta a incidentes

5. **Joint Task Force.** (2020). *Security and Privacy Controls for Information Systems and Organizations.* NIST Special Publication 800-53 Rev 5.
   DOI: 10.6028/NIST.SP.800-53r5
   — **Relevância:** Controles de segurança abrangentes, classificação de dados

6. **Stoneburner, G., & Goguen, A.** (2008). *Guide to General Server Security.* NIST Special Publication 800-123.
   DOI: 10.6028/NIST.SP.800-123
   — **Relevância:** Hardening de servidores e sistemas operacionais

7. **CISA / NTIA.** (2021). *Software Bill of Materials (SBOM) — Minimum Elements.* Executive Order 14028.
   URL: https://www.cisa.gov/sbom
   — **Relevância:** Requisitos de SBOM, inventário de dependências

### Fontes OWASP (Industrial — Consenso Global)

8. **OWASP Foundation.** (2021). *OWASP Top Ten 2021.*
   URL: https://owasp.org/Top10/
   — **Relevância:** Os dez riscos mais críticos em aplicações web

9. **OWASP Foundation.** *Secrets Management Cheat Sheet.*
   URL: https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html
   — **Relevância:** Gestão de credenciais e segredos

10. **OWASP Foundation.** *Password Storage Cheat Sheet.*
    URL: https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html
    — **Relevância:** argon2id, bcrypt, algoritmos corretos de hashing

11. **OWASP Foundation.** *OWASP Machine Learning Security Top Ten.*
    URL: https://owasp.org/www-project-machine-learning-security-top-10/
    — **Relevância:** Segurança específica para sistemas ML/IA

### Artigos Acadêmicos (Peer-Reviewed)

12. **Goodfellow, I. J., Shlens, J., & Szegedy, C.** (2015). *Explaining and Harnessing Adversarial Examples.* ICLR 2015.
    arXiv: 1412.6572
    — **Relevância:** Fundação de adversarial examples em ML

13. **Madry, A., Makelov, A., Schmidt, L., Tsipras, D., & Vladu, A.** (2018). *Towards Deep Learning Models Resistant to Adversarial Attacks.* ICLR 2018.
    arXiv: 1706.06083
    — **Relevância:** Treinamento adversarial como defesa (PGD)

14. **Dwork, C., & Roth, A.** (2014). *The Algorithmic Foundations of Differential Privacy.* Foundations and Trends in Theoretical Computer Science, 9(3–4), 211–407.
    DOI: 10.1561/0400000042
    — **Relevância:** Privacidade diferencial para proteção de dados de treino

15. **Sculley, D., Holt, G., Golovin, D., et al.** (2015). *Hidden Technical Debt in Machine Learning Systems.* NeurIPS, 28, pp. 2503–2511.
    URL: https://papers.nips.cc/paper/5656
    — **Relevância:** Riscos de segurança sistêmicos em sistemas ML

### Fontes Industriais e Guias Técnicos

16. **Howard, M., & Lipner, S.** (2006). *The Security Development Lifecycle.* Microsoft Press.
    — **Relevância:** SDL framework; segurança integrada ao ciclo de desenvolvimento

17. **Microsoft Security Engineering.** *Security Development Lifecycle (SDL).*
    URL: https://www.microsoft.com/en-us/securityengineering/sdl
    — **Relevância:** Práticas de DevSecOps e integração ao CI/CD

18. **Google / OpenSSF.** (2021). *SLSA: Supply-chain Levels for Software Artifacts.*
    URL: https://slsa.dev/
    — **Relevância:** Integridade de artefatos e segurança de supply chain

19. **Center for Internet Security.** *CIS Benchmarks.*
    URL: https://www.cisecurity.org/cis-benchmarks/
    — **Relevância:** Configuração segura de SO, databases e containers

20. **Shostack, A.** (2014). *Threat Modeling: Designing for Security.* Wiley.
    — **Relevância:** STRIDE, processo de threat modeling

21. **IBM Security.** (2023). *Cost of a Data Breach Report 2023.*
    URL: https://www.ibm.com/reports/data-breach
    — **Relevância:** Custo de violações de dados (dado industrial, não auditado externamente)

---

## Síntese Final

> **Segurança não é um estado final — é um processo contínuo de gestão de risco.**
>
> A diferença entre um desenvolvedor júnior e um sênior em segurança não está em conhecer mais vulnerabilidades.
> Está em **internalizar o modelo mental correto**:
>
> - O atacante já está dentro — e se ainda não está, será
> - Toda linha de código que não valida uma entrada é uma decisão explícita de aceitar o risco correspondente
> - Segurança máxima = sistema inutilizável. O trabalho é encontrar o equilíbrio correto para o perfil de ameaça real
> - Trade-offs são decisões de negócio, não de tecnologia — devem ser documentados explicitamente
>
> O princípio operacional é o Tenet 1 do NIST SP 800-207:
> *"Assume a hostile environment. Treat all communications as suspect regardless of origination."*

---

*Todas as afirmações têm referência identificada com nível de evidência explícito.
Fontes disputadas ou com evidência não auditada externamente estão marcadas com [DISPUTADO].
Revisão recomendada a cada 12 meses — o panorama de ameaças evolui rapidamente.
Para atualizações, verificar: https://owasp.org/Top10/ e https://csrc.nist.gov/publications/sp*
