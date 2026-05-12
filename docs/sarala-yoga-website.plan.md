# Sarala Yoga Website Implementation Plan

## 1. Project Setup & Configuration

**Tech Stack:**
- Plain HTML5, CSS3, and vanilla JavaScript (ES modules under `src/js/`)
- **No** Node.js, npm, Vite, React, Next.js, or Tailwind build pipeline in the repository
- One stylesheet: `src/css/styles.css` (plain CSS committed with the site)
- Hosting: static files on GitHub, Cloudflare Pages, Netlify, or any web server

**Project Structure:**
```
/ (repository root)
  ├── index.html, about.html, …   # Site pages
  ├── manifest.json, sitemap.xml, robots.txt, favicon.ico
  └── src/
      ├── css/
      │   └── styles.css          # All styles
      ├── js/
      │   ├── main.js
      │   ├── contact-form.js
      │   └── gallery.js
      └── assets/
          ├── images/
          └── icons/
```

**Configuration Files:**
- Optional: `.github/workflows/*` only if you add CI (not required)

## 2. Website Pages & Structure

**Pages to Create (Static HTML):**
1. **Home** (`index.html`) - Hero, services overview, testimonials, CTA
2. **About** (`about.html`) - Sarala's bio, qualifications, teaching philosophy
3. **Services** (`services.html`) - Online/Offline, Personal/Group classes
4. **Pricing** (`pricing.html`) - Detailed pricing tables for all services
5. **Gallery** (`gallery.html`) - Photos/videos of yoga sessions
6. **Contact** (`contact.html`) - Contact form, map, phone, email, address
7. **Blog** (`blog.html`) - Yoga tips, health articles (SEO boost)
8. **Privacy Policy** (`privacy.html`) - Required for compliance
9. **Terms of Service** (`terms.html`) - Legal protection

Each HTML file will include:
- Complete semantic HTML structure
- Inline Schema.org JSON-LD structured data
- Full SEO meta tags in `<head>`
- Accessibility attributes (ARIA, lang, roles)

## 3. Content Generation (English Only)

**Generated Content Includes:**
- **Home page:** Hero text ("Transform Your Life Through Yoga"), services overview, compelling CTAs
- **About Sarala:** Professional bio highlighting expertise, certifications, years of experience, teaching philosophy
- **Service descriptions:**
  - Online yoga classes (live virtual sessions)
  - Offline personal training (one-on-one sessions)
  - Group yoga sessions (community classes)
  - Specialized yoga (prenatal, senior citizens, therapeutic, stress relief)
- **Pricing tables:** Clear pricing with Indian Rupee formatting (₹) for all service types
- **Contact page copy:** Inviting text encouraging visitors to get in touch
- **3-5 SEO blog articles:**
  - "Benefits of Daily Yoga Practice"
  - "Yoga for Beginners: Getting Started Guide"
  - "Stress Relief Through Yoga and Meditation"
  - "Yoga for Senior Citizens: Safe Practices"
  - "Online vs Offline Yoga: Which is Right for You?"
- **Meta descriptions, titles, keywords** for each page
- **Alt text templates** for all images

## 4. Accessibility & Standards (WCAG 2.1 Level AAA)

**Semantic HTML5:**
- `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<footer>`
- Proper heading hierarchy (h1-h6)
- `<figure>` and `<figcaption>` for images
- `<address>` for contact information

**ARIA Implementation:**
- ARIA labels on all interactive elements
- `aria-label`, `aria-labelledby`, `aria-describedby`
- `role` attributes where needed
- `aria-live` regions for dynamic content
- `aria-expanded`, `aria-controls` for interactive widgets

**Keyboard Navigation:**
- All interactive elements accessible via Tab
- Visible focus indicators with high contrast
- Skip to main content link
- Logical tab order
- No keyboard traps

**Senior Citizen & Vision Impaired Support:**
- Base font size: 18px (1.125rem)
- All fonts scalable (rem units)
- Accessibility toolbar with:
  - Font size controls (A-, A, A+)
  - High contrast mode toggle
  - Line spacing adjustment
- Zoom support up to 200% without layout breaking
- Screen reader optimized
- No color-only information
- Minimum contrast ratio: 7:1 (AAA standard)
- Touch-friendly targets: minimum 44x44px

## 5. SEO Optimization (100% Crawlable Static HTML)

**On-Page SEO (Every HTML File):**
```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Unique Page Title (< 60 chars)</title>
  <meta name="description" content="Compelling description (< 160 chars)">
  <meta name="keywords" content="yoga, bangalore, sarala, jp nagar">
  <link rel="canonical" href="https://www.saralayoga.in/page">
  
  <!-- Open Graph (WhatsApp, Facebook) -->
  <meta property="og:title" content="Page Title">
  <meta property="og:description" content="Page description">
  <meta property="og:image" content="https://www.saralayoga.in/og-image.jpg">
  <meta property="og:url" content="https://www.saralayoga.in/page">
  <meta property="og:type" content="website">
  
  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Page Title">
  <meta name="twitter:description" content="Page description">
  <meta name="twitter:image" content="https://www.saralayoga.in/twitter-image.jpg">
</head>
```

**Structured Data (Schema.org JSON-LD):**

Each page includes relevant schemas:
- **LocalBusiness** (all pages) - Address, phone, hours
- **Person schema** (About page) - Sarala's profile
- **Service schema** (Services page) - Yoga class offerings
- **FAQPage schema** (if FAQs added)
- **Review/Rating schema** (for testimonials)
- **BreadcrumbList schema** (navigation)
- **Organization schema** (footer)

**Additional SEO Files:**
- `sitemap.xml` - Auto-generated list of all pages
- `robots.txt` - Allow all search engines
- Optimized images (WebP with fallbacks, lazy loading)

## 6. PWA Implementation

**Features:**
- `manifest.json` with app metadata at the site root (see `manifest.json`)
- Optional: add a small service worker later if you need offline HTML; not tied to any bundler
- Installable on mobile devices (Add to Home Screen) when icons and manifest are complete

## 7. Performance Optimization (Lighthouse 100%)

**Build & edge:**
- Styles and utilities live in the committed `src/css/styles.css` file (no compile step in-repo)
- Cloudflare (or similar): Brotli, caching rules, optional Auto Minify for HTML/CSS/JS

**Image Optimization:**
- Convert images to WebP format with PNG/JPG fallback
- Responsive images with `srcset` and `sizes`
- Lazy loading: `<img loading="lazy">`
- Width/height attributes to prevent layout shift

**Font Loading:**
- Preload critical fonts
- `font-display: swap` for web fonts
- System font stack fallback

## 8. JavaScript Functionality

**Vanilla JS Modules:**
- `main.js` - Navigation, accessibility toolbar, optional future service worker registration
- `contact-form.js` - Form validation and submission
- `gallery.js` - Lightbox with keyboard navigation

## 9. Core Components (Reusable HTML)

**Header/Navigation:**
```html
<header role="banner">
  <nav role="navigation" aria-label="Main navigation">
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/about.html">About</a></li>
      <li><a href="/services.html">Services</a></li>
      <li><a href="/pricing.html">Pricing</a></li>
      <li><a href="/gallery.html">Gallery</a></li>
      <li><a href="/blog.html">Blog</a></li>
      <li><a href="/contact.html" class="cta-button">Contact</a></li>
    </ul>
  </nav>
</header>
```

**Footer:**
- Contact information
- Quick links
- Social media links
- Copyright notice

## 10. Third-Party Integrations

**Google Services:**
- Google My Business embed
- Google Maps embed (address location)
- Google Analytics 4 (optional, with cookie consent)
- Google Search Console setup guide

**Media & Communication:**
- YouTube video embeds (yoga tutorials)
- WhatsApp chat button (+91 9945400870)
- Email link (yogasarala@gmail.com)
- Phone link (+91 9945400870)

## 11. Resource Recommendations

**Free Images:**
- Unsplash.com - Best quality yoga photos
- Pexels.com - Wide variety
- Pixabay.com - Free images/videos

**Icons:**
- Heroicons - Clean SVG icons
- Lucide Icons - Extensive library
- Font Awesome Free

**Illustrations:**
- unDraw.co - Customizable illustrations
- Storyset by Freepik - Animated
- Blush.design - Mix & match
- heroicons.com
- lineicons.com
- thenounproject.com/search/icon-collections/?q=yoga
- https://hexmos.com/freedevtools/svg_icons/shape/yoga/
- https://www.svgrepo.com/svg/2057/yoga
- https://dryicons.com/free-icons/yoga
- https://www.vecteezy.com/free-vector/yoga-icon
- https://iconscout.com/icons/yoga

**Image CDN:**
- GitHub repository + Cloudflare caching (recommended, free)

## 12. Deployment Configuration

**GitHub + Cloudflare Pages:**
- Push static HTML, `src/`, and root files (`manifest.json`, `sitemap.xml`, `robots.txt`, favicons) to GitHub; connect the repo to Cloudflare Pages with **no build command** and publish directory `/`
- Custom domain and DNS in Cloudflare (for example `www.saralayoga.in`)

**Cloudflare Configuration:**
- DNS and proxy settings for your domain (CNAME to Pages, or your registrar’s setup)
- SSL/TLS: Full (strict)
- Auto HTTPS Rewrites: On
- Brotli compression: On
- Auto Minify: HTML, CSS, JS (optional; Pages already ships static files)

## 13. Additional Standards

**Web Standards:**
- HTML5 validation (W3C)
- CSS validation
- Mobile-first responsive design
- Cross-browser compatibility

**Security Headers:**
- Content Security Policy
- X-Frame-Options: SAMEORIGIN
- X-Content-Type-Options: nosniff

**Legal & Compliance:**
- Privacy Policy page
- Terms of Service page
- Cookie consent (if using analytics)

## 14. Testing Checklist

Before deployment:
- [ ] Lighthouse audit (90+ all categories, target 100%)
- [ ] WAVE accessibility test (zero errors)
- [ ] W3C HTML validation
- [ ] Cross-browser testing
- [ ] Mobile responsiveness
- [ ] Screen reader testing
- [ ] Keyboard navigation
- [ ] Schema.org validation (Google Rich Results Test)
- [ ] PWA install functionality
- [ ] Offline mode
- [ ] Form submission
- [ ] 200% zoom test

## 15. Manual Tasks (Human Required)

### Pre-Development:
1. Gather photos of Sarala teaching yoga
2. Decide actual pricing for all services
3. Collect client testimonials
4. Review legal pages (Privacy, Terms)

### During Development:
5. Download images from Unsplash/Pexels
6. Review all AI-generated content for accuracy

### Deployment:
7. Create GitHub repository (saralayoga)
8. Sign up for Cloudflare account
9. Change GoDaddy nameservers to Cloudflare
10. Configure DNS in Cloudflare
11. Wait for DNS propagation (24-48 hours)

### Third-Party Services:
12. Set up Zoho email (info@saralayoga.in)
13. Add MX records to Cloudflare DNS
14. Verify Google Search Console
15. Update Google My Business with website URL
16. Upload videos to YouTube
17. Choose form service (Formspree/EmailJS)

### Testing:
18. Test contact form submission
19. Test on mobile devices
20. Test offline mode

### Quick Reference - Accounts Needed:
1. ✓ GitHub (you have: chetannr)
2. ✓ GoDaddy (domain purchased)
3. ⚠ Cloudflare (need to create)
4. ⚠ Zoho Mail (need to create)
5. ⚠ Google Search Console (need to add property)
6. ✓ Google My Business (you have)
7. ⚠ Form service - Formspree/EmailJS (need to create)

**Costs Summary:** ₹0 ongoing (only annual domain renewal)

## Implementation Order

1. Keep static HTML, committed CSS in `src/css/styles.css`, and vanilla JS — no Node-based site build
2. Maintain all 9 pages and shared header/footer
3. Generate and add English content to all pages
4. Add Schema.org JSON-LD structured data to each page
5. Build vanilla JavaScript functionality (navigation, forms, gallery)
6. Implement accessibility features (ARIA, keyboard nav, toolbar)
7. Configure PWA manifest (and optional service worker when needed)
8. Optimize performance (images, lazy loading; edge minify/caching on Cloudflare)
9. Test thoroughly using checklist
10. Deploy via Cloudflare Pages or GitHub Pages (no build step; publish repository root)
11. Configure Cloudflare (DNS, SSL, caching)
12. Submit to Google Search Console
13. Create Cloudflare and Zoho setup documentation
