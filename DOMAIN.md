# Custom domains for the meetup site

This site is served by GitHub Pages at `https://rifaterdemsahin.github.io/sixth-form-college/`.
We want two addresses to reach it:

- **meetup.cambridgeaiacademy.co.uk** (matches the deck's Cambridge AI Academy branding)
- **meetup.deliverypilot.net**

> **Key constraint:** GitHub Pages serves **one custom domain per repository**. One domain must be the *primary* (served directly by GitHub Pages). The other must *redirect* to it.

**Recommended setup**

| Domain | Role | How |
|---|---|---|
| `meetup.cambridgeaiacademy.co.uk` | **Primary**, served by GitHub Pages | DNS `CNAME` + set in repo Settings → Pages |
| `meetup.deliverypilot.net` | **Redirect** to the primary | 301 redirect at the `deliverypilot.net` DNS provider or registrar |
| `rifaterdemsahin.github.io/sixth-form-college/` | Old URL | GitHub redirects it to the primary automatically |

Paths carry through: `meetup.cambridgeaiacademy.co.uk/prerequisites.html` serves the attendee checklist.

To make deliverypilot the primary instead, swap the two domains in the steps below.

---

## Part 1: meetup.cambridgeaiacademy.co.uk (primary, GitHub Pages)

### 1. DNS record at the provider for `cambridgeaiacademy.co.uk`

Log in wherever the domain's DNS is managed (for example 123-reg, GoDaddy, Namecheap, IONOS or Cloudflare) and add:

| Type | Name / Host | Value / Target | TTL |
|---|---|---|---|
| `CNAME` | `meetup` | `rifaterdemsahin.github.io` | 3600 (or Auto) |

- The target is just `rifaterdemsahin.github.io`, with no repo name and no `https://`. Some UK registrars want a trailing dot: `rifaterdemsahin.github.io.`
- Delete any other `A`, `AAAA`, `CNAME` or forwarding record already on `meetup`.
- Some providers want the full host (`meetup.cambridgeaiacademy.co.uk`) instead of just `meetup`. Check how their other records are written.
- **Cloudflare:** set the record to **DNS only** (grey cloud) until step 3 is done.

### 2. Verify the domain with GitHub (do this first, prevents takeover)

1. Go to **GitHub → your profile picture → Settings → Pages → Verified domains → Add a domain**.
2. Enter `cambridgeaiacademy.co.uk`. GitHub shows a TXT record like this:

| Type | Name / Host | Value |
|---|---|---|
| `TXT` | `_github-pages-challenge-rifaterdemsahin` | *(code GitHub gives you)* |

3. Add it at the DNS provider and click **Verify**. This can take a few minutes to a day.

### 3. Set the custom domain on the repo

1. Go to **github.com/rifaterdemsahin/sixth-form-college → Settings → Pages**.
2. Under **Custom domain**, enter `meetup.cambridgeaiacademy.co.uk` → **Save**.
3. Wait for the green **"DNS check successful"**.
4. Tick **Enforce HTTPS**. The certificate can take up to an hour. If the box is greyed out, wait and refresh.

> The site deploys with GitHub Actions (`.github/workflows/static.yml`). With Actions deploys, GitHub ignores a `CNAME` file in the repo, so the Settings step above is the only place the domain is set. No code change is needed.

---

## Part 2: meetup.deliverypilot.net (redirect to the primary)

Pick the option your `deliverypilot.net` provider supports.

### Option A: registrar URL forwarding (simplest)

| Source | Destination | Type | Path forwarding |
|---|---|---|---|
| `meetup.deliverypilot.net` | `https://meetup.cambridgeaiacademy.co.uk` | 301 permanent | On, if offered |

- Many registrar forwarders only handle `http://`. Test `https://meetup.deliverypilot.net` afterwards. If it shows a certificate error, use Option B.

### Option B: Cloudflare redirect rule (handles HTTPS properly)

1. Add a DNS record: `AAAA` · `meetup` · `100::` · **Proxied** (orange cloud).
2. Go to **Rules → Redirect Rules → Create rule**:
   - When: *Hostname* equals `meetup.deliverypilot.net`
   - Then: *Dynamic* redirect to `concat("https://meetup.cambridgeaiacademy.co.uk", http.request.uri.path)`
   - Status: **301**. Turn **Preserve query string** on.

> Don't point `meetup.deliverypilot.net` at GitHub with a CNAME. GitHub won't serve a second custom domain, so visitors would get a 404.

---

## Checking it works

```bash
nslookup -type=CNAME meetup.cambridgeaiacademy.co.uk
```

```bash
curl -sI https://meetup.cambridgeaiacademy.co.uk/prerequisites.html | head -3
```

```bash
curl -sI https://meetup.deliverypilot.net/ | grep -i -E '^(HTTP|location)'
```

You should see:

- The CNAME resolves to `rifaterdemsahin.github.io`.
- The primary returns `HTTP/2 200`.
- deliverypilot returns `301` with `location: https://meetup.cambridgeaiacademy.co.uk/`.

## Afterwards

- Change the links in `README.md` and the footer of `prerequisites.html` to `https://meetup.cambridgeaiacademy.co.uk`, then re-export `prerequisites.pdf`.
- Send attendees the short link: `meetup.cambridgeaiacademy.co.uk/prerequisites.html`.

## Troubleshooting

| Symptom | Fix |
|---|---|
| "DNS check unsuccessful" | Wait for propagation (up to 24 h for some UK registrars). Make sure `meetup` has a single CNAME to `rifaterdemsahin.github.io`. |
| "Enforce HTTPS" greyed out | The certificate is still being issued. Wait up to an hour. With Cloudflare, switch the record to DNS only. |
| 404 "There isn't a GitHub Pages site here" | The domain isn't saved in Settings → Pages, or the last Actions deploy failed. |
| Too many redirects (Cloudflare) | Set SSL/TLS mode to **Full**. |
| "Domain is already taken" | Another GitHub account has claimed it. Verify the domain (Part 1, step 2) to reclaim it. |
