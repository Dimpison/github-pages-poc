---
title: "ADR-0001: Platform for storing ADRs and engineering standards"
---

# ADR-0001: Platform for storing ADRs and engineering standards

- **Status:** Proposed
- **Date:** 2026-09-22
- **Deciders:** Engineering leadership

## Context

We currently have no single, agreed place to record Architecture Decision
Records (ADRs) or engineering standards (coding conventions, review
checklists, definitions of done, etc.). Two candidate platforms are on the
table:

1. **A GitHub repository, published as a static site with GitHub Pages**
   (this POC).
2. **Confluence**, our existing wiki tool used for other team documentation.

Both need to satisfy the same two use cases: (a) recording ADRs, which are
short, dated, rarely-edited-after-merge decision records, and (b) hosting
engineering standards, which are longer-lived documents that get revised
gradually over time and need to be easy to browse and search.

## Decision drivers

- **Review workflow** — decisions should go through the same scrutiny as
  code changes (pull request, diff, approval).
- **Version history** — ability to see exactly what changed, when, and why,
  down to a single line.
- **Proximity to code** — engineers should be able to find and update
  standards without leaving their normal dev workflow.
- **Editing experience** — non-technical stakeholders should still be able
  to read comfortably; ideally also comment.
- **Cost and lock-in** — licensing cost and how hard it is to migrate away
  later.
- **Discoverability / search** — how easily people can find the right
  document.

## Options considered

### Option A — GitHub repo + GitHub Pages

Markdown files in a git repo, auto-published as a static site by GitHub
Pages (as demonstrated by this POC).

**Pros**

- Free, no separate license or hosting cost.
- Changes go through pull requests: diffs, required reviewers, CI checks
  (e.g. a linter or link checker) all apply for free.
- Full git history — `git log`/`git blame` per file, per line.
- Lives next to the code; one less tool/context switch for engineers.
- Plain Markdown is portable — trivial to migrate to any other renderer
  later.
- Static output is fast and trivially cacheable.

**Cons**

- Editing requires git/Markdown familiarity — a real barrier for
  non-engineering stakeholders (PMs, support, leadership).
- No in-place comments or inline discussion on the *rendered* page (only on
  the PR diff, before merge).
- Weaker full-text search than a dedicated wiki out of the box.
- No fine-grained page-level permissions — access is repo-level.

### Option B — Confluence

Our existing team wiki, using its native page hierarchy and (optionally) a
decision-record template/macro.

**Pros**

- WYSIWYG editing — approachable for every stakeholder, technical or not.
- Built-in full-text search across all spaces.
- Inline comments, page watching, and notifications out of the box.
- Fine-grained space/page permissions.
- Already adopted org-wide — no new tool to introduce.

**Cons**

- No real review gate — edits publish immediately; "approval" workflows are
  bolted-on and easy to skip.
- Version history exists but diffing is coarser (whole-page, not line-level)
  and not tied to the standard PR review habit engineers already have.
- Separate from the codebase — another tab, another login context.
- Ongoing per-seat licensing cost.
- Harder to migrate out of later (proprietary export format, macros don't
  travel).

## Comparison

| Driver | GitHub repo + Pages | Confluence |
|---|---|---|
| Review workflow | Pull request, required reviewers, CI | Ad hoc, immediate publish |
| Version history | Full git history, line-level diff | Page-level version history |
| Proximity to code | Same repo | Separate tool |
| Editing experience (non-eng) | Markdown/git required | WYSIWYG, low barrier |
| Inline discussion on published page | No (PR-time only) | Yes |
| Search | Basic (GitHub/site search) | Strong, built-in |
| Permissions | Repo-level | Page/space-level |
| Cost | Free | Per-seat license |
| Portability / exit cost | High (plain Markdown) | Low (proprietary export) |

## Decision

Adopt **Option A — GitHub repository published with GitHub Pages** for both
ADRs and engineering standards.

The deciding factors are the review workflow and version history: ADRs and
standards are exactly the kind of document that benefits from being
proposed, diffed, and approved the same way a code change is, and from a
permanent, line-level history of *why* something changed. Both are native
to a git repo and only loosely bolted on to Confluence.

To offset the editing-experience con, standards pages will keep prose short
and reviewed content will be linked from wherever non-technical stakeholders
already look (e.g. a pinned link from the relevant Confluence space), rather
than duplicating the content there.

## Consequences

- New ADRs and standards are proposed as pull requests against this repo and
  require at least one approval before merging.
- The published site (this POC) becomes the canonical, linkable source; any
  existing Confluence pages covering the same content should be marked
  deprecated and link here instead.
- We accept weaker full-text search and no non-technical WYSIWYG editing as
  a trade-off; if this becomes a recurring blocker, revisit this decision.
