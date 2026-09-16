# Site — Indiara de Lima · Psicóloga Clínica

Site estático (HTML/CSS/JS puro), sem build. Feito para hospedagem no Cloudflare Pages,
seguindo o guia [CLAUDE-NOVO-SITE.md](CLAUDE-NOVO-SITE.md).

## Estrutura

| Arquivo | Página |
|---|---|
| `index.html` | Início |
| `sobre.html` | Sobre |
| `servicos.html` | Serviços |
| `blog.html` | Blog (lista) |
| `quando-quem-sempre-deu-conta.html` | Artigo de exemplo do blog |
| `contato.html` | Contato (com mapa e orientação de crise) |
| `politica-de-privacidade.html` | Política de privacidade (LGPD) |

Os arquivos continuam com extensão `.html` no repositório, mas **as URLs públicas do site não
usam `.html`** (ex: `indiaradelima.com.br/sobre`, não `/sobre.html`). O projeto Cloudflare (tipo
"Workers com assets") serve `pagina.html` também em `/pagina` automaticamente — todos os links
internos, `canonical`, `og:url`, schema.org e `sitemap.xml` já usam a versão sem extensão.
| `css/style.css` | Todo o estilo + design system |
| `js/main.js` | Menu mobile, header ao rolar, animações de entrada |
| `assets/favicon.svg` | Ícone (símbolo do olho, azul/dourado) |
| `_headers` | CSP e cabeçalhos de segurança (Cloudflare) |
| `robots.txt` / `sitemap.xml` | SEO |

## Identidade aplicada

- **Cores da marca:** azul `#004169`, dourado claro `#cbbaa1`, branco. Fundo claro e sóbrio.
- **Tipografia:** Cormorant Garamond (títulos) + Outfit (texto), via Google Fonts.
- **Assinatura:** “Aqui, a escuta tem fundamento.” / frase-mãe na faixa após o hero.
- Textos redigidos a partir do material da cliente (dossiê de marca, ficha do paciente ideal,
  mapa de identidade). Tom sério, humano, sem promessas nem fórmulas.

## Dados já embutidos

- CRP 16/11211
- WhatsApp `5527995895080` — botões usam `api.whatsapp.com` (nunca `wa.me`)
- Instagram `https://www.instagram.com/indiaradelima`
- Endereço presencial: UMEDIC - Ed. Laguna Center, Torre A, 4º andar, salas 415/416 · Av. Presidente Vargas, 1220, Centro, Linhares - ES, 29900-215

## PENDENTE — substituir antes de publicar

Procure por `TODO` no código. Itens:

1. **Foto do hero** — `assets/indiara-inicio.webp` (retrato de corpo inteiro, fundo neutro, ~896x1200).
   Descomente o `<img>` em `index.html` e remova o `.img-placeholder`.
2. **Foto “Sobre”** — `assets/indiara-sobre.webp` (~843x1264). Em `index.html` e `sobre.html`.
3. ~~**Link do Google Meu Negócio**~~ — ✅ feito. `https://share.google/wh8gy0sHujxC8as4N` aplicado
   no botão “Avaliações do Google” em `index.html` (hero) e `contato.html`.
4. ~~**Domínio**~~ — ✅ no ar. `indiaradelima.com.br` propagado e servindo o site direto (Cloudflare
   Workers/Pages + redirect `www` → apex configurado). Falta só conferir HTTPS (Universal SSL,
   "Always Use HTTPS", modo Full/Full strict) em SSL/TLS no painel do domínio.
5. ~~**Gmail da cliente**~~ — ✅ recebido: `psiindiaradelima@gmail.com`. Usar para criar o
   repositório GitHub e a conta Cloudflare Pages em nome dela. (Não coloquei como e-mail público
   no site — o dossiê de marca define o WhatsApp/secretária como único canal de contato; avise se
   quiser exibi-lo também em `contato.html` ou no schema.org.)
6. **Logo oficial** — se houver arquivo do símbolo/wordmark da marca, substituir o SVG do olho
   feito à mão (no `<header>`, `<footer>` e `assets/favicon.svg`).
7. **Analytics (opcional)** — o `_headers` já libera o Google Tag Manager. Se for usar, colar o
   snippet do GTM/GA4 em todas as páginas.
8. **Artigos do blog** — 1 artigo pronto; os outros 3 estão marcados “Em breve” em `blog.html`.
9. **Imagens dos artigos** — cada card do blog (em `blog.html` e no bloco “Do blog” da `index.html`)
   e a capa do artigo têm um campo de foto com placeholder. Colocar os arquivos em
   `assets/blog/` (ex.: `quem-sempre-deu-conta.webp`) e descomentar o `<img>` correspondente.
   Proporções sugeridas: card da lista 4:3, card da home 3:2, capa do artigo 16:9.

## Rodar localmente

```bash
python -m http.server 4173
```

Depois abrir `http://localhost:4173`. (No editor, o preview usa `.claude/launch.json`.)

## Deploy (resumo)

1. Criar repositório GitHub em nome da cliente e fazer push.
2. Cloudflare Pages → conectar ao repositório · sem framework · pasta raiz `/`.
3. Adicionar domínio customizado e apontar os nameservers no registro.br.
4. Conferir se o `_headers` foi aplicado (aba Network → resposta com `Content-Security-Policy`).

## Observações

- Ao editar `css/style.css` ou `js/main.js`, os `<link>`/`<script>` usam `?v=4`. Suba o número
  ao publicar mudanças para furar cache (ou deixe o Cloudflare cuidar disso).
- `contato.html` e o rodapé trazem orientação de crise (CVV 188, SAMU 192) — coerente com o
  posicionamento da marca em suicidologia. Não remover.
