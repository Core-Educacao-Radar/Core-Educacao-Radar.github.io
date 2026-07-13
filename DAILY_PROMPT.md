# Rotina diária — RADAR de Assuntos Virais (Core)

Este é o roteiro que o agente das 09h deve seguir para atualizar o painel.
Objetivo: manter `index.html` com os assuntos mais virais do dia + os vídeos que estão bombando.

## Passos

1. **Pesquisar os assuntos virais do dia** (Brasil) via web:
   - Buscar o que está bombando hoje nas redes (X/Twitter trending, Google Trends BR, portais).
   - Selecionar de 4 a 6 assuntos: misturar cultura pop / celebridades / relacionamento, esporte (Copa enquanto durar), política/economia e um fenômeno cultural.
   - Para cada assunto, levantar 3–4 fatos curtos e checados (com fonte).

2. **Pegar vídeos reais que estão viralizando** com esses assuntos:
   - Achar reels/vídeos com muita repercussão sobre cada tema.
   - Extrair a **headline de tela** (texto dos primeiros 5s). Fonte prática: o alt-text do próprio Instagram (`WebFetch` no reel → trecho "text that says '...'") ou a legenda/manchete de portais.
   - Guardar: @perfil, tema, e a headline literal. NÃO inventar número de views — usar o selo "Viral".

3. **Reconstruir `index.html`** mantendo EXATAMENTE:
   - A estrutura de slides e o motor de auto-rotate (não mexer no `<script>`).
   - O branding Core: fundo preto, dourado #EFC13A, roxo #8E74F2, azul-aço #7E93C4, rosa #E8709A, labels em monospace, o logo (data URI já embutido — **preservar** a tag `<img src="data:image/png;base64,...">`).
   - `<meta charset="utf-8">` no `<head>` (senão os acentos quebram).
   - A data é dinâmica via JS — não precisa mexer.
   - Trocar só: os slides de assunto (título + fatos), o ticker da capa e os cards de "vídeos virais".
   - Atualizar o array `labels` no script se mudar a quantidade/ordem de slides.

4. **Publicar**: `git add -A && git commit -m "Atualização diária DD/MM" && git push`.
   O Netlify está conectado a este repo e republica sozinho em ~1 min.

## Regras
- Sempre em português, tom direto, sem palavrão.
- Fatos checados; se um assunto for incerto, trocar por outro mais sólido.
- Manter de 6 a 8 slides no total (capa + 4–6 assuntos + vídeos virais + agenda).
- Não adicionar dependências externas (tudo self-contained; CSP-safe).
