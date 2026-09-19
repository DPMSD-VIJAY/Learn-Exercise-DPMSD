---
name: update-github-info
description: Draft website updates for Mona's GitHub Info site from official GitHub sources.
model: gpt-4.1
on:
  workflow_dispatch:
  schedule:
    - cron: '17 9 * * *'
permissions:
  contents: read
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    fallback-as-issue: false
    allowed-files:
      - site/content/github-info.md
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.com
    - github.blog
---

# Update Mona's GitHub Info website

Read `notes/mona-notes.md` before making changes. Use it as the editorial
and review guidance for this task.

Review these official sources with web fetch:

- GitHub Blog: https://github.blog/latest/
- GitHub Changelog: https://github.blog/changelog/

Identify recent updates that are relevant to Mona's GitHub Info website. Prefer
updates that help developers learn GitHub faster and have clear support from the
source material. Review the existing content in `site/content/github-info.md`
before editing it.

When relevant, update only `site/content/github-info.md` with concise,
practical content. Preserve the existing editorial style, avoid duplicating
existing entries, and mention whether each update came from the GitHub Blog or
GitHub Changelog. Include links to the source pages when available.

After making a meaningful update, use the configured `safe-outputs` with
`create-pull-request` to open a draft pull request for Mona to review. The pull
request title must mention Mona or GitHub Info. Its body must include a clear
summary of:

- The GitHub Blog and GitHub Changelog pages reviewed.
- The specific updates selected and why they are relevant.
- The website changes proposed in `site/content/github-info.md`.

Do not write directly to `main`, and do not use git or GitHub CLI commands to
create the pull request. If the sources contain no relevant, sufficiently
supported update, make no file changes and use `noop` with a short explanation.
