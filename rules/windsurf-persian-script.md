---
trigger: model_decision
description: Persian orthography and bidi correctness — ZWNJ, Persian codepoints, digits, punctuation, dates, RTL/LTR isolation. Apply to any Persian text.
---

<!-- Portable copy of the ruleset in SKILL.md. If you change a rule, change it in both. -->

# Simplified Technical Persian (فارسی فنی ساده)

### D. Script mechanics — always apply (no English STE counterpart)

These are the Persian-only rules. The 1401 revision of دستور خط exists mainly because of the first row.

| Rule | Do | Don't |
|---|---|---|
| Half-space (نیم‌فاصله, ZWNJ U+200C) | Inside one word: ZWNJ where joining must break, never a full space. Between two words: exactly one full space, never ZWNJ. Mandatory ZWNJ: می‌/نمی‌ + verb («می‌رود»)؛ plural ها («کتاب‌ها»، obligatory after silent ه: «خانه‌ها»)؛ perfect suffixes ام/ای/اید/اند («رفته‌اند»)؛ comparatives تر/ترین («بزرگ‌تر» — exceptions: بهتر، کمتر، بیشتر)؛ noun/adjective compounds («دانش‌آموز», «کتاب‌فروشی») | «می رود» (full space inside a word)، «میرود» (joined)، «کتابها» after ه، ZWNJ between separate words |
| Ezafe after silent ه | Write هٔ («خانهٔ بزرگ»، «نسخهٔ جدید») per دستور خط. If the house style uses ه‌ی («نسخه‌ی جدید»، the ArvanCloud convention), keep it — but one form per document | Mixing هٔ and ه‌ی, or omitting the marker where the ezafe is not recoverable |
| Persian codepoints only | ی (U+06CC) and ک (U+06A9) | Arabic ي (U+064A) and ك (U+0643) — they look similar, break search and sorting, and are machine-detectable. No tanwin on Persian words (لطفاً is Arabic-derived and keeps it; گاهاً is wrong — use گاهی) |
| Persian digits | ۰–۹ in Persian prose («۳۰ ثانیه»)؛ decimal separator ممیز (٫ or the slash convention: ۲۱/۵)؛ thousands separator ٬؛ ٪ attached to the numeral in technical text, «درصد» spelled out in general prose | Latin digits 0–9 or Arabic digits ٠–٩ inside Persian sentences (Latin digits stay only inside Latin-script runs: code, version strings, URLs) |
| Singular after numerals | «۲ کتاب»، «۵ کاربر» | «۲ کتاب‌ها» — nouns after numerals and measurement units stay singular |
| Persian punctuation | ، ؛ ؟ and «» guillemets (the Iran national-standard quotation marks, even around embedded English terms). No space before a pause mark, one space after. Paired marks: no space toward content, one space outside | English , ; ? "" in Persian prose؛ hyphenation of Persian words (avoid entirely)؛ em dashes (prefer parentheses) |
| Dates and calendar | Solar Hijri (هجری خورشیدی) for Iranian audiences: «۲۲ خرداد ۱۴۰۴» — numeral day, month name in words, numeral year. Ordinals in words («هشتم» not «۸ام»). Add the Gregorian date in parentheses when the doc has non-Iranian readers | «۱۴۰۴/۳/۲۲» in running prose؛ Gregorian-only dates for an Iranian audience |
| Bidi isolation | Wrap every LTR run (English term, code, path, version) in direction markup: `<span dir="ltr">`، `<bdi>`، or `dir="auto"` for unknown content. Code blocks: `<pre dir="ltr"><code>`. In plain text, reorder the sentence so LTR runs do not sit adjacent to numbers or punctuation | Unmarked English/code inline in RTL text — adjacent numbers, leading/trailing punctuation, and consecutive LTR phrases display in the wrong order. Do not rely on invisible Unicode control characters where markup is available |
