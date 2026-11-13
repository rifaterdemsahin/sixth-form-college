# Session readiness: open tasks

Gaps to close before running **Building AI Agents for Real Business Growth**. Tick items off as they are done.

## 🔴 Blockers (must be done before the day)

- [ ] **Wi-Fi details.** Get the guest network name and password from college IT. Replace `[Network name]` and `[Password]` on the "Get connected" slide in `index.html`.
- [ ] **Wi-Fi capacity and filtering.** Ask IT whether the guest network handles ~30 laptops at once and doesn't block `fly.io`, `n8n.cloud`, `api.anthropic.com`, `stripe.com`, `github.com`, `canva.com` or outbound ports used by `git`/`flyctl`. Arrange a backup (phone hotspot or a 4G router).
- [x] **Whiteboard link.** Added `canva.link/6ruoc3i38l9870d` to the "How today works" slide.
- [ ] **Whiteboard access.** Check that the Canva board opens without sign-in. Pre-build the lanes (🗣️ Questions, 🛠️ Our build, 🚀 Ideas).
- [ ] **Send prerequisites.** Email the link to `prerequisites.html` (or the exported PDF) to all attendees **at least 5 days before** the session.
- [ ] **Custom domain.** Point `meetup.deliverypilot.net` at the site by following `DOMAIN.md`. Then switch the links in README and the prerequisites footer.
- [ ] **Session date, time and room.** Confirm these, then add them to the prerequisites page header and the email.

## 🟠 Accounts and access (audience is sixth-form, mostly under 18)

- [ ] **Age and card limits.** Fly.io, Stripe and model APIs may need users to be 18+ or to add a card. Decide the fallback: shared instructor org on Fly.io, one Stripe test account, class API keys.
- [ ] **Class API keys.** Create rate-limited, spend-capped Claude (and optional Groq) API keys for the session. Revoke them afterwards.
- [ ] **Azure Key Vault demo.** Decide whether attendees use the vault themselves or only watch the demo. If they use it, create a vault and access policy for the class.
- [ ] **Safeguarding and consent.** Check college policy on students creating third-party accounts and on photos/recordings. Get parental consent if needed.
- [ ] **Loan laptops.** Ask the college for 3–5 spare laptops with software pre-installed, for students whose machines are locked down.

## 🟡 Content and materials

- [ ] **Starter repo.** Publish a template repo (agent + Dockerfile + `fly.toml` + Stripe webhook stub) that attendees clone in Module 4.
- [ ] **n8n template.** Export the supervisor → research / writer / reviewer workflow as JSON for attendees to import.
- [ ] **Bot catalogue link.** The Module 3 "Our bot catalogue" demo has no URL yet. Add one.
- [ ] **Appendix assets.** Link the "How LLMs read tokens" video and the RAG infographic referenced in the appendix.
- [ ] **Post-session follow-up.** Prepare an email with the slides, recordings, the starter repo and next steps.

## 🟢 On the day

- [ ] Arrive 30 minutes early. Test the projector, HDMI/USB-C adapters, sound and Wi-Fi.
- [ ] Laptop check at the door (Marianna): run the commands in section 4 of the prerequisites page.
- [ ] Put the Wi-Fi details and whiteboard QR code on a printed sign at the entrance.
- [ ] Extension leads and power strips for chargers.
- [ ] Check spend dashboards for class API keys and Fly.io during the session. Tear down apps afterwards.
