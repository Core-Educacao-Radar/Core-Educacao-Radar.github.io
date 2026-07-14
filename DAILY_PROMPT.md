# Rotina diária — RADAR de Assuntos Virais (Core)

Roteiro que o agente das 09h segue para atualizar o painel. Objetivo: manter `index.html` com os assuntos mais virais do dia + players de vídeos virais do Instagram embutidos.

## Passos

1. **Pesquisar os assuntos virais do dia** (Brasil) via web:
   - Buscar o que está bombando hoje (X/Twitter trending, Google Trends BR, portais de notícia e entretenimento).
   - Selecionar de 4 a 6 assuntos VARIADOS: cultura pop / celebridade / relacionamento, esporte (quando relevante), política/economia e um fenômeno cultural.
   - Para cada assunto, 3–4 fatos curtos e CHECADOS (com fonte).

2. **Achar 3 vídeos virais de ASSUNTO SÉRIO no Instagram** (para os 3 players embutidos):
   - REGRA MAIS IMPORTANTE: têm que ser vídeos que dão pra virar CONTEÚDO SÉRIO — notícia, comportamento, relacionamento, negócios, economia, política, esporte com ângulo (integridade, apostas), tecnologia (IA/deepfake), atualidades. **NADA de meme, comédia, pegadinha, vídeo "fofo" ou clipe engraçado aleatório** (ex.: "funcionário deu 60 atestados", "levou o filho pro trabalho" = PROIBIDO).
   - Depois do filtro "sério", prefira os mais virais possível. OBS: conteúdo sério costuma ter MENOS views que meme — então priorize SÉRIO sobre número bruto de views. Boas fontes: contas de notícia/opinião (@metropoles, @choquei — mas só pegar os posts de notícia, não os de humor), criadores de comportamento/relacionamento/finanças, e reels citados em matérias.
   - Como achar o código SEM login (acesso logado é bloqueado p/ robôs): Google `site:instagram.com/reel <assunto sério do dia>`, ou matérias que incorporam o reel (URL `instagram.com/reel/CODIGO/`). Idealmente ligue os vídeos aos assuntos sérios que já estão nos slides do painel.
   - Se tiver número de views/curtidas de fonte, coloque na legenda; se não tiver, NÃO invente — use `@perfil` + uma framing séria curta do assunto.
   - Confirme que cada reel resolve (não apagado/privado); se quebrar, troque.

3. **Montar a tela "Vídeos virais"** (o `<section>` com a `div.embed-grid`, que é uma grade de 3 colunas). Coloque EXATAMENTE 3 blocos, lado a lado:
   ```html
   <figure class="embed">
     <figcaption><span class="handle">@perfil</span>Headline de tela curta · (opcional: N mil curtidas se houver fonte)</figcaption>
     <iframe src="https://www.instagram.com/reel/CODIGO/embed/" scrolling="no" allowtransparency="true" allow="clipboard-write; encrypted-media; picture-in-picture; web-share"></iframe>
   </figure>
   ```
   NÃO use `loading="lazy"` (senão o player fica em branco ao entrar a tela na TV).

4. **NÃO MEXER NAS TELAS DE RANKING** (elas se atualizam sozinhas):
   - Os 3 `<section class="slide">` de ranking — **Ranking de primeiros virais** (id `rankFirst`), **Ranking do vídeo mais viral** (ids `rankViews` + `topViralVideo`) e **Ranking de squads** (id `rankSquad`) — devem ser PRESERVADOS byte a byte.
   - O SEGUNDO bloco `<script>` no fim do arquivo (o que lê a planilha do Google via fetch) deve ser PRESERVADO byte a byte. Ele puxa os dados ao vivo das abas (squads) da planilha e re-lê a cada 10 min — não precisa de nada seu.
   - Se um squad novo for criado (aba nova na planilha), adicione a entrada `{n:'Nome', g:'GID'}` no array `SQUADS` desse script — nada mais.

5. **Reconstruir o resto do `index.html`** mantendo EXATAMENTE:
   - Estrutura de slides e o `<script>` de auto-rotate (NÃO alterar).
   - `<meta charset="utf-8">` no `<head>` (senão os acentos quebram na TV).
   - O logo (tag `<img src="data:image/png;base64,...">` — preservar).
   - Cores: dourado #EFC13A, roxo #8E74F2, azul-aço #7E93C4, rosa #E8709A; labels em monospace.
   - A data no topo é dinâmica via JS — não mexer.
   - Trocar só: o ticker da capa, os slides de assunto (título + fatos) e a tela de vídeos (embeds).
   - Se mudar a quantidade/ordem de slides, atualizar o array `labels` no `<script>`.

5. **Publicar**: rodar `bash /Users/vitortroyack/.core-radar/deploy.sh` (publica no Netlify via token; espera-se a linha "Production URL: ..."). Opcional: commit local de histórico (`git add -A && git commit -m "diária"`), sem push.

## Regras
- Português, tom direto, sem palavrão; fatos checados.
- 6 a 8 slides (capa + 4-6 assuntos + vídeos virais + agenda).
- Tudo self-contained no HTML, sem dependências externas ALÉM dos iframes de embed do Instagram (que são permitidos).
- Vídeos: priorizar os EXTREMAMENTE virais. Sem número garantido de views (limitação do Instagram) — o player mostra o vídeo e o criador; o número só entra se uma fonte disser.
