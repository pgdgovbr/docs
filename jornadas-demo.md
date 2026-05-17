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
| Pedro Alves | servidor5@pgd-demo.gov.br | servidor |
| Felipe Costa | servidor6@pgd-demo.gov.br | servidor |
| Marta Silva | servidor7@pgd-demo.gov.br | servidor |
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
        │     ├── Ana Silva      — Teletrabalho Parcial (plano em execução; plano anterior concluído)
        │     ├── João Santos    — Teletrabalho Integral
        │     ├── Carla Mendes   — Presencial
        │     ├── Lucas Ramos    — Teletrabalho Parcial (plano em rascunho)
        │     ├── Felipe Costa   — Teletrabalho Parcial (chefia ajustou, aguarda sua assinatura)
        │     └── Marta Silva    — Teletrabalho Parcial (sem plano)
        └── CGTI — Coord-Geral de TI               (chefe: Beatriz Lima)
              └── Pedro Alves    — Teletrabalho Parcial (plano aguardando assinatura da chefia)
```

---

## Jornada 0 — Servidor: Criar meu Plano de Trabalho

**Persona:** Marta Silva (`servidor7@pgd-demo.gov.br`)

**Pré-condição:** Marta entrou no PGD e não tem plano vigente.

### Passos

1. **Login** → Dashboard (`/`)
2. **Meu Plano** (`/meu-plano`) → estado vazio com dois CTAs (Criar do zero, Clonar)
3. **Criar do zero** → wizard `/meu-plano/criar`:
   - Step 1: período + vínculo com PE
   - Step 2: carga horária
   - Step 3: critérios de avaliação
   - Step 4: contribuições (somando 100%)
   - Step 5: revisão + **Assinar e enviar para chefia**
4. Marta marca os 3 checks da assinatura e envia

**Pós-condição:** plano em **"Aguardando assinatura da chefia"**; Carlos recebe notificação.

---

## Jornada 1a — Servidor: Clonar plano anterior

**Persona:** Ana Silva (`servidor1@pgd-demo.gov.br`)

**Pré-condição:** Ana tem PT em execução + PT anterior em CONCLUIDO.

### Passos

1. **Meu Plano** → clica em **"Clonar plano anterior"**
2. Modal abre listando PTs anteriores
3. Seleciona o PT-2024-ANA-002, define novas datas
4. Clica em **"Clonar e editar"** → vai para `/meu-plano/<novo_id>/editar`
5. Novo PT em rascunho com tudo copiado; ajusta o que precisa
6. Segue o fluxo padrão (assinar e enviar)

---

## Jornada 1b — Servidor: Editar meu rascunho

**Persona:** Lucas Ramos (`servidor4@pgd-demo.gov.br`)

**Pré-condição:** Lucas tem PT em RASCUNHO_PARTICIPANTE com histórico de edições.

### Passos

1. **Meu Plano** → vê seu rascunho com botão "Editar"
2. Vai para `/meu-plano/<id>/editar`
3. Vê OwnershipBanner, auto-save e timeline de edições
4. Faz ajustes, salva automaticamente
5. Quando pronto, clica em **"Assinar e enviar para chefia"**

---

## Jornada 1c — Servidor: Revisar ajuste da chefia e assinar

**Persona:** Felipe Costa (`servidor6@pgd-demo.gov.br`)

**Pré-condição:** Felipe tem PT em AGUARDANDO_ASSINATURA_PARTICIPANTE (chefia ajustou + assinou).

### Passos

1. **Login** → Dashboard com card "Aguardando sua ação" destacado
2. Acessa `/meu-plano/<id>/revisar`
3. Vê:
   - Banner "A chefia ajustou X campos"
   - Timeline de edições (criação → assinatura → ajuste chefia → assinatura chefia)
   - Card de assinatura com 3 checks
4. Marca os 3 checks → clica em **"Assinar e ativar plano"**

**Pós-condição:** PT em **"Em execução"**; pode começar a registrar.

**Variantes:**
- **Devolver para ajustes** → PT volta para "Rascunho da chefia" (zera assinatura dela)
- **Cancelar plano** → PT vai para "Cancelado"

---

## Jornada 2 — Servidor: Registrar execução

**Persona:** Ana Silva — PT em execução

**Pré-condição:** Período avaliativo atual aberto.

### Passos

1. **Meu Plano** → clica em **"Registrar execução"** → `/meu-plano/registrar`
2. Preenche descrição do que foi feito no mês
3. (Opcional) Adiciona ocorrências
4. **Enviar registro**

---

## Jornada 3 — Servidor: Contestar avaliação (recurso)

**Persona:** Ana Silva — ARE-ANA-002 (recurso já aberto na demo)

### Passos (fluxo completo)

1. **Meu Plano** → clica no período avaliativo
2. Vê a nota e justificativa
3. Dentro dos 10 dias, clica em **"Contestar avaliação"**
4. Escreve o texto do recurso
5. **Enviar recurso** → chefia tem 7 dias para responder

---

## Jornada 4a — Chefia: Revisar e assinar PT do servidor

**Persona:** Beatriz Lima (`chefe2@pgd-demo.gov.br`)

**Pré-condição:** Pedro Alves enviou PT (status AGUARDANDO_ASSINATURA_CHEFIA).

### Passos

1. **Login** → Dashboard com card "X PTs aguardando sua assinatura"
2. **Equipe** → banner consolidado de pendências + botão "Ver primeiro pendente"
3. Clica em **"Revisar e assinar"** → `/equipe/planos-trabalho/<id>/revisar`
4. Vê:
   - Plano em modo leitura
   - Timeline de edições do servidor
   - Card de assinatura com 3 checks
5. Marca os 3 checks → clica em **"Assinar e ativar plano"**

**Pós-condição:** PT em **"Em execução"**; Pedro recebe notificação.

---

## Jornada 4b — Chefia: Devolver para ajustes

**Persona:** Beatriz Lima (mesma situação)

### Passos

1. Em `/equipe/planos-trabalho/<id>/revisar`, clica em **"Devolver para ajustes"**
2. Adiciona justificativa explicando o que precisa mudar
3. Confirma → PT volta para **"Rascunho do servidor"**

---

## Jornada 4c — Chefia: Ajustar diretamente

**Persona:** Beatriz Lima (mesma situação)

### Passos

1. Clica em **"Ajustar"** → `/equipe/planos-trabalho/<id>/editar`
2. Faz os ajustes
3. Clica em **"Assinar e enviar para servidor"**
4. PT vai para **"Aguardando assinatura do servidor"**; Pedro precisa reassinar

---

## Jornada 5 — Chefia: Avaliar registro pendente

**Persona:** Carlos Souza (`chefe1@pgd-demo.gov.br`)

**Pré-condição:** João Santos registrou a execução do mês anterior.

### Passos

1. **Equipe** → clicar em João
2. Acessar o PT dele → clicar no período ARE-JOAO-001
3. Clicar em **"Avaliar"**
4. Selecionar nota (1–5); adicionar justificativa se obrigatória
5. Confirmar → João recebe notificação

---

## Jornada 6 — Chefia: Responder recurso

**Persona:** Carlos Souza

**Pré-condição:** Ana contestou a nota 4.

### Passos

1. Dashboard → notificação de recurso aberto
2. Abrir ARE-ANA-002 via link
3. Ler o recurso
4. **Acatar** ou **Não acatar** (com justificativa)
5. Confirmar → Ana é notificada

---

## Jornada 7 — Chefia: Criar PT (caso excepcional)

**Persona:** Carlos Souza

!!! warning "Caminho de exceção"
    O fluxo padrão é o próprio servidor criar.

**Pré-condição:** servidor recém-chegado ou ausente.

### Passos

1. **Equipe** → clicar no servidor → **"Criar Plano de Trabalho"**
2. **Step 0 — Confirmar exceção** — selecionar motivo
3. **Step 1 — Período**
4. **Step 2 — Carga horária**
5. **Step 3 — Critérios de avaliação**
6. **Step 4 — Contribuições**
7. **Step 5 — Revisão e envio** → **Assinar e enviar para servidor**

**Pós-condição:** PT em **"Aguardando assinatura do servidor"**; só entra em execução após servidor assinar.

---

## Jornada 8 — Chefia: Emitir convocação

**Persona:** Carlos Souza

**Pré-condição:** João em teletrabalho integral; reunião presencial necessária.

### Passos

1. **Equipe** → clicar em João → **"Convocar"**
2. Preencher data, horário, local, motivo
3. Sistema valida prazo mínimo de 5 dias
4. Confirmar → João recebe notificação

---

## Jornada 9 — Gestor: Aprovar PlanoEntregas

**Persona:** Maria Fernanda (`gestor@pgd-demo.gov.br`)

**Pré-condição:** CGTI submeteu PE aguardando aprovação.

### Passos

1. **Painel de conformidade** (`/conformidade`)
2. Ver PE_CGTI com status "Aguardando aprovação"
3. Clicar nele → revisar entregas planejadas
4. Aprovar → PE passa para "Em execução"; Beatriz é notificada

---

## Jornada 10 — Gestor: Ver relatório de servidores sem plano

**Persona:** Maria Fernanda

### Passos

1. **Relatórios** (`/relatorios`)
2. Clicar em **"Servidores sem Plano de Trabalho"**
3. Ver Marta Silva listada
4. No novo workflow, o relatório serve para identificar quem ainda não pactuou (não mais "quem aguarda a chefia criar")

---

## Jornada 11 — Admin: Ver conformidade e sync

**Persona:** Roberto Admin (`admin@pgd-demo.gov.br`)

### Passos

1. **Painel de conformidade** (`/conformidade`) — ver tabela de envios e erros
2. **Administração** (`/admin/participantes`) — lista completa
3. **Institucional** (`/admin/institucional`) — ver configuração e ato de autorização

---

## Resumo dos estados de dados habilitados

| Entidade | Quantidade | Estados |
|---|---|---|
| Usuários | 11 | admin, gestor, 2 chefes, 7 servidores |
| Participantes | 7 | 6 em CGPGD, 1 em CGTI |
| TCRs | 7 | Todos ATIVO |
| PlanoEntregas | 2 | 1 em execução, 1 aguardando aprovação |
| PlanoTrabalho | 7 | 3 em execução, 1 concluído (Ana anterior), 1 aguardando chefia (Pedro), 1 aguardando servidor (Felipe), 1 rascunho (Lucas) |
| Contribuições | 11 | Tipos 1, 2 e 3 (cross-unit) |
| AREs | 5 | Encerradas, registrada, com recurso, aberta |
| Convocações | 1 | Pendente (João) |
| Afastamentos | 1 | Férias encerradas (Carla) |
| Notificações | 6 | inclui notificação para Felipe (ajuste da chefia) |
| AuditLog | 10+ | Timelines sintéticas para Lucas, Felipe e Pedro |

---

## Datas relativas (sempre atualizadas pelo seed)

O script `seed_demo.py` calcula todas as datas em relação ao dia de execução (`date.today()`), garantindo que os prazos nunca expirem:

| Período | Referência |
|---|---|
| Início do plano | hoje − 180 dias |
| Fim do plano | hoje + 185 dias |
| Plano anterior da Ana | hoje−365 a hoje−185 |
| Período avaliativo −2 | hoje−60 a hoje−31 |
| Período avaliativo −1 | hoje−30 a hoje−1 |
| Período atual | hoje a hoje+30 |
| Convocação de João | hoje+5 dias |
| Prazo recurso de Ana | 7 dias restantes |
