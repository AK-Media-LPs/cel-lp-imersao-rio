# CEL — LP Imersão presencial Rio de Janeiro (11/12/2026)

**Cliente:** CEL (Felipe Winston)
**Evento:** "Como Empreender Lucrando em 2027", imersão presencial, sexta 11/12/2026, 9h às 12h, Barra Prime Office (Barra da Tijuca, Rio de Janeiro), 30 cadeiras, só para donos com 5+ funcionários.
**Objetivo:** vender ingresso no Hotmart (produto R108304679Q · off=j3autz3f), com UTMs/`src`/`sck` repassadas.

## Stack
HTML + runtime do Claude Design (`support.js`, não editar). React 18.3.1, ReactDOM e GSAP/ScrollTrigger 3.13.0 locais em `vendor/`. Fontes Roboto locais em `assets/fonts/`. Sem build.

## Deploy — Vercel
Import do repo · Framework Preset **Other** · Root Directory na raiz · sem Build/Install Command, sem Output Directory.

## Regras de negócio embutidas no código (`index.html`)
- 1º lote R$197 até 06/12/2026 23:59 (-03:00); 2º lote R$247 até 10/12/2026 23:59; depois "Inscrições encerradas" (`L1_END`, `L2_END`). O contador e o preço trocam sozinhos pela data.
- O link de checkout é o mesmo nos dois lotes (`rawUrl`, em `renderVals`): **a troca de preço precisa estar configurada na oferta do Hotmart**.
- Contador de vagas ("Restam X de 30") só aparece se `vagasRestantes` > 0 (hoje 0 = oculto).

## Edições sobre o exportado
- Exportado como bundle autônomo `.html` do Claude Design; desempacotado em `index.html` + `assets/` + `support.js` + `vendor/`.
- `<head>` estático com título, description, canonical, Open Graph, Twitter e favicon; GSAP e React servidos de `vendor/` (sem CDN), com `defer` antes do `support.js`.
- Imagens otimizadas (de ~4,5 MB para ~0,75 MB, JPEG); `assets/og-image.jpg` (1200×630) gerado a partir da foto do hero, pois o `og-cel.png` citado no export não vinha no bundle.
- Removido o link "Não carregou? Assistir no YouTube" abaixo dos vídeos de depoimento.
- Meta Pixel (ID 426921048860579, PageView) no `<head>` estático, direto no HTML (não via GTM).
- Ajustes mobile (<=767px): bloco `<style>` no `<head>` centraliza os blocos com título e aumenta a área de toque do link do mapa. Listas, agenda, FAQ, ingressos e dados Data/Horário/Local ficam à esquerda.
- Observação: 404 inofensivo no console (`{{ v.embed }}`) vem do template do export, sem efeito na página.
- `vercel.json`, `.gitignore`, `robots.txt` e `favicon.ico` adicionados.

## Testado localmente (17/11/2026)
Renderiza, sem requisições a CDN (só o Pixel da Meta), UTMs/`src`/`sck` chegam ao checkout, mobile 375 px sem rolagem horizontal, desktop 1440 px ok.

## Pendências
- [ ] URL real: trocar `SEU-DOMINIO.com.br` (canonical, og:url, og:image, twitter:image) após definir o domínio/Vercel e fazer segundo commit
- [ ] ID do GTM (não há tag no export): 1ª coisa do `<head>` + `<noscript>` após `<body>`; se o GTM disparar o Pixel, remover o do HTML para não duplicar
- [ ] Confirmar no Hotmart que a oferta troca de R$197 para R$247 em 07/12
- [ ] `robots.txt` hoje `Allow: /`; se for só tráfego pago, `Disallow: /` + `noindex` [DECIDIR]

Última atualização: 17/11/2026
