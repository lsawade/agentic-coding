# Starter kit: agentic coding for a research project

This folder is a starting point for using Claude Code on a research project. Codex and Cursor also work with it, since they read AGENTS.md. Copy the folder's contents into the root of your repository, fill in CLAUDE.md with the facts about your project, and commit. The agent works from CLAUDE.md, the slash commands, and the permission settings. You are the supervisor: the AI drafts, and you own the correctness of every result.

## Setup

- CLAUDE.md with layout, test command, conventions, and what not to touch
- git: commit early and often; use worktrees for parallel agent sessions
- permissions: run in a sandbox, allowlist read-only commands, never give the agent live database credentials

## Loop

- Plan first: brainstorm, run a feasibility check, then a plan session; use /grill-me on the foggy parts
- Small steps you can review; restart the session when it gets confused
- Review as a supervisor: read every line you would sign for, ask the agent to list its own problems, use a second model as adversary, rewrite clean after prototyping

## Responsibility

- Disclose AI use per the project's or journal's policy (read CONTRIBUTING.md first)
- Mind the data: unpublished results, PII, IRB-covered, and export-controlled data never go into a hosted model; use local or open-weight models there
- Never let an agent open a PR you have not read
- Have the AI write the script that does the task, not do the task, so the result is reproducible

## What is in this folder

- README.md: this checklist
- CLAUDE.md: project memory skeleton the agent reads at session start
- .claude/commands/grill-me.md: slash command that interrogates a plan until its foggy parts are explicit
- .claude/commands/pr.md: slash command that prepares a pull request for human review
- .claude/agents/test-runner.md: subagent that runs the test suite and reports only failures
- .claude/settings.json: permission allowlist of read-only commands, with secrets and destructive commands denied

Rename CLAUDE.md to AGENTS.md (or symlink it) for Codex and Cursor.
