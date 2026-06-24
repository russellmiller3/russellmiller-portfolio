# Russell Miller — Portfolio

Single-page portfolio for AI product roles and operating-partner consulting.
Static site — `index.html` + `assets/`. No build step.

## Preview locally
Open `index.html` directly, or serve the folder:
```
npx serve .
```

## Publish to GitHub Pages

### Fastest (web upload, no git)
1. Create a new repo on GitHub named **`<your-username>.github.io`** (public).
2. On the repo page, click **Add file → Upload files**, drag in `index.html`, the `assets/` folder, and `.nojekyll`, then **Commit**.
3. Site goes live at `https://<your-username>.github.io` in ~1 minute.

### With git CLI
```
cd personal-site
git init
git add .
git commit -m "Portfolio site"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-username>.github.io.git
git push -u origin main
```
Then in the repo: **Settings → Pages → Source: Deploy from a branch → main / root**.

## Custom domain (optional)
Add a file named `CNAME` containing your domain (e.g. `russellmiller.ai`), then point a CNAME/ALIAS DNS record at GitHub Pages.

## Editing content
Everything lives in `index.html`:
- **Hero / stats** — top `<header class="hero">`
- **Projects** — `<section id="work">` (5 cards: Cast, Jarvis, Enact, Baryo, FileBrain)
- **Track record** — `<section id="impact">`
- **Consulting** — `<section id="approach">`
- **Contact** — `<section id="contact">` (email, LinkedIn, phone)

Project screenshots are in `assets/`. Swap an image by replacing the file or editing the `src`.
