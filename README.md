# aedict.eu

The Aedict home page, with the pages of its companion apps (Reader Popup, OCR, KanjiPad
extension, KanjiDraw Practice): plain HTML pages built by Jekyll and served by GitHub Pages.

## Editing

- A page is an `.html` file with a `title:` front matter; `_layouts/default.html` wraps it.
- What differs per app (title, menu, reviews) is in `_data/apps.yml`, the intro under the header
  in `_includes/intro/<app>.html`. `_config.yml` picks the app per directory.
- Shared css/js/images live at the root; an app's directory holds only its own icon and
  screenshots.

**Never rename or move a page.** Installed apps and the Google Play listings link to
`faq.html`, `api.html`, `export.html`, `privacy.html` and `<app>/index.html`, and the Aedict
indexer downloads `files/jyouyou__strokeEditDistance.csv`.

## Running locally

Ruby with Bundler; the `github-pages` gem pins the Jekyll and plugins GitHub builds with.

```
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll serve
```

then open http://127.0.0.1:4000/.

## Publishing

Push to `master`; GitHub Pages builds it from the branch root.
