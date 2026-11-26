# Decisions

Why this project is the way it is and not otherwise — FAQ-shaped: each entry is a question and
its current answer. Rewrite the answer when it changes; delete the entry when nobody asks any
more. An entry is earned by what it would cost to reverse — half the code base — or by research
the next person would otherwise redo (cited as its `R_`). Not an entry: windows → panels
"because that's the trend", this red over that red, `get_foo` over `is_foo?`, the testing library,
the CI host, a version bump — a comment at the site of the choice, or nothing; nothing about
`design/` itself. Cite by slug, `D_<slug>`, never by position; `grep '^## D_' design/decisions.md`
is the index. The first entry is the ruler: every later one trims to its length — which is how
long this file gets, so keep it short. When you have written an entry, re-read it against the one
above, open the doc comments it touches and cut what they already say, then cut the fat.

---

## D_jekyll_github_pages — Why Jekyll on GitHub Pages rather than the bash build on the Aedict Online droplet?

The page used to be a bash script that sourced each `_*.vars` file and ran `envsubst` over a
per-app `_template.html`, then `scp`'d the result to `/var/www/aedict` on the Aedict Online
droplet, where Tomcat served it as a second `<Host>`. That droplet has no backups, and Tomcat is
being retired (`../aedict-online`). Jekyll does what the script did: `_*.vars` became front
matter, the five templates one layout plus `_data/apps.yml`. GitHub Pages builds it on push and
serves it over https, with no server to keep. Why not keep it on a server of ours behind Caddy:
a machine to patch for static files. Why not Jekyll built by Actions: nothing here needs a
newer Jekyll, and the `github-pages` gem keeps the local build identical to GitHub's. The cost
we carry: no server-side redirects, so a URL can never move, and a DNS that points at GitHub.

## D_no_changelog — Why no changelog pages, when every app once had one?

They went stale: Aedict's stopped at 3.50.13 in March 2019, the companion apps' in 2014–2016.
The release notes are written once per release already: Aedict's into `whatsNewText`, which the
app shows after an update and Play's "What's new" repeats (`../aedict/RELEASING.md`), Reader
Popup's straight into Play. A page here would be a third copy and one more release step, a step
that went undone for seven years. No app linked to `changelog.html` and it was never one of the
URLs the AGENTS.md invariant pins, so deleting it broke no link we control. The old entries are
in git history.
