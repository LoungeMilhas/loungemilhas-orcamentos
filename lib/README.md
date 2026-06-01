# lib/

Camada de acesso a dados e utilitarios (server-side). Estrutura prevista para a Fase 1:

- `lib/supabase/` — clientes Supabase: `anon` (rota publica), sessao do consultor (admin) e `service_role` (jobs).
- `lib/branding/` — carregamento da identidade visual (tabela `marca`) e snapshot por proposta.
- `lib/slug.*` — geracao do slug oficial `{cliente}-{destino}-{mes}-{ano}-v{versao}` (slugify, desambiguacao de homonimos, slugs reservados).
- repositorios: `clientes`, `negociacoes`, `orcamentos`, `itens`, `imagens`, `sugestoes`, `eventos`, `anexos`.

Vazio nesta etapa (Etapa 0). Implementacao na Etapa 1 (camada 1C do Plano Definitivo).
