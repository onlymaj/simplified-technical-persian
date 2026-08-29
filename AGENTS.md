# AGENTS.md

Instructions for agents working **on** this repository.

> Looking for the ruleset to install in *your* project? That is `rules/system-prompt.md`, not this
> file. See `rules/README.md` for the install matrix.

## What this repo is

A controlled-language ruleset for Persian (Farsi) technical writing, adapted from ASD-STE100.
It ships as a Claude Code skill (`SKILL.md`) and as rule files for other agents (`rules/`).
There is no application code.

## Single source of truth

`SKILL.md` holds every rule. Everything in `rules/` is a copy of it, kept in sync by hand.

- After changing `SKILL.md`, mirror the change into `rules/`. Every file there carries a banner
  saying so.
- `rules/system-prompt.md` is the full ruleset verbatim, minus the frontmatter — a straight copy.
  `rules/cursor.mdc` is the same text under MDC frontmatter.
- The two `rules/windsurf-*.md` files are condensed to fit Windsurf's ~6,000 character cap. If you
  add a rule, re-check both are still under it. `persian-script.md` carries section D in full;
  `persian-structure.md` carries sections A–C with the "Don't" and "Why" columns dropped, and
  points at `persian-script.md` by name for the script-hygiene pass.

## Writing in this repo

`README.fa.md` is written under the ruleset this repo defines, in Flavored mode. If you edit it,
follow those rules: ZWNJ (نیم‌فاصله) inside words and never between them, Persian codepoints
ی (U+06CC) and ک (U+06A9) rather than Arabic ي/ك, Persian digits ۰–۹ in prose, «» guillemets,
and هٔ for the ezafe after silent ه. The same applies to any Persian added to `README.md`.

The English prose in `README.md` and `SKILL.md` is deliberately plain and claim-checked. Do not add
marketing adjectives — the ruleset bans them, so the repo should not use them.

## Claims and sourcing

`references/research-report.md` labels every claim `[verified]`, `[single-source]`, or `[refuted]`.
Do not promote a rule in `SKILL.md` to a stronger claim than its label supports, and do not cite the
two refuted claims about Persian readability metrics. If you add a rule, add its source and
confidence label to the report.

The repo must not claim Farhangestan (فرهنگستان) certification. It follows دستور خطّ فارسی and
اصول و ضوابط واژه‌گزینی as authorities; official term approval belongs to Farhangestan alone.
