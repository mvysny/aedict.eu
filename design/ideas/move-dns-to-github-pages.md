# Move the aedict.eu DNS to GitHub Pages

The site builds and serves at https://mvysny.github.io/aedict.eu/; `aedict.eu` and
`www.aedict.eu` still resolve to the Aedict Online droplet (`188.166.5.90`), whose Tomcat serves
the old copy from `/var/www/aedict`. Moving the DNS makes this repo the live site.

## Current DNS (2026-10-23)

- Zone hosted by DigitalOcean DNS (`ns{1,2,3}.digitalocean.com`), SOA `hostmaster.aedict.eu`.
- `aedict.eu` `A 188.166.5.90`; no `AAAA`, `MX`, `TXT` or `CAA`.
- `www.aedict.eu` `CNAME aedict.eu`.

Nothing else lives on the domain, so the whole zone can follow the site.

## Steps

1. **Verify the domain** in GitHub → Settings → Pages → "Add a domain": it asks for a `TXT`
   record `_github-pages-challenge-mvysny.aedict.eu`. Without it, any GitHub repo can claim
   `aedict.eu` the moment the DNS points at GitHub.
2. **Add `CNAME`** to the repo root containing `aedict.eu` (or set the custom domain in the repo's
   Pages settings, which commits the same file). From then on github.io redirects there.
   Relative links keep working; nothing in the pages changes.
3. **Point the records** (values per GitHub's "Managing a custom domain" docs; re-check them
   then):
   - `aedict.eu` `A` → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `aedict.eu` `AAAA` → `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`
   - `www.aedict.eu` `CNAME` → `mvysny.github.io.`
4. **Wait for the certificate**: a few minutes of certificate errors until GitHub issues it, then
   tick "Enforce HTTPS".
5. **Check** that `http://aedict.eu/faq.html`, `http://www.aedict.eu/privacy.html` and
   `http://aedict.eu/files/jyouyou__strokeEditDistance.csv` answer through the https redirect:
   the apps, the Google Play listings and the indexer use exactly these.
6. **Clean up the droplet** (`../aedict-online`, with the owner): the `aedict.eu` `<Host>` in
   `scripts/dc-full-production/tomcat/docker/server.xml` and the `/var/www/aedict` mount.

## Open questions

- `Q_dns_host`: keep the zone at DigitalOcean DNS? It is tied to the DigitalOcean account the
  droplet lives in; `migrate-to-hetzner.md` in `../aedict-online` may retire that account, and
  then the zone moves too (to the registrar's DNS, Hetzner DNS, …).
- `Q_ttl`: lower the records' TTL a day before the switch, so a mistake is quick to undo?

## Graduation

Once aedict.eu serves from GitHub Pages: the domain line goes into the README's "Publishing"
section and the `AGENTS.md` invariant about relative links loses its github.io clause; the
droplet clean-up graduates in `../aedict-online`. Then delete this file.
