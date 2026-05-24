# mohsindev369-resources

Content repo for [mohsindev369.dev/resources](https://mohsindev369.dev/resources).

Each folder is one product. The actual product file lives on LemonSqueezy. This repo holds the page content, metadata, and checkout link only.

---

## Adding a New Product

1. Create a new folder: `your-product-slug/`
2. Add `resource.json` inside it (see schema below)
3. Optionally add a `cover.png` (1200x630px recommended)
4. **Add the slug to `manifest.json`** at the repo root — the site reads this file to discover products
5. Push to `main`
6. Redeploy the site on Vercel, the new product appears automatically

### Why a manifest?

The site loads products via `raw.githubusercontent.com` (GitHub's CDN), not the GitHub REST API. This avoids the 5000 req/hr authenticated rate limit entirely, no token needed. The trade-off: we can't list folders dynamically, so `manifest.json` tells the site which slugs exist.

```json
{
  "resources": ["ai-cheat-sheet", "your-new-product-slug"]
}
```

---

## resource.json Schema

```json
{
  "id": "your-product-slug",
  "title": "Product Title",
  "description": "Short description shown on the listing card (1-2 sentences).",
  "longDescription": "Hero paragraph shown on the product detail page. Make it compelling.",
  "price": "Free",
  "priceNote": "Pay what you want",
  "format": "PDF, 11 pages",
  "tags": ["Tag1", "Tag2", "Tag3"],
  "featured": false,
  "order": 2,
  "downloadUrl": "https://mohsindev369.lemonsqueezy.com/checkout/buy/YOUR_CHECKOUT_ID",
  "relatedBlog": "/blog/your-blog-slug",
  "images": ["cover.png", "page2.png", "page3.png"],

  "contentSummary": [
    "Bullet point shown on listing card (keep under 6 words)",
    "Another bullet point",
    "Another bullet point",
    "Another bullet point"
  ],

  "previewItems": [
    { "label": "Short Label", "text": "One insight from the product shown on the listing card." },
    { "label": "Another Label", "text": "Another insight." }
  ],

  "whatsInside": [
    "Full sentence describing what's covered (shown on detail page)",
    "Another item"
  ],

  "previewTips": [
    { "label": "Tip Label", "tip": "A technique or insight from the product shown as a preview on the detail page." }
  ],

  "whoIsItFor": [
    "Freelancers building client websites",
    "Developers who want to improve their SEO knowledge"
  ],

  "faq": [
    { "q": "Question?", "a": "Answer." }
  ],

  "seo": {
    "title": "SEO page title (50-60 chars)",
    "description": "Meta description (120-160 chars)",
    "schemaDescription": "Optional: longer description for Product schema. Falls back to description if omitted.",
    "keywords": ["keyword one", "keyword two"]
  }
}
```

### Field Notes

| Field | Required | Notes |
|---|---|---|
| `id` | yes | Must match the folder name exactly |
| `order` | no | Lower number = appears first on listing page |
| `relatedBlog` | no | Omit if no related blog post |
| `format` | no | e.g. "PDF, 2 pages" or "PDF + HTML checklist" |
| `images` | no | Array of image filenames in this folder. First = listing card thumbnail. All shown as gallery on detail page. |
| `featured` | no | Reserved for future use |
| `previewTips` | no | Omit array if no tips to show |
| `whoIsItFor` | no | Omit array if not applicable |
| `faq` | no | Omit array if no FAQ |

### Price Values

- Free product: `"price": "Free"`, `"priceNote": "Pay what you want"`
- Paid product: `"price": "$29"`, `"priceNote": "One-time purchase"`

---

## Repo Structure

```
mohsindev369-resources/
  ai-cheat-sheet/
    resource.json
  website-production-ready-toolkit/
    resource.json
    cover.png         (optional)
  ...
```
