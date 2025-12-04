# Copilot Instructions for Melodia Documentation

## Project Overview

This is a **MkDocs documentation site** for Melodia, a music streaming platform built as a FIUBA university project (Software Engineering 2). The documentation serves as a project log ("Bitácora") covering architecture, decisions, learnings, and known issues.

**Live site**: https://melodia-fiuba.github.io/docs/

## Repository Structure

```
docs/                    # MkDocs content directory
├── index.md             # Homepage with system overview
├── architecture.md      # GCP infrastructure, service communication
├── roadmap.md           # Checkpoint progress and retrospectives
├── decisions-and-learnings.md  # ADRs (Architecture Decision Records)
├── api-contracts.md     # OpenAPI specs (embed via swagger-ui tag)
├── known-issues.md      # Bugs and incomplete features
├── services/            # Per-service documentation
│   └── {service}.md     # Tech stack, architecture, endpoints
├── assets/diagrams/     # Images (draw.io exports, diagrams)
└── openapi/             # OpenAPI YAML specs for embedding
```

## Related Repositories (same GitHub org: Melodia-FIUBA)

| Service          | Tech Stack   | Repo                           |
| ---------------- | ------------ | ------------------------------ |
| mobile-app       | React Native | Melodia-FIUBA/mobile-app       |
| admin-backoffice | Next.js      | Melodia-FIUBA/admin-backoffice |
| songs-service    | Python/Flask | Melodia-FIUBA/songs-service    |
| users-service    | Go           | Melodia-FIUBA/users-service    |
| admin-service    | Go           | Melodia-FIUBA/admin-service    |

## Development Workflow

```bash
# Install dependencies
pip install -r requirements.txt

# Local preview (http://localhost:8000)
mkdocs serve

# Build static site (outputs to site/)
mkdocs build
```

**Deployment**: Automatic via GitHub Actions on push to `main` (see `.github/workflows/deploy-docs.yml`).

## Writing Conventions

- **Language**: Spanish for content, English for code/technical terms
- **Markdown extensions enabled**: admonitions (`!!! note`), Mermaid diagrams, tabs, emoji, tables
- **Diagrams**: Use Mermaid for inline diagrams; draw.io for complex architecture (export PNG to `assets/diagrams/`)
- **TODOs**: Use `<!-- TODO: description -->` comments for incomplete sections
- **OpenAPI embedding**: Place YAML files in `docs/openapi/`, embed with ` ```swagger-ui ` fence

## Content Guidelines

This documentation must cover (per course requirements):

1. Architecture diagrams
2. Architecture decisions with rationale (why these microservices, why these technologies)
3. Incomplete features and known issues for final delivery
4. Problems encountered and lessons learned
5. Optional: Feature demos worth highlighting

When updating content:

- Keep checkpoint retrospectives honest (what went well, what to improve)
- Document decisions in ADR format: Context → Decision → Justification → Consequences
- Update `mkdocs.yml` nav section when adding new pages

## AI Agent Guidelines

- **Ask questions** if context is unclear or information seems missing—this documentation is evolving
- Before adding new pages, check if content fits in an existing page
- Preserve `<!-- TODO -->` markers unless filling them with actual content
- When documenting services, cross-reference the actual service repo for accurate details
- Use admonitions for important notes: `!!! info`, `!!! warning`, `!!! tip`
