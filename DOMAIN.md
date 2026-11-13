# Domain forwarding: meetup.deliverypilot.net

Goal: send **meetup.deliverypilot.net** to this site, which GitHub Pages serves at
`https://rifaterdemsahin.github.io/sixth-form-college/`.

| Visitor types | Lands on |
|---|---|
| `meetup.deliverypilot.net` | Slide deck (`index.html`) |
| `meetup.deliverypilot.net/prerequisites.html` | Attendee prerequisites page |

There are two ways to do this. **Option A is recommended**: the URL stays on your own domain, HTTPS is free and automatic, and every page in the repo works under the subdomain.

---

## Option A (recommended): GitHub Pages custom domain

### 1. Add a DNS record at your DNS provider for `deliverypilot.net`

| Type | Name / Host | Value / Target | TTL |
|---|---|---|---|
| `CNAME` | `meetup` | `rifaterdemsahin.github.io` | 3600 (or Auto) |

- Don't add the repo name to the target. It's just `rifaterdemsahin.github.io` (a trailing dot is fine if your provider wants one).
- Remove any existing `A`, `AAAA` or URL-redirect record for `meetup`. A name can't have a CNAME alongside other records.
- **Cloudflare:** set the record to **DNS only** (grey cloud) until GitHub has issued the certificate (step 3). You can switch the proxy back on afterwards with SSL mode **Full**.

### 2. Set the custom domain in GitHub

1. Go to **github.com/rifaterdemsahin/sixth-form-college → Settings → Pages**.
2. Under **Custom domain**, enter `meetup.deliverypilot.net` and click **Save**.
3. Wait for the DNS check to show a green tick. This takes minutes, or up to a few hours while DNS propagates.

> This repo deploys with GitHub Actions (`.github/workflows/static.yml`). With Actions deploys, GitHub ignores any `CNAME` file in the repo. Set the domain in Settings, as above.

### 3. Turn on HTTPS

Once the DNS check passes, tick **Enforce HTTPS** on the same Settings → Pages screen. The certificate can take up to an hour to appear. If the box is greyed out, wait and refresh.

### 4. (Recommended) Verify the domain against takeover

**GitHub → your profile Settings → Pages → Add a domain** → enter `deliverypilot.net`. GitHub gives you a `TXT` record like this:

| Type | Name / Host | Value |
|---|---|---|
| `TXT` | `_github-pages-challenge-rifaterdemsahin` | *(code GitHub shows you)* |

Add it at the DNS provider, then click **Verify**. Only your account can then use subdomains of `deliverypilot.net` on GitHub Pages.

### What changes

- `https://rifaterdemsahin.github.io/sixth-form-college/` automatically redirects to `https://meetup.deliverypilot.net/`.
- Update the links in `README.md` and the footer of `prerequisites.html` to the new domain once it's live.

---

## Option B: registrar URL forwarding (redirect only)

Use this if you can't add a CNAME, or if you want the subdomain to point at one specific page.

At your registrar's **URL forwarding / redirect** settings:

| Source | Destination | Type |
|---|---|---|
| `meetup.deliverypilot.net` | `https://rifaterdemsahin.github.io/sixth-form-college/` | 301 permanent (use 302 while testing) |

- To land straight on the prerequisites page, use `https://rifaterdemsahin.github.io/sixth-form-college/prerequisites.html` as the destination.
- Turn **path forwarding** on if your registrar offers it, so `/prerequisites.html` carries through.
- Downsides: the address bar shows the github.io URL, and many registrars only forward plain `http://`. Check that `https://meetup.deliverypilot.net` works.
- **Cloudflare:** use **Rules → Redirect Rules** (hostname equals `meetup.deliverypilot.net` → dynamic redirect to `concat("https://rifaterdemsahin.github.io/sixth-form-college", http.request.uri.path)`, 301). You also need a proxied (orange cloud) DNS record for `meetup`, for example `AAAA meetup 100::`.

---

## Checking it works

```bash
nslookup -type=CNAME meetup.deliverypilot.net
```

```bash
curl -sI https://meetup.deliverypilot.net/ | head -5
```

```bash
curl -sI https://meetup.deliverypilot.net/prerequisites.html | head -5
```

Expected: the CNAME resolves to `rifaterdemsahin.github.io`, and both URLs return `HTTP/2 200` (Option A) or a `301` to the github.io URL (Option B).

## Troubleshooting

| Symptom | Fix |
|---|---|
| "DNS check unsuccessful" in GitHub | Wait for propagation. Make sure there's only one record for `meetup` and that it points to `rifaterdemsahin.github.io`. |
| "Enforce HTTPS" greyed out | The certificate is still being issued. Wait up to an hour. With Cloudflare, switch to DNS only first. |
| 404 "There isn't a GitHub Pages site here" | The custom domain isn't saved in Settings → Pages, or the last deploy failed (check the Actions tab). |
| Too many redirects (Cloudflare) | Set SSL/TLS mode to **Full**, not Flexible. |
