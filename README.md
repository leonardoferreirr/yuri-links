# yuri-links

Página de links (estilo Linktree) do Yuri Reis, na identidade visual da página da Imersão Comercial: marinho `#0B0A2E`, azul de ação `#0071BC`, Plus Jakarta Sans + Inter, corte diagonal de 2,5° com a perfuração de bilhete.

Um arquivo, sem build, sem JavaScript. Fontes auto-hospedadas: a página não depende do Google Fonts.

## Os três links

| Cartão | Destino |
| --- | --- |
| Falar com o escritório | `wa.me/5535997720153` com mensagem pronta sobre contabilidade |
| Formulário de aplicação | `quiz.carteira360.com.br` |
| Convidar para palestrar | `wa.me/5535997720153` com mensagem pronta sobre palestra |

Os dois cartões de WhatsApp caem no mesmo número, então cada um leva uma mensagem pronta diferente: é o que diz ao Yuri, na primeira linha da conversa, por qual porta a pessoa entrou. Para tirar, apague tudo a partir do `?` no `href`.

## Editar

- **Links:** `index.html`, procure por `LINK 1`, `LINK 2`, `LINK 3`.
- **Foto do cabeçalho:** `img/yuri.jpg` + `img/yuri.webp` (1000x1250). Para trocar:
  ```bash
  magick <foto-nova> -resize 1000x1250^ -gravity north -extent 1000x1250 -strip -quality 86 img/yuri.jpg && cwebp -q 82 img/yuri.jpg -o img/yuri.webp
  ```
  O enquadramento fino fica no CSS, em `.topo__foto img { object-position }`.
- **Preview de link (WhatsApp, Instagram):** `img/og.jpg` sai de `og.html`. Para regerar, abra `og.html` em 1200x630 e capture a tela.

## Pendências

1. **Domínio.** As URLs absolutas apontam para `yuri-links.vercel.app`. Ao apontar um domínio próprio, trocar no `<link rel="canonical">`, no `og:url` e no `og:image` — sem URL absoluta o WhatsApp entrega o link sem imagem.
2. **Rodapé.** Está com o CNPJ da Carteira 360º, tirado da página da Imersão. Confirmar se é esse ou o do escritório, e se entra o @ do Instagram.

## Medição

Lighthouse mobile (`--throttling-method=devtools`): performance 99, acessibilidade 100, boas práticas 100, SEO 100.
