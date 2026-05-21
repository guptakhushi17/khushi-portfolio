# Khushi Portfolio — Hosting Guide

Your site is now a self-contained static folder:

```
khushi-portfolio/
├── index.html        ← the whole website
└── videos/
    ├── reel-01.mp4  …  reel-09.mp4   ← your 9 reels (web-safe H.264)
```

9 reels are wired into the House of Sinha sections. The remaining slots stay
as "+" placeholders you can fill later (see the instructions panel at the
bottom of the page).

---

## First: put your files on GitHub (web only, no software needed)

Every file here is under 25 MB, so GitHub's website uploader handles them all.

1. Sign in at **github.com** (create a free account if needed).
2. Click **+ → New repository**. Name it `khushi-portfolio`, set it **Public**,
   tick **Add a README**, then **Create repository**.
3. Click **Add file → Upload files**. Drag in `index.html`, `HOSTING-GUIDE.md`,
   **and** the whole `videos` folder (drag the folder itself — GitHub keeps the
   structure). Wait for all files to finish, then **Commit changes**.

Your site files now live in your own GitHub repo.

---

## Option A — GitHub Pages (recommended: free, uses your own repo)

Since your files are already on GitHub, this is the most direct way to go live:

1. In your repo, go to **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Set branch to **main** and folder to **/(root)**, then **Save**.
4. Wait ~1 minute. Your site is live at
   `https://YOUR-USERNAME.github.io/khushi-portfolio/`.

(Custom domain optional under the same Pages settings.)

---

## Option B — Lovable (note the important limitation)

**Lovable cannot import an existing GitHub repo** — its GitHub integration only
goes the other way: Lovable creates the repo and syncs to it. So the working
sequence is *Lovable first, then add your files to the repo it makes:*

1. **Create a project** at lovable.dev (any prompt, e.g. "a personal portfolio").
2. **Connect GitHub:** *Settings → Connectors → GitHub*, authorize the Lovable
   GitHub App, and connect the project. Lovable creates a repo with two-way sync.
3. **Open that repo on GitHub**, go into the `public/` folder, and
   **Add file → Upload files** — drag in `index.html` and the `videos` folder.
   Commit. Lovable pulls the changes in.
4. In Lovable's chat, say: *"Serve public/index.html as the home page and remove
   the default React pages."* Then click **Publish**.

Because the videos sit in `public/`, keep the `src="videos/..."` paths as-is.

> If this feels fiddly, Option A (GitHub Pages) gets the same result with fewer
> steps — Lovable's strength is AI-built React apps, not hosting a finished
> static page.

---

## Option C — Netlify Drop (fastest of all, no GitHub needed)

If the goal is simply to get the site live with the videos working, this takes
about 60 seconds and needs no GitHub or build setup:

1. Go to **app.netlify.com/drop**
2. Drag the **entire `khushi-portfolio` folder** onto the page.
3. Done — you get a live URL instantly (e.g. `random-name.netlify.app`).
   Rename it or add a custom domain in *Site settings → Domain*.

This works because the folder is fully static and the video paths are relative.

---

## Other one-folder static hosts (all work the same way)

- **GitHub Pages** — push the folder to a repo, enable Pages on the `main`
  branch (root). Free.
- **Vercel** — *New Project → import folder* (no framework). Free tier.
- **Cloudflare Pages** — connect a repo or direct-upload the folder. Free.

---

## Adding more reels later

1. Drop the new `.mp4` into the `videos/` folder (name it e.g. `reel-10.mp4`).
   If it's a `.mov`/HEVC file, convert it to H.264 MP4 first so every browser
   can play it.
2. In `index.html`, find an empty `<div class="media-video">…</div>`
   placeholder and replace it with:

```html
<div class="media-video" style="cursor:default;">
  <video style="position:absolute;inset:0;width:100%;height:100%;object-fit:cover;border-radius:var(--radius);"
         controls playsinline preload="metadata">
    <source src="videos/reel-10.mp4" type="video/mp4">
  </video>
</div>
```

To reorder reels, just swap the filenames in each `src`.
