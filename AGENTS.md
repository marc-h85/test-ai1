# Agent Instructions for test-ai1

## What This Repo Is

Documentation-only repository for **Gastown Self-Hosted**, an agent orchestration platform. There is no application source code here—only AsciiDoc documentation and the Antora build pipeline used to publish it.

## Repository Layout

- `docs/` – All AsciiDoc content, Antora playbook, and navigation.
  - `antora-playbook.yml` – Antora site generator configuration.
  - `index.adoc` – Root documentation page.
  - `nav.adoc` – Navigation structure for the documentation site.
  - `_attributes.adoc` – Common AsciiDoc attributes (project name, version, links).
  - Additional `.adoc` files for specific topics (installation, LLM gateway, web UI).
- `build/site/` – Generated static site output (committed artifacts).
- `.github/workflows/docs-publish.yml` – CI/CD pipeline to build and deploy docs to GitHub Pages.

## Tech Stack

- **Documentation generator:** Antora 3.1.15
- **Markup:** AsciiDoc
- **CI/CD:** GitHub Actions + GitHub Pages + `antora/docker-antora` Docker image

## Development Commands

| Task | Command |
|------|---------|
| Build docs locally | `npx antora --fetch docs/antora-playbook.yml` |
| Build with stacktrace (CI flag) | `npx antora --stacktrace --fetch docs/antora-playbook.yml` |

- **Prerequisites:** Node.js with `antora` installed (it is in `node_modules/`).
- **Output directory:** `build/site/` (configured in `docs/antora-playbook.yml`).

## CI/CD & Deployment Flow

1. On every push to `main`, the GitHub Actions workflow (`.github/workflows/docs-publish.yml`) triggers.
2. The workflow uses the `antora/docker-antora` Docker image to build the site: `antora --stacktrace --fetch docs/antora-playbook.yml`.
3. The resulting `build/site` directory is uploaded as a GitHub Pages artifact and deployed.

## Conventions & Gotchas

- **Only edit files in `docs/`:** Changes outside this directory (except CI config) should be avoided.
- **Do not commit `build/site/` unless necessary:** The CI pipeline regenerates this on every push. Manual updates to `build/site` can be overwritten by CI.
- **AsciiDoc attributes:** Shared attributes (project name, version, URLs) are defined in `docs/_attributes.adoc`. Reference them in other docs when applicable rather than hardcoding values.
- **Start page:** The Antora start page is `gastown-self-hosted::index.adoc`.
