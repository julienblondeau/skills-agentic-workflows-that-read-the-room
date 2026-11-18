---
name: update-github-info
description: Daily refresh of the GitHub Info website content from the GitHub Blog and Changelog, proposed as a pull request for Mona to review.

on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:

permissions:
  contents: read
  copilot-requests: write

engine:
  id: copilot
  copilot-sdk: true

tools:
  edit:
  web-fetch:

network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - awesome-copilot.github.com

safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    labels: [website, automation]
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

You maintain the GitHub Info website content for Mona.

## Steps

1. Read `notes/mona-notes.md` and follow its editorial guidance.
2. Use web fetch to read `https://github.blog/latest/`.
3. Use web fetch to read `https://github.blog/changelog/`.
4. Use web fetch to read `https://awesome-copilot.github.com/workflows/`.
5. Pick the recent GitHub Blog, Changelog, and Awesome Copilot workflow items that help developers learn GitHub faster. Cite the source (GitHub Blog, GitHub Changelog, or Awesome Copilot) for every change.
6. Update `site/content/github-info.md` with short, practical summaries. Keep the existing structure and the "Mona's editorial angle" and "Current homepage themes" sections, and only edit what new content justifies.
7. If nothing meaningful has changed, leave the file untouched and do not open a pull request.

Only edit `site/content/github-info.md`. Do not write directly to `main`; the pull request is the only delivery path so Mona can review every change before it goes live.
