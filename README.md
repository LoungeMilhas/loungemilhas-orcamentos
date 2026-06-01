# Lounge Milhas — Orçamentos

Plataforma de geração de orçamentos da Lounge Milhas. O orçamento deixa de ser uma página
programada e passa a ser **dado** renderizado por rota dinâmica, criado por consultores via
painel administrativo e publicado em uma **URL pública versionada**.

> Stack: **Next.js 16 (App Router)** · **Supabase** (Postgres + Auth + Storage) · **Vercel**.

## Status

Em desenvolvimento — **Fase 1**. Esta etapa (Etapa 0) entregou a fundação técnica do
repositório; o schema do banco e o painel são implementados na Etapa 1.

## Requisitos

- Node.js 18+ (recomendado LTS)
- Conta Supabase (projetos **DEV** e **PROD** separados)
- Conta Vercel (deploy)

## Setup local

```bash
npm install            # instala dependências (versões fixas via package-lock.json)
cp .env.example .env.local   # preencha com as chaves do Supabase DEV
npm run dev            # http://localhost:3000
```

### Variáveis de ambiente

Veja `.env.example`. Em desenvolvimento use o projeto Supabase **DEV**; em produção, o **PROD**
(configuradas na Vercel por ambiente). Segredos (`SUPABASE_SERVICE_ROLE_KEY`, `CRON_SECRET`,
`ORCAMENTO_SHARE_SECRET`) são **server-side** e nunca devem ir ao browser.

## Scripts

| Comando | Descrição |
|---|---|
| `npm run dev` | Servidor de desenvolvimento (Turbopack) em `localhost:3000` |
| `npm run build` | Build de produção |
| `npm start` | Serve o build de produção |

## Estrutura

```
app/            rotas (App Router) — página pública [slug] + /admin (Etapa 1)
components/     UI reutilizável + blocos do orçamento (Etapa 1)
lib/            acesso a dados, Supabase, geração de slug, marca (Etapa 1)
public/         assets estáticos
supabase/       migrations versionadas (Supabase CLI) — ver supabase/README.md
```

## Estilização

**Tailwind CSS v4** (config CSS-first em `app/globals.css`, plugin em `postcss.config.mjs`).
A identidade visual oficial (logo, paleta, tipografia) é aplicada automaticamente via tabela
`marca` + bucket `marca` no Storage. As cores atuais em `globals.css` são **placeholders** até
o brand kit oficial ser fornecido.

## Padrão de URL pública (oficial)

```
orcamentos.loungemilhas.com.br/{cliente}-{destino}-{mes}-{ano}-v{versao}
ex.: fabriciaraposo-recife-junho-2026-v1
```

Slug determinístico e imutável após publicação; versionamento por negociação; proteção
server-side (handshake por cookie HttpOnly + rate-limit + noindex). Detalhes no Documento
Mestre de Arquitetura.
