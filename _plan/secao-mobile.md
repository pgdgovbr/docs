# Plano — Seção mobile da documentação (Fase 14)

## Contexto

A Fase 12 do plano de pactuação bilateral (PRs #1 e #2 em `pgdgovbr/docs`) atualizou 14+ páginas para o fluxo de pactuação. A Fase 11 deliberadamente **postergou** a cobertura mobile: o `mkdocs.yml` carrega o comentário `# TODO: adicionar seção "Mobile" quando subagente B gerar screenshots mobile (postergado nesta leva).` na linha 79.

Esta fase fecha a lacuna: captura screenshots mobile (iPhone 14 — 390×844) das telas onde o CSS responsivo da Fase 9 adicionou comportamento diferenciado, e integra a cobertura textual em **subseções "## No celular"** dentro de cada página relevante (decisão fundamentada na §3).

Estado atual relevante:

- **Páginas docs** que descrevem fluxos desktop (com screenshots): `servidor/meu-plano.md`, `servidor/criar-plano.md`, `servidor/revisar-plano.md`, `chefia/minha-equipe.md`, `chefia/revisar-plano.md`, `servidor/visao-geral.md` (dashboard), `chefia/visao-geral.md` (dashboard).
- **Screenshots desktop** já em `docs/assets/screenshots/servidor/` (13 PNGs) e `docs/assets/screenshots/chefia/` (12 PNGs) — todas a 1280×720.
- **CSS mobile** já implementado (Fase 9): 4 rotas têm `@media (max-width: 640px)` ativos.
- **Capture script:** `portal/capture-screenshots.ts` (630 linhas, headless chromium, login via dev-login). Hoje cria sempre `viewport: { width: 1280, height: 720 }`.
- **Referência visual mobile:** `portal/_design/from-claude-design/project/pactuacao-mobile.jsx` (iPhone frame 402×874, 3 telas-chave: meu-plano vazio, servidor revisar, chefia revisar).

Comportamentos mobile já implementados (verificados nos `.svelte`):

| Arquivo | Linha | O que muda em ≤640px |
|---|---|---|
| `meu-plano/+page.svelte` | 760 | `.vazio-ctas` empilha (2 CTAs lado-a-lado → coluna única) |
| `meu-plano/[id]/editar/+page.svelte` | 504 | `.cta-card` (Assinar e enviar) vira `position: sticky; bottom: 0` |
| `meu-plano/[id]/revisar/+page.svelte` | 463 | `.kpi-row` para 2 colunas, `AssinaturaCard` vira sticky no rodapé, `.diff-grid` empilha |
| `equipe/+page.svelte` | 352 | Grid `.g-3` empilha, `.tbl` ganha scroll horizontal (`min-width: 640px`) |

Não há tab bar inferior global; o "sticky" se aplica apenas ao card de CTA principal nas telas de pactuação. Não há comportamento mobile específico em `criar/`, `equipe/planos-trabalho/[id]/revisar`, dashboards (`/`) ou `equipe/planos-trabalho/novo` — neles a documentação mobile descreverá apenas o redimensionamento natural dos cards/forms.

---

## §1 · Inventário de capturas mobile

**Estrutura escolhida:** `docs/assets/screenshots/mobile/<persona>/<tela>.png` — mantém a raiz `servidor/` e `chefia/` limpa para desktop, agrupa todo mobile sob uma pasta única (facilita busca e futura limpeza/regeneração).

**Viewport:** `390×844` (iPhone 14 — mais próximo da realidade dos servidores; o design usa 402×874 mas 390 cobre o iPhone 12/13/14/15 padrão e a maior fatia de Android moderno).

10 PNGs no total — escolhidos pelos pontos onde o CSS mobile *muda comportamento* ou onde o conteúdo é a porta de entrada mais provável via celular (notificação push → revisar/assinar):

| # | Persona | Rota | Arquivo destino | Por que mobile importa aqui |
|---|---|---|---|---|
| 1 | Marta (servidor7) | `/meu-plano` (vazio) | `mobile/servidor/meu-plano-vazio.png` | CTAs empilham — entrada para "Criar do zero" no celular |
| 2 | Marta | `/meu-plano/criar` step 1 (período/vínculo) | `mobile/servidor/criar-passo1.png` | Primeira tela do wizard — confirma que datas e selects são utilizáveis |
| 3 | Marta | `/meu-plano/criar` step 4 (contribuições) | `mobile/servidor/criar-contribuicoes.png` | Step mais denso; valida que adicionar contribuição funciona no toque |
| 4 | Lucas (servidor4) | `/meu-plano/[id]/editar` | `mobile/servidor/editar.png` | `.cta-card` "Assinar e enviar" vira **sticky no rodapé** — destaque visual chave |
| 5 | Felipe (servidor6) | `/` (dashboard) | `mobile/servidor/dashboard-aguardando.png` | Card "Aguardando sua ação" — porta de entrada típica via notificação |
| 6 | Felipe | `/meu-plano/[id]/revisar` | `mobile/servidor/revisar.png` | `AssinaturaCard` sticky no rodapé; `.kpi-row` para 2 col; `.diff-grid` empilha — três mudanças simultâneas |
| 7 | Beatriz (chefe2) | `/` (dashboard) | `mobile/chefia/dashboard-aguardando.png` | Espelho do #5 para chefia — banner "X planos aguardando" |
| 8 | Beatriz | `/equipe` | `mobile/chefia/equipe.png` | Grid `.g-3` empilha; tabela ganha scroll horizontal — UX delicada |
| 9 | Beatriz | `/equipe/planos-trabalho/[id]/revisar` (PT Pedro, status 2) | `mobile/chefia/revisar.png` | Mesma estrutura responsiva da #6 mas no lado chefia |
| 10 | Ana (servidor1) | `/meu-plano` com `CloneDialog` aberto | `mobile/servidor/clonar-modal.png` | Verifica modal full-screen em mobile (não é coberto por CSS específico — depende do componente) |

Observação: **não capturar** a tela `chefia/planos-trabalho/[id]/editar` em mobile — é uma exceção rara (chefia cria PT para servidor recém-chegado) e tem o mesmo layout do `meu-plano/[id]/editar`. Cobrir só desktop.

---

## §2 · Diff exato em `capture-screenshots.ts`

### 2.1 Adicionar constante de viewport

No topo do arquivo (após linha 17, junto com `OUT`):

```ts
const MOBILE_VIEWPORT = { width: 390, height: 844 } as const;
```

### 2.2 Nova função `captureMobile`

Adicionar **antes da função `main`** (linha 605 atual):

```ts
async function captureMobile(browser: ReturnType<typeof chromium.launch> extends Promise<infer B> ? B : never) {
  console.log('\n[MOBILE — iPhone 14 (390×844)]');

  // ── 1. Marta — /meu-plano vazio ─────────────────────────────────────────
  console.log('  [Marta — mobile vazio + wizard]');
  const ctxM = await browser.newContext({ viewport: MOBILE_VIEWPORT });
  await login(ctxM, PERSONAS.servidor7);
  const pageM = await ctxM.newPage();

  await go(pageM, '/meu-plano');
  await shot(pageM, 'mobile/servidor/meu-plano-vazio.png');

  // ── 2-3. Marta — wizard step 1 + step 4 (contribuições) ─────────────────
  await go(pageM, '/meu-plano/criar');
  await pageM.waitForTimeout(400);
  await fillWizardStep0(pageM);  // helper existente — preenche datas
  await shot(pageM, 'mobile/servidor/criar-passo1.png');

  // Avançar 3 vezes até step 4 (contribuições)
  for (let i = 0; i < 3; i++) {
    await pageM.getByRole('button', { name: /próximo/i }).click();
    await pageM.waitForTimeout(250);
  }
  await addContribServidor(pageM, 'Apoio em projetos transversais da CGPGD', 60);
  await addContribServidor(pageM, 'Documentação e reuniões de equipe', 40);
  await shot(pageM, 'mobile/servidor/criar-contribuicoes.png');

  await ctxM.close();

  // ── 4. Lucas — editar rascunho (sticky CTA no rodapé) ────────────────────
  console.log('  [Lucas — mobile editar]');
  const ctxL = await browser.newContext({ viewport: MOBILE_VIEWPORT });
  await login(ctxL, PERSONAS.servidor4);
  const pageL = await ctxL.newPage();

  const lucasResp = await ctxL.request.post(`${BACKEND}/graphql`, {
    data: { query: '{ meusPlanosTrabalho { id status } }' },
  });
  const lucasPts = (await lucasResp.json())?.data?.meusPlanosTrabalho ?? [];
  const lucasPt = lucasPts.find((p: any) => p.status === 5) ?? lucasPts[0];
  if (lucasPt?.id) {
    await go(pageL, `/meu-plano/${lucasPt.id}/editar`);
    // Scroll até o final para garantir que CTA sticky aparece no viewport
    await pageL.evaluate(() => window.scrollTo(0, document.body.scrollHeight));
    await pageL.waitForTimeout(300);
    await shot(pageL, 'mobile/servidor/editar.png');
  } else {
    console.log('  ! Lucas sem PT rascunho — pulando mobile/servidor/editar.png');
  }
  await ctxL.close();

  // ── 5-6. Felipe — dashboard + revisar (sticky AssinaturaCard) ────────────
  console.log('  [Felipe — mobile dashboard + revisar]');
  const ctxF = await browser.newContext({ viewport: MOBILE_VIEWPORT });
  await login(ctxF, PERSONAS.servidor6);
  const pageF = await ctxF.newPage();

  await go(pageF, '/');
  await shot(pageF, 'mobile/servidor/dashboard-aguardando.png');

  const felipeResp = await ctxF.request.post(`${BACKEND}/graphql`, {
    data: { query: '{ meusPlanosTrabalho { id status } }' },
  });
  const felipePts = (await felipeResp.json())?.data?.meusPlanosTrabalho ?? [];
  const felipePt = felipePts.find((p: any) => p.status === 7) ?? felipePts[0];
  if (felipePt?.id) {
    await go(pageF, `/meu-plano/${felipePt.id}/revisar`);
    await pageF.evaluate(() => window.scrollTo(0, document.body.scrollHeight));
    await pageF.waitForTimeout(300);
    await shot(pageF, 'mobile/servidor/revisar.png');
  } else {
    console.log('  ! Felipe sem PT em aguardando — pulando mobile/servidor/revisar.png');
  }
  await ctxF.close();

  // ── 7-9. Beatriz — dashboard + equipe + revisar PT do Pedro ─────────────
  console.log('  [Beatriz — mobile dashboard + equipe + revisar]');
  const ctxB = await browser.newContext({ viewport: MOBILE_VIEWPORT });
  await login(ctxB, PERSONAS.chefe2);
  const pageB = await ctxB.newPage();

  await go(pageB, '/');
  await shot(pageB, 'mobile/chefia/dashboard-aguardando.png');

  await go(pageB, '/equipe');
  await shot(pageB, 'mobile/chefia/equipe.png');

  const ptsResp = await ctxB.request.post(`${BACKEND}/graphql`, {
    data: { query: '{ listarPlanosTrabalho { id status } }' },
  });
  const allPts = (await ptsResp.json())?.data?.listarPlanosTrabalho ?? [];
  const pedroPt = allPts.find((p: any) => p.status === 2);
  if (pedroPt?.id) {
    await go(pageB, `/equipe/planos-trabalho/${pedroPt.id}/revisar`);
    await pageB.evaluate(() => window.scrollTo(0, document.body.scrollHeight));
    await pageB.waitForTimeout(300);
    await shot(pageB, 'mobile/chefia/revisar.png');
  } else {
    console.log('  ! nenhum PT com status=2 — pulando mobile/chefia/revisar.png');
  }
  await ctxB.close();

  // ── 10. Ana — CloneDialog em mobile ─────────────────────────────────────
  console.log('  [Ana — mobile clonar modal]');
  const ctxA = await browser.newContext({ viewport: MOBILE_VIEWPORT });
  await login(ctxA, PERSONAS.servidor1);
  const pageA = await ctxA.newPage();
  await go(pageA, '/meu-plano');
  await pageA.waitForTimeout(400);
  const btnCtaClone = pageA.getByRole('button', { name: /clonar plano anterior/i });
  const hasCta = await btnCtaClone.isVisible({ timeout: 2000 }).catch(() => false);
  if (hasCta) {
    await btnCtaClone.click();
  } else {
    const btnAsideClone = pageA.locator('button[title="Clonar"]').first();
    const hasAside = await btnAsideClone.isVisible({ timeout: 2000 }).catch(() => false);
    if (hasAside) await btnAsideClone.click();
  }
  await pageA.waitForTimeout(400);
  const tituloModal = pageA.getByText(/Clonar plano de trabalho/i).first();
  if (await tituloModal.isVisible({ timeout: 2000 }).catch(() => false)) {
    await shot(pageA, 'mobile/servidor/clonar-modal.png');
  } else {
    console.log('  ! modal de clone não abriu em mobile');
  }
  await ctxA.close();
}
```

### 2.3 Registrar no `main()`

Adicionar uma linha ao bloco `try` (linha 611-618), **depois** de `capturePactuacao` e **antes** de `captureExtra`:

```ts
try {
  await captureServidor(browser);
  await captureChefe(browser);
  await captureGestor(browser);
  await captureAdmin(browser);
  await captureDemo(browser);
  await capturePactuacao(browser);
  await captureMobile(browser);   // ← NOVO
  await captureExtra(browser);
}
```

### 2.4 Validação manual antes de commitar

```bash
cd portal
# Backend + frontend devem estar rodando + seed_demo.py
npx tsx capture-screenshots.ts
ls -la ../docs/docs/assets/screenshots/mobile/servidor/ ../docs/docs/assets/screenshots/mobile/chefia/
# Esperado: 7 PNGs em servidor/, 3 em chefia/
```

---

## §3 · Decisão de estrutura na docs

**Recomendação: subseção `## No celular` dentro de cada página relevante** (não criar página dedicada).

### Análise das opções

| Critério | Subseção em cada página | Página única `mobile/visao-geral.md` |
|---|---|---|
| **Descoberta no contexto** | ✅ Quem lê "Revisar plano ajustado pela chefia" vê o mobile do mesmo fluxo | ❌ Usuário precisa lembrar de navegar para outra seção |
| **Manutenção** | ⚠️ 7 arquivos editados | ✅ 1 arquivo só |
| **Volume de conteúdo** | ✅ 1-2 parágrafos curtos por tela (cabem bem) | ⚠️ Página fica longa/escaneável demais |
| **Estrutura de site** | ✅ Não adiciona nova entrada de nav (`navigation.sections` já lota) | ❌ Adiciona uma 5ª seção lateral |
| **Padrão comum em docs** | ✅ Material for MkDocs / Stripe / Linear seguem este padrão | ❌ Página "Mobile" é raro fora de SDKs |
| **SEO / busca interna** | ✅ Quem busca "assinar mobile" encontra na própria página do fluxo | ⚠️ Resultado leva a página separada |

A única vantagem clara da página única seria centralizar capturas mobile para apresentação visual ("vitrine"). Como o foco da docs é **ajudar o usuário a executar um fluxo**, não exibir o produto, perdemos pouco.

**Decisão:** subseção embutida. Se no futuro houver demanda para "vitrine mobile" (ex.: pitch comercial), criar uma página complementar `sobre/mobile.md` que apenas embute as imagens já existentes — sem duplicar conteúdo.

---

## §4 · Páginas a atualizar (subseções "## No celular")

7 páginas ganham a nova subseção. Texto sugerido abaixo — curto, factual, sem rebuscar o que o screenshot já mostra.

### 4.1 `docs/docs/servidor/meu-plano.md` — subseção após "Quando você não tem plano ainda"

```markdown
### No celular

Em telas menores que 640px, os dois CTAs ("Criar do zero" e "Clonar plano anterior") empilham em coluna única para garantir alvos de toque grandes. O card de planos anteriores fica abaixo dos CTAs principais.

![Tela Meu Plano vazio no celular](../assets/screenshots/mobile/servidor/meu-plano-vazio.png){ width="320" }

O modal de clonar (quando você toca em "Clonar plano anterior") ocupa a tela inteira no celular — o conteúdo do plano atual continua acessível ao fechar.
```

### 4.2 `docs/docs/servidor/criar-plano.md` — subseção no final, antes de "Próximos passos"

```markdown
## No celular

O wizard de criação roda igual em mobile — os 5 passos aparecem em coluna, os botões "Voltar" e "Próximo" ficam no rodapé.

![Wizard de criação no celular — passo 1](../assets/screenshots/mobile/servidor/criar-passo1.png){ width="320" }

Na etapa de **contribuições** (passo 4), o teclado virtual pode cobrir o campo de descrição — role a tela após digitar o percentual para ver a lista das contribuições já adicionadas.

![Wizard no celular — passo de contribuições](../assets/screenshots/mobile/servidor/criar-contribuicoes.png){ width="320" }
```

### 4.3 `docs/docs/servidor/revisar-plano.md` — subseção no final

```markdown
## No celular

A página de revisar é o caso mais comum de uso mobile: você recebe a notificação no celular e quer assinar ou devolver sem abrir o computador.

![Página de revisar no celular](../assets/screenshots/mobile/servidor/revisar.png){ width="320" }

**Mudanças específicas no celular:**

- O card "Assinaturas e ação" (com os 3 checkboxes e o botão "Assinar e ativar plano") fica **fixo no rodapé** — você vê a ação principal sem precisar rolar.
- A grade de KPIs (carga horária, período etc.) passa de 4 para 2 colunas.
- O bloco "O que mudou desde sua última leitura" empilha cada campo em linha única.

Se preferir devolver para ajustes, a confirmação inline ("isso vai zerar a assinatura da chefia") aparece acima do botão sticky.
```

### 4.4 `docs/docs/servidor/visao-geral.md` — subseção dentro de "Dashboard" (ou similar)

```markdown
### No celular

O dashboard tem um card destacado no topo quando há plano aguardando sua ação. Tocar no card abre direto a página de revisar.

![Dashboard do servidor no celular com card "aguardando sua ação"](../assets/screenshots/mobile/servidor/dashboard-aguardando.png){ width="320" }
```

### 4.5 `docs/docs/chefia/visao-geral.md` — subseção no final

```markdown
## No celular

A chefia recebe notificações de planos aguardando assinatura e pode revisar do celular. O dashboard tem um banner consolidado no topo quando há pendências.

![Dashboard da chefia no celular com banner de pendências](../assets/screenshots/mobile/chefia/dashboard-aguardando.png){ width="320" }
```

### 4.6 `docs/docs/chefia/minha-equipe.md` — subseção no final

```markdown
## No celular

A lista de equipe passa de 3 colunas para 1 coluna empilhada. A tabela de planos ganha **rolagem horizontal** — toda a informação continua disponível, é só arrastar a tabela para o lado.

![Minha equipe no celular](../assets/screenshots/mobile/chefia/equipe.png){ width="320" }
```

### 4.7 `docs/docs/chefia/revisar-plano.md` — subseção no final

```markdown
## No celular

A revisão de plano pela chefia funciona igual ao caso do servidor: o card de assinatura fica fixo no rodapé, e a grade de informações se ajusta para 2 colunas.

![Revisar plano de servidor no celular](../assets/screenshots/mobile/chefia/revisar.png){ width="320" }

Dica: ao "Devolver para ajustes" no celular, confirme antes de tocar — a ação zera a assinatura do servidor (se ele já tinha assinado uma versão anterior) e exige que ele reassine.
```

### 4.8 Não atualizar nesta leva

- `chefia/criar-plano-excecao.md`: o wizard é igual ao do servidor — não há mobile distintivo (mesma cobertura do 4.2 implícita).
- `servidor/registrar-execucao.md`, `servidor/avaliacoes.md`, `servidor/contestar-avaliacao.md`, `chefia/avaliar-registros.md`: fluxos pós-pactuação fora do escopo desta Fase 14 (mobile para esses fluxos pode entrar numa Fase 15 futura).
- Páginas em `gestor/` e `admin/`: papéis usados majoritariamente em desktop (relatórios, conformidade, painel admin). Sem mobile previsto.

---

## §5 · Atualização do `mkdocs.yml`

### 5.1 Remover o TODO

Editar a linha 79 (e remover):

```yaml
  # TODO: adicionar seção "Mobile" quando subagente B gerar screenshots mobile (postergado nesta leva).
```

### 5.2 Não adicionar entradas novas de nav

Como a estratégia é **subseções embutidas**, não há páginas novas para registrar. O `mkdocs.yml` fica mais curto após a remoção do TODO — sem outras mudanças estruturais.

### 5.3 (Opcional) Habilitar lightbox para zoom de imagens

O usuário mobile pode querer ampliar capturas. Avaliar adicionar o plugin/extensão `glightbox` em fase futura — **não obrigatório nesta Fase 14**.

---

## §6 · Ordem de execução da Fase 14

**Recomendação: 1 subagente único** (não vale paralelizar).

Justificativa:
- A geração de markdown depende dos PNGs estarem no lugar (ou pelo menos dos paths definidos, o que já está nesta spec).
- Captura é I/O-bound (sequencial) e leva ~2-3min; markdown é texto rápido.
- Dois agentes em paralelo gerariam conflito mínimo mas overhead de coordenação maior.

**Sequência sugerida:**

1. **Pré-requisitos** (manuais antes de chamar subagente):
   - Backend `pgd-libre` rodando em `localhost:8000` com seed (`docker exec pgd-libre-app-1 python scripts/seed_demo.py`).
   - Frontend `portal` rodando em `localhost:5173` (`npm run dev`).
   - Branch nova: `git checkout -b docs/secao-mobile` em `pgdgovbr/docs`.

2. **Subagente único executa, em ordem:**
   1. Editar `portal/capture-screenshots.ts` aplicando §2 (constante + função + linha em main).
   2. Rodar `npx tsx capture-screenshots.ts` da pasta `portal/`.
   3. Verificar que os 10 PNGs apareceram em `docs/docs/assets/screenshots/mobile/{servidor,chefia}/`.
   4. Editar as 7 páginas markdown conforme §4.
   5. Remover o TODO no `mkdocs.yml` (§5.1).
   6. Rodar `mkdocs build --strict` na pasta `docs/`.
   7. Conferir visualmente com `mkdocs serve` (spot-check 2-3 páginas).
   8. Commit: `docs: adicionar cobertura mobile (capturas iPhone 14 + 7 subseções)`.

3. **Pós-execução** (manual):
   - Abrir PR em `pgdgovbr/docs` apontando para esta spec.
   - Após merge, validar https://pgdgovbr.github.io/docs/ rendeu os mobile.

---

## §7 · Critérios de aceitação

- [ ] `mkdocs build --strict` passa com zero erros e zero warnings (em particular: nenhum link quebrado para `mobile/...png`).
- [ ] 10 PNGs em `docs/docs/assets/screenshots/mobile/` (7 em `servidor/`, 3 em `chefia/`), todos a `390×844`.
- [ ] 7 páginas markdown atualizadas com subseção "No celular" ou "### No celular", cada uma com 1-2 parágrafos + ao menos 1 imagem.
- [ ] `mkdocs.yml` não tem mais o comentário "TODO mobile".
- [ ] `mkdocs serve` renderiza as imagens em tamanho razoável (≤320px de largura — sugerido via `{ width="320" }`).
- [ ] As capturas mostram o comportamento responsivo esperado: CTAs empilhados no `meu-plano-vazio`, `AssinaturaCard` sticky no `revisar`, tabela com scroll em `equipe`.
- [ ] Site não cria nova entrada na sidebar nem nova seção (segue a decisão da §3).

---

## Apêndice · Decisões pendentes (vai-perguntar-agora)

Nenhuma decisão dura fica para o usuário — as escolhas a seguir foram tomadas neste plano com a justificativa indicada. Se discordar, basta sinalizar antes de iniciar a Fase 14:

1. **Viewport `390×844` vs `402×874` (design)** — escolhido 390 por cobrir iPhone 12-15 padrão (mais comum). Diferença visual é mínima.
2. **Estrutura `mobile/<persona>/<tela>.png` vs `<persona>/mobile-<tela>.png`** — escolhido o primeiro para isolar mobile e facilitar futura regeneração total da pasta.
3. **Subseção embutida vs página dedicada** — escolhido subseção (§3). Reversível: dá para criar `sobre/mobile.md` depois sem perder o trabalho.
4. **Cobertura de gestor/admin em mobile** — fora do escopo. Esses papéis usam desktop quase exclusivamente; abrir Fase 15 se houver demanda.
5. **Páginas pós-pactuação** (`registrar-execucao`, `avaliacoes`, `contestar-avaliacao`, `avaliar-registros`) — também fora do escopo. Não têm CSS mobile específico hoje; cobrir junto com refinos visuais futuros.
6. **Plugin de lightbox/zoom** — não nesta leva. As capturas a 320px de largura são legíveis o suficiente para a leitura padrão; zoom é melhoria de UX, não bloqueador.
