<!-- Portable copy of the ruleset in SKILL.md. If you change a rule, change it in both. -->

# Simplified Technical Persian (فارسی فنی ساده)

This ruleset adapts the discipline of ASD-STE100 (Simplified Technical English) to Persian for Iranian audiences. STE removes the two biggest sources of misreading in English: words with more than one meaning, and sentences with more than one possible structure. Persian has its own, different sources of misreading — invisible ezafe links, chained اضافه constructions, polysemous شدن, bureaucratic nominalizations (مورد استفاده قرار دادن), inconsistent half-space (نیم‌فاصله) usage, and mixed-direction text that breaks when English terms or code sit inside RTL prose.

A controlled language adapted from STE must serve native readers first, not mirror English rules verbatim. That is the documented lesson of GIFAS's "Français Rationalisé," the French aerospace controlled language built to pair with Simplified English: its dual goal was easy translation *and* better readability for native French readers. This ruleset takes the same position for Persian: every rule below is stated in Persian-grammar terms, not as a translation of an English rule.

## When to Apply These Rules

- Persian text (documentation, help-center article, error message, UI string, prompt, inter-agent instruction) reads as dense, bureaucratic (اداری), or ambiguous.
- Persian text will be consumed by another agent, a translation pipeline, a screen reader, or a reader with limited technical background, and misparsing has a real cost.
- You are writing Persian docs or knowledge-base content for an Iranian audience and want consistent orthography, terminology, and sentence structure before publication.
- You want a **before/after** comparison showing which rule was violated and how the rewrite fixes it. Ask for it — the default output is the rewritten text alone (see Output Format).

This ruleset is not for creative or marketing copy — controlled Persian is deliberately flat and literal. Do not apply it to text where voice, nuance, or persuasion is the point.

## Two Modes

Pick a mode before rewriting. If the user does not say which, infer from the text type and state the choice in one line.

**Strict (سخت‌گیرانه)** — procedures, error messages, tool and function descriptions, inter-agent instructions, safety text. Anywhere a wrong reading has a cost. Apply every rule below, including length caps, the semicolon ban, and one-word-one-meaning discipline.

**Flavored (روان)** — READMEs, blog-style docs, changelogs, explanatory prose. Apply the structural rules and the script-mechanics rules in full; treat the lexical rules as advisory. In this mode the Persian semicolon (؛) is permitted sparingly between closely related independent clauses, because Persian editorial convention actively prescribes it — but a ؛ is still a signal that the sentence may deserve splitting.

**Script mechanics are never optional.** The orthography and bidi rules (ZWNJ, character codepoints, digits, punctuation marks, direction markup) apply in both modes. They are correctness rules, not style preferences: getting them wrong changes how software, search, and screen readers process the text.

## Source and Scope

No official "controlled Persian" standard exists — surveys of controlled natural languages list Easy Japanese and Français fondamental but no Persian entry. This ruleset therefore assembles its rules from the authorities that do exist, in priority order:

1. **دستور خطّ فارسی (Dastur-e Khatt-e Farsi), revised edition 1401 (2022/23)** — the Academy of Persian Language and Literature's (فرهنگستان) official orthography standard, ratified by the President of Iran and legally promulgated. Its 1401 revision exists chiefly to regularize spacing in compounds (جدانویسی/پیوسته‌نویسی) — the half-space problem. This is the binding baseline for all orthography rules below. Persian script is Iran's official script under Article 15 of the constitution.
2. **فرهنگ املایی خطّ فارسی (final version 1394)** — the companion word-level spelling dictionary, for resolving individual words.
3. **اصول و ضوابط واژه‌گزینی (3rd ed., 1388)** — Farhangestan's terminology-selection principles, the normative reference for Persian technical term choice.
4. **Microsoft Persian (fa-IR) localization style guide** — the most complete practitioner rulebook for Persian software/documentation text (register, ZWNJ, punctuation, tense, digits).
5. **Persian Wikipedia's Manual of Style (شیوه‌نامه)** and working Persian knowledge bases (ArvanCloud docs, WikiShia) — evidence of how professional Persian documentation actually applies these standards.

Where these authorities conflict (they occasionally do — e.g., هٔ vs ه‌ی for the ezafe after silent ه), this ruleset picks one form, says so, and applies it consistently. Consistency within a document outranks any single authority.

## Core Rewrite Rules

### A. Structural rules — apply these

| Rule | Do | Don't |
|---|---|---|
| Active voice, named actor | «سامانه فایل را حذف می‌کند.» — actor stated, فعل معلوم | «فایل حذف می‌شود.» — unless the actor is genuinely unknown or irrelevant. Operationalize as: prefer the کردن-form of a compound verb over its شدن-form when the actor matters («نصب کنید» not «نصب می‌شود») |
| شدن is not automatically passive | Flag only true passives (past participle + شدن with a demoted actor) | Mechanically flagging every شدن — it is also a main verb ("become") and forms active/inchoative compounds («روشن شد» = "it turned on," not a passive) |
| Imperative for instructions | Polite-plural imperative, the working convention of Iranian docs: «فایل را باز کنید. خط ۳ را بخوانید.» | Passive or impersonal instruction («فایل باز شود»، «لازم است فایل باز گردد») |
| One instruction per sentence | «فایل را باز کنید. خط ۳ را بخوانید.» | «فایل را باز کرده و خط ۳ را بخوانید و بررسی کنید که مطابقت دارد یا خیر.» |
| Sentence length | ≤20 words for instructions/procedures, ≤25 for descriptions (carried over from STE as a design cap; short sentences and roughly one verb per sentence are also the fa-IR localization guidance) | Long chains of clauses linked by «و» or nested «که» clauses |
| Verb-final discipline | Keep the sentence short enough that the reader reaches the final verb quickly; keep compound-verb parts adjacent («فایل را دانلود کنید») | Long insertions between subject and final verb; separating a compound verb's noun from its light verb with heavy material |
| Placement of را | Immediately after its object: «کتابی را که آورده بود، برد.» | را deferred to the end of a relative clause: «کتابی که آورده بود را برد.» |
| Ezafe chains (تتابع اضافات) ≤3 links | Break with a preposition or restructure: «بررسی دقیق گزارش‌های خطا در نسخهٔ جدید سرور» | 4+ chained ezafes: «بررسی دقیق گزارش‌های خطای سرور نسخهٔ جدید» — the ezafe is usually invisible in script and each link is multiply ambiguous, so chains are the Persian analog of English noun clusters |
| No semicolon in Strict mode | Split into separate sentences | Any ؛ in Strict mode. This deliberately overrides native editorial convention, which prescribes ؛ between independent clauses — flag the departure once per document. In Flavored mode ؛ is allowed sparingly |
| No mid-sentence ellipsis or colon | Complete the sentence; the Persian verb must end it | «...» or «:» inserted before the final verb — it strands the verb and breaks the sentence's one legal parse |
| No ellipsis of required words | Keep subject, verb, and را explicit even if longer | Dropping words to save space, which in verb-final Persian often makes two parses possible |
| Keep modality | «درخواست ممکن است ناموفق بوده باشد.» stays «ممکن است» | Promoting a hedge to a fact («درخواست ناموفق بود.») or inventing certainty the source did not state. Hedges (شاید، احتمالاً، ممکن است) are content |
| Paragraph limits | One topic per paragraph, ≤6 sentences | Multi-topic paragraphs |
| Lists for sequences | Numbered list for 3+ steps or conditions | A sequence buried in one prose sentence |

### B. Lexical rules — direction of travel

| Rule | Do | Don't | Why it is weaker |
|---|---|---|---|
| One word, one meaning | Pick one verb per action and reuse it («بررسی کنید» every time — never rotate بررسی/چک/کنترل/وارسی for the same action) | Synonym rotation across a document | Consistency is checkable; which synonym is "the approved one" has no official dictionary. Documented failure mode of Persian term-formation: related terms in a family translated inconsistently (عدم انسجام خوشهٔ واژگانی) |
| Verb, not nominalization | «استفاده کنید»، «تحلیل کنید» | «مورد استفاده قرار دهید»، «به تحلیل بپردازید»، «اقدام به نصب نمایید» — the bureaucratic wrapper hides the action and the actor. This is the single highest-value lexical fix in Persian technical prose |
| Compound verbs: regulate, don't ban | Use the plain, established compound («کلیک کنید»، «ذخیره کنید») and treat it as one lexical unit in the glossary | Banning light-verb constructions outright — کردن-compounds are Persian's default verb-formation strategy, not an avoidable idiom like English phrasal verbs | Most Persian verbal meanings have no simple-verb alternative |
| Formal standard register (زبان معیار) | «است»، «انجام می‌دهد»، «می‌رود» | Colloquial forms («می‌ره»، «چک کن ببین») and bureaucratic archaisms: می‌باشد → است؛ ذیل → زیر؛ فوق → بالا؛ لذا → بنابراین؛ الزاماً → حتماً | Register is a spectrum; the line between plain-formal and stiff-formal needs judgment |
| No Arabic-syntax calques | «مقالات مربوط»، «روش یادشده» | «مقالات مربوطه»، «روش مذکوره» — Arabic agreement morphology on Persian text | Some calques are fully lexicalized; flag only productive ones |
| No marketing adjectives | State the measurement | بی‌نظیر، قدرتمند، یکپارچه، پیشرفته، سریع‌ترین — delete or replace with the number that earns the claim | — |

### C. Terminology rules

| Rule | Do | Don't |
|---|---|---|
| Dual strategy (the working Iranian-docs norm) | Use the established Farhangestan-style Persian term where one has real currency («فضای ابری»، «شبکهٔ توزیع محتوا»); keep established technical terms in Latin script inline (API، DNS، CDN، SSD) | Forcing an unfamiliar coinage on a specialist audience, or transliterating Latin-script terms that Iranian practitioners read natively in English |
| First-use pairing | Pair a Persian term with its English original in parentheses on first use: «پردازش لبه (Edge Computing)» | Introducing a Persian coinage with no anchor to the term the reader will meet elsewhere |
| Calibrate by audience tier | General-audience docs: prefer approved Persian equivalents. Specialist docs: English terms acceptable — this mirrors Farhangestan's own priority tiers (عمومی، پایه، مشترک، تخصصی) | One fixed policy for all audiences |
| Prefer derivable equivalents | Choose Persian terms that can inflect and form derivatives within Persian word-formation patterns (a stated Farhangestan criterion) | Frozen transliterations that block derivation |
| Family consistency | Translate a term family consistently (اشکال‌زدایی/اشکال‌زدا؛ not اشکال‌زدایی alongside دیباگر for the same docs) | Mixing coinage and loanword within one term family |
| Never reuse Arabic localizations | Validate Persian terminology separately | Assuming Arabic translations of UI/tech terms work for Persian audiences |

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

## Scan Checklist

Each item is mechanical: you can point at the exact word or character that breaks the rule. Scan for all eight before rewriting.

1. **Bureaucratic nominalization** — «مورد ... قرار دادن»، «به عمل آوردن»، «اقدام به ... نمودن». Fix: the direct compound verb.
2. **Synonym rotation** — the same referent gets several names (کاربر/مشتری/استفاده‌کننده). Fix: one name, every time.
3. **می‌باشد register** — می‌باشد، بدین‌وسیله، مذکور، ذیل. Fix: است، این، یادشده، زیر.
4. **که-chains and و-chains** — several ideas nested or coordinated into one sentence. Fix: one idea per sentence.
5. **Ezafe pile-ups** — 4+ chained ezafe links. Fix: break with a preposition or split the sentence.
6. **Script hygiene** — Arabic ي/ك، Latin digits in prose, full spaces where ZWNJ belongs (می رود), missing ZWNJ (میرود، کتابها after ه). Fix: normalize; this pass is safe to apply mechanically.
7. **Hedge stacking** — «شاید بتوان گفت که احتمالاً ممکن است». Fix: state the claim once, or delete it.
8. **Bidi breakage** — English terms, numbers, or code inline with no direction handling. Fix: markup or reorder.

## Process

1. Pick the mode (Strict or Flavored). Say which only when the user asked for the rule table — see Output Format.
2. Read the input once for meaning — do not start rewriting before you know what the text must still say afterward.
3. Run the script-mechanics pass first (Section D + checklist item 6). It is mechanical, safe, and applies in both modes.
4. Walk the text sentence by sentence. Flag every violation from the rule tables and the checklist. In Flavored mode, flag lexical rules but do not enforce them.
5. Rewrite each flagged sentence, preserving the original meaning exactly. If a rewrite would drop necessary precision (a safety condition, a scope qualifier, a number), keep the longer phrasing and flag it.
   - **Check modality before committing.** Hedges carry the author's confidence, and confidence is content. A shorter sentence that upgrades «ممکن است ناموفق بوده باشد» to «ناموفق بود» is not a simplification — it is a different claim.
   - **Check شدن before flagging.** Only rewrite genuine passives with a knowable actor. Inchoatives («فعال شد») and main-verb شدن are not passives.
   - Never add a fact the source did not state.
6. Output the rewritten text (see Output Format). Keep the mode choice and rule analysis internal unless asked.
7. If the input already complies, say so — do not force changes onto compliant text.

## Output Format

**Default: the rewritten Persian text, and nothing else.** Print the simplified text on its own — no preamble, no mode announcement, no violation count, no closing offer.

The one permitted addition: if step 5 kept a longer phrasing on purpose, add a single line after the text, prefixed «بدون تغییر:» (or `Kept as-is:` if the conversation is in English), naming the phrase and the precision that would have been lost.

**On request: the rule table.** When the user asks to see the reasoning — «تفاوت‌ها را نشان بده»، "show the diff", "which rules did it break" — output this table instead:

```markdown
| قاعدهٔ نقض‌شده | متن اصلی | متن ساده‌شده |
|---|---|---|
| اسم‌سازی اداری | «مورد بررسی قرار خواهد گرفت» | «بررسی می‌شود» |
| زنجیرهٔ اضافه (۴+) | «تنظیمات صفحهٔ مدیریت کاربران سامانه» | «تنظیمات مدیریت کاربران در سامانه» |

Mode: Strict. ۷ مورد یافت شد.
```

Follow the table with a one-line note on anything deliberately **not** simplified, and why.

## Boundaries

**Will:**
- Rewrite ambiguous or bureaucratic Persian into short, single-meaning, active-voice, verb-final-friendly sentences.
- Normalize script mechanics (ZWNJ, codepoints, digits, punctuation, bidi) in every mode.
- Return the rewritten text alone by default, and name the rules applied when asked.
- Preserve every fact, condition, scope qualifier, and hedge in the original.
- Suggest a one-line glossary entry for domain terms that must stay.

**Will not:**
- Claim Farhangestan certification. This ruleset follows دستور خطّ فارسی and اصول و ضوابط واژه‌گزینی as authorities, but official term approval is Farhangestan's alone — check فرهنگ واژه‌های مصوب for binding equivalents.
- Ban compound (light-verb) verbs. They are Persian's default verbal strategy; the rule is *regulate and keep adjacent*, not *remove*.
- Flag every شدن as passive, or convert legitimate passives whose actor is genuinely unknown.
- Simplify creative, marketing, or persuasive copy.
- Silently drop a safety condition or hedge to shorten a sentence — it will flag the trade-off instead.
- Force Persian coinages onto specialist audiences, or transliterate established Latin-script technical terms against Iranian practitioner norms.
- Make weak content true or useful. Controlled Persian fixes the *form* of a text, not its substance. A hollow paragraph rewritten under these rules becomes a clean, short, well-punctuated hollow paragraph — say so instead of polishing it.
- Shorten past the point of clarity. The goal is removing ambiguity, not cutting words; stop when the sentence has one legal parse, not when it is shortest.

## Additional Resources

- The research behind every rule above — which claims were adversarially verified, which
  are single-sourced, and which were refuted — is in `references/research-report.md` of the
  asd-ste100-fa repository.
- Official sources: دستور خطّ فارسی ویراست ۱۴۰۱ (apll.ir)؛ فرهنگ املایی خطّ فارسی ۱۳۹۴؛ اصول و ضوابط واژه‌گزینی (terminology.apll.ir)؛ Microsoft fa-IR Style Guide؛ شیوه‌نامهٔ ویکی‌پدیای فارسی.
