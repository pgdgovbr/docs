# Visão geral — Servidor

Como servidor no PGD Libre, **você é o autor do seu Plano de Trabalho** — propõe o que vai fazer, e a chefia revisa e assina junto com você. Depois, executa as atividades e registra mensalmente.

## O que você faz no sistema

```mermaid
graph LR
    A[Você cria seu<br/>Plano de Trabalho] --> B[Você assina e envia<br/>para a chefia]
    B --> C[Chefia revisa<br/>e assina]
    C --> D[Plano em execução]
    D --> E[Você executa<br/>e registra]
    E --> F[Chefia avalia]
    F --> G{Concorda?}
    G -->|Sim| H[Período encerrado]
    G -->|Não| I[Recurso]
    I --> H
```

## Sua tela principal

![Dashboard do servidor no PGD Libre](../assets/screenshots/servidor/dashboard.png)

Ao fazer login, você vê o **Dashboard** com:

- **Aguardando sua ação** — destaque para planos em rascunho ou aguardando sua assinatura
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

- [Criar meu Plano de Trabalho](criar-plano.md) — passo a passo do wizard, incluindo clonagem de plano anterior
- [Revisar plano ajustado pela chefia](revisar-plano.md) — o que fazer quando a chefia ajusta e devolve
- [Meu Plano de Trabalho](meu-plano.md) — como entender seu plano, contribuições e estados de pactuação
- [Registrar Execução](registrar-execucao.md) — passo a passo para enviar o registro mensal
- [Minhas Avaliações](avaliacoes.md) — o que cada nota significa e como ver o histórico
- [Contestar uma Avaliação](contestar-avaliacao.md) — como abrir e acompanhar um recurso
- [Referência rápida](referencia-rapida.md) — atalhos e respostas rápidas para o dia a dia
