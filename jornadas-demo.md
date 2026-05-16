# PGD Libre — Jornadas da Demo

> **Propósito:** Este documento descreve, passo a passo, as jornadas habilitadas na instância de demonstração do PGD Libre. Serve de base para tutoriais interativos, guias de experimentação, roteiros de apresentação e treinamento.

**URL da demo:** `http://localhost:5173` (local) ou endereço da instância Cloud Run.

**Login:** Acesse `/auth/dev-login` com os e-mails abaixo, ou via Google OAuth se configurado.

---

## Como fazer login na demo

Para cada papel, use o endpoint de dev-login:

```
POST http://localhost:8000/auth/dev-login?email=<EMAIL>&name=<NOME>&role=<PAPEL>
```

| Quem | Email | Role |
|------|-------|------|
| Ana Silva | servidor1@pgd-demo.gov.br | servidor |
| João Santos | servidor2@pgd-demo.gov.br | servidor |
| Carla Mendes | servidor3@pgd-demo.gov.br | servidor |
| Lucas Ramos | servidor4@pgd-demo.gov.br | servidor |
| Carlos Souza | chefe1@pgd-demo.gov.br | chefe_imediato |
| Beatriz Lima | chefe2@pgd-demo.gov.br | chefe_imediato |
| Maria Fernanda | gestor@pgd-demo.gov.br | gestor_unidade |
| Roberto Admin | admin@pgd-demo.gov.br | admin |

> Após o POST, o cookie `access_token` é definido e o browser redireciona para o dashboard.

---

## Contexto da organização fictícia

```
MGI — Ministério da Gestão e da Inovação
  └── SEGES — Secretaria de Gestão e Inovação
        ├── CGPGD — Coord-Geral de Gestão do PGD  (chefe: Carlos Souza)
        │     ├── Ana Silva      — Teletrabalho Parcial
        │     ├── João Santos    — Teletrabalho Integral
        │     ├── Carla Mendes   — Presencial
        │     └── Lucas Ramos    — Teletrabalho Parcial (sem plano de trabalho)
        └── CGTI — Coord-Geral de TI               (chefe: Beatriz Lima)
              └── Pedro Alves    — Teletrabalho Parcial
```

---

## Jornada 1 — Servidor: Ver meu plano e registrar execução

**Persona:** Ana Silva (`servidor1@pgd-demo.gov.br`)

**Pré-condição:** Ana tem um Plano de Trabalho ativo (em execução) com 3 períodos avaliativos.

### Passos

1. **Login** → Dashboard (`/`)
   - Vê o card "Plano de Trabalho ativo" com a UrgencyPill mostrando dias restantes
   - Vê a última avaliação recebida (nota 4 — inadequado, com recurso em aberto)
   - Vê notificação de avaliação realizada

2. **Navegar para Meu Plano** → `/meu-plano`
   - Vê o PlanoTrabalho 2025 da CGPGD
   - Vê as 2 contribuições: 70% desenvolvimento + 30% suporte
   - Vê o histórico de 3 períodos avaliativos

3. **Clicar em "Registrar execução"** → `/meu-plano/registrar`
   - Preenche o período atual (aberto, sem registro)
   - Descreve o que fez no mês
   - (Opcional) Adiciona ocorrências
   - Confirma e envia

4. **Ver avaliação contestada** → `/meu-plano/avaliacao/ARE-ANA-002`
   - Vê a avaliação nota 4 do período anterior
   - Vê o recurso que ela já submeteu (3 dias atrás)
   - Aguarda resposta do chefe (prazo: 7 dias)

**Pós-condição:** Registro do período atual enviado; recurso do período anterior aguardando resposta.

---

## Jornada 2 — Servidor: Contestar avaliação (recurso)

**Persona:** Ana Silva — mas usando a ARE-ANA-002 (nota 4, recurso já aberto na demo)

> Na demo, o recurso já foi submetido. Para demonstrar o fluxo completo de contestação, use um usuário secundário (João — nota do período anterior ainda sem recurso se quiser simular).

**Pré-condição:** Ana recebeu nota 4 em um período avaliativo. Está dentro da janela de 10 dias.

### Passos

1. **Meu Plano** → clicar no período ARE-ANA-002
2. Vê a avaliação nota 4 com justificativa da chefia
3. Clica em **"Contestar avaliação"**
4. Preenche o texto do recurso explicando a situação
5. Confirma envio → notificação gerada para o chefe

---

## Jornada 3 — Chefe Imediato: Avaliar registro pendente

**Persona:** Carlos Souza (`chefe1@pgd-demo.gov.br`)

**Pré-condição:** João Santos registrou a execução do mês anterior. Aguarda avaliação.

### Passos

1. **Login** → Dashboard (`/`)
   - Vê KPIs: 4 servidores na equipe, 1 avaliação pendente, 3 planos em execução
   - Vê alerta de recurso pendente (Ana Silva)

2. **Ir para Equipe** → `/equipe`
   - Vê tabela com Ana, João, Carla e Lucas
   - Lucas aparece sem plano de trabalho (badge "Sem PT")
   - João aparece com indicador de registro pendente

3. **Clicar no PlanoTrabalho de João** → `/equipe/planos-trabalho/PT-2025-JOAO-001`
   - Vê contribuições de João (60% relatórios, 20% gestão, 20% CGTI)
   - Vê ARE-JOAO-001 com status "Registrado — aguardando avaliação"

4. **Avaliar ARE-JOAO-001**
   - Clica em "Avaliar"
   - Seleciona nota (1–5) com o NotaSelector
   - Adiciona justificativa se necessário (obrigatória para notas 1, 4, 5)
   - Confirma → notificação enviada para João

**Pós-condição:** João recebe notificação de avaliação realizada.

---

## Jornada 4 — Chefe Imediato: Responder recurso

**Persona:** Carlos Souza

**Pré-condição:** Ana contestou a nota 4. Notificação de recurso aberto no dashboard do chefe.

### Passos

1. **Dashboard** → ver notificação de recurso aberto
2. **Abrir ARE-ANA-002** via link na notificação ou via `/equipe`
3. Ler o texto do recurso de Ana
4. Decidir: **Acatar** ou **Não Acatar**
   - Se acatar: nota é revisada para cima
   - Se não acatar: adicionar justificativa detalhada
5. Confirmar → recurso encerrado, Ana notificada

---

## Jornada 5 — Chefe Imediato: Criar Plano de Trabalho

**Persona:** Carlos Souza

**Pré-condição:** Lucas Ramos está na equipe mas sem Plano de Trabalho.

### Passos

1. **Equipe** → clicar em Lucas Ramos
2. Clicar em **"Criar Plano de Trabalho"** → `/equipe/planos-trabalho/novo`
3. **Step 1 — Participante & período:** selecionar Lucas, definir datas (início, fim)
4. **Step 2 — Carga horária:** informar horas disponíveis no período
5. **Step 3 — Critérios de avaliação:** descrever os critérios que serão usados
6. **Step 4 — Contribuições:** adicionar atividades e percentuais (devem somar 100%)
7. **Step 5 — Revisão e envio:** confirmar e enviar para aprovação
8. Lucas recebe notificação de plano aprovado

---

## Jornada 6 — Chefe Imediato: Emitir convocação

**Persona:** Carlos Souza

**Pré-condição:** João Santos está em teletrabalho integral. Há reunião presencial necessária.

**Estado na demo:** A convocação já foi emitida (status pendente). João ainda não respondeu.

### Passos (fluxo completo, para apresentação)

1. **Equipe** → clicar em João Santos
2. Clicar em **"Convocar"** ou acessar menu de convocações
3. Preencher: data de comparecimento, horário, local, período presencial, motivo
4. Sistema verifica prazo mínimo de antecedência (5 dias) — respeitado ✓
5. Confirmar → João recebe notificação pelo canal configurado (Teams)

**Estado atual na demo:** João vê a convocação pendente no seu dashboard.

---

## Jornada 7 — Gestor: Aprovar PlanoEntregas

**Persona:** Maria Fernanda (`gestor@pgd-demo.gov.br`)

**Pré-condição:** CGTI submeteu um PlanoEntregas aguardando aprovação do nivel_superior.

### Passos

1. **Login** → Dashboard (`/`)
   - Vê KPIs consolidados: 5 servidores, 2 planos de entrega, status de sincronização

2. **Painel de conformidade** → `/conformidade`
   - Vê PlanoEntregas da CGTI com status "Aguardando aprovação"
   - Vê erros de sincronização para Pedro Alves (CGTI)

3. **Clicar no PlanoEntregas da CGTI**
   - Vê as 2 entregas planejadas: Sistema de Integração + Dashboard de Monitoramento
   - Vê datas e metas de cada entrega

4. **Aprovar PlanoEntregas** → PE_CGTI passa para status "Em execução"
5. Beatriz Lima (chefe CGTI) recebe notificação de PE aprovado

---

## Jornada 8 — Gestor: Ver relatório de servidores sem plano

**Persona:** Maria Fernanda

### Passos

1. **Relatórios** → `/relatorios`
2. Clicar em **"Servidores sem Plano de Trabalho"**
3. Vê Lucas Ramos (CGPGD) listado sem PT
4. Pode acionar o chefe imediato (Carlos Souza) para criar o PT

---

## Jornada 9 — Admin: Ver conformidade e sync

**Persona:** Roberto Admin (`admin@pgd-demo.gov.br`)

### Passos

1. **Login** → Dashboard administrativo
2. **Painel de conformidade** → `/conformidade`
   - Vê tabela de envios: 5 sucessos, 3 erros (Pedro/CGTI)
   - Erros: Timeout na API PGD Central (2 tentativas)
3. **Clicar no erro de Pedro** → `/conformidade/erro/<id>`
   - Vê detalhes do erro: HTTP 500, mensagem de timeout
   - Pode acionar reenvio manual
4. **Administração** → `/admin/participantes`
   - Lista completa: Ana, João, Carla, Lucas, Pedro
   - Pode editar dados cadastrais
5. **Institucional** → `/admin/institucional`
   - Vê configuração do MGI/SEGES/CGPGD/CGTI
   - Vê ato de autorização (Portaria MGI nº 001/2023)

---

## Resumo dos estados de dados habilitados

| Entidade | Quantidade | Estados |
|---|---|---|
| Usuários | 9 | admin, gestor, 2 chefes, 5 servidores |
| Participantes | 5 | 4 em CGPGD, 1 em CGTI |
| TCRs | 5 | Todos ATIVO |
| PlanoEntregas | 2 | 1 em execução, 1 aguardando aprovação |
| Entregas | 5 | 3 para CGPGD, 2 para CGTI |
| PlanoTrabalho | 4 | 3 em execução, 1 aprovado (Pedro) |
| Contribuições | 9 | Tipos 1, 2 e 3 (cross-unit) |
| AREs | 5 | Encerradas, registrada, com recurso, aberta |
| Convocações | 1 | Pendente (João) |
| Afastamentos | 1 | Férias encerradas (Carla) |
| TermoGuardaEquipamento | 1 | João (TT integral) |
| RegistroEnvioAPI | 8 | 5 ok, 3 erro |
| Notificações | 5 | 4 enviadas + 1 de convocação |

---

## Datas relativas (sempre atualizadas pelo seed)

O script `seed_demo.py` calcula todas as datas em relação ao dia de execução (`date.today()`), garantindo que os prazos nunca expirem:

| Período | Referência |
|---|---|
| Início do plano | hoje − 180 dias |
| Fim do plano | hoje + 185 dias |
| Período avaliativo −2 | hoje−60 a hoje−31 |
| Período avaliativo −1 | hoje−30 a hoje−1 |
| Período atual | hoje a hoje+30 |
| Convocação de João | hoje+5 dias |
| Prazo recurso de Ana | 7 dias restantes |
