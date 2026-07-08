# designma.ca - Page de maintenance (GitHub Pages)

Static "site en préparation" page for **designma.ca**, hosted on GitHub Pages while the
new site is being built. Keeps the contact form live via Formspree (no backend needed).

## Files

| File | Purpose |
|------|---------|
| `index.html` | The maintenance page + contact form |
| `404.html` | Copy of `index.html` so **any** path (e.g. `/portfolio`) also shows maintenance |
| `CNAME` | Tells GitHub Pages to serve the custom domain `designma.ca` |

## 1. Push to GitHub

```bash
git init
git add .
git commit -m "Maintenance page for designma.ca"
git branch -M main
git remote add origin https://github.com/<your-username>/designma-maintenance.git
git push -u origin main
```

## 2. Enable GitHub Pages

1. Repo → **Settings → Pages**
2. **Source:** Deploy from a branch
3. **Branch:** `main` / `root` → **Save**
4. Under **Custom domain** it should show `designma.ca` (from the `CNAME` file). If not, enter it and Save.
5. Wait for the DNS check, then tick **Enforce HTTPS** (may take a bit to become available).

## 3. Point the domain at GitHub (IONOS DNS)

In IONOS → **Domains → designma.ca → DNS**:

**Apex `designma.ca` - replace existing A record(s) with these four A records:**

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

Optional IPv6 (AAAA):

```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

**`www` subdomain - CNAME:**

```
www  →  <your-username>.github.io
```

> ⚠️ **Do NOT change MX records.** Leave email (`info@designma.ca`) records untouched so
> mail keeps working. Only touch A / AAAA / CNAME records.
>
> Remove/replace the old **Showit** A/CNAME records so the domain no longer points there.

## 4. Verify

- DNS + HTTPS cert can take ~15 min to a few hours to propagate.
- Check with: `https://<your-username>.github.io` first (works immediately),
  then `https://designma.ca` once DNS propagates.

## Reverting to live (later)

To bring the real site back, restore the original **Showit** DNS records in IONOS
(A / CNAME values Showit provided). No changes needed here. Showit is untouched.

## Form

The form posts to Formspree endpoint `mnjknwdz` (reused from the existing site).
Submissions arrive at the email tied to that Formspree form. Confirm the `designma.ca`
domain is allowlisted in the Formspree form settings if submissions are rejected.
