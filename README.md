# Mangia Farms — Deploy

This folder is everything you need to put the site online. Static HTML, CSS, and images. No build step.

## Files

```
mangia-farms-deploy/
├── index.html      home
├── shop.html       pantry (1 product + 2 coming-soon)
├── about.html      Skylar's story
├── contact.html    contact form + market info
├── styles.css      shared stylesheet
├── img/            5 optimized photos (~1.9 MB total)
└── README.md       this file
```

## Easiest deploy — Netlify Drop (free)

1. Open <https://app.netlify.com/drop>
2. Drag this whole `mangia-farms-deploy` folder onto the drop zone
3. Netlify gives you a live URL in seconds, e.g. `mangia-farms-abc123.netlify.app`
4. (Optional) Connect a custom domain like `mangiafarms.com` from the Netlify dashboard

That's the whole process. No account required for the free tier; sign in to keep the URL.

## Other free hosts that work the same way

- **Vercel** — drag the folder at <https://vercel.com/new>
- **Cloudflare Pages** — <https://pages.cloudflare.com>
- **GitHub Pages** — push the folder contents to a repo, enable Pages in settings
- **Surge.sh** — `npm i -g surge && surge` from inside this folder

## Custom domain

The site is being deployed to Netlify (current URL: `mangiafarms.netlify.app`) and the production domain `mangiafarms.com` is registered through **Squarespace Domains**. To connect them:

### Step 1 — Add the domain in Netlify
1. Netlify dashboard → your `mangia-farms` site → **Domain settings** → **Add a domain**
2. Enter `mangiafarms.com`
3. Netlify will tell you it needs DNS records added at Squarespace

### Step 2 — Pick a DNS strategy
There are two options. The first is what Netlify recommends.

**Option A — Use Netlify DNS (recommended)**
- Netlify becomes the DNS host; Squarespace just registers the domain.
- In Netlify → Domain settings → click **Set up Netlify DNS for mangiafarms.com**
- Netlify gives you 4 nameservers like `dns1.p01.nsone.net`, `dns2…`, etc.
- In **Squarespace Domains** → mangiafarms.com → **DNS settings** → scroll to **Nameservers** → **Use custom nameservers** → paste the 4 Netlify nameservers
- Save. DNS propagation: 24–48 hours (usually faster).

**Option B — Keep Squarespace DNS, point records to Netlify**
- In **Squarespace Domains** → mangiafarms.com → **DNS settings** → add these records:
  - **A record** · Host `@` · Value `75.2.60.5` (Netlify's load balancer)
  - **CNAME** · Host `www` · Value `mangiafarms.netlify.app`
- Save. DNS propagation: usually 15–60 minutes.
- Note: if Squarespace forces certain records for their own services, remove conflicting A/CNAME records for `@` and `www`.

### Step 3 — SSL certificate
Once DNS is propagating, Netlify auto-provisions a free Let's Encrypt SSL cert for `mangiafarms.com` and `www.mangiafarms.com`. This takes another 5–15 minutes after DNS resolves. You don't need to do anything — Netlify shows a green padlock when it's ready.

### Step 4 — Set the primary domain
In Netlify → Domain settings, click the ⋯ next to `mangiafarms.com` → **Set as primary domain**. Netlify will automatically 301 redirect `www.mangiafarms.com` → `mangiafarms.com` (or vice versa, your choice).

---

**Quick sanity check** once it's live:
- `https://mangiafarms.com` loads the site ✅
- `https://www.mangiafarms.com` redirects to the chosen primary ✅
- Padlock icon (SSL) is green ✅
- `mangiafarms.netlify.app` still works (Netlify keeps it as an alias)

## Updating the site later

Edit any file in this folder, then either:
- Drag the folder onto Netlify Drop again (it'll detect the existing site)
- Or, if you're using a Git-based deploy, push the change

## What to change before launch

Search-and-replace these placeholders in the HTML when ready:

| Placeholder              | In file(s)                  |
| ------------------------ | --------------------------- |
| Instagram / Newsletter   | footer of every page (real handles + signup link) |
| Contact form action      | `contact.html` (the form currently shows a thank-you message but doesn't email anyone — wire it to Formspree, Netlify Forms, or similar) |

### Netlify Forms (easiest)

If you deploy to Netlify, you can make the contact form actually email you with one tag:

```html
<form name="contact" netlify>
```

Add `name="contact" netlify` to the `<form>` element in `contact.html`, redeploy, and submissions show up in your Netlify dashboard + arrive by email.

## Image optimization

The photos in `img/` have already been resized to 1600px wide and re-saved at JPEG quality 78. Originals are ~3 MB each; these are ~330 KB. If you swap in a new photo, run it through TinyJPG or ImageOptim before adding it to keep page loads fast.

—

Built with care, no frameworks, no tracking, no bloat. Just HTML, CSS, and bread.
