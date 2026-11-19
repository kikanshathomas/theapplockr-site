# Architecture

Four hand-written HTML files, one stylesheet, and static assets. No template
engine, no bundler, and no package.json. Jekyll on GitHub Pages copies files
that are not excluded. Nothing in the HTML uses YAML front matter.

## Shared chrome

`index.html`, `download.html`, and `privacy.html` each repeat the same header
nav, footer, nav script, GoatCounter snippet, and copyright-year script. The
markup is copied, not included. `404.html` is the exception: a short hero, a
home link, and GoatCounter, with no nav and no footer.

The nav script (`#navToggle` / `#navLinks`) toggles the class `open` on the
link list and sets `aria-expanded` on the button. It does not add `open` to
the button. `assets/css/site.css` still has `.nav-toggle.open` rules for an
icon that would turn into an X. Those rules match nothing on the current pages.

The copyright script writes `2026` until the calendar year is later, then a
`2026–YYYY` range, into `#cpyear`. `404.html` has no year element.

## Home page pieces that are easy to miss

- Screenshot `<img>` tags use the PNG (`460×818`) as `src` and the WebP
  (`920×1636`) as `srcset`. The lightbox reads `data-full` on the button,
  which is the WebP path.
- Two JSON-LD blocks: a `MobileApplication` (name, Android, price `4.99` USD,
  publisher Ubersoft) and an `FAQPage` whose answers match the visible FAQ.
- `og.png` is `1024×500` and is the Open Graph and Twitter image on the home
  page and the download page.

## Download page

`download.html` draws the QR code with vendored `assets/js/qrcode.min.js`
(qrcodejs 1.0.0). The comment above the script tag records the upstream, the
date it was vendored (2026-08-01), and the sha256. The script encodes

`https://play.google.com/store/apps/details?id=com.theapplockr.app`

Layout that only this page uses is a `<style>` block in the head (`.dl`,
`.qr-card`, `#qr`). Shared badge and trust-strip rules are in `site.css`.

## Stylesheet and type

`assets/css/site.css` is the only stylesheet. Outfit is self-hosted as four
woff2 files, weights 400, 500, 600, and 700, under `assets/fonts/`. The legal
page `h1` asks for weight 800, which these files do not include, so the
browser synthesizes it. Light is the default. Dark follows
`prefers-color-scheme`. Body copy is uppercase; `.normalcase` and the legal
prose turn that off.

## Assets the pages reference

| Path | Use |
|---|---|
| `favicon.ico`, `favicon-32x32.png`, `apple-touch-icon.png` | Icons linked from every HTML file. Apple touch icon is 180×180. Favicon PNG is 32×32. |
| `assets/img/app-icon.png` | 512×512 icon in the home hero. |
| `assets/img/og.png` | 1024×500 share image. |
| `assets/img/google-play-badge.png` | Play badge on the home page and the download page. |
| `assets/img/shot-*.png` and `shot-*.webp` | Four screenshots (home, apps, permissions, settings). |
| `assets/fonts/outfit-*.woff2` | The four Outfit weights named above. |
| `assets/js/qrcode.min.js` | Download-page QR code. Third-party, vendored, minified. |

Art masters and the Play listing copies live in `theapplockr-dev` under
`store/`. The finished `og.png` in this repo is the file the dev readme says
is both the site share image and the Play feature graphic.

## The only third-party request

Each HTML file loads GoatCounter:

```html
<script data-goatcounter="https://theapplockr.goatcounter.com/count"
        async src="//gc.zgo.at/count.js"></script>
```

Fonts, CSS, images, and qrcodejs are served from theapplockr.com. The privacy
policy, sections 03 and 10, states that GoatCounter is the one other company
this site contacts. Adding a CDN script, a font host, or another analytics
tag would make that section wrong.

## Pages build

`_config.yml` sets `theme: null` so Pages does not inject a theme stylesheet.
`exclude` lists `CLAUDE.md`, `.claude`, `README.md`, `readme.md`, and `docs`.
`changelog.md` is not excluded. Jekyll's default skip of dotfiles keeps
`.gitattributes` off the site.

`theapplockr-dev` `site/` still has an empty `.nojekyll` and does not have
`_config.yml`. This repo dropped `.nojekyll` when `_config.yml` was added
(pull request #5) so the excludes would run. A `.nojekyll` file in this repo
would turn Jekyll off and publish `CLAUDE.md`, `README.md`, and `docs/`.
