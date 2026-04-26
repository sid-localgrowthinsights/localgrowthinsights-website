# Local Growth Insights — Website

Production-ready static website for **localgrowthinsights.com**.

## Files included

| File | Purpose |
|---|---|
| `index.html` | Home page (hero, 14 signals table, pricing, FAQ) |
| `report.html` | $97 audit sales/checkout page |
| `grade.html` | Free GBP grade tool (interactive prototype) |
| `services.html` | All three service tiers in detail |
| `about.html` | Company story, principles, India transparency section |
| `case-studies.html` | Empty state now, Founding Partner program |
| `contact.html` | Contact form + direct contact info |
| `privacy.html` | Privacy policy |
| `terms.html` | Terms of service |
| `refunds.html` | Refund policy |
| `styles.css` | Shared stylesheet (typography, layout, colors) |

## Deployment

### Option 1: Cloudflare Pages (recommended — free, fast, global CDN)

1. Sign up at https://pages.cloudflare.com (free)
2. Click "Create a project" → "Direct Upload"
3. Drag the entire folder of HTML files + styles.css into the upload zone
4. Set the custom domain to `localgrowthinsights.com` (point your DNS NS records or CNAME to Cloudflare)
5. Live in 2 minutes

### Option 2: GitHub Pages (also free)

1. Create a new GitHub repo
2. Push these files to the `main` branch
3. Settings → Pages → Source: deploy from `main` branch, root directory
4. Add custom domain in Pages settings
5. Update DNS A records to point to GitHub Pages IPs

### Option 3: Netlify (free tier)

1. Sign up at https://netlify.com
2. "Add new site" → drag folder
3. Set custom domain

## Before going live — checklist

- [ ] Replace placeholder phone number `+1 (XXX) XXX-XXXX` (search & replace across all files)
- [ ] Update Gumroad/Stripe URL in `report.html` (line ~600 — `gumroadUrl` variable)
- [ ] Connect contact form in `contact.html` to a service like Formspree or FormSubmit
- [ ] Connect grade tool in `grade.html` to your real backend (replace `simulateScrape()`)
- [ ] Add a real headshot for the "About" page if you want to add one
- [ ] Add favicon (place `favicon.ico` and `favicon.svg` in root folder)
- [ ] Add Open Graph image for social sharing (`og-image.png`, 1200×630)
- [ ] Set up Plausible.io or similar privacy-friendly analytics

## To enable the real grade tool

The `grade.html` page currently uses simulated data. To make it real:

1. Build a small backend endpoint (Python Flask/FastAPI) that:
   - Accepts POST: `{ practice: "...", city: "..." }`
   - Calls your existing GBP scraper for that practice
   - Returns JSON: `{ reviews, velocity, rating, categories, photos, posts, qa, completeness }`
2. Host the backend on Cloudflare Workers, Render, Railway, or your own server
3. In `grade.html`, replace the `simulateScrape()` function with:
   ```js
   async function simulateScrape(practice, city) {
       const r = await fetch('https://your-backend.com/grade', {
           method: 'POST',
           headers: { 'Content-Type': 'application/json' },
           body: JSON.stringify({ practice, city })
       });
       return r.json();
   }
   ```

## Design system

- **Colors**: Defined as CSS variables in `:root` of every page
  - `--ink` (deep black): primary text and dark backgrounds
  - `--paper` (warm off-white): main background
  - `--accent` (forest green #0F3F2E): highlights and links
  - `--accent-2` (burnt orange #C2410C): mono-type callouts and CTAs
  - `--highlight` (warm yellow #FEF3C7): emphasis boxes

- **Fonts**: Loaded from Google Fonts
  - Headlines: Fraunces (distinctive serif)
  - Body: Geist (clean modern sans)
  - Data/labels: Geist Mono

- **Typography rules**: Italics in headlines use the `<em>` tag (renders as italic + accent green)

## What sets this apart from typical "agency" sites

- ✅ No stock photos
- ✅ Specific numbers and data tables (not vague claims)
- ✅ Pricing visible everywhere (no "contact for pricing")
- ✅ India transparency section explicitly addresses skepticism
- ✅ Refund policies stated clearly with no friction
- ✅ FAQs answer the actual skeptical questions, not lazy ones
- ✅ Founding Partner program creates credible scarcity
- ✅ The /grade tool is unique — most competitors don't offer this

## Page hierarchy

```
Home (index.html)
├── Report ($97) — primary CTA destination
├── Grade tool — secondary CTA, lead-magnet entry point
├── Services — for prospects exploring tiers
├── About — for trust verification
├── Case Studies — empty for now, fills with Founding Partner results
└── Contact — for non-purchase inquiries

Footer pages: Privacy, Terms, Refunds
```

## Cold email integration

When sending cold emails:
- Link to `/grade` as primary CTA (free, low-commitment)
- Link to `/report` for budget-confirmed prospects
- Link to `/about` if a prospect asks "who are you?"

For the "Founding Partner" pivot when prospects say budget is too tight:
- Link to `/case-studies#founding`

## License

All content and code © 2026 Local Growth Insights.
