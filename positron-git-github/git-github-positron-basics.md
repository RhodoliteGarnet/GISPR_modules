# Git & GitHub in Positron — Basic Reference

A minimal, step-by-step reference for getting a GitHub repo onto your machine and working with it in Positron. The running example is a small practice repo, `gispr-practice`. When you're comfortable with this, the next guide, **Quarto Website on GitHub Pages via Positron**, reuses Steps 1–5 to build and publish a website.

---

## 1. Make sure Git is installed

Open a terminal in Positron: **Terminal → New Terminal** (or `` Ctrl+` ``).

```bash
# Git Bash, macOS, Linux
which git

# Windows PowerShell or Command Prompt
where.exe git

# Any shell: confirms Git runs and shows the version
git --version
```

If nothing is found, install Git from <https://git-scm.com>. On Windows, **Git for Windows** includes Git Bash and Git Credential Manager, which handles GitHub sign-in later. Restart Positron after installing.

> **Tip (Windows):** To use Git Bash as Positron's terminal, open the terminal dropdown (˅ next to +) → **Select Default Profile** → **Git Bash**. Then `which git` works.

---

## 2. Configure Git (once per computer)

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
git config --global init.defaultBranch main   # matches GitHub's default branch name

# Check your settings
git config --global --list
```

Use the same email as your GitHub account (or your GitHub-provided `noreply` address) so commits are linked to your profile.

> If the `--list` output fills the screen, press **Space** to page down and **q** to exit.

---

## 3. Create a new repository on GitHub

1. Sign in at <https://github.com> and click **+ → New repository**.
2. **Repository name:** `gispr-practice`.
3. **Visibility:** Public or Private — either works for this practice repo.
4. Check **Add a README file**.
5. **Add .gitignore:** choose the **Python** or **R** template, whichever language you'll use most.
6. **License:** optional (MIT is a common choice).
7. Click **Create repository**.

---

## 4. Copy the repository URL

On the repo page click the green **Code** button → **HTTPS** tab → copy the URL, e.g.

```
https://github.com/your-username/gispr-practice.git
```

---

## 5. Clone the repo in Positron

> **Where to clone:** Put repos in a local folder that is *not* synced by OneDrive, Dropbox, or iCloud (e.g. `C:\Users\you\Documents\GitHub` or `C:\repos`). Cloud sync fights with the hidden `.git` folder and can corrupt the repo.

**Option A — Positron UI**

1. **File → New Folder from Git…** (also on the Welcome page).
2. Paste the repo URL.
3. Choose the parent folder to clone into.
4. Open the cloned folder when prompted.

**Option B — Command Palette**

1. `Ctrl+Shift+P` (`Cmd+Shift+P` on macOS) → type **Git: Clone** → Enter.
2. Paste the URL, choose the parent folder, then **Open**.

**Option C — Terminal**

```bash
cd ~/Documents/GitHub
git clone https://github.com/your-username/gispr-practice.git
```

Then **File → Open Folder…** and select `gispr-practice`.

**First push / sign-in:** The first time you push, Git Credential Manager opens a browser window to sign in to GitHub. After that, your credentials are remembered.

---

## 6. Everyday workflow in Positron

The cycle is: **Pull → Edit → Stage → Commit → Push**.

Open the **Source Control** view from the Activity Bar (branch icon) or `Ctrl+Shift+G`.

| Task | Positron | Terminal equivalent |
|---|---|---|
| Get latest changes from GitHub | **⋯** menu → **Pull**, or the sync arrows in the status bar | `git pull` |
| See what changed | Files listed under **Changes**; click a file to see the diff | `git status` / `git diff` |
| Stage a file | Click **+** next to the file (or **+** on the *Changes* header to stage all) | `git add filename` / `git add .` |
| Unstage a file | Click **−** next to the file under *Staged Changes* | `git restore --staged filename` |
| Commit | Type a message in the box, click **Commit** (or `Ctrl+Enter`) | `git commit -m "Your message"` |
| Push to GitHub | **Sync Changes** button, or **⋯** → **Push** | `git push` |
| Discard local edits to a file | Click the ↶ (Discard Changes) icon next to the file | `git restore filename` |
| Switch or create a branch | Click the branch name in the bottom-left status bar | `git switch branch-name` / `git switch -c new-branch` |
| View history | **Source Control Graph** section in the Source Control view | `git log --oneline` |

**Status bar (bottom left):** shows the current branch and ↓/↑ counts of commits to pull/push. Clicking the arrows syncs (pull, then push).

**Note:** If you click **Commit** with nothing staged, Positron asks whether to stage and commit all changes.

---

## 7. Practice: your first round trip

Do this once end to end so the cycle in Step 6 becomes familiar.

1. **Pull** (Step 6) — nothing should come down yet, but make it a habit.
2. **Edit the README:** open `README.md` and add a line, e.g. `Practice repo for GISPR.` Save.
3. **Add a small script:** create `hello.py` (or `hello.R`) containing one line:

   ```python
   print("Hello from GISPR")          # hello.py
   ```
   ```r
   cat("Hello from GISPR\n")          # hello.R
   ```

   Run it in Positron to confirm it works.
4. **Look at the changes** in Source Control: `README.md` shows as modified (**M**), `hello.py` as untracked (**U**). Click each to see the diff.
5. **Stage** both files, write the commit message `Add README note and hello script`, and **Commit**.
6. **Push** with **Sync Changes**.
7. **Check on GitHub:** refresh the repo page — your commit message, the README change, and `hello.py` are all there.
8. **Bonus:** edit `README.md` directly on GitHub (pencil icon → **Commit changes**), then **Pull** in Positron and watch the change arrive.

---

## Quick command cheat sheet

```bash
git --version                 # is Git installed?
git config --global --list    # show your Git config
git clone <url>               # copy a GitHub repo to your machine
git status                    # what's changed?
git pull                      # get latest from GitHub
git add .                     # stage all changes
git commit -m "message"       # save a snapshot
git push                      # send commits to GitHub
git log --oneline             # short history
```

**Next:** *Quarto Website on GitHub Pages via Positron* — uses Steps 1–5 above to build and publish a site.
