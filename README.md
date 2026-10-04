# Enterprise Multi-Agent Code Review Orchestrator

Final project submission for the Udacity course **Agentic Engineering with the Claude
Agent SDK**.

This repository exists only to deliver the project archive. Everything the rubric
asks for is inside the zip file below.

## The deliverable

[`code-review-orchestrator-submission.zip`](code-review-orchestrator-submission.zip)
(204K)

SHA-256: `d104234a8745d05b60075be6d2d892275339e364de340730570c85b2205f3c23`

## What the project does

A TypeScript CLI that reviews a GitHub pull request with three specialised
subagents, coordinated by an orchestrator built on the Claude Agent SDK:

- **code-quality-analyzer** looks for security issues, bugs and maintainability problems
- **test-coverage-analyzer** finds untested paths and proposes concrete tests
- **refactoring-suggester** proposes refactorings with before and after code

The orchestrator fetches the pull request through the GitHub MCP server, lints
JavaScript and TypeScript files through the ESLint MCP server, delegates each file
to the three subagents with the `Task` tool, and validates the combined result
against a Zod schema. It then writes the report as JSON, Markdown and HTML.

## Inside the archive

```
DESIGN.md                 answers to the course's "Questions to Answer", phases 1-4
DEVIATIONS.md             where and why the implementation departs from the brief
README.md                 project overview
project/starter/
  src/                    orchestrator, subagents, prompts, MCP config, utilities
  tests/                  Vitest suite (122 tests)
  reports/                the nine required reports: three pull requests x JSON/MD/HTML
  .claude/skills/         the Claude Skills the subagents load
  logs/                   run logs showing both MCP servers in use and the subagent delegations
  .env.example            configuration template, with no real credentials
```

`node_modules/`, `dist/` and `.env` are left out on purpose.

## Running it

Requires Node.js 22 or later.

```bash
cd project/starter
npm ci
cp .env.example .env      # set ANTHROPIC_MODEL, PROJECT_ROOT and the credentials
npm test
npm start -- <owner> <repo> <pr-number>
```

The model comes only from the `ANTHROPIC_MODEL` environment variable. No model name
or credential is written into the source.

## A note on the test repository

The pull requests named in the course brief belong to a repository that no longer
exists. The analysis was run against a public copy that has the same three pull
requests. The report filenames keep the names the rubric expects, and each report
records the repository that was actually analysed. `DEVIATIONS.md` explains this in
full.
