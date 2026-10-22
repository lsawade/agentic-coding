# Starter kit: agentic coding for a research project

This folder is a starting point for using a coding agent (Claude Code, Codex, Cursor, Antigravity CLI, ...) on a research project. Copy the folder's contents into the root of your repository, fill in AGENTS.md with the facts about your project, and commit. You are the supervisor: the AI drafts, and you own the correctness of every result.

The kit has two layers:

- **Universal:** `AGENTS.md` and `prompts/`. Plain Markdown that any agent can follow. This is where the substance lives; edit these first.
- **Tool-specific:** adapters that wire the universal files into one tool's features (slash commands, subagents, permissions). The kit ships one, `.claude/`, for Claude Code. Adapters only point at the universal files, so you never have to keep two copies in sync.

## Setup

- AGENTS.md with layout, test command, conventions, and what not to touch
- git: commit early and often; use worktrees for parallel agent sessions
- permissions: run in a sandbox, allowlist read-only commands, never give the agent live database credentials

## Loop

- Plan first: brainstorm, run a feasibility check, then a plan session; use /grill-me on the foggy parts
- Small steps you can review; restart the session when it gets confused
- Review as a supervisor: read every line you would sign for, ask the agent to list its own problems, use a second model as adversary, and refactor under regression tests; consider a rewrite when the design warrants it

## Responsibility

- Disclose AI use per the project's or journal's policy (read CONTRIBUTING.md first)
- Mind the data: unpublished results, PII, IRB-covered, and export-controlled data never go into a hosted model; use local or open-weight models there
- Never let an agent open a PR you have not read
- Have the AI write the script that does the task, not do the task, so the result is reproducible

## What is in this folder

Universal (any agent):

- README.md: this checklist
- AGENTS.md: project instructions skeleton the agent reads at session start; also lists the prompts below
- prompts/grill-me.md: interrogates a plan until its foggy parts are explicit
- prompts/pr.md: prepares a pull request for human review
- prompts/test-runner.md: runs the test suite and reports only failures

Tool-specific (Claude Code adapter, delete if you do not use Claude Code):

- .claude/commands/grill-me.md: `/grill-me` slash command, runs prompts/grill-me.md
- .claude/commands/pr.md: `/pr` slash command, runs prompts/pr.md
- .claude/agents/test-runner.md: subagent on a small model (Haiku) that runs prompts/test-runner.md
- .claude/settings.json: permission allowlist of read-only commands, with secrets and destructive commands denied

## Using it with your tool

- **Any agent:** reads AGENTS.md. Ask in plain words ("grill me on this plan", "prepare a PR") and it follows the matching file in `prompts/`, or tell it the file directly.
- **Claude Code:** reads AGENTS.md (v2.1.277 or later) only when the repo has no CLAUDE.md or CLAUDE.local.md. If you already have a CLAUDE.md, or run an older version, put the line `@AGENTS.md` in a CLAUDE.md (create one if needed). The `.claude/` adapter gives you `/grill-me`, `/pr`, the test-runner subagent and the permission file.
- **Codex, Cursor, Antigravity CLI:** read AGENTS.md natively. To get slash commands or permissions there, write a small adapter in that tool's own folder that points at `prompts/`, the way `.claude/` does; permission settings are not portable and must be set per tool.
