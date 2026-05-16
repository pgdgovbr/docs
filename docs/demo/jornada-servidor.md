# Jornada do Servidor na Demo

Explore as funcionalidades do servidor usando a persona **Ana Silva** (`servidor1@pgd-demo.gov.br`).

[Faça login como Ana →](acesso.md)

---

## Jornada 1 — Ver meu plano e registrar execução

**Situação:** Ana tem um Plano de Trabalho ativo (em execução) com 3 períodos avaliativos. O período atual está aberto para registro.

### O que você verá no dashboard (`/`)

- Card "Plano de Trabalho ativo" com a pílula de urgência (dias restantes para registrar)
- Última avaliação recebida: **nota 4 — Insuficiente**, com recurso em aberto
- Notificação de avaliação realizada

### Navegando pelo Plano de Trabalho (`/meu-plano`)

1. Acesse **Meu Plano** no menu superior
2. Veja o PlanoTrabalho 2025 da CGPGD
3. Veja as 2 contribuições: **70% desenvolvimento** + **30% suporte**
4. Veja o histórico dos 3 períodos avaliativos

### Registrando a execução do mês atual

1. Clique em **"Registrar execução"** → você vai para `/meu-plano/registrar`
2. O período atual já aparece selecionado (aberto, sem registro)
3. Descreva o que você fez no mês no campo de texto livre
4. (Opcional) Adicione ocorrências relevantes
5. Clique em **"Enviar registro"**

**O que acontece:** o registro é enviado para a chefia avaliar. Ana recebe confirmação e o status muda para "Aguardando avaliação".

---

## Jornada 2 — Contestar uma avaliação (recurso)

**Situação:** Ana recebeu **nota 4 (Insuficiente)** no período anterior e abriu um recurso há 3 dias. Ela tem 7 dias restantes de prazo.

!!! note "Na demo, o recurso já está aberto"
    Para ver o fluxo completo de contestação (antes de enviar), use **João Santos** (`servidor2@pgd-demo.gov.br`), cujo período anterior ainda não tem recurso.

### Como contestar uma avaliação (fluxo completo)

1. Acesse **Meu Plano** → clique no período avaliativo com nota que você quer contestar
2. Na página da avaliação, veja a nota e a justificativa da chefia
3. Se discordar e estiver dentro do prazo de 10 dias, clique em **"Contestar avaliação"**
4. Escreva o texto do recurso explicando sua posição
5. Clique em **"Enviar recurso"**

**O que acontece:** a chefia recebe uma notificação e tem 7 dias para responder.

### Ver o recurso de Ana em aberto

1. Faça login como Ana
2. Vá para **Meu Plano** → clique no período ARE-ANA-002
3. Veja o recurso enviado com data e status "Aguardando resposta da chefia"

---

## O que explorar também

- **[Ver as avaliações →](../servidor/avaliacoes.md)** — entenda o que cada nota significa
- **[Guia completo de registro →](../servidor/registrar-execucao.md)** — com dicas e o que fazer se der erro
