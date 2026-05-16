# Papéis e responsabilidades

O PGD Libre tem quatro papéis de usuário. Cada um vê uma interface diferente e tem permissões específicas.

## Servidor

O servidor é o participante do PGD. Ele trabalha sob um Plano de Trabalho aprovado pela chefia.

**O que pode fazer:**

- **Criar seu próprio Plano de Trabalho** (do zero ou clonando um plano anterior)
- **Assinar o plano** após revisão e enviar para a chefia aprovar
- Ver seu Plano de Trabalho ativo (contribuições, datas, modalidade)
- Registrar a execução de cada período avaliativo
- Ver as avaliações recebidas com nota e justificativa
- Contestar uma avaliação (abrir recurso) dentro do prazo legal (10 dias)
- Ver suas notificações e prazos

**Quando recebe notificações:**

- Quando uma avaliação é publicada
- Quando a chefia responde a um recurso
- Quando um prazo de registro está se aproximando

---

## Chefia Imediata

A chefia imediata é responsável por sua equipe direta. Ela cria e gerencia os planos de trabalho e avalia os registros.

**O que pode fazer:**

- Ver todos os servidores da equipe com KPIs resumidos
- **Revisar e assinar** os Planos de Trabalho propostos pelos servidores; ajustar quando necessário; criar PT diretamente apenas em casos de exceção (servidor ausente, recém-chegado)
- Avaliar os registros de execução enviados pelos servidores
- Responder aos recursos (contestações) abertos pelos servidores
- Emitir convocações de comparecimento presencial para servidores em teletrabalho integral
- Ver o Plano de Entregas da unidade

**Quando recebe notificações:**

- Quando um servidor envia um registro para avaliação
- Quando um servidor abre um recurso
- Quando um Plano de Entregas é aprovado pelo gestor

---

## Gestor de Unidade

O gestor é responsável pelo nível superior da unidade. Ele aprova os planos de entregas e monitora a conformidade.

**O que pode fazer:**

- Ver o dashboard consolidado com KPIs de todas as equipes
- Aprovar Planos de Entregas submetidos pelas chefias
- Ver o painel de conformidade com a API PGD Central
- Gerar relatórios (ex.: servidores sem Plano de Trabalho)

---

## Admin

O admin gerencia a configuração do sistema e monitora o funcionamento técnico.

**O que pode fazer:**

- Gerenciar participantes (cadastrar, editar dados)
- Ver e corrigir erros de sincronização com a API PGD Central
- Configurar dados institucionais (unidades, atos de autorização)

---

## Hierarquia de unidades

```
UnidadeAutorizadora (ex.: MGI)
  └── UnidadeInstituidora (ex.: SEGES)
        ├── UnidadeExecução A (ex.: CGPGD) ← chefia: Carlos
        └── UnidadeExecução B (ex.: CGTI)  ← chefia: Beatriz
```

!!! info "Gestor vs. Chefia"
    O **gestor** atua no nível da UnidadeInstituidora (SEGES) e aprova planos de unidades subordinadas. A **chefia** atua no nível da UnidadeExecução e gerencia servidores individualmente.
