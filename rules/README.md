# rules/ — the ruleset for other agents

Most agents take a plain markdown file, so one file covers most of them: **`system-prompt.md`**,
the full ruleset with no frontmatter. Copy it and rename it to whatever your tool expects.

The other files exist only where a tool forces a different shape — Cursor needs MDC frontmatter,
and Windsurf caps a rule file at roughly 6,000 characters.

## Install matrix

| Agent / tool | Copy | To | Change |
|---|---|---|---|
| **Codex, Aider, Zed, Jules, Gemini CLI, Amp** | `system-prompt.md` | `AGENTS.md` | rename only |
| **Cline, Roo Code** | `system-prompt.md` | `.clinerules/persian-technical-writing.md` | rename only |
| **GitHub Copilot** (repo-wide) | `system-prompt.md` | `.github/copilot-instructions.md` | rename only |
| **GitHub Copilot** (path-scoped) | `system-prompt.md` | `.github/instructions/persian.instructions.md` | prepend frontmatter, below |
| **Cursor** | `cursor.mdc` | `.cursor/rules/persian-technical-writing.mdc` | rename only |
| **Windsurf** | `windsurf-persian-script.md` | `.windsurf/rules/persian-script.md` | rename only |
| | `windsurf-persian-structure.md` | `.windsurf/rules/persian-structure.md` | rename only |
| **Any chat model, Custom GPT, Gem, API** | `system-prompt.md` | the system prompt | paste |

For path-scoped Copilot, prepend:

```yaml
---
applyTo: '**/*.fa.md,**/fa/**,**/locales/fa/**,**/*.persian.md'
---
```

Widen it to `'**'` if any file in your repo can contain Persian.

## Notes per target

**Cursor** ships with `alwaysApply: false` and a description, which makes it an *agent-requested*
rule: Cursor pulls it in when the task looks like Persian writing, instead of spending ~20K
characters of context on every request. Set `alwaysApply: true` only if your repo is Persian-first.

**Windsurf** caps a rule file at roughly 6,000 characters, so the ruleset ships as two files that
install together:

- `persian-script.md` — orthography and bidi (ZWNJ, codepoints, digits, punctuation, dates,
  RTL/LTR isolation). These apply in every mode, so this file keeps its full "Don't" column: the
  negative examples are what make the rules checkable.
- `persian-structure.md` — modes, structural rules, lexical rules, terminology, scan checklist.
  Condensed to fit: the tables keep "Rule" and "Do" but drop "Don't" and "Why". It references
  `persian-script.md` by name, so keep that filename.

Both use `trigger: model_decision`. Switch to `always_on` to load them unconditionally.

The two Windsurf files together are also the best compact version of the ruleset — about 10K
characters instead of 22K — if you need a system prompt for a small model or a tight context
budget. Prefer `system-prompt.md` when the model can afford it.

## Using it from code

```python
import anthropic

RULES = open("rules/system-prompt.md", encoding="utf-8").read()

client = anthropic.Anthropic()
message = client.messages.create(
    model="claude-sonnet-5",
    max_tokens=2000,
    system=RULES + "\n\nMode: Strict. Output the rewritten Persian text only.",
    messages=[{"role": "user", "content": persian_text}],
)
```

The same string works as an OpenAI `system` message, a Gemini `system_instruction`, or the
instructions field of a Custom GPT. The ruleset names no vendor and requires no tools.

## Keeping these in sync

`SKILL.md` in the repo root is the canonical ruleset; these are hand-maintained copies of it. If you
change a rule, change it in `SKILL.md` and in the files here. `system-prompt.md` is the full text
verbatim, so it is a straight copy; the two Windsurf files need the condensation reapplied.
