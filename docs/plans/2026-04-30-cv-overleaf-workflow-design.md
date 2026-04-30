# CV authoring workflow — Overleaf-synced, local real-time compilation

**Date:** 2026-04-30
**Goal:** Edit `cv.tex` either on Overleaf web or locally in VS Code, build to `Yuzheng_CV.pdf`, publish that PDF into the website repo's `assets/`.

## Layout

```
C:\Users\huyuz\hyz\
├── Mirnegg.github.io\           # website repo (this repo)
│   └── assets\Yuzheng_CV.pdf    # built output, copied here on publish
└── Yuzheng_CV\                  # NEW — its own git repo, bound to Overleaf
    ├── .git\                    # remote: https://git.overleaf.com/<project-id>
    ├── cv.tex                   # → Yuzheng_CV.pdf (canonical)
    ├── resume.tex               # variant
    ├── 2page_cv.tex             # variant
    ├── macro.tex
    ├── hf-logo.png, hf-logo-pirate.png
    ├── .gitignore               # excludes build artifacts
    ├── .latexmkrc               # build settings (engine, output dir)
    └── publish.cmd              # builds cv.tex, copies PDF to website assets
```

The two repos stay independent. Website repo only sees the final PDF.

## Sync flow

- Overleaf web edit → `git pull` locally → file is updated.
- Local edit → `git push` → Overleaf web is updated.
- Single source of truth: the Overleaf-bound git repo.

## Build flow

- VS Code + LaTeX Workshop extension watches saves, runs `latexmk`, live-reloads PDF in editor.
- `publish.cmd` is a separate manual step — runs `latexmk cv.tex` and copies `cv.pdf` to `..\Mirnegg.github.io\assets\Yuzheng_CV.pdf`. Editing churn doesn't pollute the website repo; user invokes publish only when ready to update the live link.

## Open items

- Overleaf project's git URL (user to provide).
- Reconciliation: zip vs cloned content. Diff after clone; if identical, drop zip; otherwise user picks canonical.
- LaTeX engine: confirm from `cv.tex` preamble (likely pdflatex; could be xelatex if it uses fontspec).
- Website link: `index.html:67` currently has the CV PDF link commented out — uncomment after first publish.
