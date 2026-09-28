# yuri-links

Página de links do Yuri Reis. A primeira tela é um roteador: quem chega da bio do Instagram tem uma pergunta só, "por onde eu falo com ele", e resolve isso sem rolar, em 390x844. Abaixo da dobra a página vira site.

No desktop ela deixa de ser uma coluna de 460px no meio do vazio: a partir de 900px a capa abre em duas colunas, identidade e destinos à esquerda, retrato à direita, e os blocos que estavam empilhados ficam lado a lado.

Identidade em duas camadas, como manda a marca: o gradiente índigo do deck da Carteira 360º (`#006EB9` → `#1B1464` → `#0A0A12`) é a espinha, e a paleta da Imersão Comercial é o sistema de interface, com o azul `#0071BC` reservado para ação. Plus Jakarta Sans + Inter, corte diagonal de 2,5° com a perfuração de bilhete.

Um arquivo, sem build, sem JavaScript. Fontes auto-hospedadas: a página não depende do Google Fonts.

## A ordem da página

| Bloco | O que faz |
| --- | --- |
| Topo | Retrato, nome, posicionamento |
| Os três destinos | O roteador. Cabe acima da dobra em 390x844 e em 320x568 |
| Duas portas, dois momentos | Separa o escritório da Carteira 360º. É a camada que faltava |
| Yuri no palco | Palestras, com a foto de palco em tamanho de verdade |
| O escritório em números | **Comentado no HTML.** Ver "Pendências" |
| Vamos fazer a sua conta | Fechamento, devolve para o WhatsApp do escritório |

**Por que o cartão de palestras perdeu a foto de capa:** ela era a maior peça da página e empurrava o formulário de aplicação para fora da primeira tela. Convite para palestrar é o destino que menos gera receita, e estava ocupando o orçamento de atenção dos dois que sustentam o negócio. A foto continua no site, no bloco de palestras.

**Por que o bloco de números nasce desligado:** ele depende de dado que ainda não existe. Publicar quatro `[A PREENCHER]` no ar é pior do que não ter o bloco, porque quem chega da bio lê a página, não o nosso backlog. O HTML e o CSS estão prontos: para ligar, apague o comentário em volta da `<section>` e troque os quatro valores.

## Os três links

| Cartão | Destino |
| --- | --- |
| Falar com o escritório | `wa.me/5535997720153` com mensagem pronta sobre contabilidade |
| Formulário de aplicação | `quiz.360carteira.com.br` |
| Convidar para palestrar | `wa.me/5535999605924` (comercial) com mensagem pronta sobre palestra |

Cada link leva uma mensagem pronta: é o que diz ao Yuri, na primeira linha da conversa, por qual porta a pessoa entrou. Para tirar, apague tudo a partir do `?` no `href`. Até 28/09 os dois caíam no mesmo número; palestras passou a ter o número comercial próprio.

> **O domínio do formulário é `360carteira.com.br`, não `carteira360`.** O endereço antigo (`quiz.carteira360.com.br`) não resolvia em DNS nenhum, e foi por isso que o cartão apontou para o vazio até 28/09. O certo é `quiz.360carteira.com.br`, o mesmo domínio da landing da Imersão. Ele responde 403 para `curl` sem user-agent de navegador, o que é proteção de bot, não erro: com UA de navegador devolve 200.

## Dois formatos de cartão

- **Com capa** (`.link--capa`): foto na largura toda, texto embaixo. É o formato de quem precisa provar o que faz. Está no cartão de palestras e é para onde vai o do escritório quando a foto chegar.
- **Sem capa:** ícone à esquerda, texto ao lado. Fica no formulário de aplicação, que não tem foto para mostrar.

Para passar o cartão do escritório ao formato de capa: adicione `link--capa` na classe do `<a>` e troque o `<svg>` do `.link__midia` pelo mesmo `<picture>` do cartão de palestras. A foto entra em `1.85:1` (por exemplo 820x443) — a mesma proporção do slot, para não ser recortada de novo.

## Editar

- **Links:** `index.html`, procure por `LINK 1`, `LINK 2`, `LINK 3`.
- **Foto do cabeçalho:** `img/yuri.jpg` + `img/yuri.webp` (1000x1250). Para trocar:
  ```bash
  magick <foto-nova> -resize 1000x1250^ -gravity north -extent 1000x1250 -strip -quality 86 img/yuri.jpg && cwebp -q 82 img/yuri.jpg -o img/yuri.webp
  ```
  O enquadramento fino fica no CSS, em `.topo__foto img { object-position }`.
- **Preview de link (WhatsApp, Instagram):** `img/og.jpg` sai de `og.html`. Para regerar, abra `og.html` em 1200x630 e capture a tela.

## Pendências

O que precisa vir do Yuri, em ordem de impacto:

1. **Os quatro números do bloco de prova.** Anos de escritório, empresas atendidas hoje, cidades e palestras dadas. Nenhum foi estimado e nenhum está no ar. Com eles o bloco liga em dois minutos.
2. **Foto do escritório**, para o primeiro cartão virar capa como o de palestras. Formato 1.85:1, por exemplo 820x443.
3. **Depoimento de cliente**, se e quando houver. Nome, empresa e uma frase que diga um número, não um adjetivo. Sem isso não existe bloco de depoimento, porque depoimento inventado é pior que nenhum.
4. **Domínio.** As URLs absolutas apontam para `yuri-links.vercel.app`. Ao apontar um domínio próprio, trocar no `<link rel="canonical">`, no `og:url` e no `og:image` — sem URL absoluta o WhatsApp entrega o link sem imagem.
5. **Rodapé.** Está com o CNPJ da Carteira 360º, tirado da página da Imersão. Confirmar se é esse ou o do escritório.

## Como a capa funciona nas duas larguras

A capa é uma grade de três peças: `.capa__foto`, `.identidade` e `.links`. No celular a identidade divide a célula com a foto (`grid-area: 1 / 1`) e assenta na base dela; no desktop a mesma grade vira duas colunas e a identidade vai para a esquerda. **É por isso que a identidade é irmã da foto e não filha dela:** filha, ela não teria como sair de cima da foto no desktop sem duplicar markup.

O retrato do desktop funde no fundo por `mask-image`, não por véu pintado. O véu pintava marinho chapado sobre um fundo que ali é índigo, e a borda da foto continuava dura. A máscara apaga o pixel, então funde com o que estiver atrás, seja qual for a cor, e custa o mesmo que um gradiente.

## Armadilhas já pagas

- **A perfuração do topo dava 4px de rolagem lateral.** Ela usa `width: 101%` para cobrir a diagonal depois de girar, e o `clip-path` esconde a sobra sem impedir o `scrollWidth` de crescer. Quem resolve é o `overflow: hidden` no `.topo__foto`.
- **`animation-timeline: view()` não existe no Safari.** Por isso o estado final dos blocos é o padrão, e a animação só entra dentro do `@supports`: onde não há suporte, o bloco já está visível em vez de invisível para sempre.
- **O CNPJ partia no meio em 320px** e parecia erro de digitação. Vai com `white-space: nowrap`.
- **Blur, backdrop-filter e blend-mode ficam de fora.** O travamento no Safari não vem de um filtro, vem do conjunto. Os círculos concêntricos do fechamento são `repeating-radial-gradient`, que custa uma pintura e nenhum elemento.
- **O fundo do desktop quase saiu branco abaixo da primeira tela.** O shorthand `background:` na media query zerava a cor de base, e `background-attachment: fixed` dimensiona o gradiente pela viewport: abaixo da dobra não sobrava nem gradiente nem cor, e o texto claro ficava invisível sobre branco. Vai como `background-color` e `background-image` separados, sem `fixed`. Só apareceu no screenshot de página inteira, nunca na primeira tela.

## Medição

Lighthouse mobile em `https://www.yurievreis.com/` (`--throttling-method=devtools`, nunca `simulate`, que infla o LCP): performance **98**, acessibilidade **100**, boas práticas **100**, SEO **100**. LCP 2,2 s, CLS **0**, TBT 0 ms.

Medido na URL pública, que é o número que vale: a Vercel entrega brotli e HTTP/2. Em `localhost` a mesma página mede 99.

**Confira o `uptime` antes de acreditar em qualquer número.** Com a máquina carregada o Lighthouse não mede: ele devolve `NO_FCP` e desiste, ou devolve um número que é da carga e não do arquivo. Se precisar medir com a máquina ocupada, a API do PageSpeed da Google roda no servidor deles e é imune a isso (mas tem cota diária baixa sem chave).
