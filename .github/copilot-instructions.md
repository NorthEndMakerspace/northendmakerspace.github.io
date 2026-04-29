# Copilot Agent Instructions

## Purpose

This agent edits pages of the North End Makerspace Jekyll website based on
GitHub issue descriptions. The agent should make the **minimum number of
changes** needed to satisfy each request.

---

## Repo structure

This is a [Jekyll](https://jekyllrb.com/) 4 static site. Key facts:

- Page files are in the repository root (e.g. `index.html`, `about.html`,
  `visit.html`, `join.html`, `pricing.html`, `conduct.html`, `donate.html`,
  `events.html`, `community.html`, `volunteer.html`, etc.).
- Shared HTML snippets live in `_includes/`.
- Page layouts live in `_layouts/`.
- Site-wide config is `_config.yml`.
- Images live in `images/` (excluded from the Jekyll build; served from the
  root).
- `_data/` holds structured data (YAML/JSON).
- The build output goes to `_site/` (never commit this directory).

---

## Workflow for every page-edit task

### 1 — Understand the request

Read the issue title and body carefully. Identify:
- Which page(s) need to change.
- Exactly what text, link, image, or structure should be added, removed, or
  updated.
- Any constraints or style requirements mentioned in the issue.

### 2 — Make the minimum required edits

- Edit only the files that must change. Do **not** reformat, re-indent, or
  clean up code in sections you are not changing.
- Prefer editing a single page file or a shared `_includes/` snippet over
  touching multiple files when both would satisfy the request.
- Do not change `_config.yml` unless the issue explicitly asks for a
  site-wide config change.

### 3 — Build the site

```bash
bundle exec jekyll build
```

Fix any build errors before proceeding.

### 4 — Serve the site and take screenshots

Start the Jekyll dev server in the background:

```bash
bundle exec jekyll serve --no-watch --detach
```

Wait a moment for the server to start, then take a full-page screenshot of
every page you changed (replace `<page>` with the actual path, e.g. `/`,
`/about/`, `/join/`, etc.):

```bash
npx playwright screenshot --browser chromium \
  --full-page \
  http://localhost:4000/<page> \
  screenshots/<page-name>.png
```

Repeat for each changed page.

If `--detach` is unavailable, run the server and screenshots in a subshell:

```bash
bundle exec jekyll serve --no-watch &
SERVER_PID=$!
sleep 5
npx playwright screenshot --browser chromium --full-page \
  http://localhost:4000/ screenshots/index.png
kill $SERVER_PID
```

### 5 — Commit the screenshots

```bash
git add screenshots/
git commit -m "chore: add preview screenshots"
```

### 6 — Open (or update) the PR

Create the PR with a description that:
1. Summarizes the change in one or two sentences.
2. Lists the files changed.
3. Embeds the screenshots using their raw GitHub URL:

```markdown
## Preview

![<page-name>](https://raw.githubusercontent.com/NorthEndMakerspace/northendmakerspace.github.io/<branch>/screenshots/<page-name>.png)
```

You can obtain the current branch name with:

```bash
git rev-parse --abbrev-ref HEAD
```

---

## Style guidelines

- This site uses plain HTML with inline styles; match the surrounding style.
- Keep copy concise and friendly; match the tone of the existing page text.
- Do not introduce new JavaScript dependencies.
