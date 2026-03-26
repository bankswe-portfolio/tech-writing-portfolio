# William Banks — Technical Writing Portfolio

**Live site:** https://bankswe-portfolio.github.io/tech-writing-portfolio/

Technical writing samples across how-to documentation, conceptual explainers,
editorial redlines, and analytical essays on documentation as a technical discipline.
Built with MkDocs Material and deployed via GitHub Actions.

---

## Contents

**Case Studies** — scenario-driven samples written against real tools and products,
each demonstrating a distinct documentation mode: task-oriented guidance, structural
redlining, and conceptual onboarding for developers.

**Articles & Essays** — analytical pieces on where technical writing intersects with
AI-assisted workflows, docs-as-code pipelines, and modern software delivery. Written
as original work, not as portfolio filler.

**Governance & AI Workflows** — a framework series on running disciplined LLM-assisted
research and knowledge work, derived from direct application on a live program.

---

## Stack

- **MkDocs Material** — theme and site generation
- **GitHub Actions** — automatic deployment to GitHub Pages on push to `main`
- **Markdown + PyMdown Extensions** — content authoring with admonitions, tabs,
  code blocks, and Mermaid diagrams

---

## Local development
```bash
pip install mkdocs mkdocs-material pymdown-extensions
mkdocs serve
```

The site is available at `http://localhost:8000` while the server is running.
Changes to `docs/` reload automatically.

## Deployment

Pushing to `main` triggers the GitHub Actions workflow and redeploys automatically.
For a manual one-off deploy:
```bash
mkdocs gh-deploy --force
```

---

## Contact

william.e.banks@icloud.com · [LinkedIn](https://www.linkedin.com/in/william-banks-7a736793/)
