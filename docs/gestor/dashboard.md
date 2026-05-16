# Dashboard e KPIs

O dashboard do gestor exibe um panorama consolidado de todas as equipes sob sua unidade.

## Como acessar

Ao fazer login, você já cai no dashboard. Ou acesse `/` a qualquer momento.

## KPIs exibidos

| KPI | O que significa |
|---|---|
| **Total de participantes** | Servidores inscritos no PGD na sua unidade |
| **Planos de Trabalho ativos** | Servidores com plano "Em execução" |
| **Sem Plano de Trabalho** | Servidores participantes sem PT vigente (alerta) |
| **Avaliações pendentes** | Registros enviados ainda não avaliados pelas chefias |
| **Planos de Entregas** | Quantos PEs ativos e quantos aguardando aprovação |
| **Status de sync** | Envios ok vs. erros na API PGD Central (últimos 30 dias) |

## Alertas no dashboard

O dashboard destaca situações que precisam de ação:

- **Plano de Entregas aguardando aprovação** → [Aprovar →](aprovar-planos.md)
- **Servidores sem Plano de Trabalho** → acionar a chefia correspondente
- **Erros de sincronização** → [Ver painel de conformidade →](conformidade.md)

## Relatórios disponíveis

No menu **Relatórios** (`/relatorios`), você acessa:

- **Servidores sem Plano de Trabalho** — lista com nome, unidade e chefia responsável
- **Afastamentos** — servidores em férias, licença ou afastamento no período

## Dicas de leitura

!!! tip "Foco nos alertas"
    O dashboard prioriza automaticamente os itens que precisam de ação. Comece sempre pelos alertas antes de analisar os KPIs globais.

!!! info "Dados em tempo real"
    Os KPIs são calculados em tempo real. Recarregue a página para ver o estado mais atual.
