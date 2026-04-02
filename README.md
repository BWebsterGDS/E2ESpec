# Delegate Data Ingestion — E2E Spec (standalone)

Self-contained copy of the end-to-end spec for **hosting** or **sharing** without the rest of the Data Foundation repo.

## First-time Vercel (if the dashboard is empty)

**Pushes to GitHub do not create a Vercel project by themselves.** You must connect the repo once:

1. Open **[vercel.com/new](https://vercel.com/new)** (sign in with GitHub).
2. **Import** → choose **`BWebsterGDS/E2ESpec`** → **Import**.
3. **Project name:** `e2e-spec` (lowercase only).
4. **Framework:** Other · **Root directory:** `.` · **Build** / **Output** can stay empty (static `index.html`).
5. Click **Deploy**. After that, every **`git push` to `main`** will show up under **Deployments**.

If the project already exists: **Settings → Git** → confirm repository **E2ESpec** and production branch **`main`**. Use **Deployments → … → Redeploy** if a webhook was missed.

## Live site updates from the Data Foundation project

**Vercel only builds what is in this GitHub repo** ([BWebsterGDS/E2ESpec](https://github.com/BWebsterGDS/E2ESpec)). Edits under `docs/` in Data Foundation are **not** deployed until you sync into `E2E Spec/` and push.

From the Data Foundation project root:

```powershell
powershell -File scripts\publish_e2e_spec.ps1
```

That copies the print HTML → `index.html`, syncs Markdown + screenshots, then **commits and pushes** when there are changes.

## GitHub Pages (optional backup URL)

This repo includes **`.github/workflows/deploy-github-pages.yml`** (aligned with [GitHub’s static Pages starter](https://github.com/actions/starter-workflows/blob/main/pages/static.yml)).

1. **Settings → Pages → Build and deployment → Source:** choose **GitHub Actions** (not “Deploy from a branch”) and save.
2. Push to `main` or run the workflow manually (**Actions → Deploy static content to Pages → Run workflow**).

The site URL appears under **Pages** and in the workflow summary (often `https://bwebstergds.github.io/E2ESpec/`).

**If the workflow failed before:** the earlier YAML was missing **`actions/configure-pages`**; that is fixed on `main`. If it still fails, open the failed job log — common causes are Pages not enabled yet, or the **`github-pages` environment** waiting for approval (**Settings → Environments**).

## Contents

| File / folder | Role |
|---------------|------|
| **`index.html`** | Styled page with Mermaid + screenshots (open in a browser or deploy as static site). |
| **`assets/`** | `dashboard_data_quality.png`, `delegate_visualiser_browse.png` |
| **`DELEGATE_DATA_INGESTION_E2E.md`** | Same narrative in Markdown (GitHub renders Mermaid). |
| **`vercel.json`** | Optional Vercel config (static; root URL serves `index.html` by default). |

Mermaid loads from jsDelivr; no build step.

**Mermaid vs PNG:** GitHub and Vercel both run the same Mermaid JS — nothing is “wrong” with the push. Subgraph **titles** inside diagrams often overlap arrows (a Mermaid layout limitation). This site uses **flat** charts (no subgraph boxes) for charts 2–3 and puts phase names in the **page heading** instead. If you need **pixel-perfect** diagrams, export SVG/PNG from [mermaid.live](https://mermaid.live) (or `@mermaid-js/mermaid-cli`), add files under `assets/`, and swap the `<pre class="mermaid">` blocks for `<img>` tags — at the cost of harder edits.

## Push to Git

1. Initialise a repo **in this folder** (or copy `E2E Spec` into an empty repo root):

   ```powershell
   cd "E2E Spec"
   git init
   git add .
   git commit -m "Add E2E spec static site"
   ```

2. Create a remote on GitHub/GitLab and `git push -u origin main`.

## Deploy (examples)

- **Vercel:** Import the repo. If the repo root **is** this folder, use defaults (no framework, no build). If the repo is the **parent** monorepo, set **Root Directory** to `E2E Spec`.
- **Vercel project name:** Must be **only lowercase** letters, digits, `.`, `_`, and `-` (max 100 chars). Repo names like `E2ESpec` are invalid — on the import screen, set **Project Name** to e.g. `e2e-spec` (this repo’s `vercel.json` sets `"name": "e2e-spec"` as a hint). Avoid spaces (e.g. parent folder `Data Foundation`).
- **Netlify:** Same idea — publish directory = this folder (or monorepo subfolder `E2E Spec`).
- **GitHub Pages:** Repo Settings → Pages → deploy from branch; ensure `index.html` is at the published root (works if this folder is the repo root).

## Syncing from the main project

When the canonical spec changes under `docs/` in Data Foundation, refresh this folder by copying:

- `docs/DELEGATE_DATA_INGESTION_E2E_print.html` → `index.html`
- `docs/DELEGATE_DATA_INGESTION_E2E.md` → `DELEGATE_DATA_INGESTION_E2E.md`
- `docs/assets/dashboard_data_quality.png` and `delegate_visualiser_browse.png` → `assets/`

Then adjust the PDF section in the Markdown if paths are documented there.
