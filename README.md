# aedict.eu

The Aedict home page, with the pages of its companion apps (Reader Popup, OCR, KanjiPad
extension, KanjiDraw Practice): what each app does, its FAQ, privacy policy and changelog, and
Aedict's export and API reference. Plain HTML pages built by Jekyll and served by GitHub Pages;
the apps themselves are elsewhere.

## Running locally

Ruby with Bundler; the `github-pages` gem pins the Jekyll and plugins GitHub builds with.

```
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll serve
```

then open http://127.0.0.1:4000/.

## Publishing

Push to `master`; GitHub Pages builds it from the branch root and serves it at
https://mvysny.github.io/aedict.eu/.
