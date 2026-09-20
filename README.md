# Skills

A personal collection of Claude Code / Agent Skills, vendored from their
upstream repos and sorted by what they're for. Each skill folder below keeps
its own original `README.md`, `SKILL.md`, and `LICENSE` — this file is the
index and the "how do I actually use this" cheat sheet. Skill *source code*
(tests, build tooling, CI, Docker, lockfiles) was stripped out on import;
only the parts you need to install and run the skill were kept.

## How Claude Code skills work, in general

A skill is a folder containing a `SKILL.md` (YAML frontmatter + instructions,
optionally with `scripts/`, `references/`, `assets/` alongside it). Claude
reads the lightweight frontmatter for every installed skill up front, and
only loads the full body when your task matches its description — so having
many skills installed is cheap.

Three ways to install one, in order of how these repos tend to ship:

1. **Copy the folder.** Drop the skill directory into `~/.claude/skills/<name>/`
   (available in every project) or `<your-project>/.claude/skills/<name>/`
   (that project only).
2. **Claude Code plugin marketplace**, when the repo ships a
   `.claude-plugin/plugin.json`:
   ```
   /plugin marketplace add <owner>/<repo>
   /plugin install <skill-name>@<marketplace-name>
   ```
3. **`npx skills add <owner>/<repo>`** — the generic installer
   (see `devtools/agent-skills-cli/`), which auto-detects Claude Code, Cursor,
   Codex, etc. and places the skill correctly for whichever you're using.

Per-skill notes below tell you which of these applies.

---

## general/ — cross-cutting workflow & engineering skills

| Skill | What it does | Install / use |
|---|---|---|
| [`ponytail`](general/ponytail) — [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) | Makes Claude write like "the laziest senior dev" — reuses stdlib/existing code before writing new code; ~54% less code on average. | `/plugin marketplace add DietrichGebert/ponytail` then `/plugin install ponytail`. Commands: `/ponytail`, `/ponytail-review`, `/ponytail-audit`, `/ponytail-debt`, `/ponytail-gain`. |
| [`karpathy-skills`](general/karpathy-skills) — [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills) | Andrej Karpathy's 4 rules for LLM coding pitfalls (surface assumptions, minimal diffs, surgical edits only, verifiable success criteria) as a CLAUDE.md + skill. | Simplest path: copy `CLAUDE.md` into your project root. Or `/plugin marketplace add multica-ai/andrej-karpathy-skills` then install `karpathy-guidelines`. |
| [`mattpocock-skills`](general/mattpocock-skills) — [mattpocock/skills](https://github.com/mattpocock/skills) | Matt Pocock's real `.agents` directory, public — 50+ skills for TDD, code review, domain modeling, architecture. | Browse `skills/` and copy what you want into `~/.claude/skills/`, or `/plugin marketplace add mattpocock/skills`. |
| [`ecc`](general/ecc) — [affaan-m/ECC](https://github.com/affaan-m/ECC) ("Everything Claude Code") | Large agent-harness optimization system: skills, instincts, memory, security, research-first workflow. 280+ skills, 68 agents. | See `README.md` inside — installs via its own setup script; browse `skills/` and cherry-pick, or run the full installer if you want the whole harness. |
| [`claude-mem`](general/claude-mem) — [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | Persistent memory across sessions — captures what an agent did, compresses it, re-injects relevant context into future sessions. | `/plugin marketplace add thedotmack/claude-mem` then `/plugin install claude-mem`. |
| [`caveman`](general/caveman) — [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) | Compresses agent output/context ~65-75% by talking in terse "caveman" prose while keeping code/commands/errors byte-exact. | `/plugin marketplace add JuliusBrussee/caveman`. Command: `/caveman-compress`. |
| [`planning-with-files`](general/planning-with-files) — [OthmanAdi/planning-with-files](https://github.com/OthmanAdi/planning-with-files) | Manus-style persistent markdown planning — crash-proof task plans that survive `/clear` and context compaction. | Copy `skills/planning-with-files/` into `~/.claude/skills/`, or `npx skills add OthmanAdi/planning-with-files`. |
| [`agent-teams`](general/agent-teams) | **Not a repo** — native Claude Code feature for running parallel coordinated Claude sessions on one repo. | See `general/agent-teams/README.md` — nothing to install, it's built in. |

## frontend/ — UI/UX, design, and design-system skills

| Skill | What it does | Install / use |
|---|---|---|
| [`ui-ux-pro-max`](frontend/ui-ux-pro-max) — [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | Searchable databases of 67 UI styles, 161 color palettes, 57 font pairings, 99 UX guidelines to ground design decisions. | `/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill` then `/plugin install ui-ux-pro-max@ui-ux-pro-max-skill`. |
| [`taste-skill`](frontend/taste-skill) — [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) | Stops AI from generating generic "slop" frontends — layout, typography, spacing, hierarchy, motion guidance. | `npx skills add Leonxlnx/taste-skill`, or copy `skills/taste-skill/` directly. |
| [`superdesign`](frontend/superdesign) — [superdesigndev/superdesign-skill](https://github.com/superdesigndev/superdesign-skill) | Gives the agent design judgment so UI ships "tasteful" instead of generic-AI-looking. | `/plugin marketplace add superdesigndev/superdesign-skill` then `/plugin install superdesign@superdesign`. Invoke: `/superdesign:superdesign`. |
| [`impeccable`](frontend/impeccable) — [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | Catalogs 64+ "AI slop" design patterns (purple gradients, generic defaults) and replaces them. Commands: craft, audit, polish, harden. | `npx impeccable install` then `/impeccable init` inside Claude Code. |
| [`design-motion`](frontend/design-motion) — [kylezantos/design-motion-principles](https://github.com/kylezantos/design-motion-principles) | Motion design skill with two modes: build components with purposeful motion, or audit existing animations. | Copy the skill folder into `~/.claude/skills/`. |
| [`figma-implement`](frontend/figma-implement) — [openai/skills — figma-implement-design](https://github.com/openai/skills/tree/main/skills/.curated/figma-implement-design) | Translates a Figma design into production code with 1:1 visual fidelity. Cross-compatible skill format (works with Claude Code too). | Copy the folder into `~/.claude/skills/figma-implement-design/`. Needs a Figma MCP/API connection to actually fetch designs. |

## security/

| Skill | What it does | Install / use |
|---|---|---|
| [`trailofbits-skills`](security/trailofbits-skills) — [trailofbits/skills](https://github.com/trailofbits/skills) | Trail of Bits' real security-audit skill collection: `audit-context-building`, `agentic-actions-auditor` (audits GH Actions/CI for AI-agent-specific vulnerabilities), `building-secure-contracts`, `entry-point-analyzer`, etc. | `/plugin marketplace add trailofbits/skills` then `/plugin install <skill-name>@trailofbits`. *(Note: you asked for "claude-audit(trailofbits)" — no repo by that exact name exists there; this is Trail of Bits' actual audit skill set, which is what that attribution pointed to.)* |

## devtools/ — tooling, orchestration, and meta-skills

| Skill | What it does | Install / use |
|---|---|---|
| [`codegraph`](devtools/codegraph) — [colbymchenry/codegraph](https://github.com/colbymchenry/codegraph) | Pre-indexed, auto-syncing local code knowledge graph — fewer tokens/tool-calls to understand a codebase. | `npm install -g @colbymchenry/codegraph`, then `codegraph install` and `codegraph init` in your project. |
| [`graphify`](devtools/graphify) — [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | Turns a folder of code/docs/PDFs/images into a queryable, deterministic (AST-based) knowledge graph. | See `README.md`; installs a CLAUDE.md directive + PreToolUse hook. Command: `/graphify`. |
| [`omniroute`](devtools/omniroute) — [diegosouzapw/OmniRoute](https://github.com/diegosouzapw/OmniRoute) | Local AI-gateway: one Anthropic-compatible endpoint routing to 352 providers/1200+ models with auto-fallback. | See `README.md`. ⚠️ **Caution:** independent coverage has flagged security issues/CVEs on this project ("OmniRoute Review: Free Claude Tokens, Security Risks & CVEs" — Level Up Coding). Review the source and pin a specific commit before running it, especially since it proxies your API traffic. |
| [`firecrawl`](devtools/firecrawl) — [firecrawl/firecrawl-claude-plugin](https://github.com/firecrawl/firecrawl-claude-plugin) | Web scraping/crawling/search as Claude Code commands+skills, backed by the Firecrawl API. | `/plugin marketplace add firecrawl/firecrawl-claude-plugin`. Needs a `FIRECRAWL_API_KEY`. |
| [`codex-plugin-cc`](devtools/codex-plugin-cc) — [openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc) | Lets Claude Code delegate a task or code review to OpenAI Codex. | `/plugin marketplace add openai/codex-plugin-cc`. Commands: `/codex:rescue`, `/codex:transfer`, `/codex:status`, `/codex:result`, `/codex:cancel`. Needs a ChatGPT sub or OpenAI API key. |
| [`claude-hud`](devtools/claude-hud) — [jarrodwatts/claude-hud](https://github.com/jarrodwatts/claude-hud) | Local-only HUD plugin: live view of context usage, active tools, running agents, todo progress. No network calls. | `/plugin marketplace add jarrodwatts/claude-hud`. |
| [`wshobson-agents`](devtools/wshobson-agents) — [wshobson/agents](https://github.com/wshobson/agents) | Large multi-harness marketplace: 202 subagents, 181 skills, 105 commands, 93 plugins across every domain (backend, frontend, mobile, etc.). | Browse `plugins/`/`tools/`, install individual plugins via `/plugin marketplace add wshobson/agents` + `/plugin install <name>@wshobson`, or clone agents straight into `~/.claude/agents/`. |
| [`prompt-master`](devtools/prompt-master) — [nidhinjs/prompt-master](https://github.com/nidhinjs/prompt-master) | Writes accurate, tool-specific prompts for 30+ AI tools from a short brief; keeps a memory block of prior decisions. | `npx -y skills add nidhinjs/prompt-master --skill prompt-master --agent claude-code`. |
| [`find-skills`](devtools/find-skills) — [fockus/claude-skill-find-skill](https://github.com/fockus/claude-skill-find-skill) | Discover and install Claude Code skills from 12 community/official sources without leaving the CLI. | Copy `SKILL.md` (repo root) into `~/.claude/skills/find-skill/`, then ask Claude in natural language to find/install a skill for X. |
| [`agent-skills-cli`](devtools/agent-skills-cli) — [vercel-labs/skills](https://github.com/vercel-labs/skills) | The generic `npx skills` installer referenced throughout this table — auto-detects your agent and installs a skill in the right place/format. | `npx skills add <owner>/<repo>`. This is the "meta" tool for installing most of the other entries here. |
| [`gstack`](devtools/gstack) — [garrytan/gstack](https://github.com/garrytan/gstack) | Garry Tan's full virtual-engineering-team setup: 23 role skills (CEO, eng manager, designer, QA, security, release) + 8 power tools. | Clone into your project (each top-level folder like `design/`, `qa/`, `retro/` is its own skill), or use as a Claude Code plugin per its `SKILL.md`. |
| [`playwright-mcp`](devtools/playwright-mcp) — [microsoft/playwright-mcp](https://github.com/microsoft/playwright-mcp) | MCP server for real browser automation (not a skill folder). | See `devtools/playwright-mcp/README.md` — `claude mcp add playwright npx '@playwright/mcp@latest'`. |

## collections/ — large multi-domain skill libraries (browse & cherry-pick)

| Collection | What it is | Install / use |
|---|---|---|
| [`anthropics-skills`](collections/anthropics-skills) — [anthropics/skills](https://github.com/anthropics/skills) | Anthropic's own official skills: `docx`, `pdf`, `pptx`, `xlsx`, `algorithmic-art`, `canvas-design`, `frontend-design`, `web-artifacts-builder`, `mcp-builder`, `webapp-testing`, `brand-guidelines`, `internal-comms`, `skill-creator`, `claude-api`. | `/plugin marketplace add anthropics/skills` then `/plugin install <skill-name>`. Several of these (docx/pdf/pptx/xlsx) are already built into Claude.ai for paid plans. |
| [`alirezarezvani-claude-skills`](collections/alirezarezvani-claude-skills) — [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills) | ~380 skills across 20 domains (engineering, marketing, product, compliance, C-level advisory, research, finance, ...). | Browse the domain folder you need (e.g. `engineering/`) and copy individual skill folders into `~/.claude/skills/`. |
| [`superpowers`](collections/superpowers) — [obra/superpowers](https://github.com/obra/superpowers) | 20+ battle-tested skills: TDD, debugging, collaboration workflows. | `/plugin marketplace add obra/superpowers`. |

## reference/ — indexes & educational material (not installable skills)

| File | What it is |
|---|---|
| [`awesome-claude-skills.md`](reference/awesome-claude-skills.md) — [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) | A curated link-list of skills/collections. Browse it to find things not already vendored here. |
| [`learn-claude-code.md`](reference/learn-claude-code.md) — [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | 17-chapter course building a mini agent harness from scratch; explains *why* skill loading works the way it does. |

---

## What I deliberately left out, and why

- **`frustration-checks`** and **`token-budgets`** — no project exists under
  either exact name; you confirmed skipping both rather than guessing.
- **`agent skills`** (generic, no author given) — ambiguous; the two most
  plausible readings (Anthropic's official skills, and the generic
  `npx skills` installer) are both already here as `anthropics-skills` and
  `agent-skills-cli`.
- **Spelling corrections from your list** — the real repos are
  `alirezarezvani` (not *alirezarezvaini*), `affaan-m/ECC` (not *affan-m*),
  `Leonxlnx/taste-skill` (not *leonxinx*), and `playwright-mcp` (not
  *playright*). Linked above under their correct names.
