# Delegate Data Ingestion — E2E Spec (standalone)

Self-contained copy of the end-to-end spec for **hosting** or **sharing** without the rest of the Data Foundation repo.

## Live site (Vercel) not updating?

**Vercel deploys from this GitHub repo only** ([BWebsterGDS/E2ESpec](https://github.com/BWebsterGDS/E2ESpec)). If you change files under `docs/` in the **Data Foundation** project on disk, **the live site will not change** until those files are copied into this folder and **pushed to `main`**.

**One command** (from the Data Foundation project root, with this folder present):

```powershell
powershell -File scripts\publish_e2e_spec.ps1
```

That copies `DELEGATE_DATA_INGESTION_E2E_print.html` → `index.html`, syncs the Markdown + screenshots, then **commits and pushes** if anything changed.

**Check Vercel:** Project → **Settings → Git** → connected repo and **Production Branch** = `main`. **Deployments** should show a new build after each push. If Git is connected but nothing builds, use **Redeploy** on the latest deployment.

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
