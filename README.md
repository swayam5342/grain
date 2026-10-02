# Grain

A falling-sand sandbox. Paint sand, water, fire, acid, gas, oil, wood and stone, place spawners, and watch them interact.

Under the hood it is a cellular automaton split into 16×16 chunks. Each step only processes chunks that were disturbed in the previous step; chunks where nothing moved go to sleep and cost nothing. Turn on **Show chunks** to watch it happen.

No dependencies and no build step: plain HTML, CSS and ES modules.

## Run locally

ES modules don't load over `file://`, so serve the folder:

```sh
npx serve .
# or
python3 -m http.server 8000
```

## Project layout

```
index.html        markup
style.css         styles (light/dark tokens)
src/elements.js   element ids, densities, colour tables, tool list
src/engine.js     the simulation: chunked update loop, element rules, spawners, rendering
src/main.js       UI: toolbar, pointer + keyboard input, main loop
embed/Grain.astro drop-in Astro component that embeds the deployed page
```

## Controls

| Input | Action |
| --- | --- |
| `1`–`9` | Select element (9 is the eraser) |
| `S` | Toggle Draw / Spawner mode |
| `[` `]` | Brush size |
| `Space` | Pause / play |
| `N` | Step one frame while paused |
| `V` | Show awake chunks |
| `X` | Clear everything |
| Right-click | Erase |

## URL options

| Param | Effect |
| --- | --- |
| `?theme=dark` / `?theme=light` | Force the panel theme (otherwise follows the OS) |
| `?scene=empty` | Start with an empty world instead of the demo scene |

Combine them: `?theme=dark&scene=empty`.

## Deploy (GitHub Pages)

1. Push this repo to GitHub.
2. Settings → Pages → Source: *Deploy from a branch*, branch `main`, folder `/ (root)`.
3. The page is served at `https://<user>.github.io/<repo>/`.

All asset paths are relative, so it works from a sub-path.

## Embed in Astro

Copy `embed/Grain.astro` into your Astro project (e.g. `src/components/`) and use it:

```astro
---
import Grain from "../components/Grain.astro";
---
<Grain src="https://<user>.github.io/<repo>/?theme=dark" />
```

## License

MIT
