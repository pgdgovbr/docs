# Jornada da Chefia na Demo

Explore as funcionalidades da chefia imediata usando a persona **Carlos Souza** (`chefe1@pgd-demo.gov.br`), chefia da CGPGD.

[Faça login como Carlos →](acesso.md)

---

## Jornada 3 — Avaliar registro pendente

**Situação:** João Santos registrou a execução do mês anterior. O registro está aguardando avaliação de Carlos.

### No dashboard (`/`)

- KPIs: 4 servidores na equipe, **1 avaliação pendente**, 3 planos em execução
- Alerta de recurso pendente (Ana Silva)

### Acessando a equipe (`/equipe`)

1. Clique em **Equipe** no menu
2. Veja a tabela: Ana, João, Carla e Lucas
3. **Lucas** aparece com badge "Sem PT" (sem Plano de Trabalho)
4. **João** aparece com indicador de registro pendente de avaliação

### Avaliando o registro de João

1. Clique no nome de João → veja o Plano de Trabalho dele
2. Veja as contribuições: 60% relatórios, 20% gestão, 20% CGTI
3. Clique no período ARE-JOAO-001 com status "Registrado — aguardando avaliação"
4. Clique em **"Avaliar"**
5. Selecione a nota (1–5) usando o seletor visual
6. Adicione justificativa (obrigatória para notas 1, 4 e 5)
7. Confirme → João recebe notificação de avaliação realizada

---

## Jornada 4 — Responder um recurso

**Situação:** Ana contestou a nota 4. Carlos tem uma notificação de recurso aberto.

1. No dashboard, veja a notificação de recurso de Ana
2. Clique no link → abre a ARE-ANA-002
3. Leia o texto do recurso de Ana
4. Escolha: **"Acatar"** (revisa a nota) ou **"Não acatar"** (mantém com justificativa)
5. Se não acatar, adicione uma justificativa detalhada
6. Confirme → Ana recebe notificação da resposta

---

## Jornada 5 — Criar Plano de Trabalho para Lucas

**Situação:** Lucas Ramos está na equipe sem Plano de Trabalho vigente.

1. Na tela de equipe, clique em **Lucas Ramos**
2. Veja o badge "Sem Plano de Trabalho"
3. Clique em **"Criar Plano de Trabalho"** → `/equipe/planos-trabalho/novo`

### Wizard de criação (5 passos)

| Passo | O que fazer |
|---|---|
| 1. Participante & período | Selecionar Lucas; definir data de início e fim |
| 2. Carga horária | Informar total de horas disponíveis no período |
| 3. Critérios de avaliação | Descrever os critérios que serão usados |
| 4. Contribuições | Adicionar atividades e percentuais (soma = 100%) |
| 5. Revisão e envio | Conferir tudo e enviar |

**O que acontece:** Lucas recebe notificação e o plano fica com status "Aprovado".

---

## Jornada 6 — Emitir convocação

**Situação:** João está em teletrabalho integral. Carlos precisa convocá-lo para uma reunião presencial.

!!! info "Na demo, já existe uma convocação"
    A convocação de João já foi emitida (status pendente). Esta jornada mostra o fluxo de criação.

1. Na tela de equipe, clique em **João Santos**
2. Clique em **"Convocar"** (ou acesse o menu de convocações)
3. Preencha: data, horário, local, período presencial, motivo
4. O sistema verifica se o prazo mínimo de 5 dias é respeitado
5. Confirme → João recebe notificação

---

## O que explorar também

- **[Guia completo de avaliação →](../chefia/avaliar-registros.md)**
- **[Como responder um recurso →](../chefia/responder-recurso.md)**
- **[Como criar um Plano de Trabalho →](../chefia/criar-plano.md)**
