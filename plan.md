# Personalização do portfólio — plano de implementação

## Resumo

Base atual: Astro 7, Bento grid, SSR/Netlify, com recursos de Blog, Guestbook, Playground, mapa de viagens, temas, sons e animações de template.

Resultado alvo desta versão:

- PT-BR somente na home `/`.
- Home em tela cheia, mantendo Bento grid.
- Apenas GitHub e LinkedIn como links sociais.
- Projetos apresentados em um card resumido na home, sem imagens nesta fase.
- Dark mode atual + white mode baseado no estilo Paper.
- Accent fixo `#f4dbd6`.
- Sem Blog, Guestbook, Playground, países visitados, sons, avatar ou temas extras.
- Umami preparado por variável de ambiente; Ahrefs removido.

A internacionalização (inglês em `/en`) fica explicitamente adiada para a próxima versão.

Astro cria rotas a partir de `src/pages`; exclusões dessas páginas eliminam as URLs antigas. A configuração nativa de i18n suporta PT-BR sem prefixo e inglês em `/en`. [Routing](https://docs.astro.build/en/guides/routing/), [i18n](https://docs.astro.build/en/guides/internationalization/).

## Etapa 1 — Remover cards e efeitos da home ✅ Concluída

**Objetivo:** deixar a home somente com cards que permanecerão.

**Escopo / especificação:** remoção exclusiva, sem redesenho.

**Arquivos ou áreas provavelmente afetados:** `src/pages/index.astro`.

**ToDos:**

- Remover cards e links de Playground, Guestbook, Blog, Countries I Visited e seletor de accent.
- Remover imports de `Globe`, `ThemeChangeCard` e referências associadas.
- Remover scripts inline usados somente pelos fundos animados de Playground, Guestbook e Blog.
- Preservar Welcome, Stack & Tools, contato, timezone, Projects, Now e rodapé.
- Manter animação de entrada global dos cards; somente animações/efeitos dos cards removidos saem nesta etapa.

**Dependências de etapas anteriores:** nenhuma.

## Etapa 2 — Remover recursos, rotas e lógica obsoletos ✅ Concluída

**Objetivo:** eliminar toda funcionalidade fora do escopo, sem redirecionar URLs antigas.

**Escopo / especificação:** todas as URLs removidas passam a retornar 404.

**Arquivos ou áreas provavelmente afetados:** `src/pages/`, `src/components/`, `src/lib/`, `src/data/`, `src/assets/`.

**ToDos:**

- Excluir `src/pages/playground/**`, `src/components/playground/**`, `PlaygroundShell`, animação Rive, utilitários exclusivos e assets públicos do Playground.
- Excluir páginas e componentes do Guestbook, endpoints `/api/guestbook` e `/api/reactions`, `db.ts` e `guestbook.ts`.
- Excluir Blog, posts Markdown, coleção de conteúdo, `LayoutBlogPost`, cálculo de leitura e `/rss.xml`.
- Excluir `travel.astro`, `Globe.tsx` e `world.json`.
- Excluir galeria antiga `design-works.astro`, `illustrations.ts` e ilustrações do template; o card Projects será criado depois na home.
- Remover avatar do Welcome, `Tooltip`, assets de avatar e toda lógica relacionada.
- Remover botão “Book a call”, integração Cal.com e campos `SITE.cal`.
- Remover sons do botão global, seletor de temas e `PixelHeart`; o coração visual pode permanecer estático no rodapé.
- Remover links Medium, Dribbble e Behance, incluindo referências quebradas a `dribbble`.

**Dependências de etapas anteriores:** Etapa 1.

## Etapa 3 — Limpar dependências, estilos e assets de template ✅ Concluída

**Objetivo:** reduzir a base antes de adicionar recursos novos.

**Escopo / especificação:** remoção exclusiva de pacotes, integrações, estilos e arquivos sem uso após Etapa 2.

**Arquivos ou áreas provavelmente afetados:** `package.json`, `pnpm-lock.yaml`, `astro.config.mjs`, `uno.config.ts`, `src/style.css`, `public/`.

**ToDos:**

- Remover integrações Astro de Solid, Svelte e Markdown Remark.
- Remover dependências exclusivas removidas: banco libSQL/Drizzle, D3, Rive, Solid, Svelte, Lenis, Tweakpane, RSS, MarkdownIt, sanitize-html, reading-time e tipos D3.
- Preservar Astro, UnoCSS, `astro-icon`, Motion, GSAP, Netlify, sitemap e robots.
- Remover variantes Glass, Sharp e Neon, seletor antigo `StylePanel`, estado `cardBorder`, `portfolioStyle` e seus scripts.
- Remover paletas alternativas yellow, green, blue e purple, além de `ThemeChangeCard`.
- Remover Ahrefs; manter somente preparação para Umami.
- Remover assets públicos exclusivos do Playground e `preview.png` do template após atualizar README.
- Não remover favicon, Open Graph ou ícones PWA ainda: serão substituídos por assets pessoais na Etapa 6.

**Dependências de etapas anteriores:** Etapa 2.

## Etapa 4 — Criar card Projects e preencher conteúdo pessoal ✅ Concluída com placeholders

**Objetivo:** substituir Design Works por um card resumido de Projects na home, deixando o conteúdo pessoal pronto para edição manual posterior.

**Escopo / especificação:**

- Projects será um card da tela inicial, seguindo o padrão visual dos demais cards.
- O card exibe quatro projetos resumidos, sem página separada nesta versão.
- Cada projeto possui título, resumo curto, tecnologias e um link externo individual.
- Os quatro projetos usam textos Lorem Ipsum e links temporários para `example.com`.
- Sem imagens ou logos de tecnologias nesta primeira versão.
- Os dados permanecem definidos localmente no componente, sem coleção, CMS ou arquivo exclusivo de projetos.

**Arquivos ou áreas afetados:** `src/components/DesignWorksCard.astro`.

**ToDos:**

- [x] Adaptar card existente de Design Works para “Projects” dentro da home.
- [x] Renderizar quatro projetos resumidos com links externos seguros (`target="_blank"` e `rel="noopener noreferrer"`).
- [x] Preservar os conteúdos atuais de Welcome, Stack & Tools, contato, timezone e Now para edição manual posterior.
- [x] Manter card de copyright sem áudio.

**Dependências de etapas anteriores:** Etapa 3.

**Pendências para substituir os placeholders:**

- Substituir títulos, resumos, tecnologias e links `example.com` pelos dados reais dos quatro projetos.
- Revisar manualmente os textos atuais de Welcome, Stack & Tools, contato, timezone e Now.

## Etapa 5 — Implementar dark/white mode e accent fixo ✅ Concluída

**Objetivo:** substituir painel de estilos por alternância simples e persistente.

**Escopo / especificação:**

- Dark mode: aparência padrão atual.
- White mode: variante Paper atual.
- Adicionar um card de controles na home com dois botões: modo dark/light e idioma.
- O botão de idioma será apenas visual/desabilitado nesta etapa; sua funcionalidade fica para a próxima versão.
- Preferência persistida em `localStorage` sob chave nova, por exemplo `portfolioMode`.
- Sem sons, painel expansível, variantes extras ou seleção de borda.

**Arquivos ou áreas provavelmente afetados:** novo card/componente de controles, `BasicLayout.astro`, `GridTransition.astro`, `style.css` e composição da home.

**ToDos:**

- Criar card com dois botões acessíveis e labels claros; somente o botão dark/light deve ser funcional.
- Manter o botão de idioma visível, porém desabilitado ou marcado como indisponível até a etapa de i18n.
- Aplicar preferência antes da pintura da página e durante navegação via `ClientRouter`.
- Usar `style-paper` somente para white mode; remover a moldura nine-slice do projeto e manter cards simples nos dois modos.
- Fixar `#f4dbd6` como accent central e definir escala `primary` estável derivada dela.
- Garantir que accent não seja usado como texto principal no white mode; texto deve manter contraste suficiente.
- Simplificar `GridTransition` para reconhecer somente os dois modos.
- Remover qualquer leitura dos estados antigos de tema, estilo ou borda.

**Dependências de etapas anteriores:** Etapas 3 e 4.

## Etapa 6 — Reorganizar grid, metadados e identidade pública

**Objetivo:** concluir aparência full-screen e remover identidade residual do template.

**Escopo / especificação:**

- Manter Bento grid de quatro colunas e oito linhas em desktop.
- Reorganização desktop: Welcome ocupa 3×4; Stack 1×8; contato 1×4; timezone, Projects, Now e rodapé ocupam os espaços restantes em blocos 1×2.
- Mobile e tablet continuam responsivos; sem espaços vazios relevantes.

**Arquivos ou áreas provavelmente afetados:** composição de home, `site-config.ts`, `astro.config.mjs`, `BasicLayout.astro`, `public/site.webmanifest`, assets PWA/SEO e `README.md`.

**ToDos:**

- Ajustar spans e ordem dos cards para preencher a viewport desktop sem cards removidos.
- Limpar `site-config.ts` para conter apenas dados usados: identidade, localização, GitHub, LinkedIn e URLs do site.
- Remover textos, palavras-chave, console messages e metadados herdados de Gianmarco/template.
- Corrigir fallback de `SITE_URL` para domínio pessoal.
- Tornar Umami condicional a `UMAMI_WEBSITE_ID`; não carregar script quando variável estiver ausente.
- Atualizar manifest, Apple title, favicon, ícones PWA e OG image com identidade pessoal.
- Reescrever README para refletir funcionalidades remanescentes, rotas atuais, modo dark/white e configuração opcional de Umami.

**Dependências de etapas anteriores:** Etapas 4 e 5.

**Entradas necessárias antes desta etapa:**

- Favicon, ícones PWA e imagem Open Graph pessoais.
- Textos SEO PT-BR aprovados.
- ID do Umami, quando houver.

## Etapa 7 — Verificação final

**Objetivo:** validar remoções, rotas, responsividade, acessibilidade e build.

**Escopo / especificação:** nenhuma funcionalidade nova.

**Arquivos ou áreas provavelmente afetados:** testes manuais e comandos de validação.

**ToDos:**

- Executar `pnpm check`, `pnpm eslint` e `pnpm build`.
- Confirmar que build não exige credenciais Turso ou arquivos removidos.
- Validar `/` e o card Projects na home.
- Confirmar 404 para `/playground`, `/guestbook`, `/blog`, `/travel`, `/design-works`, `/rss.xml` e APIs do Guestbook.
- Testar alternador dark/white, persistência entre navegações e navegação por teclado.
- Validar links GitHub/LinkedIn, timezone e todos links de projetos.
- Conferir home em mobile, tablet e desktop full-screen.
- Revisar contraste e foco visível em ambos modos.
- Executar busca final por referências a recursos removidos, nome do template, Ahrefs, Cal.com, Turso e dependências eliminadas.

**Dependências de etapas anteriores:** Etapa 6.

## Etapa 8 — Internacionalização mínima (próxima versão)

**Status:** adiada; não faz parte da versão atual.

**Objetivo:** suportar PT-BR e inglês sem duplicar componentes ou conteúdo.

**Escopo / especificação:**

- Locale padrão: `pt-br`.
- Rota PT-BR: `/`.
- Rota inglesa: `/en`.
- Sem i18n por domínio, CMS ou coleção Markdown.

**Arquivos ou áreas provavelmente afetados:** `astro.config.mjs`, `src/pages/index.astro`, `src/pages/en/`, novo módulo local de i18n e componentes de página reutilizáveis.

**ToDos:**

- Configurar `locales: ["pt-br", "en"]`, `defaultLocale: "pt-br"` e `prefixDefaultLocale: false`.
- Criar tipo interno `Locale` e mapa tipado de conteúdo PT-BR/EN.
- Mover apenas a composição reutilizável de home e projetos para componentes compartilhados; rotas devem ser wrappers mínimos por locale.
- Adaptar componentes existentes para receber cópia localizada, sem criar sistema genérico de CMS.
- Ativar o botão de idioma no card de controles; links devem trocar para a rota equivalente.
- Ajustar `<html lang>`, títulos, descrições e labels acessíveis por locale.

**Dependências de etapas anteriores:** Etapa 7 da versão atual.

## Interfaces e decisões fixadas

- Rota pública desta versão: `/`.
- Rotas removidas não terão redirecionamento.
- Interface interna nesta versão: conteúdo local em PT-BR; o tipo `Locale = "pt-br" | "en"` será introduzido na próxima versão.
- Não haverá banco, endpoints, Blog, RSS, Playground, mapa, sons, avatar ou logos de stack nesta fase.
- O repositório já possui alterações locais não relacionadas em `.github/FUNDING.yml`, `AGENTS.md` e no plano inicial; elas devem ser preservadas.
