# Simplified Technical Persian

**[فارسی](README.fa.md)** · **[English](README.md)**

A Claude Code skill that rewrites Persian (Farsi) technical text so it has exactly one legal
reading. It adapts the discipline of [ASD-STE100](https://www.asd-ste100.org/) (Simplified
Technical English) to Persian, not by translating English rules but by restating each rule in
Persian-grammar terms and adding the rules Persian needs and English does not.

## Why

ASD-STE100 removes the two biggest sources of misreading in English: words with more than one
meaning, and sentences with more than one possible structure. Persian misreads for different
reasons:

- **Invisible ezafe.** The ezafe enclitic is usually not written, so most noun–modifier links are
  unmarked in print, and chained links (تتابع اضافات) are multiply ambiguous.
- **Polysemous شدن.** It is a passive auxiliary, a main verb ("become"), and an active
  compound-verb former. A mechanical "avoid passives" rule flags the wrong things.
- **Bureaucratic nominalization.** «مورد استفاده قرار دادن» hides both the action and the actor.
- **Half-space (نیم‌فاصله, ZWNJ).** Inconsistent use breaks search, sorting, and screen readers.
- **Bidi breakage.** English terms, code, and numbers inside RTL prose display in the wrong order
  when they are not isolated.

No official controlled-Persian standard exists. This skill assembles one from the authorities that
do: دستور خطّ فارسی (1401 revision), فرهنگ املایی خطّ فارسی, اصول و ضوابط واژه‌گزینی, the Microsoft
fa-IR style guide, and working Persian documentation practice.

## Install (Claude Code)

Clone the repo, then link it into your skills directory:

```bash
git clone <this-repo> ~/projects/asd-ste100
ln -s ~/projects/asd-ste100 ~/.claude/skills/persian-technical-writing
```

Or copy it into a single project instead:

```bash
mkdir -p .claude/skills && cp -R ~/projects/asd-ste100 .claude/skills/persian-technical-writing
```

## Install (other agents)

The rules are agent-agnostic; only the packaging differs. Most agents take plain markdown, so
`rules/system-prompt.md` covers them all. Copy it and rename it to whatever your tool expects:

| Agent / tool | Copy | To |
|---|---|---|
| Codex, Aider, Zed, Jules, Gemini CLI, Amp | `rules/system-prompt.md` | `AGENTS.md` |
| Cline, Roo Code | `rules/system-prompt.md` | `.clinerules/persian-technical-writing.md` |
| GitHub Copilot | `rules/system-prompt.md` | `.github/copilot-instructions.md` |
| Any chat model, Custom GPT, Gem, API | `rules/system-prompt.md` | the system prompt |
| Cursor | `rules/cursor.mdc` | `.cursor/rules/persian-technical-writing.mdc` |
| Windsurf | `rules/windsurf-persian-script.md` | `.windsurf/rules/persian-script.md` |
| | `rules/windsurf-persian-structure.md` | `.windsurf/rules/persian-structure.md` |

Only two tools need their own file: Cursor requires MDC frontmatter, and Windsurf caps a rule file
at ~6,000 characters, so the ruleset splits in two there. `rules/README.md` has the per-target notes:
why the Cursor rule is agent-requested rather than always-on, how to scope the Copilot file to
Persian paths, and what the Windsurf condensation drops. Using it from code:

```python
RULES = open("rules/system-prompt.md", encoding="utf-8").read()
client.messages.create(model="claude-sonnet-5", max_tokens=2000,
                       system=RULES + "\n\nMode: Strict.",
                       messages=[{"role": "user", "content": persian_text}])
```

The ruleset names no vendor and needs no tools, so the same string works as an OpenAI `system`
message or a Gemini `system_instruction`.

## Use

Claude invokes the skill on its own when you ask for Persian text to be simplified, or you can call
it by name:

```
/persian-technical-writing

این پاراگراف را ساده کن: ...
```

Typical prompts that trigger it:

- «این متن را ساده‌نویسی کن» / «فارسی روان بنویس» / «ویرایش فنی»
- "rewrite this Persian doc so an agent cannot misread it"
- "normalize the ZWNJ and digits in this Persian page"

### Two modes

| Mode | For | Rules applied |
|---|---|---|
| **Strict (سخت‌گیرانه)** | Procedures, error messages, tool and function descriptions, inter-agent instructions, safety text | Everything: length caps, the semicolon ban, one-word-one-meaning |
| **Flavored (روان)** | READMEs, blog-style docs, changelogs, explanatory prose | Structural and script rules in full; lexical rules advisory; ؛ permitted sparingly |

**Script mechanics are never optional.** ZWNJ, Persian codepoints (ی U+06CC, ک U+06A9), Persian
digits, punctuation, and bidi isolation apply in both modes. They are correctness rules, not style
preferences.

### Output

By default the skill prints the rewritten Persian text and nothing else: no preamble, no violation
count. Ask for the reasoning («تفاوت‌ها را نشان بده», "show the diff", "which rules did it break")
and it returns a rule table instead:

| قاعدهٔ نقض‌شده | متن اصلی | متن ساده‌شده |
|---|---|---|
| اسم‌سازی اداری | «مورد بررسی قرار خواهد گرفت» | «بررسی می‌شود» |
| زنجیرهٔ اضافه (۴+) | «تنظیمات صفحهٔ مدیریت کاربران سامانه» | «تنظیمات مدیریت کاربران در سامانه» |

## What it checks

Eight mechanical checks. Each one points at an exact word or character:

1. Bureaucratic nominalization: «مورد … قرار دادن», «به عمل آوردن», «اقدام به … نمودن»
2. Synonym rotation: کاربر / مشتری / استفاده‌کننده for one referent
3. می‌باشد register: می‌باشد, بدین‌وسیله, مذکور, ذیل
4. که-chains and و-chains: several ideas in one sentence
5. Ezafe pile-ups: 4+ chained links
6. Script hygiene: Arabic ي/ك, Latin digits in prose, «می رود», «میرود», «کتابها»
7. Hedge stacking: «شاید بتوان گفت که احتمالاً ممکن است»
8. Bidi breakage: unmarked English, code, or numbers inline

## Scope

**Will:** rewrite bureaucratic or ambiguous Persian into short, single-meaning, active sentences;
normalize script mechanics in every mode; preserve every fact, condition, scope qualifier, and hedge.

**Will not:** claim Farhangestan certification; ban compound (light-verb) constructions; flag every
شدن as passive; simplify creative or marketing copy; drop a safety condition to shorten a sentence;
or make weak content true. Controlled Persian fixes the form of a text, not its substance.

## Files

| Path | What it is |
|---|---|
| `SKILL.md` | **The single source of truth**: rules, scan checklist, process, output format, boundaries. Also the Claude Code skill |
| `references/research-report.md` | The cited research behind every rule: which claims were adversarially verified, which are single-sourced, and which were refuted |
| `rules/` | The same ruleset packaged for other agents |
| `AGENTS.md` | Instructions for agents working *on* this repo |

`SKILL.md` is canonical and `rules/` holds hand-maintained copies of it. Change a rule in `SKILL.md`
and mirror it into `rules/`. `rules/system-prompt.md` is the full text verbatim, so it is a straight
copy; the two Windsurf files are condensed to fit that tool's character cap and need the
condensation reapplied.

The research report is deliberately honest about confidence: two claims that would have supported the
sentence-length caps were **refuted** in verification, so those caps are documented as design
decisions carried over from STE, not as Persian-validated metrics.

## Precedent

Adapting a controlled language across languages is not new. GIFAS built «le Français Rationalisé» to
pair with AECMA Simplified English, with a dual goal: easy mapping to Simplified English *and* better
readability for native French readers. A working group ran from 1985 to publication in 1999. This
skill takes the same position for Persian: native readers first.

## License

MIT.
