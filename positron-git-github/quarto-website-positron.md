# Quarto Website on GitHub Pages via Positron

Build a Quarto website in Positron and publish it free on GitHub Pages. The site is rendered into a `docs/` folder on your `main` branch, and GitHub Pages serves that folder. Everything lives on one branch, and you can see exactly what's published in the repo.

**Before you start:** work through Steps 1–5 of *Git & GitHub in Positron — Basic Reference* (install and configure Git, create a repo on GitHub, clone it). Use the settings below when you create the repo in its Step 3. You also need Quarto installed (<https://quarto.org/docs/get-started/>); check with `quarto --version` in Positron's terminal.

---

## Step 1: Create and clone the repository

Follow the Basics guide Steps 3–5 with these settings:

- **Repository name:** e.g. `my-quarto-site` (this becomes part of the site URL)
- **Visibility:** **Public** — free GitHub Pages needs a public repo on personal accounts
- **Add a README file:** checked
- **Add .gitignore:** **Python** or **R** template
- **Clone it** to a local folder that is **not** synced by OneDrive or Dropbox, and open the folder in Positron

---

## Step 2: Create the website inside the repo

Open a terminal in Positron (**Terminal → New Terminal**). It starts in the repo folder. Run:

```bash
quarto create project website .
```

The `.` means "here, in this repo" — don't skip it. Quarto asks for a site title, then adds `_quarto.yml`, `index.qmd`, `about.qmd`, and `styles.css` to the repo folder.

> Positron's Command Palette option **Quarto: Create Project** creates a *new* subfolder instead, which would put the site one level down from your repo. Use the terminal command above.

---

## Step 3: Send the rendered site to `docs/`

Open **`_quarto.yml`** and add `output-dir: docs` under `project:`:

```yaml
project:
  type: website
  output-dir: docs
```

GitHub Pages can serve a folder named `docs` from your `main` branch, so this is what makes publishing work.

---

## Step 4: Update `.gitignore` and add `.nojekyll`

1. Open **`.gitignore`** and check that this line is at the end (Quarto usually adds it in Step 2; add it if it's missing):

   ```text
   /.quarto/
   ```

   This is Quarto's internal working folder. Do **not** ignore `docs/` — that folder *is* your published site.

2. Create an empty file named **`.nojekyll`** in the repo root. It tells GitHub Pages to serve your files as-is instead of running its own Jekyll site builder:

   ```bash
   touch .nojekyll          # Git Bash, macOS, Linux
   ```
   ```powershell
   New-Item .nojekyll       # Windows PowerShell
   ```

---

## Step 5: Preview and render

1. Open **`index.qmd`** and click **Preview** in the editor toolbar (or `Ctrl+Shift+K` / `Cmd+Shift+K`). The site opens in Positron's Viewer and refreshes when you save.
2. Edit `index.qmd` — change the title or add a paragraph — save, and watch the preview update.
3. When you're happy, render the whole site so `docs/` is complete:

   ```bash
   quarto render
   ```

   A `docs/` folder appears containing `index.html` and the rest of the site.

---

## Step 6: Commit and push

In **Source Control** (`Ctrl+Shift+G`):

1. Stage everything: `_quarto.yml`, the `.qmd` files, `styles.css`, `.gitignore`, `.nojekyll`, and the **`docs/`** folder.
2. Commit with a message like `Create Quarto website`.
3. Click **Sync Changes** to push.

On GitHub, refresh the repo page and check that `docs/` is there.

---

## Step 7: Turn on GitHub Pages

1. On GitHub, open the repo → **Settings** → **Pages** (left sidebar).
2. Under **Build and deployment**:
   - **Source:** Deploy from a branch
   - **Branch:** `main`
   - **Folder:** `/docs`
3. Click **Save**.

After a minute or two the page shows your site's address:

```
https://your-username.github.io/my-quarto-site/
```

You can watch the deployment under the repo's **Actions** tab.

---

## Updating the site later

The cycle is **Edit → Render → Commit → Push**:

```bash
quarto render                       # rebuild docs/
git add .
git commit -m "Update site"
git push                            # or Stage / Commit / Sync Changes in Positron
```

GitHub Pages republishes automatically after each push.

### Site didn't update?

| Symptom | Likely cause | Fix |
|---|---|---|
| Old version still showing | Forgot to render, so `docs/` didn't change | `quarto render`, then commit and push `docs/` |
| Changes pushed but not live yet | Deployment still running, or the browser cached the old page | Check the **Actions** tab; hard-refresh the browser (`Ctrl+F5`) |
| 404 at the site URL | Pages set to `/ (root)`, or `docs/` was never pushed | Settings → Pages → Folder `/docs`; confirm `docs/index.html` is on GitHub |
| Styles or images missing | `.nojekyll` missing | Add `.nojekyll` to the repo root, commit, push |
| New page doesn't appear in the menu | Page not listed in `_quarto.yml` | Add it under `website: navbar:` and re-render |
