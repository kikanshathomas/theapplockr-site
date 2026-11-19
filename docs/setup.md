# Setup

Nothing to install. The site is the files in the repo root.

## Preview

From the repo root:

```sh
python3 -m http.server 8000
```

Then open:

- http://127.0.0.1:8000/
- http://127.0.0.1:8000/download.html
- http://127.0.0.1:8000/privacy.html
- http://127.0.0.1:8000/a-page-that-is-not-here for `404.html`
  (Python's server only serves `404.html` if you ask for that filename.
  GitHub Pages is what maps unknown paths to it.)

The local server does not read `_config.yml`. `README.md`, `docs/`, and
`CLAUDE.md` are fetchable on localhost. On theapplockr.com, the first two and
`CLAUDE.md` are excluded. `changelog.md` is public in both places.

There is no test suite and no lint config in this repo. A preview pass is
opening the three content pages, confirming the Play links still use
`id=com.theapplockr.app`, and confirming the privacy `<time>` still matches
the wording you shipped.

## What you edit

| Change | Where |
|---|---|
| Home, download, or policy copy | The matching HTML file. The same sentence often also sits in the home page JSON-LD or in the FAQ. |
| Shared look | `assets/css/site.css` |
| Download-page layout only | The `<style>` block in `download.html` |
| A new public URL | The HTML file, plus `sitemap.xml` if it should be crawled |

Policy wording changes update the effective date in `privacy.html` (both the
`datetime` attribute and the visible text). QA records the site change in
`changelog.md` in its own pull request. Other departments leave that file
alone.
