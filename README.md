# yuzecai.com — portfolio site

Static HTML/CSS portfolio, prepared for hosting on GitHub Pages. No build step —
everything under this folder is served as-is.

## Structure

- `index.html` — home page
- `projects/` — individual project pages (each links back to `../index.html` and `../css/styles-v5.css`)
- `css/styles-v5.css` — site styles
- `assets/images/` — images, project photos, and the 7dof HLS video clips
- `.nojekyll` — tells GitHub Pages to skip Jekyll processing (this is a plain static site)
- `CNAME` — custom domain for GitHub Pages (currently `www.yuzecai.com`)
- `.htaccess` — leftover from the old Apache/LiteSpeed host; GitHub Pages ignores it, kept only for reference and safe to delete

## Remaining steps to go live (not done yet — nothing has been pushed or published)

1. **Create the GitHub repo.** Recommended: a user site named exactly
   `curryabalone.github.io` (matches the `curryabalone` GitHub account already
   linked from the site) — this publishes at the repo root with no `/reponame/`
   path prefix, which is the simplest match for this site's relative links.
   A project repo under any other name also works (Pages just serves it at
   `/<reponame>/` instead, or at the domain root once the custom domain + CNAME
   file below are set).
2. **Push this repo** to `main` on GitHub (`git remote add origin ...`, `git push -u origin main`).
3. **Enable Pages**: repo Settings → Pages → Build and deployment → Source =
   "Deploy from a branch" → Branch = `main`, folder = `/ (root)`.
4. **Custom domain + DNS** (for `yuzecai.com` / `www.yuzecai.com`):
   - `www` CNAME record → `curryabalone.github.io`
   - Apex (`yuzecai.com`) A records → GitHub Pages IPs:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
     (or an ALIAS/ANAME record → `curryabalone.github.io` if your DNS provider supports it)
   - These are set at whatever registrar/DNS host currently serves yuzecai.com —
     Settings → Pages will also let you re-enter the custom domain there, which
     re-writes this repo's `CNAME` file to match.
   - Enable "Enforce HTTPS" in Settings → Pages once DNS has propagated (can take up to 24h).
5. Verify no old host is still authoritative for DNS before decommissioning it.

## Notes from the migration audit

- All asset/link paths in the HTML are already relative — verified no absolute
  local paths, no hardcoded `yuzecai.com` URLs outside the `<meta og:*>` tags,
  and no server-side includes. Nothing needed to change for this to work as a
  static Pages site.
- Site is ~151 MB total; largest single file is 33 MB (`assets/images/7dof/3.mp4`).
  Both are comfortably under GitHub Pages' recommended 1 GB repo size and GitHub's
  100 MB per-file hard limit, so no Git LFS is needed.
