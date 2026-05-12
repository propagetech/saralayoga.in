# Sarala Yoga Website

Professional yoga training website for Sarala — a certified yoga instructor in Bangalore, India.

## What this is

Plain **HTML** at the repository root, **CSS** in `src/css/styles.css`, and **JavaScript** in `src/js/`. There is **no** Node.js, npm, Vite, React, or build step in the repo. The live site is **static files only** — nothing runs on a server except the host’s static file delivery.

**Hosting:** [GitHub Pages](https://pages.github.com/) (free).  
**DNS (and optional CDN / SSL at the edge):** [Cloudflare](https://www.cloudflare.com/) (free tier).  

Python is **not** part of the website. Any Python you may have seen elsewhere was only optional one-off tooling to download placeholder images; those assets are already in `src/assets/images/`, and that script has been removed.

## Project structure

```
saralayoga/
├── index.html, about.html, services.html, pricing.html
├── gallery.html, contact.html, blog.html, privacy.html, terms.html
├── src/
│   ├── css/styles.css
│   ├── js/main.js, gallery.js, contact-form.js
│   └── assets/images/, assets/icons/
├── manifest.json, sitemap.xml, robots.txt, favicon.ico
├── docs/          # Detailed guides (deployment, images, etc.)
└── README.md
```

## Documentation

| Doc | Purpose |
|-----|--------|
| [docs/GETTING-STARTED.md](docs/GETTING-STARTED.md) | First edits, folder tour, common tasks |
| [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md) | GitHub Pages, **Cloudflare DNS**, HTTPS, Search Console, email |
| [docs/DEV-MODE-SETUP.md](docs/DEV-MODE-SETUP.md) | Local preview (no site build) |
| [docs/IMAGE-GUIDE.md](docs/IMAGE-GUIDE.md) | Image sizes and replacing assets |

Other files under `docs/` are optional notes (fonts, design history, old plans).

## Local preview

Absolute paths like `/src/css/styles.css` need a **local HTTP server** (opening `index.html` as a `file://` URL often breaks CSS).

- **Editor:** Use a “Live Server” style extension in Cursor/VS Code and open the project folder.
- **CLI (optional):** From the repo root, if you have Node.js installed only for tooling:  
  `npx --yes serve . -l 3000`  
  then open `http://localhost:3000`.

## Deploy (GitHub Pages + Cloudflare)

1. Push this repository to GitHub.
2. **GitHub:** Settings → Pages → deploy from branch `main` (or default branch), folder `/` (root).
3. **Custom domain:** In Pages settings, enter your domain (e.g. `www.saralayoga.in`) and enable **Enforce HTTPS** once DNS is valid.
4. **Cloudflare:** Add the domain, point nameservers from your registrar to Cloudflare, then add the DNS records GitHub documents for Pages (apex `A` records to GitHub’s IPs, `www` as `CNAME` to `YOUR_USERNAME.github.io` — exact values in [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md)).

Step-by-step DNS, SSL mode, Search Console, and Zoho mail records are in **[docs/DEPLOYMENT.md](docs/DEPLOYMENT.md)**.

## Everyday edits

- **Copy / layout:** edit the root `.html` files.
- **Look and feel:** edit `src/css/styles.css`.
- **Behavior:** edit `src/js/*.js`.
- **New page:** add a root `.html` file, link it from the nav on all pages, add the URL to `sitemap.xml`.

## License

© 2024 Sarala Yoga. All rights reserved.
