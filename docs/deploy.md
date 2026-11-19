# Deploy

GitHub Pages publishes this repo. Checked with the Pages API on 2026-11-19:

| Setting | Value |
|---|---|
| Source | branch `main`, path `/` |
| Build | `legacy` (Jekyll) |
| Custom domain | `theapplockr.com` (`CNAME`) |
| Also on the certificate | `www.theapplockr.com` |
| HTTPS | enforced, certificate approved |
| Custom 404 | on (`404.html`) |
| Public | yes |

DNS the same day:

- `theapplockr.com` A: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
- `www.theapplockr.com` CNAME: `kikanshathomas.github.io`

Those four A records are GitHub Pages' apex addresses. There is no workflow
file in `.github/`. A push to `main` is the deploy.

## How a change ships

1. Branch off `main`. Do not push to `main` directly.
2. Edit the files. Leave `changelog.md` for QA & Security.
3. Open a pull request into `main`.
4. DevOps reviews it, then QA. Because the merge is the live site, QA records
   clearance in `kikanshathomas/ubersoft-company` `company/audit/cleared.md`,
   and Thomas gives the go, before anyone merges.
5. Pages rebuilds `main`. The live site can lag the merge by a few minutes,
   and the CDN caches responses (the live responses on 2026-11-19 sent
   `cache-control: max-age=600`).

After a merge, compare a live URL with the file in git before calling it
published. A cache-busting query string avoids a stale copy:

```sh
curl -s "https://theapplockr.com/privacy.html?v=$(date +%s)" | cmp - privacy.html
```

HTML comments and excluded markdown are the only bytes that should differ
from what a visitor's browser paints. The comparison above is against the
file, so it includes comments.

## What has to keep answering

| URL | Why |
|---|---|
| `https://theapplockr.com/` | Play listing website |
| `https://theapplockr.com/privacy` and `/privacy.html` | Policy section 11 posts the policy at `/privacy`. Both returned 200 on 2026-11-19. ubersoft.pro links `/privacy`. |
| `https://theapplockr.com/download` and `/download.html` | Nav "Get the app", and the sitemap entry for the `.html` path |
| `mailto:support@ubersoft.pro` | Footer, policy section 12, and the Play support email |
| `https://play.google.com/store/apps/details?id=com.theapplockr.app` | Every store badge and the QR code |

`sitemap.xml` lists the three public HTML URLs with the `.html` suffix for
the two inner pages, and `/` for the home page.

## Copy from theapplockr-dev

`theapplockr-dev` `tools/build.bat` does not publish this site. The dev
readme says an auditor copies `site/` onto this repo and does not delete
`README.md`, `.gitignore`, or `CHANGELOG.md`.

On 2026-11-19 these paths were the same blob in both places: `download.html`,
`404.html`, `assets/css/site.css`, `sitemap.xml`, `robots.txt`, `CNAME`.
`index.html` and `privacy.html` were not. This repo has the system-log
wording from 2026-10-21. `site/` in the dev repo is the older text.

`site/` also still has `.nojekyll`. This repo does not. Pages is running
Jekyll so `_config.yml` can exclude `CLAUDE.md`, `README.md`, and `docs/`.
Putting `.nojekyll` back would publish those files at theapplockr.com.

`site/` in the dev repo still has `assets/theapplockr-fgs-demo.mp4` and
`assets/img/app-icon-512.png`. This repo removed them because nothing here
linked them. A later copy of `site/` will bring both files back unless that
tree is cleaned in its own pull request.
