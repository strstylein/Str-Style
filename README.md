# STR Style — strstyle.in

Static, dependency-free site (plain HTML/CSS/JS — no build step) covering three routes:

```
/               → STR Style parent landing page
/salon          → STR Salon (black + metallic gold)
/tailors        → STR Tailors (ivory + rose gold)
```

## Why this structure never 404s on refresh

Instead of a single-page app with JS-based routing (which needs special
server rewrite rules to avoid 404s on `/salon` or `/tailors`), each route
is a **real folder with its own `index.html`**:

```
strstyle/
├── index.html          ← "/"
├── robots.txt
├── sitemap.xml
├── .htaccess            ← HTTPS + non-www canonical (Apache hosts)
├── salon/
│   └── index.html       ← "/salon"
├── tailors/
│   └── index.html       ← "/tailors"
└── assets/
    ├── css/  (main.css, salon.css, tailors.css)
    └── js/   (main.js)
```

Any static web server (Apache, Nginx, GitHub Pages, Netlify, Vercel,
Cloudflare Pages, standard cPanel hosting) serves `salon/index.html`
automatically for both `/salon` and `/salon/` — no rewrite rules, no
client-side router, no 404 on direct load or refresh.

## Deploying

1. Upload everything inside this folder to your web root (e.g. `public_html`
   on cPanel hosting), keeping the folder structure intact.
2. Point `strstyle.in` DNS at your host, enable a free SSL certificate
   (Let's Encrypt / AutoSSL — most Indian hosts include this).
3. Keep `.htaccess` in the root if you're on Apache — it forces HTTPS and
   redirects `www.strstyle.in` → `strstyle.in` so you have one canonical URL.
   If you're on Nginx or a platform like Netlify/Vercel instead, set the
   equivalent HTTPS-redirect and www-redirect rule in that platform's
   settings — `.htaccess` only works on Apache.

## After going live

- **Google Search Console**: verify `strstyle.in`, submit
  `https://strstyle.in/sitemap.xml`.
- **Google Business Profile**: create separate listings for STR Salon and
  STR Tailors (they're two businesses at two door numbers on the same
  street) using the exact name, address and phone number already on each
  page — matching NAP (name/address/phone) exactly helps local ranking.
- **Google Analytics**: drop your GA4 snippet just before `</head>` on all
  three `index.html` files.

## Images

No real photos were supplied, so the Gallery sections currently use
line-drawn placeholder tiles instead of stock or invented photography.
Swap them for real shop/work photos in `assets/img/` when available —
each `<img>` should get a descriptive `alt` (e.g. "Beard trim in progress
at Str Salon, Thoothukudi" / "Hand embroidery detail on a blouse at Str
Tailors"). Also add `assets/img/og-strstyle.jpg`, `og-salon.jpg` and
`og-tailors.jpg` (1200×630px) — these are already referenced in the
Open Graph tags and will make link previews on WhatsApp/Facebook/Twitter
show a real image once added.

## Content still using placeholder categories

Service names on `/salon` and `/tailors` are real service categories, but
no prices were provided, so **no pricing is shown anywhere** — add prices
directly in the `.service` / `.service-row` blocks if you want them listed.
