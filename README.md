# custom-yt-player

Player de vídeo no estilo YouTube, baseado no [PlayerJS](https://playerjs.com) (v21.2.4, com hls.js), com o código desempacotado e **todas as cores controladas por variáveis de tema**.

## Como colocar no seu site

**1.** Suba o arquivo `custom-yt-player.js` para o seu site (ex.: na pasta `js/`).

**2.** Na página onde o vídeo vai aparecer, carregue o script antes de `</body>`:

```html
<script src="js/custom-yt-player.js"></script>
```

**3.** Coloque uma `div` onde o player deve ficar e crie o player logo abaixo do script:

```html
<div id="player" style="width:100%; aspect-ratio:16/9;"></div>

<script>
  new Playerjs({
    id: "player",                                // id da div acima
    file: "https://seusite.com/videos/aula.mp4", // link do vídeo (MP4 ou HLS .m3u8)
    title: "Nome do vídeo",                      // opcional: título no canto superior
    poster: "img/capa.jpg"                       // opcional: imagem de capa antes do play
  });
</script>
```

Pronto, o player já funciona.

**4. (Opcional) Trocar as cores.** Antes do `<script src="js/custom-yt-player.js">`, defina só as cores que quiser mudar:

```html
<script>
  window.PLAYER_THEME = { "theme-color": "#c4a65e", "center-play": "#000000" };
</script>
```

Outra forma: editar os valores direto em `PLAYER_THEME_DEFAULT`, no topo do `custom-yt-player.js`. A lista completa de cores está em **Variáveis de tema**, abaixo.

**Vários vídeos na mesma página:** crie uma `div` com `id` diferente para cada um e um `new Playerjs({ id: "...", file: "..." })` para cada `div`.

**Como embed (iframe):** suba também o `index.html` e use `index.html?file=URL_DO_VIDEO&title=Título` como endereço do iframe.

## Variáveis de tema

Definidas em `PLAYER_THEME_DEFAULT`, no topo do `custom-yt-player.js`. Aceitam cor com ou sem `#`.

| Variável | Padrão | Controla |
|---|---|---|
| `theme-color` | `#ff0000` | Botão central, barra de progresso, bolinha, hover dos menus |
| `center-play` | `#fefefe` | Triângulo de play dentro do botão central |
| `icons` | `#ffffff` | Ícones da barra de controles |
| `background` | `#000000` | Fundo da tela do player |
| `toolbar` | `#000000` | Fundo (degradê) da barra de controles |
| `progress-bg` | `#ffffff` | Trilho da barra de progresso |
| `progress-load` | `#ffffff` | Parte já carregada da barra de progresso |
| `progress-hover` | `#ffffff` | Prévia ao passar o mouse na barra de progresso |
| `volume` | `#ffffff` | Barra de volume preenchida |
| `volume-bg` | `#ffffff` | Trilho da barra de volume |
| `volume-hover` | `#ffffff` | Barra de volume ao passar o mouse |
| `menu-bg` | `#000000` | Fundo dos menus (configurações e playlist) |
| `menu-text` | `#ffffff` | Texto dos menus |

Para trocar as cores, defina `window.PLAYER_THEME` **antes** de carregar o script (como no exemplo acima) ou edite os valores padrão direto no arquivo.

## Estrutura do `custom-yt-player.js`

1. **Tema**: `PLAYER_THEME_DEFAULT`.
2. **Configuração** (`PLAYERJS_CONFIG`): botões, posições, comportamento (`on: 1` liga, `on: 0` desliga).
3. **Código do PlayerJS**: desempacotado e formatado.
4. **hls.js**: biblioteca de streaming, sem alterações.

## Eventos

Passe `eventstracker: 1` ao criar o player e defina `window.PlayerjsEvents = function (event, id, data) { ... }`. Exemplo: `event === "end"` quando o vídeo termina.

## Obs.: Content-Security-Policy

Só se o seu site usa o cabeçalho `Content-Security-Policy`: libere `'unsafe-eval'` em `script-src`, `'unsafe-inline'` em `style-src` e o domínio dos vídeos em `media-src`. Sem isso, o player não carrega.
