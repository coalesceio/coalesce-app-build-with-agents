# Build with Agents

A Coalesce workspace app. Describe the pipelines you need, or attach a spec, and Claude Code plans and builds them in a private copy of your workspace. You approve the plan, review what was built (Coalesce validates it), and apply it to your workspace when you're happy. Nothing in your workspace changes until you apply.

## What it needs

- Coalesce Desktop 7.51 or later, or `coa serve`.
- [Claude Code](https://code.claude.com) installed and signed in on the same computer. The app runs your own Claude Code, so usage counts against your Claude plan or API key. The app's setup page checks this.
- Source nodes and storage locations in the workspace.

## How it works

- Each request is a thread that moves through Draft, Plan, Build, Validate, Review and Apply.
- A thread works in two copies of the workspace: one as it was when the thread started, and one the agent writes to. The changes are the difference between them. Apply copies only those files into your workspace, uncommitted, and can take them back out until you commit.
- Agents use the bundled [Coalesce Platform Skills](https://github.com/Coalesce-Software-Inc/coalesce-platform-skills) (`vendor/`; update them with `scripts/update-skills.sh <tag>`). They work with file tools only: no shell and no network tools.
- Threads are kept in `~/.coa/apps/build-with-agents/`, outside the workspace. The agent conversations are ordinary Claude Code sessions.

## This repository

The app's source is in this folder: `server.js` (no dependencies) and the page in `public/`.

To release a version: add the changes to the `## [Unreleased]` section of `CHANGELOG.md`, merge them, then run **Release app** in [coalesce-app-releases](https://github.com/coalesceio/coalesce-app-releases).
