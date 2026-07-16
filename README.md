# Awesome Codex Themes [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of themes, skins, galleries, and theming tools for [OpenAI Codex](https://developers.openai.com/codex/) — the Codex CLI, the Codex desktop app, and the Codex IDE extension.

Codex theming happens on three surfaces:

1. **Codex CLI (terminal TUI)** — 32 bundled syntax themes, switched with the `/theme` slash command (live preview) or `tui.theme = "..."` in `~/.codex/config.toml`. Custom themes are standard TextMate `.tmTheme` files dropped into `$CODEX_HOME/themes/` — thousands of existing Sublime Text / TextMate color schemes work out of the box.
2. **Codex desktop app** — full appearance customization (base theme, accent/ink/surface colors, fonts, semantic diff colors) shipped in late March 2026. Themes travel as portable `codex-theme-v1:{...}` JSON strings, imported via **Settings → Appearance → Dark/Light Theme → Import**.
3. **Skins (CDP injection)** — community tools inject CSS/artwork into the Codex desktop app at runtime over the local Chrome DevTools Protocol, enabling wallpaper-level customization far beyond color themes, without patching official binaries.

## Contents

- [Official Resources](#official-resources)
- [How Theming Works](#how-theming-works)
- [Codex CLI Themes](#codex-cli-themes)
- [Codex App Themes](#codex-app-themes)
  - [Galleries & Builders](#galleries--builders)
  - [Individual Themes](#individual-themes)
- [Skins & Deep Customization](#skins--deep-customization)
  - [CodexThemes](#codexthemes)
- [Shared on X (Twitter)](#shared-on-x-twitter)
- [Ports to Other Editors](#ports-to-other-editors)
- [Articles & Guides](#articles--guides)
- [Contributing](#contributing)

## Official Resources

- [openai/codex](https://github.com/openai/codex) — The official Codex CLI repository; TUI theming lives in `codex-rs/tui`.
- [Codex Config Reference](https://developers.openai.com/codex/config-reference) — Official `config.toml` reference, including `tui.theme` and `tui.status_line`.
- [Codex App Settings](https://developers.openai.com/codex/app/settings) — Official docs for the desktop app's appearance settings.
- [Codex TUI Style Guide](https://github.com/openai/codex/blob/main/codex-rs/tui/styles.md) — The color/style conventions the Codex TUI itself follows.

## How Theming Works

### CLI: `.tmTheme` + `config.toml`

```toml
# ~/.codex/config.toml
[tui]
theme = "catppuccin-mocha"   # any bundled name, or a custom .tmTheme in ~/.codex/themes/
```

Type `/theme` inside Codex for a live-preview picker that persists your choice. Custom themes are plain TextMate `.tmTheme` files: place `my-theme.tmTheme` in `~/.codex/themes/` and set `theme = "my-theme"` (the kebab-case filename becomes the theme name).

The CLI bundles 32 themes (defaults: `catppuccin-mocha` on dark terminals, `catppuccin-latte` on light):

| Family | Theme names |
| --- | --- |
| Catppuccin | `catppuccin-mocha` · `catppuccin-latte` · `catppuccin-frappe` · `catppuccin-macchiato` |
| Base16 | `base16` · `base16-256` · `base16-eighties-dark` · `base16-mocha-dark` · `base16-ocean-dark` · `base16-ocean-light` |
| Monokai Extended | `monokai-extended` · `monokai-extended-bright` · `monokai-extended-light` · `monokai-extended-origin` |
| Gruvbox | `gruvbox-dark` · `gruvbox-light` |
| Solarized | `solarized-dark` · `solarized-light` |
| One / Two | `one-half-dark` · `one-half-light` · `two-dark` |
| Coldark | `coldark-cold` · `coldark-dark` |
| GitHub | `github` · `inspired-github` |
| Classics | `dracula` · `nord` · `zenburn` · `sublime-snazzy` · `dark-neon` · `1337` · `ansi` |

### App: `codex-theme-v1` import strings

Desktop app themes are JSON payloads prefixed with `codex-theme-v1:`. Fields include `codeThemeId`, `theme.accent`, `theme.ink` (text), `theme.surface` (background), `theme.contrast`, `theme.opaqueWindows`, `theme.fonts.{ui,code}`, `theme.semanticColors.{diffAdded,diffRemoved,skill}`, and `variant` (`dark`/`light`). Import via **Settings → Appearance → Dark/Light Theme → Import**.

> **Gotcha:** `codeThemeId` must match a built-in id (`tokyo-night`, `one-dark`, `nord`, `dracula`, `catppuccin`, `gruvbox`, `solarized`, `github-light`, `matrix`, `one`) — unknown ids fail silently ([openai/codex#14766](https://github.com/openai/codex/issues/14766)). Theme authors work around this by reusing a built-in id and overriding all colors.

The app ships built-in classics (Catppuccin, Monokai, Solarized) plus official partner themes including Linear, Notion, Raycast, and OpenClaw.

## Codex CLI Themes

- [ychampion/codex-themes](https://github.com/ychampion/codex-themes) — Open-source theme manager for Codex CLI: validates community themes, previews in the terminal, installs `.tmTheme` files, writes reversible `config.toml`, ships status-line presets, and exports matching palettes for Windows Terminal, iTerm2, Ghostty, and Alacritty. `MIT`
- [Nick2bad4u/codex-terminal-themes](https://github.com/Nick2bad4u/codex-terminal-themes) — Gallery, installer, picker, and diagnostic CLI for 200+ TextMate themes packaged specifically for Codex terminal syntax highlighting. `MIT`
- Any `.tmTheme` collection works too — e.g. the hundreds of schemes bundled with [bat](https://github.com/sharkdp/bat) or from [TextMate/Sublime theme galleries](https://tmtheme-editor.glitch.me/); drop the file into `~/.codex/themes/`.

## Codex App Themes

### Galleries & Builders

- [DexThemes](https://www.dexthemes.com/) — Community site to discover and create Codex themes: searchable catalog, dark/light preview with accent controls, copyable import strings. By [@daeshawn](https://x.com/daeshawn).
- [samuxbuilds/codex-themes](https://github.com/samuxbuilds/codex-themes) — Interactive gallery of 1000+ themes with live preview and one-click export ([live site](https://codex.instantlandingpages.xyz)): editor presets (Dracula, Nord, Tokyo Night, GitHub), brand palettes (Vercel, Stripe, Linear), color families, gradients, and accessibility/WCAG variants. `MIT`

  <img src="images/samuxbuilds-codex-themes/gallery.png" width="560" alt="samuxbuilds codex-themes gallery">

- [shaw-baobao/codex-themes](https://github.com/shaw-baobao/codex-themes) — Curated Codex app themes with previews and ready-to-import strings; each theme ships `theme.json` + `preview.svg` + `import.txt`, with a JSON schema and build scripts. English/中文. `MIT`

  | | | |
  |---|---|---|
  | <img src="images/shaw-baobao-codex-themes/codex-dark.svg" width="260" alt="Codex Dark"><br><sub>Codex Dark</sub> | <img src="images/shaw-baobao-codex-themes/tokyo-night.svg" width="260" alt="Tokyo Night"><br><sub>Tokyo Night</sub> | <img src="images/shaw-baobao-codex-themes/catppuccin-mocha.svg" width="260" alt="Catppuccin Mocha"><br><sub>Catppuccin Mocha</sub> |
  | <img src="images/shaw-baobao-codex-themes/dracula.svg" width="260" alt="Dracula"><br><sub>Dracula</sub> | <img src="images/shaw-baobao-codex-themes/nord.svg" width="260" alt="Nord"><br><sub>Nord</sub> | <img src="images/shaw-baobao-codex-themes/rose-pine.svg" width="260" alt="Rosé Pine"><br><sub>Rosé Pine</sub> |

- [lafllamme/codex-themes](https://github.com/lafllamme/codex-themes) — TypeScript toolkit that converts raw terminal palettes (e.g. `.itermcolors` from iTerm2-Color-Schemes) into Codex-compatible JSON presets, with a [browsable site](https://codex-theme.pages.dev/). `MIT`
- [Railly/tinte](https://github.com/Railly/tinte) — Agent-native design-system compiler and previewer with a Codex provider, useful for generating Codex themes alongside matching themes for other tools. `MIT`
- [meownoid/meowtheme](https://github.com/meownoid/meowtheme) — Multi-target color-scheme generator with ready-made light and dark Codex Desktop outputs. `MIT`
- [CosmicCoderDev/codex-themes](https://github.com/CosmicCoderDev/codex-themes) — Small bilingual collection of desktop share strings with an interactive skin preview and light/dark Muse, Nebula, and Hacker variants. `MIT`
- [Kronosnxs/codex-theme-builder](https://github.com/Kronosnxs/codex-theme-builder) — Single-file web app for building and exporting custom Codex theme strings: tune light and dark variants, preview instantly, copy a ready-to-import string. `MIT`

  <img src="images/codex-theme-builder/builder.png" width="560" alt="Codex theme builder web app">
- [Utility Materials for Codex](https://themes.utility.materials.nyc/themes/codex/) — Dark mineral surfaces with warm sand text; ships theme `.json` payloads plus paste-ready `codex-theme-v1:` import strings.

### Individual Themes

- [miniLV/Anthropic-codex-theme](https://github.com/miniLV/Anthropic-codex-theme) — Anthropic-style light & dark themes, one-click import. `MIT`

  <img src="images/anthropic-codex-theme/anthropic.jpg" width="560" alt="Anthropic-style Codex theme">
- [mundizzle/claude-theme](https://github.com/mundizzle/claude-theme) — Anthropic-inspired light and dark palettes for Codex, VS Code, Ghostty, and Zed, with paste-ready Codex import strings. `MIT`
- [YuChenSSR/claude-warm-codex-app-theme](https://github.com/YuChenSSR/claude-warm-codex-app-theme) — Warm Claude-inspired light and dark Codex app themes, distributed as importable `codex-theme-v1` payloads. `MIT`
- [chainshieldai/codex-cobalt-gold-theme](https://github.com/chainshieldai/codex-cobalt-gold-theme) — Cobalt2-inspired Codex desktop theme with safe runtime Markdown styling. `MIT`
- [zh1665/cobalt-for-codex](https://github.com/zh1665/cobalt-for-codex) — Cobalt theme installer for Codex Desktop on Windows. `MIT`
- [ziyue67/midnight-purple-2077-codex-theme](https://github.com/ziyue67/midnight-purple-2077-codex-theme) — High-contrast dark purple theme inspired by VS Code's Midnight Purple 2077, optimized for Chinese UI fonts.
- [alexh/umi-codex-theme](https://github.com/alexh/umi-codex-theme) — "Umi", a single hand-crafted Codex theme.
- [Arishawke/fadetouched-theme](https://github.com/Arishawke/fadetouched-theme) — Earthy dark teal-green palette with a generated Codex port alongside other editor and terminal targets. `MIT`
- [FabianBeiner/lagoon-colors](https://github.com/FabianBeiner/lagoon-colors) — OKLab-designed Midnight Lagoon and Morning Lagoon themes with Codex import files and WCAG-oriented contrast. `MIT`
- [jarith/everforest-night-codex-app](https://github.com/jarith/everforest-night-codex-app) — Everforest Night theme compiled into a ready-to-import Codex app string. `MIT`
- [victorcrbt/sovietwave](https://github.com/victorcrbt/sovietwave) — SovietWave and Zhukov dark themes with Codex installers and matching ports for VS Code and Warp.
- [hsnovel/codex-theme](https://github.com/hsnovel/codex-theme) — Simple high-contrast theme that is easy on the eyes. `GPL-3.0`

  <img src="images/hsnovel-codex-theme/preview.png" width="560" alt="hsnovel high-contrast Codex theme">
- [leiniaozl229/codex-claude-theme](https://github.com/leiniaozl229/codex-claude-theme) — Local macOS Codex theme patcher with a Claude-inspired visual style. `MIT`
- [LiteraryUniverse/omarchy-codex-theme](https://github.com/LiteraryUniverse/omarchy-codex-theme) — Omarchy-styled Codex theme.

## Skins & Deep Customization

Community tools for decorative backgrounds, glass surfaces, theme switching, and deeper UI tweaks. Most use local CDP injection without modifying the signed app; entries that patch the local installation are separated and labeled below.

<div align="center">

<h3 id="codexthemes"><a href="https://codexthemes.ai">✨ CodexThemes</a></h3>
<p><strong>Discover a large collection of beautiful themes and skins for the Codex desktop app.</strong></p>
<p><a href="https://codexthemes.ai"><strong>Explore CodexThemes →</strong></a></p>

</div>

---

### Runtime CDP Skins

- [Fei-Away/Codex-Dream-Skin](https://github.com/Fei-Away/Codex-Dream-Skin) ⭐3.5k — External skins for the Codex desktop app; swap in any image as a full-window mood background while sidebar, cards, and input stay native. Ships 8 example skins, one-click restore, macOS + Windows installers. `MIT`

  | | |
  |---|---|
  | <img src="images/codex-dream-skin/skin-01.jpg" width="400" alt="Pink Custom"><br><sub>Pink Custom</sub> | <img src="images/codex-dream-skin/skin-02.jpg" width="400" alt="God of Wealth"><br><sub>God of Wealth</sub> |
  | <img src="images/codex-dream-skin/skin-03.jpg" width="400" alt="Red-White Sci-Fi"><br><sub>Red-White Sci-Fi</sub> | <img src="images/codex-dream-skin/skin-04.jpg" width="400" alt="Clear Custom"><br><sub>Clear Custom</sub> |
  | <img src="images/codex-dream-skin/skin-05.jpg" width="400" alt="Inspiration"><br><sub>Inspiration</sub> | <img src="images/codex-dream-skin/skin-06.jpg" width="400" alt="Purple Night"><br><sub>Purple Night</sub> |
  | <img src="images/codex-dream-skin/skin-07.jpg" width="400" alt="Hatsune Miku"><br><sub>Hatsune Miku</sub> | <img src="images/codex-dream-skin/skin-08.jpg" width="400" alt="Stage Black-Gold"><br><sub>Stage Black-Gold</sub> |

- [CodeDrobe/codex-skill](https://github.com/CodeDrobe/codex-skill) ⭐88 — Open-source Codex theming Skill, AI theme generator, and cross-platform runtime for custom desktop themes; exports shareable `.codex-theme` files. Install with `npx skills add anhao/codedrobe-codex-skill`. macOS/Windows. `Apache-2.0`

  | | |
  |---|---|
  | <img src="images/codedrobe/desktop.jpg" width="400" alt="CodeDrobe desktop app"><br><sub>CodeDrobe Desktop</sub> | <img src="images/codedrobe/codex-01.jpg" width="400" alt="KUN Stage theme"><br><sub>KUN Stage theme</sub> |

- [HeiGeAi/heige-codex-skin-studio](https://github.com/HeiGeAi/heige-codex-skin-studio) ⭐82 — One-click skin switcher for Codex Desktop: "one image = one theme," 9 presets (Hatsune Miku, Genshin Impact, Wuthering Waves, Naruto, Love & Deepspace) plus color extraction from any custom image. English/中文. `MIT`

  | | |
  |---|---|
  | <img src="images/heige-skin-studio/miku-switcher-live.jpg" width="400" alt="Miku theme with switcher menu"><br><sub>Hatsune Miku + switcher</sub> | <img src="images/heige-skin-studio/genshin-night-live.jpg" width="400" alt="Genshin starry night theme"><br><sub>Genshin starry night</sub> |

- [aiwenjie777/codex-skin-switcher](https://github.com/aiwenjie777/codex-skin-switcher) ⭐18 — Codex skin manager (中文).

  <img src="images/codex-skin-switcher/skin-09.jpg" width="560" alt="codex-skin-switcher preview">

- [tree0519/Codex-Dream-Skin-Forge](https://github.com/tree0519/Codex-Dream-Skin-Forge) — Dream Skin derivative with a Windows multi-theme pack, in-app switching, animated GIF skins, fixes, and AI-assisted theme creation. macOS/Windows.
- [xnydl/codex-dream-skin](https://github.com/xnydl/codex-dream-skin) — Free macOS/Windows Dream Skin Skill with guided installation, switching, verification, and restoration.
- [aiwenjie777/codex-skin-skill](https://github.com/aiwenjie777/codex-skin-skill) — Agent-operated one-image skin installer for macOS and Windows, with theme switching and rollback.
- [Finderchangchang/codex-autoskin](https://github.com/Finderchangchang/codex-autoskin) — Agent-native skin engine that extracts a palette from one image, writes an inspectable theme spec and manifest, then applies or restores it through CDP. Windows. `MIT`
- [fishcold789/Taffy-Codex-Theme-Studio](https://github.com/fishcold789/Taffy-Codex-Theme-Studio) — Taffy-inspired theme studio with replaceable images, 20 palettes, light/dark modes, acrylic, and liquid-glass styles. Windows.
- [ismoshushi/codex-skinkit](https://github.com/ismoshushi/codex-skinkit) — Switchable built-in and custom themes for Codex Desktop on Windows, including verification and restore commands. `MIT`
- [xiongwenhao112/raccoon-dream-skin](https://github.com/xiongwenhao112/raccoon-dream-skin) — Agent Skill with six built-in office-raccoon themes, conversational switching, and one-click restoration. `MIT`
- [kongxcer555/codex-skin-builder](https://github.com/kongxcer555/codex-skin-builder) — A Codex Skill for building and customizing Codex skins. `MIT`

  <img src="images/codex-skin-builder/cloud-crane-study.jpg" width="560" alt="Cloud Crane Study skin">
- [z0rgoyok/codex-theme-controller](https://github.com/z0rgoyok/codex-theme-controller) — macOS utility that applies color themes to Codex via the Chrome DevTools Protocol.
- [Alhamdulillah-R/cyberpunk-codex-skin](https://github.com/Alhamdulillah-R/cyberpunk-codex-skin) — Cyberpunk/Edgerunners-flavored skin.

### App Tweak Frameworks

- [b-nnett/codex-plusplus](https://github.com/b-nnett/codex-plusplus) — Large cross-platform tweak system for Codex Desktop with UI modifications, extra settings surfaces, a native bridge, and a tweak SDK. Unlike the runtime-only skin tools above, it patches the local app installation; review its backup and restore workflow before use. `MIT`

### Historical

- [jstxn/codex-themes](https://github.com/jstxn/codex-themes) — macOS launcher that ran Codex with an in-app theme button and 16 bundled themes (Ayu Mirage, Catppuccin, Dracula, Everforest, Flexoki, Gruvbox, Monokai Pro, Nightfox, Nord, Sonokai, TokyoNight Storm…), from before official theming support. Now deprecated by its author, but the minimal 4-field theme JSON remains a nice reference.

  <img src="images/jstxn-codex-themes/picker.png" width="560" alt="jstxn codex-themes picker">

## Shared on X (Twitter)

Theme shares and theming moments worth knowing:

- [@liyue_ai — Codex skin transformation showcase](https://x.com/liyue_ai/status/2077676358734614758) — Before-and-after style showcase demonstrating how dramatically a skin can change the character of the Codex desktop app.
- [@vista8 — prompt-driven skin workflow](https://x.com/vista8/status/2077660576655032678) — A compact recipe for asking Codex to read the Dream Skin repository, generate artwork with its built-in image tool, and apply a new theme.
- [@cnyzgkc — open-source skin tool spotlight](https://x.com/cnyzgkc/status/2077584412351586535) — Chinese-language introduction to Codex Dream Skin, its agent-assisted installation workflow, and the emerging custom-skin market.
- [@joyforjoker43 — Codex skin showcase roundup](https://x.com/joyforjoker43/status/2077573173294563615) — Chinese-language roundup of branded, fandom, and anime-style Codex skins, plus ideas for turning customized Codex setups into products.
- [@ianneo_ai — themes as a product opportunity](https://x.com/ianneo_ai/status/2077558478273712568) — Commentary on Codex themes as a simple product category that could extend to reskinning other popular software.
- [@dkundel (OpenAI Codex team) — Catppuccin × Comic Sans](https://x.com/dkundel/status/2032224113025302535) — The canonical `codex-theme-v1:` share-string example: Catppuccin base, custom colors, Comic Sans font overrides. "Probably good that I didn't become a designer 😂"
- [@dkundel — Raycast partner theme](https://x.com/dkundel/status/2037552817385467967) — Pairing Codex with the matching Raycast theme; "the dark mode one looks pretty fresh 👀".
- [@_chenglou — Mariana for Codex](https://x.com/_chenglou/status/2032587449927671994) — Ready-to-import port of Sublime Text's Mariana theme, overriding the One theme id to work around the importer restriction.
- [@testingcatalog — theming launch coverage](https://x.com/testingcatalog/status/2032226272152043910) — Coverage of OpenAI releasing Themes for the Codex app with partner themes.
- [@xjstxn — early Codex theme switcher](https://x.com/xjstxn/status/2021847462609400239) — Launch post and visual preview for the now-historical [jstxn/codex-themes](https://github.com/jstxn/codex-themes) launcher.

Machine-readable metadata for these posts lives in [`data/x-posts.json`](data/x-posts.json); see the [data notes](data/README.md) for collection rules.

## Ports to Other Editors

- [BXCQ/Codex-Theme-Collection](https://github.com/BXCQ/Codex-Theme-Collection) — Ports all official Codex UI themes to VS Code, faithfully reproducing accent, background, diff, and skill-highlight colors. `MIT`
- [Codex Theme Collection (VS Code Marketplace)](https://marketplace.visualstudio.com/items?itemName=Xuanxi1111.codex-theme) — Codex-flavored VS Code themes such as `codex-tokyo-night` and `codex-github-dark`.

## Articles & Guides

- [Codex App Theming & Customisation](https://codex.danielvaughan.com/2026/03/30/codex-app-theming-customisation/) — Walkthrough of the app's appearance settings, partner themes, and the `codex-theme-v1` import format.
- [Codex CLI TUI Customisation: Keymaps, Themes, Status Lines](https://codex.danielvaughan.com/2026/05/05/codex-cli-tui-customisation-keymaps-themes-status-lines/) — Guide to `/theme`, custom `.tmTheme` installation, status lines, and the rest of the TUI customization surface.

### Issues worth watching

- [openai/codex#14766](https://github.com/openai/codex/issues/14766) — Theme importer rejects custom `codeThemeId` values unless they match dropdown ids.
- [openai/codex#21130](https://github.com/openai/codex/issues/21130) — Request: configure semantic TUI colors beyond syntax highlighting.
- [openai/codex#1618](https://github.com/openai/codex/issues/1618) — The original "control over color theme in TUI" request (closed).

## Contributing

Contributions welcome! Please read the [contribution guidelines](CONTRIBUTING.md) first, then open a pull request adding your theme or resource.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the authors have waived all copyright and related or neighboring rights to this work.

Theme preview images under [`images/`](images/) are sourced from their respective upstream projects and remain the property of their authors; they are reproduced here for identification and preview purposes only.
