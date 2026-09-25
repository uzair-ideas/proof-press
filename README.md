# Proof Press

Turn raw app screenshots into finished store artwork — in the browser, with nothing uploaded anywhere.

**Live: https://uzair-ideas.github.io/proof-press/**

Drop the plain shots straight off a phone, emulator or simulator. Pick a background, type a headline per shot, and download PNGs at exactly the sizes Google Play and the App Store ask for. The whole thing is one HTML file drawn on a `<canvas>` — no build step, no server, no account.

## What it makes

| Asset | Google Play | App Store |
|---|---|---|
| Phone screenshots | 1080 × 1920 portrait, 1920 × 1080 landscape · 2–8 files | iPhone 6.9″ 1290 × 2796 and 1320 × 2868, 6.5″ 1242 × 2688, 5.5″ 1242 × 2208 · 1–10 files |
| Tablet screenshots | — | iPad 13″ 2048 × 2732, iPad 11″ 1668 × 2388 |
| App icon | 512 × 512 | 1024 × 1024, no transparency |
| Feature graphic | 1024 × 500 | not required |

Pick **Google Play**, **App Store** or **Both** at the top of the page. The output sizes, the icon size and the checklist all follow that choice, and "Download everything as one ZIP" lays the files out in `google-play/` and `app-store/` folders.

Each screenshot row in **What the stores need** has its own size picker — Play portrait or landscape, iPhone 6.9″ / 6.5″ / 5.5″, iPad 13″ / 11″. **Build** and the one-ZIP download both use the size picked there, and the ZIP names the folder after it (`app-store/iphone-6.5/`). Picking a size in **Output size** updates the matching row too.

## How to use it

1. Drop your screenshots on the page, or use **Choose files** — you can also paste with `Ctrl+V`.
2. Pick **Publishing to**: Play, App Store, or both.
3. Write a headline for each shot in **Auto layout**, then hit **Generate layout**. It picks the layouts, angles, splits and backdrop for you; your words are kept.
4. Fine-tune from there — background, backdrop shape, device frame, font, and per-shot text and phone position.
5. Download a single PNG, the whole set as a ZIP, or everything including icon and feature graphic.

While you work the controls, a **live rail** pins the proofs under the top bar so a colour or shape change is visible immediately instead of a scroll away. Click any proof in the rail to jump to it.

## Controls

**Across the whole set**
- 8 background themes plus a free colour picker and gradient angle
- Backdrop shapes: card, arcs, dots, band, none — with position and size
- Device frame: dark, light, or bare (no frame)
- Headline font: Archivo, Bricolage Grotesque, Space Grotesk, Instrument Serif
- Text colour: auto, light, dark
- **One long image** mode paints one background across the whole set and slices it, so the screenshots read as a single picture when scrolled. Upload in the numbered order or the picture breaks.

**Per shot**
- Headline and supporting line
- Layout: text above, below, tilted, floating, or none
- Title position (6 anchors), alignment, text size and angle
- Phone size, offset, rotation — drag the corner handles directly on the selected proof
- **Split this phone across 2 panels**, so one device spans two screenshots

**Store assets**
- App icon from your logo, with a gradient/solid/logo-only backdrop and a corner guide showing what the stores round off
- Feature graphic with three layouts (icon left, centred, phone right) and the same backdrop shapes

## Privacy

Nothing leaves the browser. The images are read with `FileReader`, drawn on a canvas and saved straight back to disk. There is no server, no analytics and no upload. The only network request the page makes is to Google Fonts for the four headline typefaces.

## Running it locally

One file, no dependencies:

```bash
git clone https://github.com/uzair-ideas/proof-press.git
cd proof-press
# open index.html in a browser, or serve it:
python -m http.server 8000
```

Opening `index.html` directly with `file://` works too.

## Notes and limits

- Needs a Chromium, Firefox or Safari build with `<canvas>`, `IntersectionObserver` and ES5 — anything from the last few years.
- The ZIP is written by hand (stored, uncompressed) so there is no library to load. PNGs are already compressed, so the size difference is negligible.
- Saving uses the browser's normal download flow. Inside a Claude artifact it uses the host's downloads capability instead, so it works there as well.
- Fonts are loaded from Google Fonts. Offline, the page still works but falls back to system typefaces, and the rendered PNGs will use those.

## Deploying

The repo is served by GitHub Pages from `main` at the repository root. `.nojekyll` is there so Pages serves the file as-is. Push to `main` and the site rebuilds:

```bash
git add -A
git commit -m "Update"
git push
```

## Files

```
index.html   the whole app — markup, styles and script
.nojekyll    tells GitHub Pages to skip Jekyll processing
README.md    this file
```
