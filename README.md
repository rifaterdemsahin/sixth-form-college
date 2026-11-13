# 🤖 Building AI Agents for Real Business Growth

A 120-minute hands-on masterclass for sixth-form college students, from Cambridge AI Academy. Attendees go from single-turn prompts to a multi-agent bot deployed at a public URL with a test Stripe checkout.

🔗 **Slides (live):** https://rifaterdemsahin.github.io/sixth-form-college/
📋 **Attendee prerequisites:** https://rifaterdemsahin.github.io/sixth-form-college/prerequisites.html
🌐 **Custom domains (setup pending):** https://meetup.cambridgeaiacademy.co.uk (primary) and https://meetup.deliverypilot.net (redirect). See [`DOMAIN.md`](DOMAIN.md)
🎨 **Session whiteboard (Canva):** https://canva.link/6ruoc3i38l9870d

## 🗓️ Agenda

| Time | Segment | Topics |
|---|---|---|
| 00:00–00:10 | 👋 Welcome & setup | Wi-Fi, whiteboard, Tell · Show · Do · Apply |
| 00:10–00:35 | 🧠 Module 1: Agent architecture | Prompts → execution loops, ReAct, tool JSON schemas |
| 00:35–00:55 | 📚 Module 2: Memory & grounding | RAG, hybrid search, citations, memory types |
| 00:55–01:00 | ☕ Break | |
| 01:00–01:30 | 🛠️ Module 3: Multi-agent teams | n8n supervisor-worker flows, MCP (Slack, Gmail, Sheets) |
| 01:30–01:50 | 🚀 Module 4: Deploy & monetise | Fly.io London, Azure Key Vault, Stripe metered billing |
| 01:50–02:00 | ✅ Launch & wrap-up | Live launch checklist, next steps |

## 🌐 Custom domain status

| Step | Status |
|---|---|
| 1️⃣ DNS `CNAME` record added | ✅ Done |
| 2️⃣ Domain verified on GitHub (TXT record) | ⏳ To do |
| 3️⃣ Custom domain saved in repo Settings → Pages | ⏳ To do |
| 4️⃣ Enforce HTTPS ticked | ⏳ To do |
| 5️⃣ `meetup.deliverypilot.net` redirects (301) to the primary | ⏳ To do |

📡 **DNS record in place for `meetup.cambridgeaiacademy.co.uk`:**

| 🏷️ Type | 🖥️ Name / Host | 🎯 Value / Target | ⏱️ TTL |
|---|---|---|---|
| `CNAME` | `meetup` | `rifaterdemsahin.github.io` | 3600 (or Auto) |

👉 Next: verify the domain, set it in **Settings → Pages**, then tick **Enforce HTTPS**. See [`DOMAIN.md`](DOMAIN.md) for the steps.

## 📁 Repository contents

| File | Purpose |
|---|---|
| `index.html` | The slide deck (self-contained HTML, 1920×1080 slides) |
| `Building AI Agents for Real Business Growth.pdf` | PDF export of the deck |
| `prerequisites.html` | Printable checklist to send attendees before the session |
| `prerequisites.pdf` | A4 PDF export of the prerequisites page, ready to attach to an email |
| `DOMAIN.md` | How to point `meetup.cambridgeaiacademy.co.uk` and `meetup.deliverypilot.net` at this site |
| `TASKS.md` | Open tasks and gaps to close before the session (Wi-Fi, accounts, materials) |
| `.github/workflows/static.yml` | Deploys the repo to GitHub Pages on every push to `main` |

## 📨 Sending prerequisites to attendees

1. Open `prerequisites.html` (or the live link above) in Chrome.
2. Click **Save as PDF**, or use **Print → Save as PDF**, paper size A4.
3. Send the PDF, or just the link, **at least 5 days before** the session.

`prerequisites.pdf` in this repo is a ready-made export. Regenerate it after editing the page.

## ✅ Before the session

See [`TASKS.md`](TASKS.md). The main open gaps are:

- Wi-Fi network name and password are still placeholders on the "Get connected" slide.
- Fallback accounts are needed for under-18 attendees (Fly.io, Stripe, API keys).
- The starter repo and n8n workflow template still need to be published.

## 🚀 Deployment

GitHub Pages serves everything in the repo root. Pushing to `main` triggers `.github/workflows/static.yml`, which publishes the site.

🌿 **One branch only:** all work lands on `main`, and there are no long-lived feature branches.
