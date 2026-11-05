# Privacy policy refresh and Terms of Service

Why now: Google Play's trader declaration (deadline 2027-02-01) needs a Terms of Service link per
app, and the privacy policy Play links to is a stale blog post. Every contact address becomes
`support@aedict.eu`, deletion requests included.

## 1. One canonical privacy policy: `privacy.html`

`privacy.html` stays where it is (published URLs never move) and becomes the only copy.
Problems in today's text:

- It says dictionaries come over HTTP from `www.baka.sk`; they come from `aedict-online.eu`.
- It doesn't mention Google Play Billing (subscriptions, one-time purchases).
- It doesn't say who the controller is, what legal basis applies, or which GDPR rights users have.
- Deletion requests go to `martin@vysny.me` → `support@aedict.eu`.
- Broken markup: the `<ul>` is never closed, and the "accont" typo.

What the rewrite says, all checked against the app (dependencies: androidx, AnkiDroid API,
Billing 8; no analytics, crash reporting or ads):

- Controller: Martin Vysný, contact `support@aedict.eu`.
- Offline by design; the app collects no analytics and shows no ads.
- Dictionary downloads from `aedict-online.eu`: the server sees the IP address and the standard
  HTTP request, nothing else.
- Aedict Online sync, only when the user asks for it: username, password, notepad, SRS,
  recently viewed. Account and data deletion: e-mail `support@aedict.eu`.
- Purchases: handled by Google Play; Aedict receives only whether a product is owned, never
  payment details. Link Google's privacy policy.
- AnkiDroid export: stays on the device, via the AnkiDroid API.
- GDPR rights (access, rectification, erasure, complaint to a supervisory authority — Finland's
  is the Data Protection Ombudsman, tietosuoja.fi).

`reader/privacy.html` (Aedict Reader Popup) is accurate apart from the missing contact line; add
one. `kanjipadextension/privacy.html` belongs to a retired app; leave it alone.

## 2. Blog post → pointer

`../aedict-blog/_posts/2025-08-21-privacy-policy.md` becomes a single line linking to
`https://aedict.eu/privacy.html`, so old links still lead somewhere. Then Play Console: Aedict's
privacy policy URL → `https://aedict.eu/privacy.html`.

Also switch the other `martin@vysny.me` mentions in the blog to `support@aedict.eu`:
`2026-10-23-Aedict-Is-Alive.md`, `2019-10-23-EPWING-Support.md`, `2019-09-10-Daijirin.md`.

## 3. New page: `terms.html`

Add it to `_data/apps.yml`'s menu next to Privacy, and in Play's trader declaration give it as
each app's Terms of Service link. A draft:

> **Terms of Service**
>
> These terms apply to Aedict and its companion apps (together "the app"), published on Google
> Play by Martin Vysný, Finland, contact `support@aedict.eu`.
>
> **Using the app.** You may install and use the app on your devices for personal use. The app
> and its source code remain the property of the author.
>
> **Dictionary data.** The dictionaries are the work of their authors and are used under their
> licences: JMdict and Kanjidic2 (EDRDG, CC BY-SA 4.0), KanjiVG (CC BY-SA 3.0), Tatoeba
> (CC BY 2.0 FR), and the other sources the app lists. Those licences, not these terms, govern
> the data.
>
> **Purchases and subscriptions.** Purchases are made and paid through Google Play under Google
> Play's terms. A subscription renews automatically until you cancel it in Google Play →
> Payments & subscriptions; cancelling stops the next renewal, and you keep access until the
> paid period ends. Refunds go through Google Play; for anything Google won't resolve, write to
> `support@aedict.eu`.
>
> **Right of withdrawal (EU/EEA/UK).** Digital content starts being supplied the moment the
> purchase completes. By buying, you agree to that and acknowledge that you therefore lose the
> 14-day right of withdrawal. This doesn't affect your statutory rights if the content is
> faulty.
>
> **Aedict Online.** Sync is optional. Keep your password to yourself. An account may be
> deleted if it is used to abuse the service. You can ask for your account to be deleted at any
> time; see the Privacy Policy.
>
> **No warranty.** The app is provided as it is. The dictionaries are compiled by volunteers and
> may contain errors; don't rely on them where a mistake would be costly. To the extent the law
> allows, the author isn't liable for indirect damage or loss of data. Nothing here limits
> liability that the law doesn't allow to be limited, nor your mandatory rights as a consumer.
>
> **Changes.** These terms may change; the current version is always at
> `https://aedict.eu/terms.html`, with its date.
>
> **Law.** Finnish law applies, without taking away the protection that the law of your country
> of residence gives you as a consumer.
>
> *Last updated: YYYY-MM-DD*

## Open questions

- `Q_withdrawal_waiver`: the "you lose the right of withdrawal" paragraph only holds if the
  buyer gave express consent *before* the purchase (Consumer Rights Directive, art. 16(m)).
  Google Play's purchase sheet collects that today, while Google is the seller. From 2027-03-01
  Play's marketplace model makes the developer the seller in the EEA/UK: does Play's sheet still
  collect the consent on our behalf? Have someone qualified read this paragraph.
- `Q_reader_tos`: Aedict Reader sells nothing. Does Play want a ToS link for it anyway? The
  draft covers "companion apps", so the same URL works if it does.
- `Q_licence_versions`: check the licence versions of each dictionary source against what the
  indexer actually ships (EDRDG's current licence page, KanjiVG, Tatoeba), and list the rest.
- `Q_photocloud`: PhotoCloud isn't on aedict.eu and needs its own ToS and privacy policy in its
  own repo. Separate task.
