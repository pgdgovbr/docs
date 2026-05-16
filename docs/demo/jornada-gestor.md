# Jornada do Gestor e Admin na Demo

---

## Gestor — Maria Fernanda (`gestor@pgd-demo.gov.br`)

[Faça login como Maria Fernanda →](acesso.md)

---

## Jornada 7 — Aprovar Plano de Entregas

**Situação:** A CGTI submeteu um Plano de Entregas que aguarda aprovação do nível superior (SEGES).

### No dashboard (`/`)

- KPIs consolidados: 5 servidores, 2 planos de entrega, status de sincronização

### No painel de conformidade (`/conformidade`)

1. Clique em **Conformidade** no menu
2. Veja o Plano de Entregas da CGTI com status **"Aguardando aprovação"**
3. Veja os erros de sincronização de Pedro Alves

### Aprovando o Plano de Entregas

1. Clique no Plano de Entregas da CGTI
2. Veja as 2 entregas planejadas:
   - Sistema de Integração com a API Central
   - Dashboard de Monitoramento de Conformidade
3. Veja datas e metas de cada entrega
4. Clique em **"Aprovar"** → o PE passa para status "Em execução"

**O que acontece:** Beatriz Lima (chefia da CGTI) recebe notificação de PE aprovado.

---

## Jornada 8 — Ver servidores sem Plano de Trabalho

**Situação:** Lucas Ramos (CGPGD) ainda não tem Plano de Trabalho.

1. Acesse **Relatórios** → `/relatorios`
2. Clique em **"Servidores sem Plano de Trabalho"**
3. Veja Lucas listado (CGPGD, modalidade: Teletrabalho Parcial)
4. Use o botão para acionar a chefia (Carlos Souza) via notificação

---

## Admin — Roberto Admin (`admin@pgd-demo.gov.br`)

[Faça login como Roberto →](acesso.md)

---

## Jornada 9 — Ver conformidade e erros de sincronização

**Situação:** Pedro Alves (CGTI) tem 3 erros de sincronização com a API PGD Central.

### No painel de conformidade (`/conformidade`)

1. Veja a tabela de envios: **5 sucessos** + **3 erros** (Pedro/CGTI)
2. Erros: Timeout na API PGD Central (2 tentativas)

### Detalhando um erro

1. Clique no erro de Pedro → `/conformidade/erro/<id>`
2. Veja detalhes: HTTP 500, mensagem de timeout, timestamp
3. Opção de **reenvio manual**

### Administração de participantes (`/admin/participantes`)

- Lista completa: Ana, João, Carla, Lucas, Pedro
- Editar dados cadastrais de qualquer participante

### Configuração institucional (`/admin/institucional`)

- Veja a hierarquia: MGI → SEGES → CGPGD / CGTI
- Veja o ato de autorização (Portaria MGI nº 001/2023)

---

## O que explorar também

- **[Aprovar Planos de Entregas →](../gestor/aprovar-planos.md)**
- **[Painel de Conformidade →](../gestor/conformidade.md)**
