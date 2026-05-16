# O que é o PGD Libre

O **PGD Libre** é uma plataforma de gestão do [Programa de Gestão e Desempenho](../conceitos/programa.md) desenvolvida como software livre para o serviço público federal brasileiro.

## O problema que resolve

Muitos órgãos gerenciam o PGD em planilhas Excel, e-mails ou sistemas internos sem integração — o que gera:

- Prazos de registro perdidos por falta de alertas
- Avaliações sem rastreabilidade (quem avaliou o quê, quando)
- Dificuldade de sincronização com a **API PGD Central** do MGI
- Falta de visibilidade para gestores e chefias

## O que o PGD Libre oferece

| Funcionalidade | O que você ganha |
|---|---|
| **Planos de trabalho** | Criação guiada com wizard passo a passo, com pactuação bilateral — servidor propõe, chefia revisa e assina |
| **Registro de execução** | Servidor registra mensalmente; prazo automático |
| **Avaliação e recurso** | Fluxo completo: nota 1–5, contestação, prazo legal |
| **Gestão de equipe** | Chefe vê KPIs da equipe em tempo real |
| **Conformidade** | Painel de sincronização com a API Central do MGI |
| **Multi-tenant** | Um sistema para múltiplos órgãos, com isolamento de dados |

## Base legal

O PGD Libre implementa integralmente os requisitos do marco normativo:

- **Decreto 11.072/2022** — institui o Programa de Gestão e Desempenho
- **IN SEGES/MGI nº 24/2023** — regulamenta o teletrabalho e o PGD
- **IN SEGES/MGI nº 52/2023** — atualiza critérios e procedimentos

## Stack tecnológico

- **Backend:** FastAPI + Strawberry GraphQL + PostgreSQL
- **Frontend:** SvelteKit + SSR
- **Infraestrutura:** Docker / Cloud Run (GCP)
- **Autenticação:** Google OAuth / Gov.br OIDC
- **Licença:** MIT (código aberto e gratuito)

## Quer explorar o sistema?

[Acesse a instância de demo →](../demo/acesso.md)
