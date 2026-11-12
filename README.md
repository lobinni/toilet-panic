# TOILET PANIC — Landing Page

The public website for the game: a short introduction plus the Privacy Policy used for the
Google Play Console listing.

**This folder is 100% self-contained.** It is plain HTML, CSS and images with **no build step**,
no dependencies and no references to anything outside this folder. Push it to GitHub and point
Vercel at it — it just serves.

---

## Contents

```
landing/
├── index.html               # game introduction (hero, about, features, gallery, availability)
├── privacy-policy/
│   └── index.html           # the URL you paste into Google Play Console
├── 404.html
├── styles.css
├── icon.svg
├── robots.txt
├── vercel.json              # clean URLs + cache/security headers
└── images/                  # every image used by the pages (self-contained)
    ├── logo.png / logo.webp
    ├── favicon.png / apple-touch-icon.png
    ├── hero-desktop.jpg|.webp / hero-mobile.jpg|.webp
    ├── feature.jpg|.webp     (destruction + hazards)
    ├── bathroom.jpg          (the room)
    └── og.jpg                (1200×630 social share card)
```

There is deliberately **no playable web build here**. The public release is the Android app;
the browser build lives in the main game repo and is used only for development and testing.

---

## Deploying to Vercel

1. Push this `landing/` folder to a GitHub repository (it can be its own repo, or a subfolder).
2. In Vercel: **Add New → Project → import the repository**.
3. Configure:
   - **Framework Preset:** `Other`
   - **Root Directory:** `landing` (only if the repo contains the whole project; skip if the repo root *is* this folder)
   - **Build Command:** leave empty
   - **Output Directory:** leave empty (Vercel serves the folder as static files)
   - **Install Command:** leave empty
4. Deploy. Vercel gives you a URL such as `https://<project>.vercel.app`.

Your Privacy Policy URL for Google Play Console is then:

```
https://<your-domain>/privacy-policy/
```

Verify it loads in a private/incognito window (no login, no redirect) before submitting.

---

## Before you publish — required edits

| What | Where | Why |
|---|---|---|
| Developer / publisher name | `privacy-policy/index.html` — replace the `OWNER_INPUT_REQUIRED` line | Google Play requires the responsible entity to be identified |
| Privacy contact email | `privacy-policy/index.html` — replace the second `OWNER_INPUT_REQUIRED` line | Users and Google must have a contact route |
| Effective / last-updated date | `privacy-policy/index.html` — the `.meta` paragraph | Keep accurate when you change the policy |
| Copyright name | footer in `index.html`, `privacy-policy/index.html`, `404.html` | Currently generic |

Both `OWNER_INPUT_REQUIRED` markers are visibly highlighted in red on the page, so they cannot be
shipped by accident.

### When the Google Play listing goes live

In `index.html`, replace the Coming Soon badge:

```html
<span class="badge-soon" role="note">GOOGLE PLAY — COMING SOON</span>
```

with the real link:

```html
<a class="btn-play" href="https://play.google.com/store/apps/details?id=com.toiletpanic.game"
   rel="noopener">DOWNLOAD ON GOOGLE PLAY</a>
```

(There is already a `.btn-play` style for this.) Do the same in the `#availability` section.

### Adding a sitemap (optional, after you have a domain)

Sitemaps need absolute URLs, so one is intentionally not shipped. Once you know the domain,
create `sitemap.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url><loc>https://YOUR-DOMAIN/</loc></url>
  <url><loc>https://YOUR-DOMAIN/privacy-policy/</loc></url>
</urlset>
```

and append `Sitemap: https://YOUR-DOMAIN/sitemap.xml` to `robots.txt`.

---

## Updating the artwork

The images were produced from the game project's asset pipeline. To refresh them, export new
files from the game repo and copy them into `images/` using the **same filenames**. Nothing else
needs to change, and this folder stays self-contained.

Recommended sizes: hero ≤1200px wide, gallery ≤1200px wide, OG card exactly 1200×630,
favicon 64×64, apple-touch-icon 180×180, logo 256×256.

---

## Accuracy note

The Privacy Policy states that the game collects no personal data, has no accounts, no ads,
no analytics and no tracking. That reflects an audit of the actual application code and its
dependencies. **If the app ever adds an SDK, analytics, ads or any network feature, this page must
be updated before that version is published** — Google Play requires the policy and the Data
Safety form to match real behaviour.
