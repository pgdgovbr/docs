# Revisar plano ajustado pela chefia

Quando a sua chefia **ajusta** o Plano de Trabalho que você enviou (em vez de só assinar), o plano volta para você revisar e assinar a nova versão. Esta página explica como funciona.

## Quando essa tela aparece

A tela de revisão aparece quando o plano está no status **"Aguardando sua assinatura"** (em código: `AGUARDANDO_ASSINATURA_PARTICIPANTE`). Isso acontece em dois cenários:

1. Você enviou um plano → a chefia ajustou alguns campos e assinou a versão dela → agora falta você reassinar.
2. A chefia criou o plano em modo exceção e assinou → falta você revisar e assinar para o plano entrar em execução.

## Como acessar

- **Pela notificação**: você recebe uma notificação ("A chefia ajustou e assinou seu Plano de Trabalho"). Clique no link.
- **Por Meu Plano**: acesse **Meu Plano** → o plano aparecerá com badge "Aguardando sua assinatura" e botão **"Revisar e assinar"**.

Ambos levam para `/meu-plano/<id>/revisar`.

## O que você vê na tela

![Tela de revisar plano com banner de mudanças, timeline e card de assinatura](../assets/screenshots/servidor/revisar-ajuste.png)

A tela tem três blocos principais:

### 1. Banner do que mudou

No topo, um banner destaca **o que a chefia ajustou**. Por exemplo: _"A chefia ajustou 2 campos: carga horária disponível e data de término."_

Use isso como guia: você não precisa ler o plano inteiro de novo, basta conferir os campos que mudaram.

### 2. Histórico de edições

Abaixo do banner, a **linha do tempo** mostra todas as edições com autor, data e ação:

| Quando | Quem | O que fez |
|---|---|---|
| 10 dias atrás | Você | Criou o plano |
| 9 dias atrás | Você | Assinou e enviou para chefia |
| 12 horas atrás | Chefia | Ajustou carga horária e data de término |
| 8 horas atrás | Chefia | Assinou e enviou para você |

### 3. Card de assinatura

À direita (ou no rodapé, dependendo do tamanho da tela), o **card de assinatura** com 3 checks e o botão "Assinar e ativar plano".

## Suas 3 ações

A partir desta tela, você tem três caminhos:

### Assinar e ativar o plano

1. Marque os 3 checks no card de assinatura:
   - Li e entendi o conteúdo do Plano de Trabalho.
   - Concordo com as contribuições, percentuais e critérios.
   - Estou ciente de que esta assinatura tem valor formal de pactuação.
2. Clique em **"Assinar e ativar plano"**.

**Resultado:** o plano vai para o status **"Em execução"**. Você já pode começar a registrar.

### Devolver para ajustes

Se você discorda das mudanças e quer reabrir a discussão:

1. Clique em **"Devolver para ajustes"**.
2. Adicione uma justificativa explicando o que precisa mudar.

**Resultado:** o plano volta para **"Rascunho da chefia"**. A assinatura dela é zerada — ela terá que ajustar de novo, assinar de novo, e devolver para você revisar.

!!! warning "A assinatura da chefia é zerada"
    Devolver para ajustes invalida a assinatura prévia da chefia. Ela só volta a valer quando ela reassinar a próxima versão. Use esta opção quando há uma discordância real — não como passo de leitura.

### Cancelar o plano

Em casos excepcionais (mudança de unidade, afastamento longo, etc.), você pode cancelar o plano:

1. Clique em **"Cancelar plano"**.
2. Adicione a justificativa do cancelamento.

**Resultado:** o plano vai para o status **"Cancelado"**. Você ficará sem plano vigente — terá que [criar um novo](criar-plano.md) quando for o caso.

## Depois de assinar

- O plano passa para **"Em execução"**.
- A chefia recebe notificação de que o plano foi pactuado.
- Você pode começar a registrar a execução do período atual.

→ [Como registrar execução](registrar-execucao.md)

## Veja também

- [Criar meu Plano de Trabalho](criar-plano.md)
- [Pactuação bilateral — diagrama completo de estados](../conceitos/pactuacao-bilateral.md)
- [Meu Plano de Trabalho — estados de pactuação](meu-plano.md)
