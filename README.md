# GitHub Pages POC — ADRs & engineering standards

A minimal proof of concept: Markdown files in this folder, published as a
static site by GitHub Pages, with a left-hand navigation panel across
sections. The ADR compares this approach against Confluence for storing
ADRs and engineering standards — see
[`adr/0001-platform-for-adrs-and-standards.md`](adr/0001-platform-for-adrs-and-standards.md).

## Layout

```text
github-pages-poc/
├── _config.yml              # Jekyll config (title, default layout)
├── _data/nav.yml             # left-nav entries (title + url), rendered by the layout
├── _layouts/default.html     # page shell: sidebar nav + content area
├── assets/css/style.css      # sidebar + content styling
├── index.md                  # homepage
├── adr/                       # Architecture Decision Records
│   ├── index.md
│   └── 0001-platform-for-adrs-and-standards.md
├── standards/                 # Engineering standards (placeholder)
│   ├── index.md
│   └── 0001-placeholder.md
├── language-recommendations/  # Language-specific recommendations & agreements (placeholder)
│   ├── index.md
│   └── 0001-placeholder.md
├── cicd/                       # CI/CD framework documentation (placeholder)
│   ├── index.md
│   └── 0001-placeholder.md
└── README.md                  # this file (not part of the published site)
```

No plugins are used — only Jekyll's built-in `_layouts`, `_data`, and
`_includes` handling, all of which GitHub Pages builds automatically on
push, no Gemfile or npm install required.

To add a new nav entry, add a line to [`_data/nav.yml`](_data/nav.yml) and
create the matching directory with its own `index.md`.

## Running it as a real GitHub Pages site

1. Push this repo to GitHub.
2. GitHub Pages can only serve from the repo root or a `/docs` folder on a
   branch (or from any path via a GitHub Actions workflow). For this POC,
   either:
   - move this folder's contents to the repo root (or a repo of its own), or
   - add a `.github/workflows/pages.yml` that builds and deploys the
     `github-pages-poc/` folder specifically via `actions/deploy-pages`.
3. In **Settings → Pages**, point the source at whichever of the above you
   chose. GitHub will build and publish within a minute or two of the push.

## Previewing locally (optional)

Requires Ruby + Bundler:

```bash
cd github-pages-poc
bundle exec jekyll serve
```
