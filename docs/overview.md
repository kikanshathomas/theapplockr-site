# Overview

The App Lockr's public website, https://theapplockr.com.

It is a static marketing site for one Android app: lock chosen apps behind the
phone's fingerprint or PIN, with no account, no cloud, and no internet
permission. The Play package is `com.theapplockr.app`. The price the pages
state is $4.99, one time. Ubersoft publishes the app and the site.

People who land here are deciding whether to install the app. The public Play
listing text gives the website as `https://theapplockr.com` and support as
`support@ubersoft.pro`. Section 11 of the policy says the current text lives
at `theapplockr.com/privacy`. The Ubersoft site's product list links that
same path (`ubersoft.pro/privacy.html`).

## Repos

| Repo | Role |
|---|---|
| `kikanshathomas/theapplockr-site` | This repo. GitHub Pages publishes `main` to theapplockr.com. |
| `kikanshathomas/theapplockr-dev` | App source, native locker, build, Play listing assets, and a `site/` tree an auditor copies from. |
| `kikanshathomas/theapplockr` | Capacitor Android project the build syncs into. |

What the app does is written in `theapplockr-dev` `docs/overview.md`. This
folder describes the website only.

## Pages

| URL | File |
|---|---|
| `/` and `/index.html` | `index.html` — home (features, benefits, security notes, FAQ) |
| `/download` and `/download.html` | `download.html` — Play badge and QR code |
| `/privacy` and `/privacy.html` | `privacy.html` — privacy policy, effective date in the header `<time>` |
| any unknown path | `404.html` — short not-found page, no nav or footer |
| `/sitemap.xml` | Lists `/`, `/download.html`, and `/privacy.html` |
| `/robots.txt` | Allows `/` and names the sitemap |
| `/changelog.md` | Site changelog. QA owns the file. No page links to it. |

`CNAME` is the single line `theapplockr.com`.

## Who it is for

- A visitor comparing the app to other lockers, and the Play reviewer following the privacy URL.
- Marketing and Design, when the words or screenshots change.
- Engineering, when the pages, comments, or unused files change.
- DevOps, for Pages and DNS.
- QA & Security, for the changelog and for clearance before `main`.
