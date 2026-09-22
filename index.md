---
title: Home
---

# Engineering Docs POC

This site is itself the proof of concept: it's a folder of Markdown files in a
git repo, published for free with GitHub Pages, no build step required
beyond what GitHub does automatically.

It exists to answer one question — **where should we store Architecture
Decision Records (ADRs) and engineering standards: a GitHub repo + Pages, or
Confluence?** — and the answer is written up as the ADR below, using the same
mechanism it's arguing for.

## Sections

- **[Architecture Decision Records](adr/)** — one ADR so far, comparing
  this approach against Confluence.
- **[Engineering Standards](standards/)** — placeholder.
- **[Language-Specific Recommendations](language-recommendations/)** — placeholder.
- **[CI/CD Framework](cicd/)** — placeholder.

Use the navigation panel on the left to jump between sections.

## Why this POC

- **No plugins, no server, no license.** Push Markdown to `main`, GitHub
  builds and serves it.
- **Same repo, same review process** as the code the decisions are about —
  an ADR can be proposed, reviewed, and merged via a normal pull request.
- **Full version history for free** — `git log` / `git blame` on any
  standard or decision, down to the line.
