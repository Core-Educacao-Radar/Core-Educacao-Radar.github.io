# Core · RADAR de Assuntos Virais

Painel de TV que mostra, em loop, os assuntos mais virais do momento e os vídeos que estão bombando com cada tema. Feito pra deixar passando numa TV.

- **`index.html`** — o painel (arquivo único, self-contained: logo embutido, sem dependências externas). Auto-rotate, tela cheia com `F`, data automática.
- **`DAILY_PROMPT.md`** — o roteiro que a rotina das 09h segue pra pesquisar e reconstruir o painel.

## Deploy
Conectado ao Netlify (deploy contínuo): cada `push` na branch principal republica o site automaticamente.

## Atualização diária
Uma rotina roda todo dia às 09h (horário de Brasília), pesquisa os virais do dia, regenera o `index.html` e dá `push` — o Netlify republica sozinho.

## Marca
Core Educação — preto + dourado, roxo, azul-aço e rosa; labels em monospace; logo losango dourado.
