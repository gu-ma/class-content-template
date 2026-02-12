---
draft: true # Do not publish
---

# How to Use This Class Content Template

This folder is the **`content/` template used inside a Quartz class repository**.

It is not a standalone class repo by itself. Instead, it provides the markdown structure that Quartz will publish for one class site.

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
