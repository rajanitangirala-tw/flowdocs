# FlowDocs — FlowSync API Documentation

**Live Site:** [flowdocs.github.io](https://flowdocs.github.io) *(replace with your GitHub Pages URL)*
**Owner:** Rajani Tangirala — Content Experience Lead
**Last Updated:** July 2026

---

## About This Project

FlowDocs is the official documentation site for the **FlowSync API** — a workflow
automation platform for enterprise SaaS teams. This repository contains all
developer-facing and user-facing documentation, written in Markdown and published
via GitHub Pages.

---

## My AI-Assisted Documentation Workflow

This project demonstrates a real-world AI-assisted documentation pipeline. Here
is exactly how I use AI tools at every stage:

### Stage 1 — Setup and Configuration
I created a `CLAUDE.md` file and a `.cursorrules` file in the repository root.
These files brief Claude Code and Cursor on our documentation standards —
terminology rules, writing style, folder structure, and what to flag for manual
review. Every AI interaction in this project automatically follows these standards
without me re-explaining them each session.

### Stage 2 — First Draft Generation
For each documentation article, I use **Claude** (claude.ai) with a structured
prompt that provides:
- The engineering spec or API endpoint definition as input
- A request for a specific output format (getting started guide, API reference, etc.)
- A reference to our style standards

**Example prompt I used for the Authentication guide:**
> "I am a technical writer documenting the FlowSync API. Here is the
> authentication endpoint spec: [spec pasted]. Please draft a getting started
> guide covering API key generation, request authentication, and common errors.
> Follow these standards: second person, active voice, present tense, numbered
> steps with a result statement at the end."

Claude produced a first draft in under two minutes. I then moved to Stage 3.

### Stage 3 — Review and Validation in Cursor
I opened the draft in **Cursor** alongside the existing documentation files.
Using Cursor's AI chat (Command+L), I asked:
> "Does this new content conflict with anything already in the repository?
> Is the terminology consistent with the rest of the docs?"

Cursor checked across all files and flagged two terminology inconsistencies
(using "token" instead of "API key" in two places). I corrected these before
publishing.

### Stage 4 — Manual Review Checklist
Before publishing, I ran through my five-layer review:
1. **Technical accuracy** — walked through every step in a test environment
2. **Consistency** — verified all terminology against CLAUDE.md
3. **Structure** — confirmed every procedure had a result statement
4. **AI risk check** — verified all specific values and tested all code examples
5. **Read aloud** — read the full article aloud to catch awkward phrasing

### Stage 5 — Publishing
Committed to GitHub. GitHub Actions automatically builds and publishes to
GitHub Pages. The documentation is live within 2 minutes of commit.

---

## Repository Structure

```
flowdocs/
├── CLAUDE.md               # Claude Code project standards (AI briefing file)
├── .cursorrules            # Cursor AI configuration
├── README.md               # This file — workflow documentation
├── index.md                # Homepage
├── getting-started/
│   ├── quickstart.md       # 5-minute quickstart guide
│   ├── authentication.md   # API key setup and authentication
│   └── first-workflow.md   # Creating your first workflow
├── api-reference/
│   ├── overview.md         # API overview and base URL
│   ├── workflows.md        # Workflows endpoint documentation
│   ├── triggers.md         # Triggers endpoint documentation
│   └── errors.md           # Error codes reference
├── release-notes/
│   ├── v2.1.0.md           # Latest release
│   └── v2.0.0.md           # Previous release
└── docs/
    └── best-practices.md   # Documentation best practices guide
```

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Claude (claude.ai) | First draft generation, style auditing, release note drafting |
| Cursor | Code-aware editing, cross-file consistency checking, agent-mode bulk updates |
| Claude Code | Autonomous repo-level tasks, finding documentation gaps |
| GitHub | Version control and collaboration |
| GitHub Pages | Free documentation hosting |

---

## What This Project Demonstrates

- **AI-assisted documentation workflow** from engineering input to published article
- **CLAUDE.md and .cursorrules configuration** for consistent AI behavior across a team
- **Five-layer review process** that catches what AI misses
- **Doc-as-Code practices** using Git, Markdown, and automated publishing
- **API documentation** including endpoints, parameters, request/response examples
- **Release notes** generated from engineering change summaries

---

*This project was built as a portfolio demonstration of AI-assisted technical
documentation practices. The FlowSync API is fictional and used for demonstration
purposes only.*
