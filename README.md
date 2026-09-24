# yuri-links

Página de links (estilo Linktree) do Yuri Reis, na identidade visual da página da Imersão Comercial: marinho `#0B0A2E`, azul de ação `#0071BC`, Plus Jakarta Sans + Inter, corte diagonal de 2,5° com a perfuração de bilhete.

Um arquivo, sem build, sem JavaScript. Fontes auto-hospedadas: a página não depende do Google Fonts.

## Editar

- **Links:** `index.html`, procure por `LINK 1`, `LINK 2`, `LINK 3`.
- **Foto do cabeçalho:** `img/yuri.jpg` + `img/yuri.webp` (1000x1250). Para trocar:
  ```bash
  magick <foto-nova> -resize 1000x1250^ -gravity north -extent 1000x1250 -strip -quality 86 img/yuri.jpg && cwebp -q 82 img/yuri.jpg -o img/yuri.webp
  ```
  O enquadramento fino fica no CSS, em `.topo__foto img { object-position }`.
- **Preview de link (WhatsApp, Instagram):** `img/og.jpg` sai de `og.html`. Para regerar, abra `og.html` em 1200x630 e capture a tela.

## Antes de publicar

1. Trocar os três `href="#"` pelos destinos reais.
2. Escrever a linha do Inlead (está com `[A PREENCHER]`).
3. Trocar `https://EXEMPLO.com.br/` pelo domínio final no `<link rel="canonical">` e nas metatags `og:` — sem URL absoluta o WhatsApp entrega o link sem imagem.

## Medição

Lighthouse mobile (`--throttling-method=devtools`): performance 99, acessibilidade 100, boas práticas 100, SEO 100.
