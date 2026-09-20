# Skills

A personal collection of Claude Code / Agent Skills, vendored from their upstream
repos and sorted by category. Each folder keeps the upstream `SKILL.md`, `README.md`,
and `LICENSE` — this file is the full index: what each skill is, how to invoke it,
and where it actually works.

## How to use any of this

**Legend for "Where":**
- 🖥️ **CLI-only** — needs a real shell/filesystem/git (Claude Code, not claude.ai chat)
- 💬 **CLI + chat** — pure guidance/knowledge, so it also works uploaded as a skill zip to claude.ai (Settings → Capabilities → Skills)

**Three ways to get a skill installed, anywhere:**

1. **This repo's own marketplace (easiest, works in *any* repo, new or old):**
   ```
   /plugin marketplace add Astral176131/skills
   /plugin install <skill-name>@astral-skills
   ```
   See `.claude-plugin/marketplace.json` for the exact list of installable names — it
   covers every entry in `general/`, `frontend/`, and `devtools/` below (not the big
   `collections/` — those already ship their own marketplace; add those directly from
   their own repo instead, e.g. `/plugin marketplace add obra/superpowers`).

2. **Personal, global (every project on your machine):**
   ```bash
   cp -r general/caveman/skills/caveman-compress ~/.claude/skills/caveman-compress
   ```

3. **One project only:**
   ```bash
   cp -r general/caveman/skills/caveman-compress <your-repo>/.claude/skills/caveman-compress
   ```

**How invocation actually works:** most skills are *not* typed commands — Claude reads
every installed skill's short description up front and silently pulls in the full one
when your request matches it. Where a skill also defines an explicit **slash command**
(`/name`), that's called out below and always works too.

---

## general/ — cross-cutting workflow & engineering skills

### ponytail — [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail)
Makes Claude write like "the laziest senior dev in the room" — reuses stdlib/existing
code before writing anything new (~54% less code on average).
- **Sub-skills:** `ponytail`, `ponytail-review`, `ponytail-audit`, `ponytail-debt`, `ponytail-gain`, `ponytail-help`
- **Invoke:** `/ponytail`, `/ponytail-review`, `/ponytail-audit`, `/ponytail-debt`, `/ponytail-gain`, `/ponytail-help`
- **Where:** 🖥️ CLI-only
- **Install:** `/plugin marketplace add DietrichGebert/ponytail` or `/plugin install ponytail@astral-skills`

### karpathy-skills — [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills)
Andrej Karpathy's 4 rules for LLM coding pitfalls: surface assumptions, minimal diffs,
surgical edits only, verifiable success criteria.
- **Sub-skill:** `karpathy-guidelines`
- **Invoke:** automatic (matches on any coding task); simplest alternative is copying the bundled `CLAUDE.md` straight into your project root
- **Where:** 💬 CLI + chat (it's pure guidance text)
- **Install:** `/plugin install karpathy-skills@astral-skills`

### mattpocock-skills — [mattpocock/skills](https://github.com/mattpocock/skills)
Matt Pocock's real `.agents` directory: 37 engineering skills (TDD, code review,
domain modeling, architecture, merge-conflict resolution) + productivity skills
(grilling/interviewing yourself for clarity, handoff docs, writing-for-agents).
- **Sub-skills include:** `tdd`, `code-review`, `codebase-design`, `diagnosing-bugs`, `domain-modeling`, `implement`, `improve-codebase-architecture`, `prototype`, `research`, `resolving-merge-conflicts`, `to-spec`, `to-tickets`, `triage`, `wayfinder`, `grill-with-docs`, `grill-me`, `handoff`, `teach`, `writing-for-agents`
- **Invoke:** automatic by task description, or ask by name ("use the tdd skill")
- **Where:** 🖥️ CLI-only (most touch your repo directly)
- **Install:** `/plugin install mattpocock-skills@astral-skills`

### ecc — [affaan-m/ECC](https://github.com/affaan-m/ECC) ("Everything Claude Code")
Large agent-harness system bundling skills, memory, security review, and a
research-first workflow discipline.
- **Invoke:** automatic by task match; browse `general/ecc/skills/` for the full list, or `general/ecc/README.md` for the harness overview
- **Where:** 🖥️ CLI-only
- **Install:** `/plugin install ecc@astral-skills`

### claude-mem — [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)
Persistent memory across sessions — captures what an agent did, compresses it with AI,
and re-injects relevant context into future sessions. Also bundles ~20 bonus utility
skills.
- **Core sub-skills:** `mem-setup`, `mem-search`
- **Bonus sub-skills:** `weekly-digests`, `pathfinder`, `oh-my-issues`, `learn-codebase`, `what-the`, `smart-explore`, `mode-creator`, `cloud-sync`, `timeline-report`, `design-is`, `wowerpoint`, `make-plan`, `ccs-align`, `version-bump`, `how-it-works`, `do`, `standup`, `babysit`, `knowledge-agent`
- **Invoke:** memory capture/injection is automatic via hooks once installed; the others are `/mem-search`, or by name (e.g. "run standup")
- **Where:** 🖥️ CLI-only (hooks into session lifecycle)
- **Install:** `/plugin marketplace add thedotmack/claude-mem` then `/plugin install claude-mem`

### caveman — [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman)
Compresses agent output/context ~65-75% by talking in terse "caveman" prose while
keeping code/commands/errors byte-exact.
- **Sub-skills include:** `caveman-compress`, `caveman-review`, `caveman-audit`, `caveman-setup`, `caveman-stats`, `caveman-learn`, `caveman-optimize`, `caveman-discover`, `caveman-explore`, `caveman-commit`, `caveman-manage`, `caveman-evidence-review`, `caveman-help`, `cavecrew`, `verify-and-stop`, `safe-refactor`, `investigate-first`, `surgical-patch`, `lean-build`, `migration`
- **Invoke:** `/caveman-compress` (main one); others by name
- **Where:** 🖥️ CLI-only
- **Install:** `/plugin install caveman@astral-skills`

### planning-with-files — [OthmanAdi/planning-with-files](https://github.com/OthmanAdi/planning-with-files)
Manus-style persistent markdown planning — crash-proof task plans that survive
`/clear` and context compaction.
- **Sub-skill:** `planning-with-files` (+ localized variants: de, ar, es, zh, zh-TW)
- **Invoke:** automatic on long-running/multi-step tasks (writes `task_plan.md` and re-reads it before major decisions)
- **Where:** 🖥️ CLI-only
- **Install:** `/plugin install planning-with-files@astral-skills`

### agent-teams — built-in Claude Code feature (not a repo)
Runs multiple Claude sessions in parallel on one repo, coordinating through a shared
git-based task system instead of you juggling terminal tabs by hand.
- **Invoke:** native Claude Code team/agent-spawning tools — nothing to install
- **Where:** 🖥️ CLI-only
- **Details:** see `general/agent-teams/README.md`

---

## frontend/ — UI/UX, design, and design-system skills

### ui-ux-pro-max — [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)
Searchable databases of 67 UI styles, 161 color palettes, 57 font pairings, 99 UX
guidelines, chart types and tech stacks, to ground design decisions in specifics
instead of vibes.
- **Sub-skills:** `ui-ux-pro-max`, `design`, `design-system`, `brand`, `banner-design`, `slides`, `ui-styling`
- **Invoke:** automatic on UI/UX tasks — designing pages, choosing color/typography, reviewing for accessibility/consistency
- **Where:** 💬 CLI + chat (mostly reference data + guidance)
- **Install:** `/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill` then `/plugin install ui-ux-pro-max@ui-ux-pro-max-skill`, or `/plugin install ui-ux-pro-max@astral-skills`

### taste-skill — [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill)
Stops AI from generating generic "slop" frontends — layout, typography, spacing,
hierarchy, motion. Ships style-specific variants.
- **Sub-skills:** `taste-skill` (default), `taste-skill-v1`, `gpt-tasteskill` (stricter, for GPT/Codex), `minimalist-skill`, `brutalist-skill`, `soft-skill`, `redesign-skill`, `image-to-code-skill`, `imagegen-frontend-web`, `imagegen-frontend-mobile`, `brandkit`, `stitch-skill`, `output-skill`
- **Invoke:** automatic whenever generating or redesigning frontend UI
- **Where:** 💬 CLI + chat
- **Install:** `npx skills add Leonxlnx/taste-skill`, or `/plugin install taste-skill@astral-skills`

### superdesign — [superdesigndev/superdesign-skill](https://github.com/superdesigndev/superdesign-skill)
Gives the agent design judgment so UI ships "tasteful" instead of generic-AI-looking.
- **Invoke:** `/superdesign:superdesign`
- **Where:** 🖥️ CLI-only
- **Install:** `/plugin marketplace add superdesigndev/superdesign-skill` then `/plugin install superdesign@superdesign`, or `/plugin install superdesign@astral-skills`

### impeccable — [pbakaus/impeccable](https://github.com/pbakaus/impeccable)
Catalogs 64+ "AI slop" design patterns (purple gradients, generic defaults) and
replaces them with better ones.
- **Invoke:** `/impeccable init` once, then the phases: `craft`, `audit`, `polish`, `harden`
- **Where:** 🖥️ CLI-only
- **Install:** `npx impeccable install` then `/impeccable init`, or `/plugin install impeccable@astral-skills`

### design-motion — [kylezantos/design-motion-principles](https://github.com/kylezantos/design-motion-principles)
Motion design skill with two modes: build components with purposeful motion, or
audit existing animations.
- **Sub-skill:** `design-motion-principles`
- **Invoke:** automatic when building animated components or asked to review motion/animation
- **Where:** 💬 CLI + chat
- **Install:** `/plugin install design-motion@astral-skills`

### figma-implement — [openai/skills — figma-implement-design](https://github.com/openai/skills/tree/main/skills/.curated/figma-implement-design)
Translates a Figma design into production code with 1:1 visual fidelity.
- **Invoke:** automatic when you say "implement this design/component" with a Figma link, or asked explicitly
- **Where:** 🖥️ CLI-only (needs a Figma MCP/API connection to fetch the design)
- **Install:** `/plugin install figma-implement@astral-skills`

---

## security/

### trailofbits-skills — [trailofbits/skills](https://github.com/trailofbits/skills)
Trail of Bits' real security-audit skill collection — 85 skills for static analysis,
vulnerability detection, and audit workflows.
- **Notable sub-skills:** `audit-context-building` (bootstraps an audit on an unfamiliar codebase), `agentic-actions-auditor` (audits GitHub Actions/CI for AI-agent-specific vulnerabilities), `building-secure-contracts`, `entry-point-analyzer`
- **Invoke:** by name, or automatically when you ask for a security audit / code review with a security lens
- **Where:** 🖥️ CLI-only
- **Install:** `/plugin marketplace add trailofbits/skills` then `/plugin install <skill-name>@trailofbits` (not wrapped in this repo's own marketplace — install straight from theirs since it's already its own multi-plugin marketplace)

---

## devtools/ — tooling, orchestration, and meta-skills

### codegraph — [colbymchenry/codegraph](https://github.com/colbymchenry/codegraph)
Pre-indexed, auto-syncing local code knowledge graph — fewer tokens/tool-calls needed
to understand a codebase.
- **Sub-skills:** `agent-eval`, `add-lang`
- **Invoke:** MCP tools `codegraph_context` / `codegraph_explore` (automatic once registered), or CLI `codegraph init`
- **Where:** 🖥️ CLI-only
- **Install:** `npm install -g @colbymchenry/codegraph`, then `codegraph install` and `codegraph init` in your project

### graphify — [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify)
Turns a folder of code/docs/PDFs/images into a queryable, deterministic (AST-based)
knowledge graph.
- **Invoke:** `/graphify`
- **Where:** 🖥️ CLI-only
- **Note:** ships a lowercase `skill.md`, not `SKILL.md` — case matters on Linux; verify it actually loads before relying on it, or rename it locally.
- **Install:** installs a CLAUDE.md directive + PreToolUse hook; see `devtools/graphify/README.md`

### omniroute — [diegosouzapw/OmniRoute](https://github.com/diegosouzapw/OmniRoute)
Local AI-gateway: one Anthropic-compatible endpoint routing to 352 providers/1200+
models with auto-fallback. Bundles ~45 sub-skills (`omni-*`, `cli-*`) for routing,
caching, auth, MCP, billing, etc.
- **Invoke:** run as a local service, point clients at its port; individual `omni-*`/`cli-*` skills invoked by name
- **Where:** 🖥️ CLI-only
- **⚠️ Caution:** independent coverage has flagged security issues/CVEs on this project. Review the source and pin a commit before running it — it proxies your API traffic.
- **Install:** see `devtools/omniroute/README.md`

### firecrawl — [firecrawl/firecrawl-claude-plugin](https://github.com/firecrawl/firecrawl-claude-plugin)
Web scraping/crawling/search as Claude Code commands, backed by the Firecrawl API.
- **Sub-skills:** `firecrawl`, `firecrawl-scrape`, `firecrawl-crawl`, `firecrawl-map`, `firecrawl-search`, `firecrawl-parse`, `firecrawl-monitor`, `firecrawl-download`, `firecrawl-interact`, `firecrawl-agent`, `firecrawl-research-index`, `firecrawl-developer-index`
- **Invoke:** `/firecrawl-scrape <url>`, `/firecrawl-crawl <url>`, `/firecrawl-search <query>`, etc.
- **Where:** 🖥️ CLI-only
- **Install:** `/plugin marketplace add firecrawl/firecrawl-claude-plugin`. Needs a `FIRECRAWL_API_KEY`.

### codex-plugin-cc — [openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc)
Lets Claude Code delegate a task or code review to OpenAI Codex.
- **Sub-skills:** `gpt-5-4-prompting`, `codex-cli-runtime`, `codex-result-handling`
- **Invoke:** `/codex:rescue` (delegate a task), `/codex:transfer`, `/codex:status`, `/codex:result`, `/codex:cancel`
- **Where:** 🖥️ CLI-only. Needs a ChatGPT subscription or OpenAI API key.
- **Install:** `/plugin marketplace add openai/codex-plugin-cc`

### claude-hud — [jarrodwatts/claude-hud](https://github.com/jarrodwatts/claude-hud)
Local-only HUD plugin: live view of context usage, active tools, running agents, todo
progress. No network calls.
- **Invoke:** passive — shows automatically once installed
- **Where:** 🖥️ CLI-only
- **Install:** `/plugin marketplace add jarrodwatts/claude-hud`

### wshobson-agents — [wshobson/agents](https://github.com/wshobson/agents)
Large multi-harness marketplace: 202 subagents, 181 skills, 105 commands, 93 plugins
across nearly every domain.
- **Categories include:** `backend-development`, `frontend-mobile-development`, `python-development`, `javascript-typescript`, `database-design`, `api-scaffolding`, `cloud-infrastructure`, `kubernetes-operations`, `cicd-automation`, `security-scanning`, `machine-learning-ops`, `llm-application-dev`, `data-engineering`, `blockchain-web3`, `game-development`, `quantitative-trading`, `payment-processing`, `documentation-generation`, `ui-design`, `incident-response`, `observability-monitoring`, `agent-teams`
- **Invoke:** name a subagent directly ("use the backend-architect agent"), or `/plugin install <plugin-name>@wshobson` for a specific category
- **Where:** 🖥️ CLI-only
- **Install:** `/plugin marketplace add wshobson/agents`, or `/plugin install wshobson-agents@astral-skills` for the whole bundle

### prompt-master — [nidhinjs/prompt-master](https://github.com/nidhinjs/prompt-master)
Writes accurate, tool-specific prompts for 30+ AI tools from a short brief; keeps a
memory block of prior decisions so new prompts don't contradict old ones.
- **Invoke:** automatic when you ask "write me a prompt for X"
- **Where:** 💬 CLI + chat
- **Install:** `npx -y skills add nidhinjs/prompt-master --skill prompt-master --agent claude-code`, or `/plugin install prompt-master@astral-skills`

### find-skills — [fockus/claude-skill-find-skill](https://github.com/fockus/claude-skill-find-skill)
Discover and install Claude Code skills from 12 community/official sources without
leaving the CLI.
- **Invoke:** ask in natural language — "find me a skill for X", "install a skill that does Y"
- **Where:** 🖥️ CLI-only (installs things into your filesystem)
- **Install:** `/plugin install find-skills@astral-skills`

### agent-skills-cli — [vercel-labs/skills](https://github.com/vercel-labs/skills)
The generic `npx skills` installer referenced throughout this file — auto-detects
your agent (Claude Code, Cursor, Codex, ...) and installs a skill in the right
place/format.
- **Invoke:** run in your terminal, not inside a Claude conversation: `npx skills add <owner>/<repo>`
- **Where:** 🖥️ CLI-only (it's a standalone CLI tool)
- **Install:** nothing to install — it *is* the installer

### gstack — [garrytan/gstack](https://github.com/garrytan/gstack)
Garry Tan's full virtual-engineering-team setup: role-based skills covering CEO, eng
manager, designer, QA, security, and release, plus power tools.
- **Sub-skills include:** `design`, `design-review`, `design-consultation`, `design-html`, `design-shotgun`, `devex-review`, `qa`, `qa-only`, `review`, `retro`, `health`, `guard`, `freeze`/`unfreeze`, `diagram`, `ship`, `land-and-deploy`, `learn`, `investigate`, `office-hours`, `plan-ceo-review`, `plan-design-review`, `plan-devex-review`, `plan-eng-review`, `make-pdf`, `document-generate`, `document-release`, `browse`, `scrape`, `benchmark`, `ios-clean`/`ios-fix`/`ios-qa`/`ios-sync`/`ios-design-review`
- **Invoke:** each top-level name is its own slash command, e.g. `/design`, `/qa`, `/retro`, `/ship`
- **Where:** 🖥️ CLI-only
- **Install:** clone into your project, or `/plugin install gstack@astral-skills`

### playwright-mcp — [microsoft/playwright-mcp](https://github.com/microsoft/playwright-mcp)
MCP **server** (not a skill folder) — real browser automation via the accessibility
tree, no vision model needed.
- **Invoke:** automatic once registered — Claude calls tools like `browser_navigate`, `browser_click`, `browser_snapshot`, `browser_type`
- **Where:** 🖥️ CLI-only
- **Install:** `claude mcp add playwright npx '@playwright/mcp@latest'` — see `devtools/playwright-mcp/README.md`

---

## collections/ — large multi-domain skill libraries (browse & cherry-pick)

These already ship (or effectively are) their own marketplace, so install straight
from their upstream repo rather than through `astral-skills`.

### anthropics-skills — [anthropics/skills](https://github.com/anthropics/skills)
Anthropic's own official skills.
- **Skills:** `docx`, `pdf`, `pptx`, `xlsx`, `algorithmic-art`, `canvas-design`, `slack-gif-creator`, `frontend-design`, `web-artifacts-builder`, `mcp-builder`, `webapp-testing`, `brand-guidelines`, `internal-comms`, `skill-creator`, `claude-api`
- **Invoke:** automatic by file type or task ("make me a pptx", "extract this pdf's tables")
- **Where:** 💬 CLI + chat — `docx`/`pdf`/`pptx`/`xlsx` are already built into claude.ai for paid plans
- **Install:** `/plugin marketplace add anthropics/skills` then `/plugin install <skill-name>`

### alirezarezvani-claude-skills — [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills)
~380 skills across 20 domains: engineering, marketing, product, C-level advisory,
compliance, research, finance, business ops, commercial, and personal productivity.
- **Invoke:** browse the domain folder you need and install its plugin, e.g. `/plugin install engineering-skills@claude-code-skills`
- **Where:** 🖥️ mostly CLI-only (a handful of pure-writing skills would also work in chat)
- **Install:** `/plugin marketplace add alirezarezvani/claude-skills`

### superpowers — [obra/superpowers](https://github.com/obra/superpowers)
15 battle-tested workflow skills.
- **Skills:** `test-driven-development`, `systematic-debugging`, `diagnosing-superpowers`, `brainstorming`, `writing-plans`, `executing-plans`, `requesting-code-review`, `receiving-code-review`, `subagent-driven-development`, `dispatching-parallel-agents`, `using-git-worktrees`, `finishing-a-development-branch`, `verification-before-completion`, `writing-skills`, `using-superpowers`
- **Invoke:** automatic by task match, or by name
- **Where:** 🖥️ CLI-only
- **Install:** `/plugin marketplace add obra/superpowers`

---

## reference/ — indexes & educational material (not installable skills)

- **`awesome-claude-skills.md`** — [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills): a curated link-list to browse for anything not already vendored here.
- **`learn-claude-code.md`** — [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code): 17-chapter course explaining *why* skill loading works the way it does.

---

## What was deliberately left out, and why

- **`frustration-checks`**, **`token-budgets`** — no project exists under either exact
  name; skipped per your confirmation.
- **`agent skills`** (generic, no author given) — covered by `anthropics-skills` and
  `agent-skills-cli` above, the two most plausible readings.
- **Spelling corrections** from the original list — the real repos are
  `alirezarezvani` (not *alirezarezvaini*), `affaan-m/ECC` (not *affan-m*),
  `Leonxlnx/taste-skill` (not *leonxinx*), `playwright-mcp` (not *playright*).
