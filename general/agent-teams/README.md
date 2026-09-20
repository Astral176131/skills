# Agent Teams (built-in Claude Code feature)

Not a third-party skill — "Agent Teams" is a native Claude Code capability for
running several Claude sessions in parallel on the same repo, coordinating
through a shared git-based task system instead of you manually juggling
multiple terminal tabs.

## What it does

- Spawns multiple Claude instances that work on different subtasks at once.
- Agents claim tasks, commit their own work, and merge continuously.
- Conflicts between agents' changes are resolved automatically rather than
  left for you to untangle by hand.
- Useful for large refactors, multi-package changes, or "review + implement
  in parallel" workflows.

## How to use it

1. In Claude Code, use the `Agent` / team-spawning tools (or `/agents` in
   newer CLI versions) to start a team instead of a single subagent.
2. Give each agent a scoped task (a package, a directory, a layer of the
   stack) so their work doesn't overlap.
3. Let the coordinator session monitor progress; it merges each agent's
   commits and flags real conflicts for you to resolve.
4. Prefer this over ad-hoc multi-terminal Claude Code sessions once a task
   naturally splits into independent chunks — it removes the manual
   copy-paste-merge loop.

## Learning resources (community, not required)

- `panaversity/claude-code-agent-teams-exercises` — 8 exercises + 2 capstones
  that walk through team creation, task coordination, quality hooks, and
  parallel code review. Good for practicing the feature hands-on; it is a
  tutorial repo, not an installable skill.

No files to copy for this one — it ships with Claude Code itself.
