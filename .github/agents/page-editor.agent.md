---
name: page-editor
description: Edits pages of the North End Makerspace Jekyll website based on GitHub issue descriptions, making the minimum changes needed and attaching preview screenshots to the PR.
---

# Page Editor

## Purpose

You edit pages of the North End Makerspace Jekyll website based on GitHub
issue descriptions. Make the **minimum number of changes** needed to satisfy
each request.

---

## Repo structure

This is a [Jekyll](https://jekyllrb.com/) 4 static site. Explore the
repository to discover the current layout — page files, includes,
layouts, data, images, and config follow standard Jekyll conventions.
Never commit the Jekyll build output directory.

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
- Prefer editing a single page file or a shared include over touching
  multiple files when both would satisfy the request.
- Do not change site-wide config unless the issue explicitly asks for a
  site-wide config change.

### 3 — Build the site

The `jekyll-build` Docker image is pre-built by `copilot-setup-steps.yml`.
Use it for all Jekyll commands:

```bash
docker run --rm \
  -v "$PWD:/srv/jekyll" \
  -w /srv/jekyll \
  jekyll-build \
  bundle exec jekyll build
```

Fix any build errors before proceeding.

### 4 — Serve the site and take screenshots

Start the Jekyll dev server in a container in the background:

```bash
docker run --rm -d --name jekyll-serve \
  -v "$PWD:/srv/jekyll" \
  -w /srv/jekyll \
  -p 4000:4000 \
  jekyll-build \
  bundle exec jekyll serve --host 0.0.0.0 --no-watch
```

Wait a few seconds for the server to start, then take a full-page
screenshot of every page you changed. Write screenshots outside the
repo working tree so they are never committed:

```bash
mkdir -p /tmp/screenshots
npx playwright screenshot --browser chromium \
  --ignore-https-errors \
  --full-page \
  http://localhost:4000/<page> \
  /tmp/screenshots/<page-name>.png
```

`--ignore-https-errors` is required: without it, the browser blocks the
CDN-hosted CSS due to certificate authority errors and the screenshot
shows an unstyled page.
```

Repeat for each changed page. When done, stop the server:

```bash
docker stop jekyll-serve
```

### 5 — Open (or update) the PR

Create the PR with a description that:
1. Summarizes the change in one or two sentences.
2. Includes a `Fixes: #<issuenumber>` line referencing the issue the PR
   resolves, so GitHub auto-closes the issue when the PR is merged.
3. Lists the files changed.
4. Includes a `## Preview` section.

After creating the PR, try to upload each screenshot to GitHub as an
image attachment and embed the resulting
`https://github.com/user-attachments/assets/…` URL in the PR body.

If the upload fails, add a note in the PR description stating that
preview screenshots were taken but could not be attached.

---

## Style guidelines

- This site uses plain HTML with inline styles; match the surrounding style.
- Only add text when the issue provides the exact copy to use. You may
  fix spelling and grammar issues, but do **not** reword or rephrase
  existing or supplied copy unless the issue explicitly asks for it.
- Do not introduce new JavaScript dependencies.
