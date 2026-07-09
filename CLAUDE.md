# Project: FlowDocs — Workflow Automation API Documentation
# Owner: Rajani Tangirala — Content Experience Lead
# Last updated: July 2026

## About This Project
FlowDocs is the official documentation site for the FlowSync API — a fictional
workflow automation platform used by enterprise SaaS teams. Documentation is
written in Markdown, managed through GitHub, and published via GitHub Pages.

## My Role
I am the Content Experience Lead responsible for all developer and user-facing
documentation. I use AI-assisted workflows to draft, review, and publish content
efficiently while maintaining accuracy and quality standards.

## Writing Standards — Follow These Always
- Use second person: say "you" not "the user" or "the developer"
- Use active voice: say "click Save" not "Save should be clicked"
- Use present tense: say "the API returns" not "the API will return"
- Use sentence case for all headings: "Setting up your account" not "Setting Up Your Account"
- Keep sentences under 20 words wherever possible
- Use numbered lists for procedures, bullet lists for options or features
- Every procedure must end with a result statement telling the user what they should see
- Never use "simple," "easy," "just," or "simply" — it is condescending

## Terminology — Use These Exact Terms
- Say "workflow" not "flow" or "pipeline"
- Say "trigger" not "event" or "hook"
- Say "step" not "action" or "task" within a workflow
- Say "API key" not "token" or "credential" (unless referring to OAuth tokens specifically)
- Say "workspace" not "organization," "tenant," or "account"
- Say "endpoint" not "route" or "URL"
- Say "request" and "response" not "call" and "result"
- The product name is always "FlowSync" with capital F and S — never "flowsync" or "Flowsync"

## Terminology — Never Use These
- Do not say "click on" — say "click"
- Do not say "in order to" — say "to"
- Do not say "utilize" or "leverage" — say "use"
- Do not say "please" in instructions
- Do not say "Note that" — say "Note:" followed by the note
- Do not use passive voice in procedures

## Folder Structure
- /getting-started — onboarding guides for new users and developers
- /api-reference — API endpoint documentation
- /release-notes — release notes by version
- /docs — general product documentation and guides

## Output Format
- All documentation is written in Markdown (.md files)
- Headings: use ## for H2 and ### for H3 — never use H1 inside articles (H1 is the page title only)
- Code samples: use triple backtick fences with language specified (```json, ```bash, etc.)
- API parameters: always use a table with columns: Parameter, Type, Required, Description
- Never generate screenshots — reference UI elements by their exact label in bold: **Save**

## What I Need From You
- Always check if content is consistent with existing files before suggesting updates
- Always match the tone and structure of the surrounding content in any file you edit
- When editing a file, tell me exactly what you changed and why
- If you are unsure about a technical detail, flag it with [VERIFY] for me to check
- Never invent API behavior — flag any gap with [NEEDS ENGINEERING INPUT]
- Always validate that step numbers are sequential and no steps are missing
