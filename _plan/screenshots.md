# Plano — Screenshots da Aplicação nas Docs do PGD Libre

## Contexto

A docs tem 27 páginas com guias passo a passo detalhados, mas **zero imagens**. Os tutoriais descrevem formulários, tabelas e fluxos de aprovação só em texto. A aplicação está rodando localmente (`localhost:5173`) com seed data rico (9 personas com estados variados: recurso aberto, avaliação pendente, erros de sync). O objetivo é capturar ~20 screenshots reais e integrá-los nas páginas de maior impacto.

---

## Personas do seed a usar (CLAUDE.md)

| Persona | Email | Estado relevante |
|---|---|---|
| Ana Silva | `servidor1@pgd-demo.gov.br` | PT em execução; ARE com recurso aberto |
| João Santos | `servidor2@pgd-demo.gov.br` | ARE registrada aguardando avaliação; convocação pendente |
| Carlos Souza | `chefe1@pgd-demo.gov.br` | CGPGD; recurso e avaliação pendentes |
| Beatriz Lima | `chefe2@pgd-demo.gov.br` | CGTI; PE aguardando aprovação |
| Maria Fernanda | `gestor@pgd-demo.gov.br` | Pode aprovar PE_CGTI |
| Roberto Admin | `admin@pgd-demo.gov.br` | Vê erros de sync de Pedro |

---

## 1. Script de captura — `portal/capture-screenshots.ts`

### Abordagem

- **Arquivo:** `portal/capture-screenshots.ts` (TypeScript, usa `@playwright/test` já instalado)
- **Execução:** `cd portal && npx tsx capture-screenshots.ts`
  - Se `tsx` não disponível: `npx ts-node --esm capture-screenshots.ts`
- **Auth:** Cada persona faz seu próprio `POST /auth/dev-login` — independente do global-setup dos testes
- **Output:** `docs/docs/assets/screenshots/{role}/{nome}.png`
- **Viewport:** 1280×720 (Desktop Chrome, consistente com playwright.config.ts)
- **Wait strategy:** `waitForLoadState('networkidle')` + `expect(locator).toBeVisible()` para elementos-chave

### Estrutura do script

```typescript
import { chromium, expect } from '@playwright/test';
import path from 'path';
import fs from 'fs';

const BACKEND = 'http://localhost:8000';
const FRONTEND = 'http://localhost:5173';
const OUT = path.resolve('../docs/docs/assets/screenshots');

async function login(page, email, name, role) {
  await page.request.post(`${BACKEND}/auth/dev-login`, {
    params: { email, name, role }
  });
}

async function shot(page, file, opts = {}) {
  const dir = path.dirname(file);
  fs.mkdirSync(dir, { recursive: true });
  await page.screenshot({ path: file, fullPage: false, ...opts });
  console.log(`✓ ${file}`);
}
```

### Roteiro de captura (20 screenshots)

#### Servidor — Ana Silva (servidor1)
| Arquivo | Rota | O que mostra |
|---|---|---|
| `servidor/dashboard.png` | `/` | Dashboard com status do plano ativo e urgência |
| `servidor/meu-plano.png` | `/meu-plano` | Plano com contribuições (70%/30%) e períodos |
| `servidor/registrar-execucao.png` | `/meu-plano` → clicar em "Registrar" | Formulário de registro com período aberto |
| `servidor/avaliacoes.png` | `/meu-plano` | Histórico de avaliações (grade + status) |
| `servidor/contestar-avaliacao.png` | via UI | Formulário de contestação com contagem de prazo |

#### Chefia — Carlos Souza (chefe1)
| Arquivo | Rota | O que mostra |
|---|---|---|
| `chefia/dashboard.png` | `/` | Dashboard com alertas de equipe (urgências) |
| `chefia/minha-equipe.png` | `/equipe` | Tabela com badges (Avaliação pendente, Recurso aberto) |
| `chefia/avaliar-registros.png` | `/equipe` → clicar em servidor | Formulário de avaliação com escala 1-5 |
| `chefia/responder-recurso.png` | via UI | Interface de resposta ao recurso (acatar/não acatar) |
| `chefia/criar-plano-passo1.png` | `/equipe/planos-trabalho/novo` | Wizard passo 1: participante e datas |
| `chefia/criar-plano-contribuicoes.png` | wizard passo 4 | Tabela de contribuições (% + tipo) |
| `chefia/criar-plano-confirmacao.png` | wizard passo 5 | Revisão completa + botão de confirmação |
| `chefia/emitir-convocacao.png` | via UI | Formulário de convocação com validação de prazo |

#### Gestor — Maria Fernanda
| Arquivo | Rota | O que mostra |
|---|---|---|
| `gestor/dashboard.png` | `/` | KPIs da unidade (total participantes, planos ativos) |
| `gestor/aprovar-planos-lista.png` | via UI | Plano de Entregas aguardando aprovação |
| `gestor/aprovar-planos-detalhe.png` | via UI | Detalhes do PE com botão "Aprovar" / "Devolver" |
| `gestor/conformidade.png` | `/conformidade` | Tabela OK/ERROR de sync com API Central |

#### Seção Demo — via João Santos (servidor2 — convocação pendente)
| Arquivo | Persona | O que mostra |
|---|---|---|
| `demo/login-demo.png` | qualquer | Tela de acesso ao sistema |
| `demo/dashboard-servidor.png` | João Santos | Dashboard mostrando convocação pendente |
| `demo/dashboard-chefia.png` | Carlos Souza | Dashboard chefia com alertas |
| `demo/dashboard-gestor.png` | Maria Fernanda | Dashboard gestor |

---

## 2. Integração nas páginas da docs

### Sintaxe a usar

```markdown
![Tabela da equipe com badges de status](../assets/screenshots/chefia/minha-equipe.png)
/// caption
A coluna **Pendências** sinaliza ações que requerem atenção imediata.
///
```

> Nota: MkDocs Material 9.x suporta `/// caption` como alternativa a `<figure>`. Verificar versão instalada — se não suportado, usar HTML `<figure>` + `<figcaption>` ou simplesmente texto após a imagem.

### Páginas a atualizar (prioridade)

| Página | Screenshots a adicionar |
|---|---|
| `chefia/minha-equipe.md` | `chefia/minha-equipe.png` (âncora visual da tabela) |
| `chefia/avaliar-registros.md` | `chefia/avaliar-registros.png` (escala de notas) |
| `chefia/criar-plano.md` | `chefia/criar-plano-passo1.png` + `chefia/criar-plano-contribuicoes.png` + `chefia/criar-plano-confirmacao.png` |
| `chefia/responder-recurso.md` | `chefia/responder-recurso.png` |
| `chefia/emitir-convocacao.md` | `chefia/emitir-convocacao.png` |
| `servidor/meu-plano.md` | `servidor/meu-plano.png` |
| `servidor/registrar-execucao.md` | `servidor/registrar-execucao.png` |
| `servidor/contestar-avaliacao.md` | `servidor/contestar-avaliacao.png` |
| `gestor/aprovar-planos.md` | `gestor/aprovar-planos-detalhe.png` |
| `gestor/conformidade.md` | `gestor/conformidade.png` |
| `demo/acesso.md` | `demo/login-demo.png` |
| `demo/jornada-servidor.md` | `demo/dashboard-servidor.png` |
| `demo/jornada-chefia.md` | `demo/dashboard-chefia.png` |
| `demo/jornada-gestor.md` | `demo/dashboard-gestor.png` |

### Posicionamento padrão por página

- **Logo após o parágrafo de introdução**, antes do "Passo a passo"
- Para wizards multi-step: uma imagem por seção de passo (não bloquear o fluxo)
- Screenshots de tabelas/listas: antes de descrever as colunas

---

## 3. Pré-requisitos antes de rodar

Ambos os servidores devem estar no ar:
```bash
# Backend
cd pgd-libre && docker compose up -d
# Verificar: curl http://localhost:8000/health

# Frontend
cd portal && npm run dev
# Verificar: curl http://localhost:5173
```

Seed data populado:
```bash
docker exec pgd-libre-app-1 python scripts/seed_demo.py
```

---

## 4. Verificação

1. `cd portal && npx tsx capture-screenshots.ts` → confirmar 20 PNGs em `docs/docs/assets/screenshots/`
2. `cd docs && poetry run mkdocs serve -a localhost:8001` → navegar por todas as 14 páginas atualizadas
3. Confirmar que imagens renderizam com dimensões adequadas (não distorcidas, não muito pequenas)
4. Commit + push → CI rebuilda e deploya no GitHub Pages

---

## 5. Arquivos a criar / modificar

| Ação | Arquivo |
|---|---|
| Criar | `portal/capture-screenshots.ts` |
| Criar | `docs/docs/assets/screenshots/` (estrutura de dirs + PNGs) |
| Modificar (×14) | Páginas de docs listadas acima |
