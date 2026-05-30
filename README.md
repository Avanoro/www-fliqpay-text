# FLIQ website text

All editable copy for the FLIQ marketing site lives here, split out of the
HTML so it can be changed without touching code. Edits to `main` go live on the
site automatically (see "How updates reach the site" below).

## Layout

Each folder matches a page on the site:

```
index/content.json                      → home page
careers/content.json                    → careers landing
press/content.json                      → press page
careers/account-manager/content.json    → job pages
careers/brand-communications-lead/content.json
careers/full-stack-developer/content.json
careers/mobile-app-developer/content.json
roadmap/invoice-payments/content.json   → roadmap feature pages
roadmap/crossborder-payments/content.json
roadmap/offline-payments/content.json
roadmap/gift-cards/content.json
roadmap/split-pay/content.json
roadmap/bonus-system/content.json
roadmap/in-store-payments/content.json
roadmap/start-accepting/content.json
```

## How to edit text

Open the `content.json` for the page. It looks like:

```json
{
  "en": {
    "heroLine1": "Give value,",
    "heroLede": "Turn your gift cards into a new revenue stream..."
  },
  "sv": {
    "heroLine1": "Ge värde,",
    "heroLede": "Förvandla era presentkort till en ny intäktström..."
  }
}
```

- `en` = English, `sv` = Swedish.
- Edit the text **on the right side of the colon**, inside the quotes.
- Do **not** change the keys (left side, e.g. `heroLine1`) — they link the text
  to its place on the page.
- Keep the quotes and the trailing commas. Special characters (— · å ä ö) are fine.

Commit to `main` (or open a PR and merge it).

> **Job pages:** Swedish (`sv`) is filled in; English (`en`) fields are blank,
> ready for translation. Until filled, those pages display Swedish.

## How updates reach the site

The site loads these files through the jsDelivr CDN, pinned to `@main`:

```
https://cdn.jsdelivr.net/gh/Avanoro/www-fliqpay-text@main/<page>/content.json
```

jsDelivr caches each file for up to **12 hours**, so an edit may take that long
to appear on its own. To make it appear **immediately**, purge the cache for the
files you changed by visiting (in a browser, once each):

```
https://purge.jsdelivr.net/gh/Avanoro/www-fliqpay-text@main/roadmap/gift-cards/content.json
```

(Replace the path with the file you edited.) After the purge returns success,
reload the site and the new text is live. Cloudflare on the site side may add a
short additional cache; a hard refresh clears that.
