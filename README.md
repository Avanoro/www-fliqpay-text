# FLIQ transactional email copy

This repo now holds **only the copy for transactional emails**.

Page copy used to live here too. It moved into the website repo
([`Avanoro/www-fliqpayments`](https://github.com/Avanoro/www-fliqpayments))
under `content/<page>/content.json`, where the build reads it straight off
disk. Edit page text there, not here.

## Layout

```
email/waitlist/content.json   → the waitlist welcome email
```

## Why the email copy stayed

`functions/api/waitlist.js` in the website repo fetches this file **at request
time**, cached for five minutes:

```
https://raw.githubusercontent.com/Avanoro/www-fliqpay-text/main/email/waitlist/content.json
```

That means a reworded email goes out on the next signup without deploying the
site. Page copy has no equivalent need — it is baked into the HTML at build
time — so keeping it here only bought two copies that could drift.

## How to edit

```json
{
  "en": { "subject": "..." },
  "sv": { "subject": "..." }
}
```

- `en` = English, `sv` = Swedish.
- Change the text **to the right of the colon**, inside the quotes.
- Do **not** change the keys on the left — they map the text to its slot in the
  email template.
- Keep the quotes and commas. Accented characters (å ä ö — ·) are fine.

Commit to `main`. The change is live on the next signup once the five-minute
cache expires; no deploy needed.

## A note on the publish workflow

`.github/workflows/publish.yml` fires a Cloudflare Pages deploy hook on any
`**/*.json` push. It existed to rebuild the site when page copy changed. Since
the email copy is read at request time, a rebuild does nothing for it — the
workflow is now harmless but redundant, and can be removed whenever someone
feels like tidying up.
