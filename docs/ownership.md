# Ownership

| Work | Who edits it |
|---|---|
| Sentences on the pages, and which screenshots are shown | Marketing |
| Icon, screenshots, `og.png`, Play badge art | Design. Masters live in `theapplockr-dev` `store/`. |
| Claims about what the app does (permissions, logging, price, offline) | Product, checked against the shipped app in `theapplockr-dev` |
| `privacy.html` | Product for the wording, QA & Security for the review. This is the policy URL. |
| `changelog.md` | QA & Security only. Other departments do not edit it. |
| Pages, DNS, `CNAME`, `_config.yml` | DevOps |
| Docs, comments, and removal of unused files | Engineering |

A pull request that changes the live site follows the company review order:
the department that did the work, then DevOps, then QA, then Thomas merges.
QA clearance is a line in `kikanshathomas/ubersoft-company`
`company/audit/cleared.md`.

`CLAUDE.md` is the agent working rules. It is excluded from the public site.
It is not a substitute for this folder.

This product has no Punchi Park or Punchi Guide paths. Those "do not edit"
zones are in `punchi-site` only.
