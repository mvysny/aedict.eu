# Move the aedict.eu DNS to GitHub Pages

The site builds and serves at https://mvysny.github.io/aedict.eu/; `aedict.eu` and
`www.aedict.eu` still resolve to the Aedict Online droplet (`188.166.5.90`), whose Tomcat serves
the old copy from `/var/www/aedict`, http only (`Q_aedict_eu_https` in `../aedict-online`).
Moving the DNS makes this repo the live site, and gives it https.

## Current DNS (2026-10-23)

- Registrar GoDaddy; zone hosted by DigitalOcean DNS (`ns{1,2,3}.digitalocean.com`), SOA
  `hostmaster.aedict.eu`.
- `aedict.eu` `A 188.166.5.90`, TTL 3600; no `AAAA`, `MX`, `TXT` or `CAA`.
- `www.aedict.eu` `CNAME aedict.eu`, TTL 43200.

Nothing else lives on the domain, so the whole zone can follow the site. Every file deployed in
`/var/www/aedict` is in this repo (checked 2026-10-23), so no URL is lost.

## Steps

0. **Lower the TTLs a day ahead**: both records to 300, so a mistake undoes in minutes rather than
   in the `www` CNAME's 12 hours. Raise them back once step 5 passes.
1. **Verify the domain** in the *account's* settings (github.com/settings/pages → "Add a domain"),
   not the repo's: it asks for a `TXT` record `_github-pages-challenge-mvysny.aedict.eu`. Without
   it, any GitHub repo can claim `aedict.eu` the moment the DNS points at GitHub.
2. **Set the custom domain** `aedict.eu` in the repo's Pages settings (or
   `gh api -X PUT repos/mvysny/aedict.eu/pages -f cname=aedict.eu`); with the legacy build this
   commits a `CNAME` file to `master`, so pull it. GitHub wants this before step 3, against
   takeover. From then on github.io redirects to `aedict.eu`, which serves the droplet's older copy
   until step 3, so do step 3 right after. Relative links keep working; nothing in the pages changes.
3. **Point the records** (values per GitHub's "Managing a custom domain" docs, re-checked
   2026-10-23):
   - `aedict.eu` `A` → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `aedict.eu` `AAAA` → `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`
   - `www.aedict.eu` `CNAME` → `mvysny.github.io.`; GitHub redirects `www` to the apex.
4. **Wait for the certificate**: minutes, up to 24 hours, of certificate errors until GitHub issues
   it, then "Enforce HTTPS" (`gh api -X PUT repos/mvysny/aedict.eu/pages -F https_enforced=true`).
5. **Check** that `http://aedict.eu/faq.html`, `api.html`, `export.html`, `privacy.html`,
   `http://www.aedict.eu/` and `http://aedict.eu/files/jyouyou__strokeEditDistance.csv` answer
   through the https redirect: the apps, the Google Play listings and the indexer (`wget`, which
   follows it) use exactly these.
6. **Clean up the droplet** (`../aedict-online`, with the owner): the `aedict.eu` `<Host>` in
   `scripts/dc-full-production/tomcat/docker/server.xml` and the `/var/www/aedict` mount.

## Decided

- Keep the zone at DigitalOcean DNS for now. It is tied to the droplet's DigitalOcean account, and
  `migrate-to-hetzner.md` in `../aedict-online` may retire that account; the zone then moves on its
  own (registrar's DNS, Hetzner DNS, …), a handful of records to re-create.
- Lower the TTLs first (step 0).

## Graduation

Once aedict.eu serves from GitHub Pages: the domain line goes into the README's "Publishing"
section and the `AGENTS.md` invariant about relative links loses its github.io clause. In
`../aedict-online`: the droplet clean-up, `modernize-aedict-eu-website.md` graduates,
`migrate-to-hetzner.md` drops its "`www.aedict.eu` on its own VM" first step, and
`Q_aedict_eu_https` is answered. Then delete this file.
