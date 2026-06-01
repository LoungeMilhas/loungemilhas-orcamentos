# supabase/

Schema versionado via **Supabase CLI**. Regra: schema so muda por migration versionada
(`supabase/migrations`), aplicada em **DEV -> validar -> PROD**. Nunca editar pelo painel.

## Ambientes (decisao #16 do Plano Definitivo)
- **DEV**: projeto Supabase de desenvolvimento.
- **PROD**: projeto Supabase de producao.

## Migrations planejadas (Etapa 1 - ainda NAO criadas)
- M001 base: extensoes (pgcrypto, pg_cron) + enums + `set_updated_at` + `is_admin`
- M002 atores: `consultores` -> `clientes`
- M003 reuso: `templates`, `marca`
- M004 nucleo: `negociacoes` -> `orcamentos` (+ FK tardia `versao_ativa_id`)
- M005 versao: funcao `reservar_versao`
- M006 filhos: `orcamento_itens` -> `orcamento_sugestoes` -> `orcamento_imagens` -> `orcamento_eventos`
- M007 prints: `orcamento_anexos` -> `extracoes`
- M008 integracoes: `lugares` -> `places_cache` (vazias)
- M009 indices
- M010 RLS (multi-tenant + leitura anon de publicados)
- M011 cron: pg_cron de expiracao diaria
- M012 seed: admin + template Premium + marca inicial

## Setup (a executar quando os projetos DEV/PROD existirem)
1. `supabase login`
2. `supabase init` (gera config local)
3. `supabase link --project-ref <ref-do-DEV>`
4. criar migrations da Etapa 1 e aplicar com `supabase db push` em DEV; depois promover a PROD.
