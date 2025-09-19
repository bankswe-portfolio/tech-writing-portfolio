# Technical Writing Portfolio

👉 **[View the site](https://bankswe-portfolio.github.io/tech-writing-portfolio/)**

This project contains my portfolio of technical writing case studies. 
Each study focuses on a real scenario and demonstrates how I approach documentation—structuring information, addressing reader needs, and presenting technical details with care.

- 🗂 **Case Studies:** practical examples with real product contexts  
- 🧾 **Source:** Markdown under `/docs` using a docs-as-code workflow  
- ✍️ **Goal:** treat documentation with the same rigor as code and product  

## Local development
Preview the site locally:

    pip install mkdocs mkdocs-material pymdown-extensions
    mkdocs serve

## Deployment
Choose one method:

- One-off publish:  

      mkdocs gh-deploy --force

- Continuous deploy: push to `main` with GitHub Actions enabled
