# Yeng Cards Creator

Web-based admin tool for designing and exporting **Yeng** collectible trading cards.

Sister project to [`pvl_card_creator`](https://github.com/gbaaron/pvl_card_creator) — same card engine, simpler field set, tailored for Yeng collectibles (e.g. tour moments, concert commemoratives, album drops).

## What it does

A single-page, zero-backend card creator that lets you:

- Upload a photo and fill in **name** + **card title** (e.g. "Live in Pasay")
- Pick primary / secondary colors, rarity, and card number/total
- Write a bio for the card back
- Define the **physical reward** — reward description and total Yeng Credits
- See a **live preview** of Digital, Physical, and Card Back layouts as you type
- Export three self-contained HTML files + a metadata JSON as a ZIP

Each exported HTML file is fully self-contained (photo as base64, QR inline, CSS inlined) so it renders perfectly when opened standalone.

## Differences vs. `pvl_card_creator`

This version is deliberately stripped down — no jersey number, no position, no team short name, no stats grid. The card front becomes:

- **Name** (Oswald, bold, uppercase)
- **Card title** (Playfair Display italic, in primary color)
- Rarity badge + card number
- Photo background with holographic overlay and rarity glow

The physical card keeps the QR code and an autograph area (larger than the PVL version since there are no stats taking up space).

## Tech

Pure HTML / CSS / JS. No build step, no backend.

- [`qrcode-generator`](https://github.com/kazuhikoarase/qrcode-generator) via cdnjs
- [`JSZip`](https://stuk.github.io/jszip/) via cdnjs
- Google Fonts: Oswald, Rajdhani, Barlow, Barlow Condensed, Playfair Display

## Running locally

```bash
open index.html
```

## Deployment

Deployed to Netlify. `netlify.toml` publishes root as static site — no build command.

## Output format

### Physical card metadata
Each `*_physical.html` embeds reward data in three places:

1. `<meta>` tags in `<head>` (`yeng-reward`, `yeng-credits`, `yeng-redeem-url`)
2. HTML comment block (`YENG_CARDS_METADATA`)
3. `data-*` attributes on `<body>`

### QR code URL format
```
https://pvlcardgame.netlify.app?redeem=Yeng-[Name]-[CardNumber]
```
Spaces replaced with hyphens.

## Notes

- Gb logo on the card back is a placeholder SVG. Swap `GB_LOGO_SVG` in `index.html` for the real logo when ready.
- Default reward is "Unlocks the digital card" — editable per card.
