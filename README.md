# The App Lockr — website

Public marketing site for [The App Lockr](https://theapplockr.com), the Android
app locker from Ubersoft (`com.theapplockr.app` on Google Play).

The app locks chosen apps behind the phone's own fingerprint or PIN. It has no
account, no cloud, and no internet permission. The Play price shown on the site
is $4.99, one time.

This repository is the site GitHub Pages publishes from `main`. The app source
is [`kikanshathomas/theapplockr-dev`](https://github.com/kikanshathomas/theapplockr-dev).
The Capacitor Android project is
[`kikanshathomas/theapplockr`](https://github.com/kikanshathomas/theapplockr).

Longer notes live in [`docs/`](docs/overview.md). There is no API, so there is
no `docs/api.md`.

## Page map

GitHub Pages serves each HTML file at its filename and at the path without
`.html`. Checked against the live site on 2026-11-19.

| URL | File | Role |
|---|---|---|
| `/`, `/index.html` | `index.html` | Home: features, benefits, security notes, FAQ, Play badge |
| `/download`, `/download.html` | `download.html` | Play badge and a QR code of the Play listing |
| `/privacy`, `/privacy.html` | `privacy.html` | Privacy policy. Section 11 posts it at `/privacy`. Pages also serves `/privacy.html`. Keep this filename. |
| any other path | `404.html` | Not-found page. Pages custom 404 is on. No nav, no footer. |
| `/sitemap.xml` | `sitemap.xml` | `/`, `/download.html`, `/privacy.html` |
| `/robots.txt` | `robots.txt` | Allows all crawlers and points at the sitemap |
| `/changelog.md` | `changelog.md` | Site changelog. QA & Security owns it. Served, not linked from the pages. |

Support on every page, and the support email on the Play listing, is
`support@ubersoft.pro`. The Play listing's website is `https://theapplockr.com`.
`CNAME` is `theapplockr.com`.

## How it is hosted and published

GitHub Pages builds `main` with Jekyll (legacy build, source path `/`). The
custom domain is `theapplockr.com`, HTTPS is enforced, and the certificate also
covers `www.theapplockr.com`.

DNS, checked 2026-11-19:

- `theapplockr.com` A records: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
- `www.theapplockr.com` CNAME: `kikanshathomas.github.io`

No page has YAML front matter, so Jekyll copies published files unchanged.
`_config.yml` turns the default theme off and keeps `CLAUDE.md`, `.claude`,
`README.md`, and `docs/` off the public site. `changelog.md` stays published
because `/changelog.md` already answers.

Merging to `main` is the publish. Push to a branch and open a pull request.
A change that should go live still needs QA clearance in
`kikanshathomas/ubersoft-company` `company/audit/cleared.md` and Thomas's go.
Details: [docs/deploy.md](docs/deploy.md).

## How to edit and preview

Edit the HTML, `assets/css/site.css`, and the images in place. There is no
package, no bundler, and no generate step in this repo.

```sh
python3 -m http.server 8000
```

Open `http://127.0.0.1:8000/`. That server ignores `_config.yml`, so `README.md`
and `docs/` show up locally. They do not show up on theapplockr.com.

Leave these alone while editing copy:

- `assets/js/qrcode.min.js` is vendored. The comment in `download.html` says why it is not loaded from a CDN.
- GoatCounter (`https://theapplockr.goatcounter.com/count` via `//gc.zgo.at/count.js`) is the only third-party request. Sections 03 and 10 of the privacy policy describe it.
- `changelog.md` belongs to QA & Security.
- The effective date in `privacy.html` (the `<time>` element) moves only when the policy wording changes.

## Relation to theapplockr-dev

| Repo | What it holds |
|---|---|
| `theapplockr-dev` | App source (`app/`, `native/`), `tools/build.bat`, Play listing assets under `store/`, docs, and a `site/` tree |
| `theapplockr` | Capacitor Android project. `build.bat` syncs `native/` into it. |
| `theapplockr-site` | This repo. The site visitors and Play see. |

`build.bat` stops before any git command. It does not update this repo.
`theapplockr-dev`'s readme says an auditor copies `site/` onto this repo and
keeps files that exist only here. It names `README.md`, `.gitignore`, and
`CHANGELOG.md`. The changelog file in this repo is `changelog.md`. There is no
`.gitignore`. `docs/`, `CLAUDE.md`, and `_config.yml` also exist only here.

Checked 2026-11-19: `download.html`, `404.html`, `assets/css/site.css`,
`sitemap.xml`, `robots.txt`, and `CNAME` are the same blobs as
`theapplockr-dev` `site/`. `index.html` and `privacy.html` are not. This repo
has the 2026-10-21 system-log wording recorded in `changelog.md`. Copying
`site/` over those two files would publish the older wording again.
`theapplockr-dev` `site/` still contains `.nojekyll`. This repo uses
`_config.yml` instead, so `CLAUDE.md` stays off the public site (it 404s today).

What the app does, screen by screen, is `theapplockr-dev` `docs/overview.md`.
How it is built is `docs/architecture.md` there. Decisions are `docs/decisions.md`.

## Docs in this repo

| File | Contents |
|---|---|
| [docs/overview.md](docs/overview.md) | What the site is, who it is for, page map |
| [docs/architecture.md](docs/architecture.md) | How the pages, assets, and Pages build fit together |
| [docs/setup.md](docs/setup.md) | Local preview |
| [docs/deploy.md](docs/deploy.md) | Pages, DNS, and the copy from `theapplockr-dev` |
| [docs/ownership.md](docs/ownership.md) | Which department edits what |
| [docs/changelog.md](docs/changelog.md) | Pointer to the root changelog, which QA owns |
