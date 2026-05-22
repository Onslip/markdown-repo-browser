# Markdown Repo Browser

*Browse, search and view Markdown files locally — serverless &amp; buildless!*

**Live demo:** <https://onslip.github.io/markdown-repo-browser/>

A single self-contained HTML file that turns any folder of Markdown files
into a navigable, searchable mini-site. No build step, no server, no
dependencies to install. Works from `file://`, any static web host, or as a
drop-in front page for a documentation repo.

## What it does

- Renders `.md` / `.mdx` files with syntax highlighting, tables, task
  lists, footnotes and an auto-generated table of contents.
- Sidebar file tree, breadcrumbs and full-text search across the repo.
- Honours `.gitignore` so build outputs and `node_modules` stay out of
  view.
- Light/dark theme that follows the system preference.

## Adding it to a folder of Markdown files

The browser opens `index.md` from the folder root by default, so put your
landing content there (or link to other files from it).

1. Drop [`markdown-repo-browser.html`](markdown-repo-browser.html) into
   the root of your folder (next to your `index.md`). You can rename it
   to `index.html` if you want it to be served as the default page.
2. Open it — either by double-clicking the file (`file://`) or by serving
   the folder over HTTP (e.g. `python3 -m http.server`).
3. From `file://`, click **Open local directory…** and pick the folder.
   Over HTTP, files are fetched directly from the server.

If you'd rather not vendor the file at all, create a tiny `index.html`
in your folder that always loads the latest published version from
GitHub:

```html
<script>
  fetch('https://raw.githubusercontent.com/Onslip/markdown-repo-browser/refs/heads/main/markdown-repo-browser.html')
    .then(r => r.text())
    .then(d => document.write(d));
</script>
```

Serve that `index.html` and the browser will pull in the current
`markdown-repo-browser.html` on every load.

## Adding a search index

Search works automatically when you open a local directory. For
`http://` / `https://` hosting, generate a static index so search works
without prompting the user for local-folder access:

1. Open `markdown-repo-browser.html` locally and pick your folder.
2. Wait for indexing to finish (progress is shown in the sidebar).
3. Click the **⬇ download** icon next to the search bar to save
   `index.json`.
4. Place `index.json` next to your root `index.md`. It is picked up
   automatically on load.

Regenerate `index.json` whenever your content changes.
