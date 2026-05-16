# Plano — Documentação de Usuário do PGD Libre (MkDocs + GitHub Pages)

## Contexto

O PGD Libre tem backend e frontend funcionando, com dados de demonstração já disponíveis. O próximo passo é disponibilizar uma **documentação pública voltada ao usuário final** (servidor público, chefia imediata, gestor de unidade) — não ao desenvolvedor. A docs também servirá de base para tutoriais, roteiros de apresentação e material de adoção.

**Decisões já tomadas pelo usuário:**
- Navegação **por papel** (Sou Servidor / Sou Chefia / Sou Gestor)
- Profundidade **dupla**: tutorial completo para onboarding + referência rápida para uso recorrente
- Escopo: **conceitos do PGD** (glossário, contexto legislativo) + **demo interativa** (sem seção técnica de deploy ou FAQ por enquanto)
- Tom: **amigável e direto**, usando "você", linguagem de produto — não de manual de governo

---

## 1. Infraestrutura (copiar padrão de `destaquesgovbr/docs`)

### 1.1 Tornar `pgdgovbr/docs/` um repositório Git independente

```bash
cd /Users/nitai/dev/destaquesgovbr/pgdgovbr/docs
git init
git add .
git commit -m "chore: initial commit"
# Criar repo no GitHub (org a definir) e adicionar remote
```

### 1.2 Arquivos de infraestrutura a criar (inspirados em `destaquesgovbr/docs`)

| Arquivo | Origem | Adaptações |
|---|---|---|
| `mkdocs.yml` | Copiar de `destaquesgovbr/docs/mkdocs.yml` | Novo site_name, site_url, nav, sem plugin blog por ora |
| `pyproject.toml` | Copiar de `destaquesgovbr/docs/pyproject.toml` | Nome do projeto atualizado |
| `.github/workflows/docs.yml` | Copiar de `destaquesgovbr/docs/.github/workflows/docs.yml` | Sem alterações necessárias |
| `.gitignore` | Copiar | Idêntico |
| `docs/assets/` | Criar | Logo do PGD Libre (a criar) |
| `docs/stylesheets/` | Opcional | CSS customizado se necessário |

### 1.3 Configuração do `mkdocs.yml`

```yaml
site_name: PGD Libre
site_description: Guia do usuário do PGD Libre
site_url: https://<org>.github.io/docs/  # definir
repo_url: https://github.com/<org>/docs

theme:
  name: material
  language: pt-BR
  palette:
    primary: blue
    accent: blue
  features:
    - navigation.tabs
    - navigation.sections
    - navigation.top
    - search.highlight
    - content.code.copy

plugins:
  - search:
      lang: pt

markdown_extensions:
  - admonition
  - pymdownx.superfences
  - pymdownx.tabbed:
      alternate_style: true
  - tables
  - toc:
      permalink: true
```

---

## 2. Arquitetura da Informação

### Estrutura de navegação (nav)

```
Início (index.md)
├── O que é o PGD Libre?         ← produto, proposta de valor, diferenciais
├── Conceitos do PGD             ← glossário + contexto da legislação
│   ├── O Programa de Gestão
│   ├── Papéis e responsabilidades
│   └── Glossário
├── Experimente a Demo           ← guia interativo, migrado de jornadas-demo.md
│   ├── Como acessar a demo
│   ├── Jornada: Servidor
│   ├── Jornada: Chefia
│   └── Jornada: Gestor e Admin
├── Sou Servidor
│   ├── Visão geral do papel
│   ├── Meu Plano de Trabalho
│   ├── Registrar Execução       ← tutorial completo
│   ├── Referência rápida        ← cheat sheet de ações frequentes
│   ├── Minhas Avaliações
│   └── Contestar uma Avaliação
├── Sou Chefia Imediata
│   ├── Visão geral do papel
│   ├── Minha Equipe
│   ├── Avaliar Registros        ← tutorial completo
│   ├── Referência rápida
│   ├── Responder um Recurso
│   ├── Criar Plano de Trabalho
│   └── Emitir Convocação
└── Sou Gestor de Unidade
    ├── Visão geral do papel
    ├── Dashboard e KPIs
    ├── Aprovar Planos de Entregas
    └── Painel de Conformidade
```

> **Admin:** não recebe seção própria na v1 — as páginas técnicas podem vir depois.

### Padrão por página de guia

Cada guia de tarefa segue este template:

```
## [Nome da Tarefa]

> **Antes de começar:** [pré-condição em 1 linha]

### Passo a passo

1. Acesse **Menu → Seção**
2. Clique em **Botão**
3. Preencha [campo] com [o quê]
4. Confirme com **Salvar**

!!! tip "Referência rápida"
    | Ação | Onde encontrar |
    |---|---|
    | Registrar execução | Meu Plano → Registrar |

!!! warning "O que fazer se..."
    Se [situação de erro], [solução].
```

---

## 3. Mapa de conteúdo — páginas a criar

| Página | Arquivo | Conteúdo base |
|---|---|---|
| Home | `docs/index.md` | Novo (product-brief.md como referência) |
| O que é o PGD Libre | `docs/sobre/pgd-libre.md` | Novo (product-brief.md) |
| O Programa de Gestão | `docs/conceitos/programa.md` | Novo |
| Papéis e responsabilidades | `docs/conceitos/papeis.md` | Novo |
| Glossário | `docs/conceitos/glossario.md` | Novo |
| Como acessar a demo | `docs/demo/acesso.md` | jornadas-demo.md (intro) |
| Jornada: Servidor | `docs/demo/jornada-servidor.md` | jornadas-demo.md (Jornadas 1–2) |
| Jornada: Chefia | `docs/demo/jornada-chefia.md` | jornadas-demo.md (Jornadas 3–6) |
| Jornada: Gestor e Admin | `docs/demo/jornada-gestor.md` | jornadas-demo.md (Jornadas 7–9) |
| Visão geral: Servidor | `docs/servidor/visao-geral.md` | Novo |
| Meu Plano de Trabalho | `docs/servidor/meu-plano.md` | Novo |
| Registrar Execução | `docs/servidor/registrar-execucao.md` | jornadas-demo.md (Jornada 1) |
| Referência rápida: Servidor | `docs/servidor/referencia-rapida.md` | Novo |
| Minhas Avaliações | `docs/servidor/avaliacoes.md` | Novo |
| Contestar Avaliação | `docs/servidor/contestar-avaliacao.md` | jornadas-demo.md (Jornada 2) |
| Visão geral: Chefia | `docs/chefia/visao-geral.md` | Novo |
| Minha Equipe | `docs/chefia/minha-equipe.md` | Novo |
| Avaliar Registros | `docs/chefia/avaliar-registros.md` | jornadas-demo.md (Jornada 3) |
| Referência rápida: Chefia | `docs/chefia/referencia-rapida.md` | Novo |
| Responder Recurso | `docs/chefia/responder-recurso.md` | jornadas-demo.md (Jornada 4) |
| Criar Plano de Trabalho | `docs/chefia/criar-plano.md` | jornadas-demo.md (Jornada 5) |
| Emitir Convocação | `docs/chefia/emitir-convocacao.md` | jornadas-demo.md (Jornada 6) |
| Visão geral: Gestor | `docs/gestor/visao-geral.md` | Novo |
| Dashboard e KPIs | `docs/gestor/dashboard.md` | Novo |
| Aprovar Planos de Entregas | `docs/gestor/aprovar-planos.md` | jornadas-demo.md (Jornada 7) |
| Painel de Conformidade | `docs/gestor/conformidade.md` | jornadas-demo.md (Jornada 8–9) |

**Total:** ~25 páginas. As marcadas "jornadas-demo.md" são reescrituras com tom amigável do conteúdo existente.

---

## 4. Ordem de implementação

1. **Infraestrutura** (git init, mkdocs.yml, pyproject.toml, .github/workflows/docs.yml, .gitignore)
2. **Scaffold de arquivos** (criar todos os `.md` com título e placeholder)
3. **Home + Sobre + Conceitos** (páginas que independem do sistema estar no ar)
4. **Seção Demo** (migrar e reescrever jornadas-demo.md nas 4 páginas)
5. **Seções por papel** — Servidor → Chefia → Gestor (ordem de complexidade crescente)
6. **Referências rápidas** (sintetizar após ter os tutoriais prontos)
7. **Deploy** (configurar GitHub Pages no repo, testar CI)

---

## 5. Verificação

- `poetry run mkdocs serve` → navegar localmente em `http://127.0.0.1:8000`
- Checar: todas as páginas do nav carregam sem 404
- Checar: busca funciona com termos em português ("registro", "plano", "avaliação")
- Checar: CI/CD constrói e deploya corretamente após push para main
- Checar: URL pública do GitHub Pages responde

---

## Arquivos a criar

| Arquivo | Local |
|---|---|
| `mkdocs.yml` | `pgdgovbr/docs/` |
| `pyproject.toml` | `pgdgovbr/docs/` |
| `.github/workflows/docs.yml` | `pgdgovbr/docs/` |
| `.gitignore` | `pgdgovbr/docs/` |
| `docs/index.md` | `pgdgovbr/docs/` |
| ~25 páginas de conteúdo | `pgdgovbr/docs/docs/**` |
