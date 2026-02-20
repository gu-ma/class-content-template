---
draft: true # Do not publish
---

# How to Use This Class Content Template

This folder is the **`content/` template used inside a Quartz class repository**.

It is not a standalone class repo by itself. Instead, it provides the markdown structure that Quartz will publish for one class site.

> [!WARNING]
> This template auto-generates `README.md` from `index.md` on push (via GitHub Actions).
> The workflow may create one extra bot commit after your push.
> Before your next push, run `git pull` to avoid non-fast-forward errors.

## README Sync Workflow (GitHub + Quartz)

This template uses a GitHub Actions workflow to keep `README.md` synchronized from `index.md`.

- `index.md` is the source of truth for content.
- On push, the workflow copies `index.md` to `README.md`.
- Frontmatter is removed from `README.md` so GitHub displays it cleanly.
- The workflow commits this update automatically with `github-actions[bot]`.

### What this means for your Git routine

After you push your changes, the workflow may create one additional commit.
Before your next push, run:

```bash
git pull
```

This avoids "branch is behind" / non-fast-forward errors.

## Intended Architecture

- **Blocks (`block-*`)**: markdown-only repositories (reusable learning units)
- **Slides (`slides-*`)**: Slidev-only repositories (independent deployment)
- **Classes (`class-*`)**: Quartz repositories that compose blocks via submodules

Dependency flow:

`Blocks → Classes` (technical)  
`Blocks → Slides` (conceptual only)

No circular dependencies.

## `content/` Structure

- **index.md**: Class landing page
- **syllabus.md**: Class syllabus and roadmap
- **blocks/**: Block repositories added as git submodules
- **class-notes/**: Instructor/session notes specific to this class

Example inside a Quartz class repo:

```text
class-name/
├── quartz.config.ts
├── package.json
└── content/
    ├── index.md
    ├── syllabus.md
    ├── blocks/
    │   ├── block-ai-intro/      (submodule)
    │   ├── block-ml-basics/     (submodule)
    │   └── block-ethics/        (submodule)
    └── class-notes/
        └── session1.md
```

## Adding Block Submodules

From the **class repo root** ( inside `content/`), add each block like this:

```bash
git submodule add <repo-url> blocks/block-ai-intro
```

Repeat for each required block.

## Slides Integration

Slides live in separate `slides-*` repositories and deploy independently.

- Do **not** embed Slidev sources in this class template.
- Link slides from markdown using their deployed URL, for example:

```md
[Presentation](https://subdomain.yourdomain.com/slides-ai-intro/)
```

## Publishing Conventions

Typical runtime URLs:

- `subdomain.yourdomain.com/class-*`
- `subdomain.yourdomain.com/slides-*`

One DNS entry can serve both class and slide sites under different paths.

---

Keep this `content/` folder focused on class composition and notes.
Keep blocks and slides in their own repositories for long-term reuse and low maintenance.
