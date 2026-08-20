# Deploying GUKIN — GitHub + Netlify

From the zip on your desktop to a live site on your own domain. No terminal, no build tools. Budget 25 minutes the first time.

**What you need**

- The `gukin-final` folder, unzipped
- A free GitHub account — github.com
- A free Netlify account — netlify.com
- Your domain registrar login (Part 5 only)

---

## Part 0 — Check the folder before you start

Unzip the download and open `gukin-final`. You should see six `.md`/`.toml` files, a `.gitignore`, and a `site` folder containing twelve `.html` files plus `media/`.

**74 files in total.** `FILES.md` lists every one — what it is, where it's used, and which are safe to delete.

Two rules that govern everything below:

1. **Upload the *contents* of `gukin-final`, not the folder itself.** `netlify.toml` must land at the top level of the repository. Nested inside another folder, Netlify won't find it and every page returns "Page not found".
2. **Never rename `site/` or `site/media/`.** Every image is referenced as `media/filename`.

If your unzip produced `gukin-final/gukin-final/`, open the inner one — that's the real folder.

---

## Part 1 — Create the GitHub repository

1. Sign in at **github.com**.
2. Top-right **+** → **New repository**.
3. **Repository name:** `gukin-website` — lowercase, no spaces.
4. **Public** or **Private** — both work with Netlify. Private is fine.
5. Leave **Add a README**, **.gitignore** and **licence** all **unticked**. The zip already has them; ticking these creates merge conflicts on your first upload.
6. **Create repository.**

You'll land on an empty repository page. Ignore the terminal commands.

---

## Part 2 — Upload the files

On the empty repository page, click **"uploading an existing file"**. (If you've navigated away: **Add file → Upload files**.)

1. Open `gukin-final` in Finder or File Explorer.
2. **Select everything inside it** — `netlify.toml`, the five `.md` files, `.gitignore`, and the `site` folder.
3. **Drag it all onto the GitHub upload area.** GitHub expands `site/` and lists every file inside, including all 55 images. This takes a few minutes.
4. Wait until every file shows as uploaded. **Do not navigate away mid-upload.**
5. In **Commit changes**, type `Initial site`, then **Commit changes**.

### If `.gitignore` doesn't appear

Dotfiles are hidden by default. Press **Cmd + Shift + .** on macOS, or tick **Hidden items** in the Windows View ribbon. Or skip it — the site deploys fine without it.

### Verify the upload

Your repository root should show `netlify.toml` and `site` side by side. Click into `site` — twelve `.html` files. Click into `media` — 55 images. If `netlify.toml` is inside a subfolder, move it to the root before deploying.

---

## Part 3 — Connect Netlify

1. Sign in at **netlify.com**. Signing in **with GitHub** authorises both accounts in one step.
2. **Add new site → Import an existing project**.
3. Choose **GitHub**, authorise if prompted.
4. **Install the Netlify GitHub App** when asked. Choose **All repositories**, or **Only select repositories** → `gukin-website`. This is what lets Netlify read your code — skip it and the repo won't appear in the list.
5. Select `gukin-website`.
6. Confirm the build settings:
   - **Branch to deploy:** `main`
   - **Build command:** *leave empty*
   - **Publish directory:** `site`

   `netlify.toml` sets these automatically, so they should be pre-filled. If the publish directory is blank or shows `/`, type `site` yourself — this is the single most common cause of a failed first deploy.
7. **Deploy site.**

Netlify builds for 30–90 seconds and gives you a URL like `random-name-12345.netlify.app`. Open it. Click through to Shop, About, Journal, Terms, Privacy and Shipping — all twelve pages should load.

### Rename the subdomain

**Site configuration → Site details → Change site name** → enter `gukin`. Your URL becomes `gukin.netlify.app`.

---

## Part 4 — Running the site day to day

**Every push to `main` redeploys automatically.** Commit a change on GitHub, wait about a minute, refresh.

### Editing text

1. On GitHub, open the file — e.g. `site/privacy.html` or `site/about.html`.
2. Click the **pencil** icon.
3. **Ctrl/Cmd + F** and search for the words you see on the live page.
4. Change the text between the tags. Don't touch anything inside `< >`.
5. Scroll down → **Commit changes.**

The content pages (`shop`, `about`, `blog`, the four articles, and the three policy pages) are plain HTML and easy to edit this way. `index.html` and `product.html` are compiled application files — editable, but search carefully and change only the visible text.

### Replacing a photo

1. Open `site/media/` on GitHub.
2. **Add file → Upload files**, drag your new photo in.
3. Give it **exactly** the filename it replaces — lowercase, same extension.
4. **Commit changes.**

`FILES.md` maps every filename to where it appears.

### Adding a journal article

Duplicate one of the four existing article files, rename it, and edit the heading, body and meta tags. Then add a card for it in `blog.html` by copying an existing card block. Nothing else needs changing.

### Watching a deploy

Netlify → **Deploys**. Green **Published** means live. Red means failed — click for the log.

### Rolling back

Netlify → **Deploys** → click an earlier successful deploy → **Publish deploy**. The site reverts instantly and GitHub is untouched, so you can fix the file without time pressure.

---

## Part 5 — Your own domain

1. Netlify → **Domain management → Add a domain** → enter `gukinwell.com` → **Verify**.
2. Netlify shows the records you need. Two routes:

   **Route A — point DNS at Netlify (simplest)**
   At your registrar, edit DNS:
   - `A` record, host `@`, value `75.2.60.5`
   - `CNAME` record, host `www`, value `your-site.netlify.app`

   **Route B — move DNS to Netlify (more control)**
   Netlify gives you four nameservers. Replace your registrar's nameservers with those; Netlify then manages all DNS for the domain.

3. Wait for propagation — usually under an hour, occasionally up to 24.
4. Netlify issues a free **Let's Encrypt certificate** automatically. If the padlock doesn't appear once DNS resolves, go to **Domain management → HTTPS → Verify DNS configuration**, then **Provision certificate**.
5. Set the primary domain. Netlify redirects the other variant automatically, so `www` and the bare domain both work with one canonical version.

The canonical URLs in the page headers are already set to `https://gukinwell.com/`. If you deploy on a different domain, search and replace `gukinwell.com` across the twelve HTML files.

---

## Part 6 — Before you promote the site

### Compress the photos — do this first

This is the highest-value remaining task. Several files in `site/media/` are 3–7 MB. The pages already lazy-load and defer everything below the fold, but no amount of clever loading fixes a 7 MB JPEG.

1. Go to **squoosh.app**.
2. Drag in one photo.
3. Right panel: format **MozJPEG**, quality around **80**, and under Resize set the longest edge to **1600 px**.
4. Download, then upload to `site/media/` on GitHub **with the original filename**.
5. Target: every file under 300 KB.

Keep the original extension (`.jpg` stays `.jpg`) and no HTML edit is needed. If you export `.webp`, you must also update every `src` referencing that file.

Expect this alone to cut load time by more than half.

### Then

- **Test on a real phone**, not just a narrow browser window.
- **Connect the two forms.** The waitlist and the welcome popup currently validate and show a confirmation but don't send anywhere. Netlify Forms is the least-effort option: add `netlify` and `name="..."` attributes to the form, and submissions appear in your Netlify dashboard. Klaviyo or Mailchimp if you want automated flows.
- **Wire up the cart.** The cart drawer, quantity steppers, subtotal and free-delivery bar all work as a front end, but Checkout isn't connected to a payment processor. See `SHOPIFY-AND-TODO.md`.
- **Add analytics** — Netlify Analytics needs no code, or paste a Plausible/Google Analytics snippet before `</head>` in each page.
- **Submit a sitemap** to Google Search Console once the domain is live. The FAQ and article schema is already in place, so rich results should follow.

---

## Troubleshooting

**"Page not found" on every page**
Publish directory is wrong. **Site configuration → Build & deploy → Publish directory** → set to `site` → redeploy. If `netlify.toml` sits in a subfolder, that's the cause — move it to the repository root.

**Homepage works, other pages 404**
Those HTML files didn't upload. Open `site/` on GitHub and count — there should be twelve.

**Site loads but no photos**
`site/media/` uploaded incompletely, or a case mismatch — `Photo.JPG` will not match `photo.jpg`. Compare the folder against `FILES.md`.

**One photo missing**
Filename mismatch, nearly always. The `src` in the HTML and the file in `media/` must match exactly, extension included.

**Deploy succeeded but the change isn't visible**
Browser cache. Hard-refresh with **Cmd + Shift + R** or **Ctrl + F5**. Note that `netlify.toml` deliberately caches `media/` for a year — a replaced image under the same filename may take a moment to appear. Netlify busts this on deploy, but your browser may not.

**Netlify can't see the repository**
The GitHub App isn't installed for it. GitHub → **Settings → Applications → Netlify → Configure** → add the repository.

**Upload keeps failing on GitHub**
The web uploader caps at 100 files per commit. 74 files should fit, but if it stalls, upload in batches: root files and the twelve HTML files first, then `site/media/` in two or three commits.

**A change broke the layout**
Roll back in Netlify (**Deploys** → an earlier deploy → **Publish deploy**), then fix the file at your own pace.

---

## Quick reference

| Task | Where |
| --- | --- |
| Edit page text | GitHub → `site/<page>.html` → pencil icon |
| Replace a photo | GitHub → `site/media/` → Upload, same filename |
| Add an article | Duplicate an article file, add a card in `blog.html` |
| Watch a deploy | Netlify → Deploys |
| Roll back | Netlify → Deploys → older deploy → Publish deploy |
| Change the subdomain | Netlify → Site configuration → Change site name |
| Add a domain | Netlify → Domain management |
| Compress photos | squoosh.app |

## For a developer

Handing this to an engineer to rebuild in Next.js or wire up Shopify: point them at `HANDOFF.md` for the component spec, tokens and motion, and `SHOPIFY-AND-TODO.md` for the Storefront API query and field mapping.
