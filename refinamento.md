# CHECKLIST DE REFINAMENTO DE HISTÓRIAS DE USUÁRIO
**Arquiteturas Distribuídas: Microserviços .NET 8/9 & Micro Frontends (ReactJS)**

---

## ✅ GATE 0 — CRITÉRIOS DE ENTRADA (Antes de iniciar o refinamento)

> Valide estes itens antes de colocar a história na agenda de refinamento. Se algum estiver faltando, devolva ao PO para maturação.

- [ ] A história possui título descritivo e está linkada ao Épico correspondente.
- [ ] A narrativa no formato **"Como / Quero / Para que"** está escrita.
- [ ] O PO consegue explicar o valor de negócio da história em 2 frases.
- [ ] Protótipos ou wireframes (Figma) estão disponíveis e linkados.
- [ ] A história não depende de outra história não refinada ou não entregue.
- [ ] O escopo está focado em **uma única entrega de valor** (não é um épico disfarçado).

---

## ✅ GATE 1 — REFINAMENTO FUNCIONAL E DE NEGÓCIO

**Participantes:** Product Owner, Time de Desenvolvimento, QA, UX/UI Designer

### 1.1 Contexto e Valor
- [ ] O time compreende o problema de negócio que a história resolve.
- [ ] O usuário-alvo (persona) foi identificado.
- [ ] O valor de negócio foi validado e é claro para todo o time.

### 1.2 Critérios de Aceite (BDD)
- [ ] Os cenários BDD (*Given-When-Then*) cobrem o **fluxo principal (happy path)**.
- [ ] Os cenários BDD cobrem os principais **fluxos de exceção e erro de negócio**.
- [ ] Os critérios de aceite são objetivos, mensuráveis e testáveis.
- [ ] Não há critérios ambíguos ou sujeitos a interpretação dupla.

### 1.3 Regras de Negócio e Interface
- [ ] Todas as regras de negócio relevantes estão documentadas na história.
- [ ] Os protótipos de tela foram apresentados e validados pelo time.
- [ ] Os **4 estados da UI** foram mapeados: Loading, Sucesso, Erro e Empty State.
- [ ] Comportamento da UI em caso de falha de rede ou serviço indisponível está definido.

---

## ✅ GATE 2 — REFINAMENTO TÉCNICO E ARQUITETURAL

**Participantes:** Time de Engenharia (Frontend, Backend, DevOps, QA/Automation)

### 2.1 Análise de Impacto e Dependências
- [ ] Impacto na arquitetura atual foi analisado.
- [ ] Dependências com outros times, squads ou serviços foram mapeadas.
- [ ] Dependências externas (APIs de terceiros, parceiros) foram identificadas e validadas.

### 2.2 Front-end: Micro Frontend (ReactJS)

| Categoria | Item de Verificação | Status |
| :--- | :--- | :---: |
| **Arquitetura MFE** | Mapeamento claro de MFE Host (Shell) vs Remote. | [ ] |
| **Module Federation** | Configuração de dependências compartilhadas (`singleton` para React/React-Query). | [ ] |
| **Fallback & Isolation** | Tratativas com *Error Boundaries* para mitigar quedas do MFE remoto. | [ ] |
| **Estados de UI** | Mapeamento dos estados de Loading, Sucesso, Erro e Empty State. | [ ] |
| **State & Cache** | Estratégia de cache com React Query (`staleTime`, `optimistic updates`). | [ ] |
| **Segurança & Token** | Injeção e renovação transparente do token JWT/OAuth via interceptor HTTP. | [ ] |

### 2.3 Back-end: Microserviços (.NET 8/9)

| Categoria | Item de Verificação | Status |
| :--- | :--- | :---: |
| **Arquitetura** | Separação em Clean Architecture / CQRS via MediatR. | [ ] |
| **Validação** | Validação de entrada com FluentValidation (curto-circuito antes do domínio). | [ ] |
| **Erros** | Middleware global formatando erros no padrão RFC 7807 (*ProblemDetails*). | [ ] |
| **Persistência** | Queries Dapper parametrizadas, restrições `UNIQUE` e índices otimizados no banco. | [ ] |
| **Performance BD** | Uso de `QueryMultiple` para queries compostas e mitigação de N+1 com projeções explícitas. | [ ] |
| **Mensageria** | Implementação do *Transactional Outbox Pattern* e consumidor idempotente. | [ ] |
| **Resiliência** | Políticas de Retry (Exponential Backoff), Circuit Breaker e Timeout com Polly. | [ ] |
| **Cache** | Invalidação ativa e fallback gracioso no Redis (`IDistributedCache`). | [ ] |

### 2.4 Infraestrutura, Segurança e Observabilidade

| Categoria | Item de Verificação | Status |
| :--- | :--- | :---: |
| **Observabilidade** | Propagação do `CorrelationId` / W3C Trace Context em logs e chamadas HTTP/Broker. | [ ] |
| **Logging** | Serilog formatado em JSON estruturado sem exposição de dados sensíveis (PII). | [ ] |
| **Health Check** | Endpoints `/healthz/live` e `/healthz/ready` checando BD, Redis e Broker. | [ ] |
| **Containerization** | Dockerfile Multi-stage build com runtime minimalista executado como não-root. | [ ] |
| **Segurança** | CORS restrito às origens dos MFEs e validação estrita de Claims do JWT. | [ ] |

### 2.5 Contratos e Modelagem
- [ ] Contrato de API (REST/JSON) definido e documentado (OpenAPI/Swagger ou payload de exemplo).
- [ ] Schema de eventos de integração definido (quando aplicável).
- [ ] Modelagem de dados revisada e scripts SQL validados.
- [ ] Queries Dapper críticas revisadas quanto a parâmetros e performance.
- [ ] Estratégia de cache definida (quando aplicável).

---

## ✅ GATE 3 — FATIAMENTO E ESTIMATIVA

**Participantes:** Time de Desenvolvimento e PO

### 3.1 Princípios INVEST
- [ ] **I**ndependente — a história pode ser desenvolvida sem bloquear ou ser bloqueada por outra.
- [ ] **N**egociável — o escopo pode ser ajustado sem perder o valor central.
- [ ] **V**aliosa — entrega valor real ao usuário ou ao negócio.
- [ ] **E**stimável — o time consegue estimar o esforço com as informações disponíveis.
- [ ] **S**mall (Pequena) — cabe em uma Sprint sem precisar de fatiamento adicional.
- [ ] **T**estável — possui critérios de aceite objetivos que permitem validação.

### 3.2 Fatiamento e Subtarefas
- [ ] A história foi fatiada em subtarefas técnicas claras e atribuíveis.
- [ ] Cada subtarefa tem responsável definido (Frontend, Backend, DevOps, QA).
- [ ] Nenhuma subtarefa isolada é maior do que 2 dias de trabalho.

### 3.3 Estimativa
- [ ] Estimativa de esforço realizada (Story Points / Planning Poker).
- [ ] O time está confortável com a estimativa (sem objeções não resolvidas).

---

## ✅ GATE 4 — DEFINITION OF READY (DoR) — VALIDAÇÃO FINAL

> A história só entra na Sprint se **todos** os itens abaixo estiverem marcados.

- [ ] A narrativa "Como / Quero / Para que" está escrita e validada pelo PO.
- [ ] Os Critérios de Aceite em formato BDD estão completos e sem ambiguidade.
- [ ] Os protótipos de tela estão aprovados e linkados na tarefa.
- [ ] Os contratos de API / schemas de eventos estão definidos.
- [ ] As dependências externas estão mapeadas e não bloqueiam o desenvolvimento.
- [ ] As subtarefas técnicas estão criadas no board (Azure DevOps).
- [ ] A estimativa de Story Points foi atribuída.
- [ ] O checklist técnico (Gates 2.2, 2.3 e 2.4) foi revisado pelo time de engenharia.
- [ ] Não há dúvidas em aberto sem responsável e prazo para resolução.

---

## 📋 TEMPLATE PARA CRIAÇÃO DA HISTÓRIA NO AZURE DEVOPS

```markdown
### 📝 Descrição da História
**Como** [tipo de usuário]
**Quero** [funcionalidade/ação]
**Para que** [benefício/valor de negócio]

---

### 🔗 Rastreabilidade
- **Épico:** [link]
- **Squad responsável:** [nome da squad]
- **Data do refinamento:** [DD/MM/AAAA]
- **Refinamento aprovado por:** [nome do PO]

---

### 🎯 Critérios de Aceite (BDD)

**Cenário 1: Fluxo Principal (Happy Path)**
- **Dado que** [contexto inicial]
- **Quando** [ação realizada pelo usuário]
- **Então** [resultado esperado]

**Cenário 2: Fluxo de Exceção**
- **Dado que** [contexto inicial]
- **Quando** [ação ou condição de erro]
- **Então** [comportamento esperado do sistema]

---

### 🛠️ Subtarefas Técnicas de Engenharia
- [ ] **[MFE React]** Criar componente UI com os estados de Loading, Erro e Sucesso.
- [ ] **[MFE React]** Configurar Hook React Query com suporte a Optimistic Update.
- [ ] **[.NET API]** Implementar Command/Handler no MediatR com FluentValidation.
- [ ] **[.NET API]** Criar scripts SQL e executar no banco de dados (Dapper).
- [ ] **[.NET API]** Configurar envio de evento assíncrono via MassTransit (Outbox Pattern).
- [ ] **[DevOps/QA]** Criar testes de integração com Testcontainers e atualizar Dockerfile.

---

### 📎 Artefatos Anexados
- [ ] Protótipo/Wireframe (Figma)
- [ ] Especificação de Contrato de API (OpenAPI/Swagger ou payload JSON)
- [ ] Schema de Eventos (Message Broker)
- [ ] Diagrama técnico / fluxo de dados (se necessário)
- [ ] Scripts de banco de dados / Scripts SQL (Dapper)
```

---

## 📦 DELIVERABLES DO REFINAMENTO

Ao concluir o ciclo de refinamento, os seguintes artefatos devem estar anexados à tarefa:

### 🔵 Geral (toda história)
1. **História Detalhada** — escopo focado em entrega de valor único, validado com o PO.
2. **Critérios de Aceite (BDD)** — cenários *Given-When-Then* cobrindo fluxo principal e exceções.
3. **Diagramas Técnicos** — fluxo de sequência ou arquitetura (Mermaid) quando o fluxo envolver múltiplos sistemas.
4. **Lista de Subtarefas** — quebra do trabalho técnico para acompanhamento no board (Azure DevOps).
5. **Estimativa de Complexidade** — Story Points refletindo o esforço total de engenharia.

### 🟢 Frontend — Micro Frontend (ReactJS)
6. **Especificação de Componentes** — inventário dos componentes novos ou modificados com nome, responsabilidade, props de entrada/saída e estados gerenciados.
7. **Mapeamento de Estados da UI** — descrição explícita dos 4 estados de cada tela/componente: Loading, Sucesso, Erro e Empty State (pode ser anotação no Figma).
8. **Contrato de Integração MFE** — definição do que o remote expõe via Module Federation: nome do módulo, props esperadas e eventos emitidos para o Shell.
9. **Dependências Compartilhadas** — lista das libs configuradas como `singleton` no `webpack.config.js` do remote (React, React Query etc.).
10. **Fluxo de Navegação** — diagrama (Mermaid) dos estados de navegação: origem, destino após sucesso, erro e cancelamento.
11. **Estratégia de Cache (React Query)** — definição de `queryKey`, `staleTime`, `cacheTime` e política de atualização (optimistic update ou invalidação pós-mutação).

### 🟠 Backend — Microserviços (.NET 8/9)
12. **Especificação de Contratos de API** — payloads JSON de Request/Response com exemplos de sucesso e erro (RFC 7807).
13. **Schemas de Eventos** — estrutura dos eventos de integração publicados no Message Broker (exchange, routing key e payload).
14. **Scripts de Banco de Dados** — scripts SQL validados para uso com Dapper (DDL, índices e constraints).
