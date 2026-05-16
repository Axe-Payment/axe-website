# Push to GitHub + connect Vercel

This is a one-time setup. After it's done, your workflow becomes:

```
edit → git commit → git push → Vercel auto-deploys
```

---

## Step 1 — Create the repo on GitHub

In a browser, log into GitHub as **mosin.hafeez112@gmail.com** (or whichever account you want):

1. Go to **https://github.com/new**
2. **Repository name:** `axe-website` (or anything you want)
3. **Description:** `Marketing site for Axe Payments`
4. **Visibility:** Private is fine. Public is fine. Either works with Vercel.
5. **Do NOT** initialise with a README, .gitignore, or licence — your local folder already has those.
6. Click **Create repository**.

GitHub will show a "quick setup" page with a URL like `git@github.com:<your-handle>/axe-website.git`. Copy it — you'll paste it in step 2.

---

## Step 2 — Push the local folder

In your terminal:

```bash
cd "/Users/mosin/Library/Application Support/Claude/local-agent-mode-sessions/82641a72-73bb-419c-baad-7c693d33b058/2ca43635-b47e-4aa0-814d-768fbc333242/local_335e1bbf-6c30-4f72-8c5b-3d237696d4de/outputs/axe-website"

git init
git add .
git commit -m "axe payments — initial site"
git branch -M main
git remote add origin git@github.com:<your-handle>/axe-website.git   # paste the URL from step 1
git push -u origin main
```

If `git@github.com:...` asks for permission and you've never set up SSH:
- Either set up an SSH key (https://docs.github.com/en/authentication/connecting-to-github-with-ssh) — recommended,
- Or use the HTTPS URL instead: `https://github.com/<your-handle>/axe-website.git` (GitHub will prompt for a personal access token; create one at https://github.com/settings/tokens).

After `git push` succeeds, refresh the GitHub page — your files are there.

---

## Step 3 — Connect Vercel for auto-deploys

This is what makes every future `git push` deploy automatically.

1. Go to **https://vercel.com/new**
2. If you used `vercel --prod` earlier, the project already exists — skip to step 3a.
   Otherwise, click **Add New → Project** and **Import** the `axe-website` repo from GitHub.
3. **Framework preset:** select **Other** (it's a static HTML site).
4. **Root directory:** leave as `./`.
5. **Build command:** leave **empty**.
6. **Output directory:** leave as `./`.
7. Click **Deploy**.

   3a. *(If the project already exists from a CLI deploy)* Open it in Vercel → **Settings → Git** → click **Connect Git Repository** → pick the GitHub repo. Done.

Vercel will build the first time. From now on:

- **Push to `main`** → Vercel deploys to production.
- **Open a PR** → Vercel deploys a preview URL on the PR.

---

## Step 4 — Custom domain (optional, anytime)

In the Vercel project → **Settings → Domains**:

1. Add `axepayments.com` (and `www.axepayments.com`).
2. Vercel shows DNS records. At your registrar (Namecheap / GoDaddy / Cloudflare):
   - Root: an `A` record pointing to `76.76.21.21`.
   - `www`: a `CNAME` to `cname.vercel-dns.com`.
3. SSL is provisioned automatically (a few minutes).

---

## Day-2 workflow

Once everything above is wired up, your loop is:

```bash
# 1. edit index.html (or any file)
# 2. preview locally
python3 -m http.server 5173

# 3. commit
git add .
git commit -m "update hero copy"

# 4. push
git push

# Vercel deploys within ~30 seconds.
# Watch progress at https://vercel.com/<your-org>/axe-website
```

For a feature branch + preview URL:

```bash
git checkout -b experiment-new-hero
# edit
git push -u origin experiment-new-hero
# open a PR on GitHub — Vercel posts the preview URL in the PR comments
```

---

## Common gotchas

- **`git push` rejected because remote contains commits**
  This happens if you initialised the GitHub repo with a README. Run `git pull origin main --allow-unrelated-histories` to merge, then push.
- **Vercel deploy succeeds but shows the wrong page**
  Check the **Output Directory** in Vercel project settings is `./` (not `dist` or `public`).
- **Custom domain shows a Vercel error page**
  DNS hasn't propagated yet. Give it 10–60 minutes and check again with `dig axepayments.com`.
- **Can't `git push` — permission denied**
  Either your SSH key isn't added to GitHub, or you used the wrong URL. Test with `ssh -T git@github.com`. Should print "Hi `<your-handle>`".

---

## Where things live

- **Source:** this folder, mirrored on GitHub.
- **Builds + hosting:** Vercel.
- **Domain:** your registrar.
- **DNS:** wherever your domain's DNS is hosted (often the registrar; Cloudflare is also common).

That's the entire stack. Three services, one source of truth (this folder).
