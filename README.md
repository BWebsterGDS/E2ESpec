# Delegate Data Ingestion — E2E Spec (standalone)

Self-contained copy of the end-to-end spec for **hosting** or **sharing** without the rest of the Data Foundation repo.

## Contents

| File / folder | Role |
|---------------|------|
| **`index.html`** | Styled page with Mermaid + screenshots (open in a browser or deploy as static site). |
| **`assets/`** | `dashboard_data_quality.png`, `delegate_visualiser_browse.png` |
| **`DELEGATE_DATA_INGESTION_E2E.md`** | Same narrative in Markdown (GitHub renders Mermaid). |
| **`vercel.json`** | Optional Vercel config (static; root URL serves `index.html` by default). |

Mermaid loads from jsDelivr; no build step.

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
- **Netlify:** Same idea — publish directory = this folder (or monorepo subfolder `E2E Spec`).
- **GitHub Pages:** Repo Settings → Pages → deploy from branch; ensure `index.html` is at the published root (works if this folder is the repo root).

## Syncing from the main project

When the canonical spec changes under `docs/` in Data Foundation, refresh this folder by copying:

- `docs/DELEGATE_DATA_INGESTION_E2E_print.html` → `index.html`
- `docs/DELEGATE_DATA_INGESTION_E2E.md` → `DELEGATE_DATA_INGESTION_E2E.md`
- `docs/assets/dashboard_data_quality.png` and `delegate_visualiser_browse.png` → `assets/`

Then adjust the PDF section in the Markdown if paths are documented there.
