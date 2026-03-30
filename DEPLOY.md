# Deploying clrtxt.com via GitHub Pages + Cloudflare

This is the fastest path to getting clrtxt.com live with zero hosting cost.

---

## Step 1 — Push to GitHub

1. Create a new **public** repository on GitHub (e.g. `clrtxt-site`).
2. Push this folder to it:

```bash
git init
git add .
git commit -m "initial site"
git remote add origin https://github.com/YOUR_USERNAME/clrtxt-site.git
git push -u origin main
```

---

## Step 2 — Enable GitHub Pages

1. In your repo, go to **Settings → Pages**.
2. Under **Source**, choose **Deploy from a branch**.
3. Select branch: `main`, folder: `/ (root)`.
4. Click **Save**.

GitHub will give you a URL like `https://yourusername.github.io/clrtxt-site/`. The site is live — now we point your real domain to it.

---

## Step 3 — Add a CNAME file

Create a file called `CNAME` (no extension) in this folder with exactly one line:

```
clrtxt.com
```

Commit and push it. GitHub Pages uses this to accept requests for your custom domain.

---

## Step 4 — Configure Cloudflare

Assuming clrtxt.com is already in Cloudflare (if not, transfer the nameservers from your registrar to Cloudflare first — takes ~24h).

In the Cloudflare dashboard for clrtxt.com, go to **DNS** and add these records:

| Type  | Name | Content                | Proxy |
|-------|------|------------------------|-------|
| A     | @    | 185.199.108.153        | ✅ Proxied |
| A     | @    | 185.199.109.153        | ✅ Proxied |
| A     | @    | 185.199.110.153        | ✅ Proxied |
| A     | @    | 185.199.111.153        | ✅ Proxied |
| CNAME | www  | YOUR_USERNAME.github.io | ✅ Proxied |

These four IPs are GitHub Pages' servers (they don't change).

---

## Step 5 — Set custom domain in GitHub Pages

Back in **Settings → Pages**, under **Custom domain**, enter `clrtxt.com` and click Save. GitHub will verify the DNS and issue a free TLS certificate (takes a few minutes to an hour).

Once verified, check **Enforce HTTPS** in that same settings panel.

---

## Step 6 — Cloudflare settings to check

- **SSL/TLS mode**: Set to **Full** (not Full Strict, since GitHub Pages certificates are self-managed). Go to SSL/TLS → Overview.
- **Always Use HTTPS**: On (SSL/TLS → Edge Certificates).
- **Minify**: Optional, but you can turn on Auto Minify under Speed → Optimization for a tiny perf bump.

---

## You're live

`clrtxt.com` should now resolve to the site through Cloudflare's CDN, with HTTPS, for free.

To update the site, just edit `index.html`, commit, and push. GitHub Pages redeploys automatically within ~1 minute.

---

## Later upgrades (when you need them)

- **Contact form**: Swap the `mailto:` link for a [Formspree](https://formspree.io) or [Basin](https://usebasin.com) endpoint — free tiers are generous.
- **Analytics**: Drop in [Fathom](https://usefathom.com) or [Plausible](https://plausible.io) (privacy-friendly, no cookie banner needed).
- **CMS**: If you want to edit copy without touching code, [Decap CMS](https://decapcms.org) works directly on top of GitHub Pages.
