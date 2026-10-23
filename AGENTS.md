# aedict.eu

## What this is

The Aedict home page, with the pages of its companion apps (Reader Popup, OCR, KanjiPad
extension, KanjiDraw Practice): what each app does, its FAQ, privacy policy and changelog, and
Aedict's export and API reference. Plain HTML pages built by Jekyll and served by GitHub Pages;
the apps themselves are elsewhere.

## Promises

- **Plain static pages.** No server-side code and no tracking; any static host can serve the built `_site/`.

## Design docs

| File | Owns | Loaded |
|---|---|---|
| `README.md` | the pitch, running it locally, publishing | — |
| `AGENTS.md` (this) | promises, invariants, the module map, conventions, commands | every turn |
| `design/decisions.md` | why this and not that — `D_` entries, FAQ-shaped | lazy |
| `design/ideas/` | loose ideas, one per file, deleted once graduated into the files above | lazy |

Every fact lives in exactly one of these; the others link to it.

## Invariants

- **A published URL never moves.** Installed apps (`../aedict`), the Google Play listings and the indexer link to `faq.html`, `api.html`, `export.html`, `privacy.html`, `<app>/index.html` and `files/jyouyou__strokeEditDistance.csv`, and Pages has no redirects. See `D_jekyll_github_pages`.
- **Links are relative, never root-absolute.** The layout's `app.root` relies on it, and the site then serves under any path: `aedict.eu`, or a fork's github.io project URL.
- **Everything a page loads is https.** An `http://` script, stylesheet, image or iframe is blocked as mixed content.
- **A file that is not part of the site is in `_config.yml`'s `exclude`.** Jekyll publishes everything else, Markdown included.

## Module map

- `*.html` at the root — Aedict's pages; `reader/`, `ocr/`, `kanjipadextension/`, `kanjidrawpractice/` — the companion apps'.
- `_layouts/default.html` — the one layout: header, menu, intro, footer.
- `_data/apps.yml` — per app: title, menu, reviews, `root`; `_config.yml` picks the app per directory.
- `_includes/intro/<app>.html` — each app's intro and store badges under the header.
- `css/`, `js/`, `images/`, `templatemo_style.css` — the shared templatemo 388 "Runner" theme.
- `files/` — data files other projects download.
- `CNAME` — the custom domain `aedict.eu`; GitHub's Pages settings write it.

## Conventions

- **Jekyll 3.10 through the `github-pages` gem**, nothing GitHub Pages' own build lacks.
- **A page is HTML with a `title:` front matter**; the layout and the app come from `_config.yml` defaults.
- **Shared assets live once at the root**; an app's directory holds only its own icon and screenshots, and the layout reaches the shared ones through `app.root`.
- **Public repo: no secrets.**

## Commands

- `bundle config set --local path vendor/bundle && bundle install` — once, gems into `vendor/`.
- `bundle exec jekyll serve` — the site at http://127.0.0.1:4000/, rebuilt on save.
- `bundle exec jekyll build` — the site into `_site/`.
- Push to `master` — GitHub's `pages-build-deployment` run builds and publishes it; there is no other CI.
- `design/verify_design_tripwires.sh` — the doc-layer checks; hooked into no build.

## Maintenance of this file

Loaded every turn; cap 34 KB, a module's own `AGENTS.md` 10 KB. Over it, in this order:
delete what has no home — status, history, class lists, what the code already says; trim
each line to its fact plus one clause and send the explanation home — why →
`design/decisions.md`, how across symbols → `design/architecture.md`, how in one symbol →
its doc comment, what upstream does → `design/research.md`; only then a module's own
`AGENTS.md`, peripheral modules first, never the core. Never paraphrase a lazy entry into a
line here. `design/verify_design_tripwires.sh` checks the caps and the cites.
