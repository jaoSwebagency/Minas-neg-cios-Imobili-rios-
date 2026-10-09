# Minas Negócios Imobiliários — site

React + TypeScript + Vite + Tailwind CSS v4 + GSAP/ScrollTrigger + Lucide.

## Rodar

```bash
npm install
cp .env.example .env   # preencha com os dados REAIS da imobiliária
npm run dev            # desenvolvimento
npm run build          # typecheck + build de produção
npm run preview
```

> Em hospedagem estática, configure o fallback de SPA (todas as rotas → `index.html`).

## O que já funciona

- Home: hero animado, busca (finalidade, bairro, tipo, preço), diferenciais, carrossel de destaques
  (setas, indicadores, gesto de arrastar no celular), sobre, chamada para ação, contato, rodapé.
- `/imoveis`: filtros reais via URL (`?finalidade=&local=&tipo=&preco=&ordem=&lancamento=1&favoritos=1`),
  ordenação, "carregar mais", estados de carregamento / vazio / erro, limpar filtros.
- `/imovel/:slug`: galeria com miniaturas, dados, características, WhatsApp contextual, formulário.
- Favoritos salvos no navegador (localStorage), contador no cabeçalho.
- SEO por página (título, descrição, Open Graph, JSON-LD), semântica, foco visível, `prefers-reduced-motion`.
- Animações GSAP: `src/lib/gsap.ts` (registro do ScrollTrigger), `src/hooks/useReveal.ts` (reveals
  por `data-reveal`), timeline da hero, parallax só ≥768px. Tudo com `gsap.matchMedia()` e `revert()`
  na desmontagem; sem JS ou com movimento reduzido, o conteúdo fica visível.

## Dados que ainda precisam ser informados (nada foi inventado)

| O quê | Onde |
|---|---|
| WhatsApp, telefone, e-mail, endereço, horário, cidade | `.env` (`VITE_*`) |
| Imóveis reais | `src/data/properties.ts` (hoje são `DEMO-xxx`, marcados "Imagem demonstrativa") ou `src/lib/api.ts` p/ Supabase |
| Endpoint do formulário (opcional) | `VITE_FORM_ENDPOINT` |
| Política de privacidade e termos | `src/pages/Legal.tsx` (texto provisório) |
| Fotos reais | trocar as URLs do Unsplash (hero, sobre, CTA, imóveis) |

Sem WhatsApp nem endpoint configurados, o formulário **avisa que não enviou** (não finge sucesso) e os
botões de WhatsApp levam ao formulário de contato.

## Não implementado

- Painel administrativo / Supabase (a camada `src/lib/api.ts` está pronta para receber a troca).
- Mapa no detalhe do imóvel (os dados demonstrativos não têm coordenadas).
- Logo: recortada de uma captura de tela (`public/logo.png`, ~460 px). Troque pelo arquivo original em
  alta resolução (de preferência SVG/PNG transparente) assim que o cliente enviar.
