# Geicha — Art of Pleasure 🍵

Single-page storefront for Geicha premium Japanese green tea (matcha, sencha, hojicha).
Built as **one static HTML file** — no build step, no dependencies, no backend.

## What's inside

- `index.html` — the website (HTML + CSS + JS in one file)
- `assets/` — brand logos (wordmarks, hero mark, favicon) and `assets/products/` product photos
- 11 products from the THAIFEX 2026 catalog with real prices (THB)
- Size selector per product (40 g / 200 g / 1 kg) + 10 g sampler info
- Grade filters (Ceremonial / Single Origin / Premium / Hojicha / Culinary)
- Volume pricing table (1 / 3 / 10 pcs)
- Demo cart (in-memory; resets on refresh)

## Run locally

Just open `index.html` in any browser. That's it.

Or serve it (avoids any browser quirks with local files):

```bash
# Python
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploy to GitHub Pages (free hosting)

### Option A — via GitHub website (no command line)

1. Go to https://github.com/new and create a repository, e.g. `geicha-site` (Public).
2. On the repo page, click **Add file → Upload files**, drag in `index.html`, the `assets/` folder, and this `README.md`, then **Commit changes**.
3. Go to **Settings → Pages** (left sidebar).
4. Under **Build and deployment**: Source = **Deploy from a branch**, Branch = **main**, Folder = **/ (root)**. Click **Save**.
5. Wait 1–2 minutes. Your site will be live at:
   `https://<your-username>.github.io/geicha-site/`

### Option B — via command line

```bash
cd geicha-site
git init
git add .
git commit -m "Geicha storefront"
git branch -M main
git remote add origin https://github.com/<your-username>/geicha-site.git
git push -u origin main
```

Then enable Pages in **Settings → Pages** as in Option A, steps 3–5.

### Custom domain (optional)

1. In **Settings → Pages → Custom domain**, enter e.g. `www.geicha.com` and save.
2. At your domain registrar, add a CNAME record pointing `www` to `<your-username>.github.io`.
3. Tick **Enforce HTTPS** once the certificate is issued.

## Updating products & prices

All product data lives in one place — the `products` array near the bottom of `index.html`:

```js
{id:'kitami', kanji:'北', tin:'#3E5C3A', cat:'Ceremonial',
 grade:'Ceremonial · 100% First Flush', name:'Geicha Kitami Matcha',
 headline:'Nutty. Roasted. Bold.', origin:'Kyoto',
 notes:'Nutty · roasted peanut · toasted grain',
 use:'Best for koicha & straight drinking',
 prices:{'40g':680,'200g':2040,'1kg':8500}, sampler:170},
```

- Change a price → edit the number in `prices`
- Add a product → copy a block, change `id` and details
- Mark pre-order → add `preorder:'Pre-order · ships June 2026'`
- Volume pricing table is plain HTML in the `#pricing` section

Commit + push, and GitHub Pages redeploys automatically in ~1 minute.

## Taking real orders

The cart is a demo. To sell for real, wire the **checkout button** to one of:

- **LINE OA / phone** — simplest: link checkout to your LINE Official Account or sales line (093-142-8538)
- **Shopify Buy Button** — embed per-product buy buttons, Shopify handles payment & stock
- **Stripe Payment Links / Omise** — create a payment link per product+size and open it on checkout

## License / data

Product names, prices, and tasting notes from the Geicha THAIFEX 2026 catalog.
Verify prices before publishing publicly.
