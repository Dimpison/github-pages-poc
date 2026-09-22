# GitHub Pages POC — ADRs & engineering standards

A minimal proof of concept: a single ADR, stored as Markdown in this folder,
published as a static site by GitHub Pages. The ADR itself compares this
approach against Confluence for storing ADRs and engineering standards —
see [`adr/0001-platform-for-adrs-and-standards.md`](adr/0001-platform-for-adrs-and-standards.md).

## Layout

```text
github-pages-poc/
├── _config.yml   # Jekyll config (theme, title) — GitHub Pages builds this automatically
├── index.md      # homepage, links to the ADR(s)
├── adr/
│   └── 0001-platform-for-adrs-and-standards.md
└── README.md     # this file (not part of the published site)
```

No build tooling, Gemfile, or npm install is required — this uses only
[themes GitHub Pages supports out of the box](https://pages.github.com/themes/),
so GitHub builds and serves it directly on push.

## Running it as a real GitHub Pages site

1. Push this repo to GitHub.
2. In **Settings → Pages**, set the source to the branch this folder is on,
   with `/github-pages-poc` as the folder (or move this folder's contents to
   repo root / a dedicated repo if you want the whole repo to be the site).
3. GitHub will build and publish at
   `https://<org>.github.io/<repo>/` (or `/github-pages-poc/` if serving a
   subfolder) within a minute or two of the push.

## Previewing locally (optional)

Requires Ruby + Bundler:

```bash
cd github-pages-poc
bundle exec jekyll serve
```
