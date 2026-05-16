# Visão geral — Servidor

Como servidor no PGD Libre, você executa atividades conforme seu **Plano de Trabalho** e registra mensalmente o que foi feito.

## O que você faz no sistema

```mermaid
graph LR
    A[Recebe o<br/>Plano de Trabalho] --> B[Executa as<br/>atividades do mês]
    B --> C[Registra a execução<br/>no sistema]
    C --> D[Aguarda avaliação<br/>da chefia]
    D --> E{Concorda com<br/>a nota?}
    E -->|Sim| F[Período encerrado]
    E -->|Não| G[Contesta<br/>recurso]
    G --> H[Aguarda resposta<br/>da chefia]
    H --> F
```

## Sua tela principal

![Dashboard do servidor no PGD Libre](../assets/screenshots/servidor/dashboard.png)

Ao fazer login, você vê o **Dashboard** com:

- **Plano de Trabalho ativo** — status, modalidade e dias restantes para o próximo registro
- **Última avaliação** — nota e data da avaliação mais recente
- **Notificações recentes** — prazos, avaliações publicadas, respostas a recursos

Acesse o sino no canto superior para ver todas as notificações:

![Lista de notificações do servidor](../assets/screenshots/servidor/notificacoes.png)

## Seus prazos

Fique atento a dois prazos principais:

| Prazo | Quando | O que acontece se perder |
|---|---|---|
| **Registro de execução** | Até o último dia do período avaliativo | Período fica sem registro; pode impactar a avaliação |
| **Contestação de avaliação** | 10 dias após a publicação da nota | Perde o direito ao recurso naquele período |

!!! warning "Pílula de urgência"
    Quando faltam 7 dias ou menos para um prazo, o sistema exibe uma pílula colorida no dashboard. **Vermelho** = vencido ou hoje. **Amarelo** = menos de 7 dias. **Verde** = dentro do prazo.

## Guias disponíveis

- [Meu Plano de Trabalho](meu-plano.md) — como entender seu plano, contribuições e status
- [Registrar Execução](registrar-execucao.md) — passo a passo para enviar o registro mensal
- [Minhas Avaliações](avaliacoes.md) — o que cada nota significa e como ver o histórico
- [Contestar uma Avaliação](contestar-avaliacao.md) — como abrir e acompanhar um recurso
- [Referência rápida](referencia-rapida.md) — atalhos e respostas rápidas para o dia a dia
