# PGD Libre — Product Brief

> **Propósito:** Este documento é um briefing do produto para orientar a criação de materiais de comunicação: slides, landing page, vídeo demo e outros artefatos. Não contém os artefatos em si — apenas o conteúdo, tom e estrutura que cada um deve ter.

---

## Identidade do produto

**Nome:** PGD Libre

**Tagline (sugestão):** _"Gestão de desempenho pública: simples, transparente e conforme."_

**Posicionamento:** Plataforma de código aberto para gestão do Programa de Gestão e Desempenho (PGD) no serviço público federal brasileiro. Implementa integralmente o Decreto 11.072/2022 e as Instruções Normativas 24/2023 e 52/2023.

**Público-alvo:**
- **Primário:** Gestores de TI e equipes de inovação em órgãos federais
- **Secundário:** Chefias imediatas e servidores participantes do PGD
- **Terciário:** Tomadores de decisão (secretários, diretores) buscando conformidade regulatória

---

## Proposta de valor

### Problema atual
Órgãos federais gerenciam o PGD em planilhas Excel, e-mails ou sistemas locais não integrados, resultando em:
- Não conformidade com prazos da legislação (registros fora do prazo, avaliações atrasadas)
- Falta de rastreabilidade (sem auditoria, sem histórico)
- Dificuldade de sincronização com a API PGD Central do MGI
- Baixa transparência para gestores e servidores

### Solução PGD Libre
- **100% conforme:** implementa todos os 37 requisitos funcionais do marco normativo
- **Ciclo completo:** do ato de autorização ao recurso de avaliação, tudo em um sistema
- **Integração nativa:** sincronização automática com a API PGD Central (MGI)
- **Código aberto:** sem custo de licença, auditável, customizável
- **Multi-tenant:** uma instância para múltiplos órgãos, com isolamento de dados

### Diferenciais vs. sistema legado (API PGD Central)
| Aspecto | API PGD Central | PGD Libre |
|---|---|---|
| Interface | Somente API REST | Interface web completa |
| Workflow | Nenhum | Ciclo completo (plano → registro → avaliação → recurso) |
| Auditoria | Não | Log imutável de todos os eventos |
| Notificações | Não | E-mail + sistema |
| Multi-usuário | Não | Roles hierárquicos (servidor → chefe → gestor → admin) |
| Código aberto | Não | Sim (MIT) |

---

## Arquitetura e stack (para audiências técnicas)

- **Backend:** FastAPI + Strawberry GraphQL + PostgreSQL
- **Frontend:** SvelteKit + SSR
- **Infraestrutura:** Docker / Cloud Run (GCP)
- **Auth:** Google OAuth + Gov.br OIDC
- **CI/CD:** GitHub Actions + Artifact Registry

---

## Briefing: Slides / Deck de apresentação

**Duração:** 10–15 slides, 15–20 minutos

**Estrutura sugerida:**

1. **Capa:** Logo PGD Libre + tagline
2. **O problema:** "Como seu órgão gerencia o PGD hoje?" — foto de planilha Excel como metáfora
3. **O marco normativo:** Decreto 11.072/2022 + IN 24 e 52/2023 em linguagem simples (3 obrigações principais)
4. **O que é o PGD Libre:** print do dashboard + 3 bullets de valor
5. **Ciclo completo:** diagrama dos 4 papéis × fluxo de dados (servidor → chefe → gestor → admin)
6. **Módulos:** 6 cards (Planos de trabalho / Registro de execução / Avaliação / Equipe / Conformidade / Admin)
7. **Integração API Central:** diagrama de sincronização automática
8. **Demo ao vivo / screenshots:** 3–4 telas mais impactantes (dashboard chefe, avaliação, conformidade)
9. **Código aberto:** GitHub link + licença MIT + arquitetura em 1 slide
10. **Roadmap:** próximos módulos (delegação, afastamentos, LGPD)
11. **Como adotar:** 3 passos (fork → configurar → deploy no Cloud Run)
12. **CTA:** link da demo + contato

**Tom:** técnico mas acessível; evitar jargão jurídico; usar capturas de tela reais da demo.

---

## Briefing: Landing Page

**URL sugerida:** `pgdlibre.gov.br` ou `pgd-libre.seges.gov.br`

**Estrutura da página (seções):**

### Hero
- **Headline:** "Gestão do PGD sem planilhas. Sem retrabalho. Sem risco de inconformidade."
- **Subheadline:** "Plataforma de código aberto que implementa o Decreto 11.072/2022 e as INs 24 e 52/2023 — do ato de autorização à avaliação de desempenho."
- **CTA primário:** "Acessar a demo" (link para instância pública)
- **CTA secundário:** "Ver no GitHub"
- **Visual:** screenshot animado do dashboard chefe com KPIs

### Problema (social proof da dor)
- 3 cards com dores reais:
  - "Planilhas não têm controle de prazo"
  - "Servidores perdem prazos de registro"
  - "API Central sem interface — suporte manual"

### Solução (features)
- 6 cards com ícone + título + 1 frase:
  1. **Planos de trabalho** — Criação e acompanhamento com wizard guiado
  2. **Registro de execução** — Servidor registra mensalmente com prazo automático
  3. **Avaliação e recurso** — Fluxo completo 1–5 com contestação e prazo legal
  4. **Gestão de equipe** — Chefe vê KPIs da equipe em tempo real
  5. **Conformidade** — Painel de sincronização com API Central do MGI
  6. **Multi-tenant** — Um sistema, múltiplos órgãos com isolamento total

### Como funciona (diagrama)
- Fluxograma horizontal dos 4 papéis e suas ações principais

### Social proof
- Legislação como âncora: "Implementa 100% dos 37 requisitos do marco normativo"
- Badges: Decreto 11.072/2022 | IN 24/2023 | IN 52/2023

### Código aberto
- "MIT License — fork, customize, contribua"
- GitHub stars counter
- Tech stack badges (FastAPI / SvelteKit / PostgreSQL / Docker)

### CTA final
- "Experimente a demo agora" + "Instale em 5 minutos"

**Tom:** direto, confiante, governo-friendly (sem ser burocrático); PT-BR formal.

---

## Briefing: Vídeo demo

**Duração:** 2–3 minutos

**Formato sugerido:** screencast com narração em voz + legendas

**Roteiro:**

```
[0:00–0:20] Abertura
  Logo PGD Libre + música institucional leve
  "Gerenciar o Programa de Gestão não precisa ser complicado."

[0:20–0:50] Jornada do Servidor (Ana Silva)
  - Login → Dashboard com plano ativo
  - Registrar execução do mês
  - Ver avaliação recebida

[0:50–1:30] Jornada do Chefe (Carlos Souza)
  - Ver equipe com KPIs
  - Avaliar registro de João (escolher nota, justificar)
  - Responder recurso de Ana

[1:30–2:00] Jornada do Gestor (Maria Fernanda)
  - Ver painel de conformidade
  - Aprovar PlanoEntregas da CGTI

[2:00–2:20] Integração e conformidade
  - Diagrama de sincronização com API Central
  - "Seus dados sincronizados automaticamente com o MGI"

[2:20–2:40] Encerramento
  - "PGD Libre — código aberto, gratuito, pronto para produção"
  - CTA: "Acesse a demo" + GitHub
```

**Estilo visual:** UI real do sistema (sem animações exageradas); cursor destacado; transições rápidas.

---

## Assets necessários (a criar)

| Asset | Status | Prioridade |
|---|---|---|
| Logo SVG (ícone + wordmark) | Pendente | Alta |
| Screenshots da demo (8–10 telas) | Pendente — depende do seed | Alta |
| Paleta de cores oficial | Usar tokens de `app.css` | Já existe |
| Ícones dos módulos | Usar `Icon.svelte` | Já existe |
| Diagrama de arquitetura | Pendente | Média |
| Diagrama de fluxo de papéis | Pendente | Média |
| Vídeo demo | Pendente — depende do seed | Baixa |

---

## Próximos passos

1. **Agora:** executar `seed_demo.py`, tirar screenshots das jornadas principais
2. **Próxima sprint:** criar logo e identidade visual
3. **Depois:** gravar vídeo demo com screencast
4. **Deploy:** publicar instância demo + landing page
