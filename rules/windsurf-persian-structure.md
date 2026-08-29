---
trigger: model_decision
description: Use when Persian (Farsi) text for Iranian audiences must be parsed without a human to resolve ambiguity — documentation, knowledge-base articles, error messages, tool descriptions, inter-agent instructions, help-center content — and misreading has a real cost, or when Persian text reads as dense, bureaucratic, or easy to misparse.
---

<!-- Portable copy of the ruleset in SKILL.md. If you change a rule, change it in both. -->

# Simplified Technical Persian (فارسی فنی ساده)

## Two Modes

Pick a mode before rewriting. If the user does not say which, infer from the text type and state the choice in one line.

**Strict (سخت‌گیرانه)** — procedures, error messages, tool and function descriptions, inter-agent instructions, safety text. Anywhere a wrong reading has a cost. Apply every rule below, including length caps, the semicolon ban, and one-word-one-meaning discipline.

**Flavored (روان)** — READMEs, blog-style docs, changelogs, explanatory prose. Apply the structural rules and the script-mechanics rules in full; treat the lexical rules as advisory. In this mode the Persian semicolon (؛) is permitted sparingly between closely related independent clauses, because Persian editorial convention actively prescribes it — but a ؛ is still a signal that the sentence may deserve splitting.

**Script mechanics are never optional.** The orthography and bidi rules (ZWNJ, character codepoints, digits, punctuation marks, direction markup) apply in both modes. They are correctness rules, not style preferences: getting them wrong changes how software, search, and screen readers process the text.

## Core Rewrite Rules

### A. Structural rules — apply these

| Rule | Do |
|---|---|
| Active voice, named actor | «سامانه فایل را حذف می‌کند.» — actor stated, فعل معلوم |
| شدن is not automatically passive | Flag only true passives (past participle + شدن with a demoted actor) |
| Imperative for instructions | Polite-plural imperative, the working convention of Iranian docs: «فایل را باز کنید. خط ۳ را بخوانید.» |
| One instruction per sentence | «فایل را باز کنید. خط ۳ را بخوانید.» |
| Sentence length | ≤20 words for instructions/procedures, ≤25 for descriptions (carried over from STE as a design cap; short sentences and roughly one verb per sentence are also the fa-IR localization guidance) |
| Verb-final discipline | Keep the sentence short enough that the reader reaches the final verb quickly; keep compound-verb parts adjacent («فایل را دانلود کنید») |
| Placement of را | Immediately after its object: «کتابی را که آورده بود، برد.» |
| Ezafe chains (تتابع اضافات) ≤3 links | Break with a preposition or restructure: «بررسی دقیق گزارش‌های خطا در نسخهٔ جدید سرور» |
| No semicolon in Strict mode | Split into separate sentences |
| No mid-sentence ellipsis or colon | Complete the sentence; the Persian verb must end it |
| No ellipsis of required words | Keep subject, verb, and را explicit even if longer |
| Keep modality | «درخواست ممکن است ناموفق بوده باشد.» stays «ممکن است» |
| Paragraph limits | One topic per paragraph, ≤6 sentences |
| Lists for sequences | Numbered list for 3+ steps or conditions |

### B. Lexical rules — direction of travel

| Rule | Do |
|---|---|
| One word, one meaning | Pick one verb per action and reuse it («بررسی کنید» every time — never rotate بررسی/چک/کنترل/وارسی for the same action) |
| Verb, not nominalization | «استفاده کنید»، «تحلیل کنید» |
| Compound verbs: regulate, don't ban | Use the plain, established compound («کلیک کنید»، «ذخیره کنید») and treat it as one lexical unit in the glossary |
| Formal standard register (زبان معیار) | «است»، «انجام می‌دهد»، «می‌رود» |
| No Arabic-syntax calques | «مقالات مربوط»، «روش یادشده» |
| No marketing adjectives | State the measurement |

### C. Terminology rules

| Rule | Do |
|---|---|
| Dual strategy (the working Iranian-docs norm) | Use the established Farhangestan-style Persian term where one has real currency («فضای ابری»، «شبکهٔ توزیع محتوا»); keep established technical terms in Latin script inline (API، DNS، CDN، SSD) |
| First-use pairing | Pair a Persian term with its English original in parentheses on first use: «پردازش لبه (Edge Computing)» |
| Calibrate by audience tier | General-audience docs: prefer approved Persian equivalents. Specialist docs: English terms acceptable — this mirrors Farhangestan's own priority tiers (عمومی، پایه، مشترک، تخصصی) |
| Prefer derivable equivalents | Choose Persian terms that can inflect and form derivatives within Persian word-formation patterns (a stated Farhangestan criterion) |
| Family consistency | Translate a term family consistently (اشکال‌زدایی/اشکال‌زدا؛ not اشکال‌زدایی alongside دیباگر for the same docs) |
| Never reuse Arabic localizations | Validate Persian terminology separately |

## Scan Checklist

Each item is mechanical: you can point at the exact word or character that breaks the rule. Scan for all eight before rewriting.

1. **Bureaucratic nominalization** — «مورد ... قرار دادن»، «به عمل آوردن»، «اقدام به ... نمودن». Fix: the direct compound verb.
2. **Synonym rotation** — the same referent gets several names (کاربر/مشتری/استفاده‌کننده). Fix: one name, every time.
3. **می‌باشد register** — می‌باشد، بدین‌وسیله، مذکور، ذیل. Fix: است، این، یادشده، زیر.
4. **که-chains and و-chains** — several ideas nested or coordinated into one sentence. Fix: one idea per sentence.
5. **Ezafe pile-ups** — 4+ chained ezafe links. Fix: break with a preposition or split the sentence.
6. **Script hygiene** — Arabic ي/ك، Latin digits in prose، ZWNJ errors. Apply the companion rule file `persian-script.md`; that pass is safe to apply mechanically.
7. **Hedge stacking** — «شاید بتوان گفت که احتمالاً ممکن است». Fix: state the claim once, or delete it.
8. **Bidi breakage** — English terms, numbers, or code inline with no direction handling. Fix: markup or reorder.
