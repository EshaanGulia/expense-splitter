# Technical Design

> Full system architecture: see [`ARCHITECTURE.md`](../ARCHITECTURE.md).

## Components

- **Static HTML Landing Page** — Smoke test for GitHub Pages deployment pipeline; validates end-to-end deployment from git commit to live URL
- **GitHub Repository** — Version control and source of truth for application code
- **GitHub Pages** — Static hosting and automatic deployment
- **Web Browser** — Render and display the HTML page to the user
- **React/Next.js Frontend (Phase 2+)** — Interactive user interface for expense management
- **Node.js Backend API (Phase 2+)** — Business logic; expense calculations; settlement algorithms
- **Database (Phase 2+)** — Persistent storage of groups, expenses, participants, users

## Technology Choices

- **Git + GitHub** — Industry standard for distributed version control; GitHub provides integrated hosting, issue tracking, and GitHub Pages; no additional configuration needed
- **GitHub Pages** — Free, automatic deployment from git push, no separate infrastructure setup, validates the deployment pipeline as a smoke test
- **HTML5** — Current standard for web pages; semantic elements (h1, p, meta) provide structure; utf-8 encoding support for Unicode characters like em-dash
- **UTF-8** — Web standard; supports Unicode characters (em-dash U+2014); ensures correct rendering across browsers and platforms
- **React or Next.js** — Component-based, modern, large ecosystem, strong community support; Next.js provides full-stack JavaScript and built-in optimization
- **Node.js + Express or Next.js API Routes** — Same language as frontend (JavaScript/TypeScript), reduces context switching, large ecosystem, suitable for MVP and scalable architectures
- **SQLite** — Zero-configuration, file-based, sufficient for single-user or small team development; no separate database server needed
- **PostgreSQL** — Robust, multi-user support, ACID transactions, rich features for complex queries, industry-standard for production web applications
- **npm (with Node.js)** — Default package manager for JavaScript/TypeScript; lock files ensure reproducible builds; large ecosystem of reusable libraries
- **TypeScript** — Type safety reduces runtime bugs, better IDE support, improved refactoring, easier to maintain large codebases

## Planned Changes

- `./index.html` (create) — Create a new static HTML5 file at the repository root with the following structure:
- DOCTYPE html declaration
- <html> root element
- <head> section containing:
  - <meta charset="UTF-8"> as the first meta tag
  - <title>Expense Splitter</title>
- <body> section containing:
  - Exactly one <h1> tag with text 'Expense Splitter — Coming Soon' (with em-dash U+2014)
  - Exactly one <p> tag with text 'Coming soon. Check back later.'
- No external stylesheets, scripts, images, or other assets
- File must be saved with UTF-8 encoding
- Minimal HTML5 boilerplate; no CSS or JavaScript
- `.git/objects (internal)` (implicit) — Git commit and push workflow:
1. Stage the file: git add index.html
2. Create commit: git commit -m 'Add index.html smoke test for GitHub Pages deployment'
3. Push to main: git push origin main
4. Verify commit appears in git log --oneline main
