# iXMaps Documentation — Quarto Project

Quarto-based documentation for the iXMaps JavaScript framework.

## Prerequisites

- [Quarto](https://quarto.org/docs/get-started/) ≥ 1.4

Verify: `quarto --version`

## Project structure

```
ixmaps/
├── _quarto.yml              # Site config, navigation, sidebar
├── index.qmd                # Overview / home page
├── getting_started.qmd      # Quick start with correct flat API
├── api_documentation.qmd    # Complete API reference
├── theme_styles.qmd         # .style() property reference
├── map_types.qmd            # Basemaps, visualization types, colors
├── chart_scaling.qmd        # Sizing mechanisms
├── user_charts.qmd          # Custom D3 chart functions
├── examples.qmd             # Copy-paste examples
├── troubleshooting.qmd      # Silent failures and common issues
├── about.qmd                # Project info
├── styles.css               # Custom CSS
├── pics/                    # Images
├── docs/                    # Generated output (quarto render)
└── .github/workflows/
    └── publish.yml          # GitHub Actions CI/CD
```

## Local development

```bash
# Live preview with auto-reload:
quarto preview

# Full render to docs/:
quarto render
```

## GitHub Pages deployment

The `.github/workflows/publish.yml` workflow renders the site on every push to `main`/`master` and deploys it to the `gh-pages` branch.

### First-time setup

1. Create a new GitHub repository (e.g. `ixmaps-docs`)
2. In the repository **Settings → Pages**, set source to **Deploy from a branch → `gh-pages` → `/ (root)`**
3. Push this project:
   ```bash
   git init
   git add .
   git commit -m "Initial iXMaps documentation"
   git remote add origin https://github.com/<your-user>/ixmaps-docs.git
   git push -u origin main
   ```
4. The workflow runs automatically; the site is live at `https://<your-user>.github.io/ixmaps-docs/`

### Alternative: deploy from `docs/` on `main`

If you prefer not to use GitHub Actions, commit the `docs/` folder and set GitHub Pages to serve from **`main` → `docs/`**:

```bash
quarto render
git add docs/
git commit -m "Render documentation"
git push
```

## Adding a new page

1. Create `new_topic.qmd`
2. Add to `render:` list in `_quarto.yml`
3. Add to `sidebar: contents:` in `_quarto.yml`

## License

CC-BY 4.0 — same as the iXMaps framework.
