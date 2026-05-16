# Como acessar a demo

A instância de demonstração do PGD Libre já vem com dados pré-configurados para que você explore todas as funcionalidades sem precisar instalar nada.

## URL da demo

Acesse: **`http://localhost:5173`** (instância local) ou o endereço da instância pública, se disponível.

## Usuários disponíveis

A demo tem 9 usuários pré-criados, um para cada papel e situação interessante:

| Nome | E-mail | Papel | Situação na demo |
|---|---|---|---|
| Ana Silva | `servidor1@pgd-demo.gov.br` | Servidor | Plano ativo; recurso em aberto |
| João Santos | `servidor2@pgd-demo.gov.br` | Servidor | Registro aguardando avaliação; convocação pendente |
| Carla Mendes | `servidor3@pgd-demo.gov.br` | Servidor | Avaliação nota 2 (alto desempenho); afastamento encerrado |
| Lucas Ramos | `servidor4@pgd-demo.gov.br` | Servidor | Sem Plano de Trabalho (a chefia pode criar) |
| Pedro Alves | `servidor5@pgd-demo.gov.br` | Servidor | CGTI; erros de sync com a API Central |
| Carlos Souza | `chefe1@pgd-demo.gov.br` | Chefia | CGPGD; recurso e avaliação pendentes |
| Beatriz Lima | `chefe2@pgd-demo.gov.br` | Chefia | CGTI; Plano de Entregas aguardando aprovação |
| Maria Fernanda | `gestor@pgd-demo.gov.br` | Gestor | Pode aprovar o Plano de Entregas da CGTI |
| Roberto Admin | `admin@pgd-demo.gov.br` | Admin | Vê erros de sync de Pedro |

## Como fazer login

A demo usa um endpoint de acesso rápido que dispensa senha:

1. Abra o terminal (ou qualquer ferramenta de requisição HTTP)
2. Faça uma requisição POST para o backend:

```
POST http://localhost:8000/auth/dev-login?email=<EMAIL>&name=<NOME>&role=<PAPEL>
```

**Exemplo — login como Ana Silva (servidor):**
```bash
curl -X POST "http://localhost:8000/auth/dev-login?email=servidor1@pgd-demo.gov.br&name=Ana%20Silva&role=servidor" \
  -c cookies.txt -b cookies.txt
```

Depois de fazer o POST, acesse `http://localhost:5173` — você já estará autenticado.

!!! tip "Página de login rápido"
    Se a demo tiver a página de acesso rápido habilitada, você verá botões diretamente no navegador para cada persona. Basta clicar.

## Organização fictícia da demo

```
MGI — Ministério da Gestão e da Inovação
  └── SEGES — Secretaria de Gestão e Inovação
        ├── CGPGD (chefia: Carlos Souza)
        │     ├── Ana Silva      — Teletrabalho Parcial
        │     ├── João Santos    — Teletrabalho Integral
        │     ├── Carla Mendes   — Presencial
        │     └── Lucas Ramos    — Teletrabalho Parcial (sem plano)
        └── CGTI (chefia: Beatriz Lima)
              └── Pedro Alves    — Teletrabalho Parcial
```

## Prazos sempre atualizados

O script de seed recalcula todas as datas em relação ao dia atual, então os prazos nunca expiram. O recurso de Ana sempre tem 7 dias restantes, o período de registro está sempre aberto.

## Próximos passos

Escolha a jornada que quer explorar:

- [Jornada do Servidor →](jornada-servidor.md)
- [Jornada da Chefia →](jornada-chefia.md)
- [Jornada do Gestor e Admin →](jornada-gestor.md)
