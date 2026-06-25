# Russell Miller — Portfolio

Single-page portfolio positioning Russell Miller as an AI operating partner, architect, and value-creation strategist for PE/VC portfolios.
Static site. No build step.

## Repo layout
- **`docs/`** — the live site (`index.html` + `assets/` + `CNAME` + `.nojekyll`). GitHub Pages serves from here.
- **`designs/`** — scratch design explorations (`design-options*.html`), kept for reference, not published.
- **`README.md`** — this file.

`docs/` is used (not the repo root) because GitHub Pages' branch deploy only serves from the root or a `/docs`
folder — keeping the site in `docs/` lets the explorations live alongside it without being published.

**Design:** sky-blue + slate-gray on light gray ("sky and rain on slate"), Bricolage Grotesque display + Space Grotesk + IBM Plex Mono.
The hero band has an animated LLM app pipeline (prompt → retrieval → agent → tools → output) where a
sparse subset of nodes activates and propagates forward each cycle. Background is a subtle bloom +
film-grain layer (`.bg-deep` / `.bg-grain`) with a light scroll parallax. No external deps beyond Google
Fonts and the Lucide icon CDN. Scratch design explorations live in `design-options*.html` (not part of the site).

## Preview locally
Open `docs/index.html` directly, or serve that folder:
```
npx serve docs
```

## Go live at russellmiller.io (GitHub Pages + Porkbun)

The repo already contains a `CNAME` file (`russellmiller.io`) and `.nojekyll`, so the domain
re-applies automatically on every deploy. Three stages: push → enable Pages → point DNS.

### 1. Push to GitHub
Create a repo (any name, e.g. `russellmiller-portfolio` — the custom domain makes the repo name
irrelevant). Then, from this folder:
```
git remote add origin https://github.com/<your-username>/<repo>.git
git push -u origin main
```
(Repo already initialized and committed locally.)

### 2. Enable Pages
Repo **Settings → Pages**:
- **Source:** Deploy from a branch → **`main`** / **`/docs`** → Save.
- **Custom domain:** it should already show `russellmiller.io` (from the `CNAME` file). If not, type it and Save.
- Wait for the DNS check, then tick **Enforce HTTPS** (may take a few minutes to become available).

### 3. Point Porkbun DNS at GitHub
Porkbun dashboard → **russellmiller.io → Details → DNS Records**. Delete Porkbun's default
parking A/ALIAS records, then add these.

**Apex (`russellmiller.io`) — four A records.** Type `A`, Host blank (or `@`), TTL 600:
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```
**Apex IPv6 (recommended) — four AAAA records.** Type `AAAA`, Host blank, TTL 600:
```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```
**www → GitHub.** Type `CNAME`, Host `www`, Answer `<your-username>.github.io` (with trailing dot if required), TTL 600.

> Porkbun also offers an `ALIAS` record that can flatten the apex to `<your-username>.github.io` —
> either works, but the A + AAAA set above is GitHub's documented, most reliable path. Use one or the other, not both.

DNS propagates in ~5–30 min (up to a few hours). Verify with `dig russellmiller.io +short`
(should return the four GitHub IPs), then load `https://russellmiller.io`.

### Quick local test path
Open `docs/index.html` directly, or `npx serve docs` and visit the printed URL.

## Editing content
Everything lives in `index.html`:
- **Hero / stats / photo** — top `<header class="hero">`
- **LLM animation** — `.llm` band in the hero; built in the `buildLLM()` script (layers array = the pipeline stages)
- **Background texture** — `.bg-deep` (blooms) + `.bg-grain` (noise); tune the alphas in CSS, parallax factor in the `paint()` scroll handler
- **Projects** — `<section id="work">` (5 cards: Cast, Jarvis, Enact, Baryo, FileBrain)
- **Track record** — `<section id="impact">`
- **Consulting** — `<section id="approach">`
- **Contact** — `<section id="contact">` (email, LinkedIn, phone)

Project screenshots are in `assets/`. Swap an image by replacing the file or editing the `src`.
