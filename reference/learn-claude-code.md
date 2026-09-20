# learn-claude-code (educational reference, not a skill)

Source: [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code)

This is a 17-chapter, MIT-licensed course ("Bash is all you need") that
builds a nano Claude-Code-like agent harness from scratch in Python —
context management, the agent loop, tool use, and (chapter s05) how skill
loading actually works under the hood: the model sees cheap skill
*descriptions* up front and only loads the expensive full `SKILL.md` body
when a task matches.

It's not an installable skill — it's for understanding *why* skills are
structured the way they are, which is useful background if you're going to
write your own SKILL.md files rather than just install other people's.

## How to use it

```bash
git clone https://github.com/shareAI-lab/learn-claude-code.git
cd learn-claude-code
pip install -r requirements.txt
export ANTHROPIC_API_KEY=...
python s01_agent_loop/code.py   # start at chapter 1, read s01 -> s17 in order
```

Read `docs/en/s05-skill-loading.md` specifically if you just want the skill-
loading mental model without doing the whole course.
