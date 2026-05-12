# Sarala Yoga Website - Deployment Guide

**Hosting:** GitHub Pages (free). **DNS / edge:** Cloudflare (free tier) in front of the domain. There is no server-side code and no build step—upload or push static files only.

## Pre-Deployment Checklist

Before deploying, ensure you have:

- [ ] Updated all contact information (phone, email, address)
- [ ] Replaced placeholder images with actual photos
- [ ] Generated and added favicon files
- [ ] Tested all pages locally
- [ ] Verified all links work correctly
- [ ] Checked responsiveness on different screen sizes
- [ ] Run accessibility tests
- [ ] Validated HTML/CSS

## GitHub Pages

**Step 1: Create GitHub Repository**
```bash
# Initialize git if not already done
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit: Sarala Yoga website"

# Add remote repository (create repo on GitHub first)
git remote add origin https://github.com/YOUR_USERNAME/saralayoga.git

# Push to GitHub
git push -u origin main
```

**Step 2: Enable GitHub Pages**
1. Go to your repository on GitHub
2. Click **Settings** → **Pages**
3. Source: Deploy from a branch
4. Branch: `main` / root
5. Click **Save**
6. Your site will be live at: `https://YOUR_USERNAME.github.io/saralayoga/`

**Step 3: Add Custom Domain**
1. In GitHub Pages settings, add custom domain: `www.saralayoga.in`
2. Check "Enforce HTTPS"
3. Configure DNS in Cloudflare (see below)

---

## Other static hosts (optional)

The same repository works on Netlify, Cloudflare Pages, Vercel, or classic FTP hosting: **no build command**, publish directory **/** (repository root). Use that provider’s DNS instructions if you are not using GitHub Pages.

---

## DNS Configuration

### For Custom Domain: www.saralayoga.in

**If using Cloudflare (Recommended):**

1. **Add Domain to Cloudflare**
   - Sign up at cloudflare.com
   - Add domain: `saralayoga.in`
   - Cloudflare will scan existing records

2. **Change Nameservers at GoDaddy**
   - Go to GoDaddy domain management
   - Update nameservers to Cloudflare's (provided during setup)
   - Example:
     ```
     ns1.cloudflare.com
     ns2.cloudflare.com
     ```

3. **Configure DNS records in Cloudflare (GitHub Pages)**

   GitHub’s current IPs for apex (`@`) are documented at  
   https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain  
   Typically you add **four** `A` records for `@` to GitHub’s addresses, and one **CNAME** for `www` pointing to `YOUR_USERNAME.github.io` (replace with your GitHub username; for a project site, the Pages hostname may be `YOUR_USERNAME.github.io` with the repo path—follow GitHub’s “Custom domain” checklist for your repo).

   Example shape (verify IPs in GitHub’s docs; they can change):

   ```
   Type: A
   Name: @
   Content: 185.199.108.153
   Proxy: Proxied (orange cloud)
   (repeat A for 185.199.109.153, 185.199.110.153, 185.199.111.153 as GitHub documents)

   Type: CNAME
   Name: www
   Content: YOUR_USERNAME.github.io
   Proxy: Proxied (orange cloud)
   ```

   If you host elsewhere (Netlify, etc.), use **that** provider’s required DNS targets instead of GitHub’s.

4. **Enable SSL/TLS**
   - In Cloudflare: SSL/TLS → Overview
   - Select "Full" or "Full (strict)"
   - Enable "Always Use HTTPS"
   - Enable "Automatic HTTPS Rewrites"

5. **Performance Settings**
   - Enable "Auto Minify" (HTML, CSS, JS)
   - Enable "Brotli" compression
   - Set Browser Cache TTL to "4 hours" or longer

---

## 📧 Zoho Email Configuration

**Setup Email: yogasarala@gmail.com or your@saralayoga.in**

1. **Sign up for Zoho Mail**
   - Go to https://www.zoho.com/mail/
   - Sign up for free tier (5 users, 5GB storage)

2. **Add Your Domain**
   - Go to Zoho Mail Control Panel
   - Add domain: `saralayoga.in`
   - Verify ownership (TXT record or HTML file)

3. **Add DNS Records to Cloudflare**
   
   **MX Records:**
   ```
   Type: MX
   Name: @
   Mail Server: mx.zoho.in
   Priority: 10
   
   Type: MX
   Name: @
   Mail Server: mx2.zoho.in
   Priority: 20
   
   Type: MX
   Name: @
   Mail Server: mx3.zoho.in
   Priority: 50
   ```
   
   **SPF Record:**
   ```
   Type: TXT
   Name: @
   Content: v=spf1 include:zoho.in ~all
   ```
   
   **DKIM Record:**
   ```
   Type: TXT
   Name: zoho._domainkey
   Content: [Provided by Zoho - copy from Zoho control panel]
   ```
   
   **DMARC Record:**
   ```
   Type: TXT
   Name: _dmarc
   Content: v=DMARC1; p=none; rua=mailto:yogasarala@gmail.com
   ```

4. **Create Email Account**
   - Create: sarala@saralayoga.in
   - Or: contact@saralayoga.in
   - Or: info@saralayoga.in

5. **Forward to Gmail (Optional)**
   - In Zoho: Settings → Email Forwarding
   - Forward to: yogasarala@gmail.com

---

## 🔍 SEO Setup

### 1. Google Search Console

1. Go to https://search.google.com/search-console
2. Add property: `www.saralayoga.in`
3. Verify ownership:
   - DNS verification (add TXT record), or
   - HTML file upload, or
   - HTML meta tag
4. Submit sitemap: `https://www.saralayoga.in/sitemap.xml`

### 2. Google My Business

1. Already created: https://share.google/uJrVQLC0vjhxz4Oth
2. Verify business
3. Add website URL: `https://www.saralayoga.in`
4. Add photos
5. Respond to reviews
6. Post updates regularly

### 3. Google Analytics (Optional)

1. Sign up at https://analytics.google.com
2. Create property for `www.saralayoga.in`
3. Get tracking code
4. Add to all HTML files before `</head>`:
   ```html
   <!-- Google Analytics -->
   <script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
   <script>
     window.dataLayer = window.dataLayer || [];
     function gtag(){dataLayer.push(arguments);}
     gtag('js', new Date());
     gtag('config', 'GA_MEASUREMENT_ID');
   </script>
   ```

### 4. Bing Webmaster Tools

1. Sign up at https://www.bing.com/webmasters
2. Add site: `www.saralayoga.in`
3. Verify ownership
4. Submit sitemap

---

## 🧪 Post-Deployment Testing

### 1. Functionality Tests
- [ ] All links work (no 404 errors)
- [ ] Images load correctly
- [ ] Contact form validation works
- [ ] Gallery filtering and lightbox work
- [ ] Mobile menu opens/closes
- [ ] All pages accessible

### 2. Performance Tests
- [ ] Run Lighthouse in Chrome DevTools
  - Target: 90+ for all metrics
- [ ] Test on https://pagespeed.web.dev
- [ ] Check loading time on 3G network

### 3. SEO Tests
- [ ] Google Search Console: No errors
- [ ] Rich Results Test: https://search.google.com/test/rich-results
- [ ] Mobile-Friendly Test: https://search.google.com/test/mobile-friendly
- [ ] Schema markup validator

### 4. Accessibility Tests
- [ ] WAVE: https://wave.webaim.org/
- [ ] Keyboard navigation (Tab through all elements)
- [ ] Screen reader test (NVDA or JAWS)
- [ ] Color contrast check

### 5. Cross-Browser Tests
- [ ] Chrome (desktop & mobile)
- [ ] Firefox
- [ ] Safari (desktop & iOS)
- [ ] Edge
- [ ] Opera

### 6. Device Tests
- [ ] iPhone (various sizes)
- [ ] Android phones
- [ ] iPad/tablets
- [ ] Desktop (1920px, 1440px, 1280px)

---

## 🔄 Update Process

**To update content:**

1. Edit HTML files locally
2. Test changes in browser
3. Upload to hosting:
   
   **GitHub:**
   ```bash
   git add .
   git commit -m "Update: description of changes"
   git push
   ```
   
   **FTP:**
   - Upload modified files only
   - Ensure permissions are correct
   
   **Netlify/Vercel:**
   - Push to GitHub (auto-deploys)
   - Or drag & drop new files

---

## 🆘 Troubleshooting

### Website not loading after deployment

1. **Check DNS propagation**
   - Use: https://dnschecker.org
   - DNS can take 24-48 hours to propagate

2. **Clear browser cache**
   - Hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)

3. **Check SSL certificate**
   - Ensure HTTPS is enabled
   - Wait for SSL provisioning (can take 20 minutes)

### Images not displaying

1. Check file paths are correct
2. Ensure images uploaded to correct directory
3. Verify file names match (case-sensitive on Linux)
4. Check file permissions (644 for files)

### Email not working

1. Verify MX records in DNS
2. Wait 24 hours for DNS propagation
3. Check SPF and DKIM records
4. Test with https://mxtoolbox.com

### Form submissions not working

1. Contact forms need backend processing
2. Options:
   - Use FormSpree: https://formspree.io
   - Use Netlify Forms (if hosted on Netlify)
   - Use EmailJS: https://www.emailjs.com
   - Display contact info only (current approach)

---

## 📊 Monitoring & Maintenance

### Weekly Tasks
- [ ] Check Google Search Console for errors
- [ ] Monitor website uptime
- [ ] Respond to form submissions/emails
- [ ] Update blog with new content

### Monthly Tasks
- [ ] Review analytics
- [ ] Check for broken links
- [ ] Update content as needed
- [ ] Backup website files

### Quarterly Tasks
- [ ] Review and update SEO
- [ ] Update photos/images
- [ ] Check accessibility compliance
- [ ] Performance audit

---

## 📞 Support

If you need help:
- Email: yogasarala@gmail.com
- Phone: +91 9945400870

---

## ✅ Deployment Checklist

- [ ] Files uploaded to hosting
- [ ] DNS configured correctly
- [ ] SSL certificate active
- [ ] Custom domain working
- [ ] Email configured
- [ ] Sitemap submitted to Google
- [ ] Google My Business linked
- [ ] All pages tested
- [ ] Performance optimized
- [ ] Accessibility verified
- [ ] Analytics set up (optional)
- [ ] Backup created

---

**🎉 Congratulations! Your website is now live!**

Visit: https://www.saralayoga.in

Share on social media and start growing your yoga business online! 🧘‍♀️✨
