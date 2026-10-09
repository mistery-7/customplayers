# customplayers

Cada pasta é um player. Troque `NOME` pelo nome do player (ex.: `custom-yt-player`).

## Instalar

```html
<div id="player" style="width:100%; aspect-ratio:16/9;"></div>

<script src="NOME.js"></script>
<script>
  new Playerjs({ id: "player", file: "https://seusite.com/video.mp4", title: "Título", poster: "capa.jpg" });
</script>
```

`title` e `poster` são opcionais.

## Cores

Antes do `<script src="NOME.js">`, defina só as cores que quiser mudar:

```html
<script>
  window.PLAYER_THEME = { "theme-color": "#c4a65e" };
</script>
```

A lista de cores de cada player fica no topo do `.js`, em `PLAYER_THEME_DEFAULT`. Também dá para editar direto ali.
