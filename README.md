# Ioskeley Mono

![Ioskeley Mono Cover](assets/SocialPreview.png)

A free, open-source alternative to [Berkeley Mono](https://berkeleygraphics.com/typefaces/berkeley-mono/) — built by configuring [Iosevka](https://github.com/be5invis/Iosevka) to match its look and feel as closely as possible.

The name is a mashup: **Iosevka** + **Berkeley** = **Ioskeley**.

---

## Preview

| Ioskeley Mono | Berkeley Mono |
| --- | --- |
| ![Ioskeley Mono Sample](assets/IoskeleyMono.png) | ![Berkeley Mono Sample](assets/BerkeleyMono.png) |

> Theme: [Kintsugi Dark Flared](https://marketplace.visualstudio.com/items?itemName=ahmedhatem.kintsugi)

![Ioskeley Mono in Action](assets/InAction.png)

---

## Installation

Download the latest release from the [Releases page](https://github.com/ahatem/IoskeleyMono/releases).

### Which file should I download?

**Step 1 — Pick your use case:**

| I want to… | Download |
|---|---|
| Use it in my editor / IDE | A TTF zip |
| Use it in my terminal with icons | A Nerd Font zip |
| Use it on the web | `IoskeleyMono-Web.zip` |

**Step 2 — Pick your width:**

| Width | Best for |
|---|---|
| `Normal` | Default — works everywhere |
| `SemiCondensed` | More columns without sacrificing readability |
| `Condensed` | Maximum density |

> Not sure? Start with **Normal**.

### Installing the fonts

1. Download and unzip your chosen file
2. Select all `.ttf` files inside
3. Install on your system:
   - **macOS** — double-click any font → Install Font, or drag all into Font Book
   - **Windows** — select all → right-click → Install
   - **Linux** — copy to `~/.local/share/fonts/` then run `fc-cache -fv`

---

## Kitty Terminal (macOS)

A reliable way to get full Nerd Font icon coverage in Kitty without shipping a patched Ioskeley build: install plain **Ioskeley Mono** as your text font, install **Symbols Nerd Font Mono** alongside it, and use `symbol_map` to route icon codepoints to the symbols file.

### Prerequisites

1. Install Ioskeley Mono (see [Installation](#installation)) — any TTF zip works; you don't need the Nerd Font variant for this setup.
2. Install **Symbols Nerd Font Mono** from [NerdFontsSymbolsOnly](https://github.com/ryanoasis/nerd-fonts/releases) — grab `NerdFontsSymbolsOnly.zip` from the latest release.

### `~/.config/kitty/kitty.conf`

```conf
font_family      family="Ioskeley Mono"
bold_font        auto
italic_font      auto
bold_italic_font auto

# If you don't want ligatures
# disable_ligatures always
# font_features "Ioskeley Mono" -liga

include kitty-nerd-mappings.conf

# Emoji-only codepoints in the Dingbats block → color emoji
symbol_map U+2705,U+2728,U+274C,U+274E,U+2753,U+2754,U+2755,U+2757,U+2795,U+2796,U+2797,U+27B0,U+27BF Apple Color Emoji
```

### `~/.config/kitty/kitty-nerd-mappings.conf`

Routes every icon from the Nerd Fonts v3.x catalog to **Symbols Nerd Font Mono** (ships every icon at 1-cell width). Keep these rules **above** any broader/shotgun `symbol_map` entries — Kitty resolves `symbol_map` first-match-wins in file order.

```conf
# Pomicons
symbol_map U+E000-U+E00A Symbols Nerd Font Mono

# Powerline
symbol_map U+E0A0-U+E0A2 Symbols Nerd Font Mono
symbol_map U+E0B0-U+E0B3 Symbols Nerd Font Mono

# Powerline Extra
symbol_map U+E0A3-U+E0A3 Symbols Nerd Font Mono
symbol_map U+E0B4-U+E0C8 Symbols Nerd Font Mono
symbol_map U+E0CA-U+E0CA Symbols Nerd Font Mono
symbol_map U+E0CC-U+E0D7 Symbols Nerd Font Mono

# IEC Power Symbols (real Unicode block, re-drawn by Nerd Fonts for consistency)
symbol_map U+23FB-U+23FE Symbols Nerd Font Mono
symbol_map U+2B58-U+2B58 Symbols Nerd Font Mono

# Font Awesome Extension
symbol_map U+E200-U+E2A9 Symbols Nerd Font Mono

# Weather
symbol_map U+E300-U+E3E3 Symbols Nerd Font Mono

# Seti-UI + Custom
symbol_map U+E5FA-U+E6B7 Symbols Nerd Font Mono

# Devicons
symbol_map U+E700-U+E8EF Symbols Nerd Font Mono

# Codicons
symbol_map U+EA60-U+EC1E Symbols Nerd Font Mono

# Font Awesome
symbol_map U+ED00-U+EFCE Symbols Nerd Font Mono

# Font Awesome (legacy block — kept for back-compat with older configs)
symbol_map U+F000-U+F2FF Symbols Nerd Font Mono

# Font Logos (née Font Linux)
symbol_map U+F300-U+F381 Symbols Nerd Font Mono

# Octicons
symbol_map U+F400-U+F533 Symbols Nerd Font Mono

# Material Design Icons (Plane 1 — by far the largest set, ~6880 glyphs)
symbol_map U+F0001-U+F1AF0 Symbols Nerd Font Mono
```

Restart Kitty (or run `kitty @ load-config`) to pick up the changes.

---

## Weights

Ioskeley Mono matches Berkeley Mono's full weight axis across all widths:

| Weight | CSS value |
|---|---|
| Thin | 100 |
| ExtraLight | 200 |
| Light | 300 |
| SemiLight | 350 |
| Regular | 400 |
| Medium | 500 |
| SemiBold | 600 |
| Bold | 700 |
| ExtraBold | 800 |
| Black | 900 |

Every weight is available in both **Upright** and **Italic**.

---

## Design Choices

Ioskeley Mono uses specific character variants and custom metrics to closely match Berkeley Mono's aesthetic.

**Custom metrics** — vertical proportions, letter spacing, and parenthesis size are tuned to capture Berkeley's compact, geometric feel.

**Distinctive glyphs** — single-storey `g`, flat-arc parentheses `()`, two-circle `8`, dotted `0`, open-contour `6` and `9`, square punctuation dots, and a raised underscore.

For the full list of configuration choices, see [`private-build-plans.toml`](./private-build-plans.toml).

---

## Building from Source

The font is built automatically via GitHub Actions on every version tag push. To build locally:

```bash
git clone https://github.com/ahatem/IoskeleyMono.git
git clone --depth 1 https://github.com/be5invis/Iosevka.git

cp IoskeleyMono/private-build-plans.toml Iosevka/
cd Iosevka
npm install
npm run build -- contents::IoskeleyMono
```

Output will be in `Iosevka/dist/IoskeleyMono/`.

---

## Contributing

This project is just a build configuration on top of Iosevka — changes are often just a few lines in `private-build-plans.toml`. If you spot something off or have an idea, open an issue or send a PR. All contributions are welcome!

---

## License & Credits

Ioskeley Mono is a custom configuration of [Iosevka](https://github.com/be5invis/Iosevka). All credit for the original design and build system goes to [Belleve Invis](https://github.com/be5invis) and the Iosevka contributors.

Licensed under the [SIL Open Font License 1.1](./LICENSE).