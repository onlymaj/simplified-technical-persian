# Research Report: Adapting ASD-STE100 to Persian Technical Writing

**Question:** What are the best practices for technical writing, documentation, and knowledge-base writing in Persian for Iranian audiences, and how should a controlled-language standard modeled on ASD-STE100 be adapted for Persian?

**Method:** Deep-research workflow (2026-08-23) — 5 parallel search angles, 22 sources fetched, 96 claims extracted, top 25 adversarially verified with 3 independent refutation votes each. **17 claims confirmed (mostly 3-0), 2 refuted, 6 left unverified** when the verification/synthesis agents hit the session usage limit; this report was synthesized manually from the saved workflow journal. Confidence labels: **[verified]** = survived 3-vote adversarial check; **[single-source]** = extracted from a fetched source but not adversarially verified; **[refuted]** = killed 0-3.

---

## 1. The authority stack: what a Persian style standard should defer to

- **[verified 3-0]** دستور خطّ فارسی (Dastur-e Khatt-e Farsi) is not merely academic guidance: it was ratified by the Academy (فرهنگستان) and given official status through endorsement by the President of Iran, who chairs the Academy. It is *the* authoritative reference for Persian orthography. ([apll.ir](https://apll.ir/1401/12/15/%D8%AF%D8%B3%D8%AA%D9%88%D8%B1-%D8%AE%D8%B7%D9%91-%D9%81%D8%A7%D8%B1%D8%B3%DB%8C/))
- **[verified 3-0]** The single most important driver of its 1401 (2022/23) revision was regularizing spacing (فاصله‌گذاری) in compounds — rule-governing detached (جدانویسی, half-space/ZWNJ) vs attached (پیوسته‌نویسی) writing. Half-space rules are the core Persian-specific orthography issue. (apll.ir)
- **[verified 3-0]** The revised edition's topics: definitions of space types; spacing of prefixes/prefix-like elements; spacing in compound prepositions and conjunctions; general rule revision. (apll.ir)
- **[single-source]** Persian script is Iran's official script under Article 15 of the constitution; all official documents and textbooks must use it — giving Farhangestan rules legal-institutional weight. The Academy's stated design philosophy is moderation: it refused rules whose enforcement would generate long exception lists. (apll.ir)
- **[single-source]** Companion references: فرهنگ املایی خطّ فارسی (final version 1394) for word-level spelling; اصول و ضوابط واژه‌گزینی (3rd ed. 1388) for terminology. (apll.ir, vokalapress.ir)
- **[verified 3-0]** Working Persian knowledge bases anchor their house style to Farhangestan norms rather than inventing orthography: WikiShia's editorial manual explicitly adopts دستور خط as its baseline. ([fa.wikishia.net](http://fa.wikishia.net/view/%D9%88%DB%8C%DA%A9%DB%8C%E2%80%8C%D8%B4%DB%8C%D8%B9%D9%87:%D8%B4%DB%8C%D9%88%D9%87%E2%80%8C%D9%86%D8%A7%D9%85%D9%87_%D9%88%DB%8C%D8%B1%D8%A7%DB%8C%D8%B4%DB%8C)) Virastaran (professional editing institute) treats it as the single binding standard and applies it to 31,767 dictionary entries. ([virastaran.net](https://virastaran.net/khat/))

## 2. Precedent: STE has been adapted to another language before

- **[single-source]** The French aerospace association GIFAS built «le Français Rationalisé» (Rationalized French), a controlled French explicitly designed to pair with AECMA Simplified English — with a **dual goal: easy mapping to Simplified English AND better readability for native French readers**. A dedicated working group ran from 1985 to publication in 1999 — cross-language controlled-language adaptation is sustained institutional work, not a one-shot rule translation. (Technical Communication 46(2), Barthe et al., 1999)
- **[single-source]** Controlled-natural-language surveys (Wikipedia CNL inventory) list Easy Japanese and Français fondamental but **no controlled or simplified Persian** — no established controlled-Persian standard is documented. ASD-STE100 is the canonical readability-type CNL. IETF's BCP 47 reserves the variant subtag `simple`, so a simplified Persian could be formally tagged (e.g., `fa-simple`).

## 3. Which English STE rules transfer directly

- **[single-source, Microsoft fa-IR guide]** Microsoft's official Persian style guide directs writers to **avoid passive voice and keep sentences short**; for accessibility, roughly **one verb per sentence** and short paragraphs — directly supporting STE's active-voice, sentence-length, and one-instruction-per-sentence rules in Persian. It also prescribes **simple present instead of future tense** (literal future translations produce odd Persian) — the Persian analog of STE's simple-tenses rule. ([fas-irn-StyleGuide.pdf](https://download.microsoft.com/download/3/e/c/3ec58a9a-70ff-4a31-8cfd-d185983111be/fas-irn-StyleGuide.pdf))
- **[single-source, ArvanCloud docs]** Iranian docs practice confirms imperative instructions: ArvanCloud's Persian docs address the reader with second-person-plural imperatives in active voice (بسازید، حذف کنید، اجرا کنید) — STE's "active + imperative" rule transfers as polite-plural imperatives, not passive شدن constructions. ([docs.arvancloud.ir](https://docs.arvancloud.ir/fa/))
- **[verified 3-0]** Persian's structural distance from English is real but bounded: extensive affixation and flexible word order "do not make Persian much different from other Indo-European languages" for readability modeling. ([arxiv 1810.06639](https://arxiv.org/pdf/1810.06639)) **[single-source]** Persian is SOV vs English SVO, but shares ordering in ~half of 26 word-order parameters; divergences concentrate in adpositions, noun/relative-clause order, verb/auxiliary order. (sciencepublishinggroup.com)
- Transfer as-is: one instruction per sentence; sentence caps; paragraph limits; lists for sequences; preserve modality/hedges; no marketing adjectives; one-word-one-meaning (as a consistency rule).

## 4. Rules that need Persian-specific reformulation

### Phrasal verbs → light-verb (compound) constructions
- **[verified 3-0]** Persian compound verbs = light verb + non-verbal element (noun, verbal noun, adjective, past stem, preposition) — the structural analog of English phrasal verbs and nominalizations, which must be **regulated rather than banned**. ([UT Austin Persian Online Resources](https://sites.la.utexas.edu/persian_online_resources/verbs/complex-compound-verbs/))
- **[verified 3-0]** کردن is the most common verbal member — compounds are the default productive verb-formation strategy; a ban is impossible. (same source)
- **[single-source]** Persian's light-verb inventory is small and closed (~16 verbs: کردن، دادن، زدن…), combining productively; new tech vocabulary enters as loanword + light verb («کلیک کردن»، «ایمیل زدن»). Compounds are syntactically separable (object clitics can intervene) → a rule on keeping components adjacent is warranted. Compounds split into compositional (انجام دادن) and non-compositional (گوش کردن) → treat compounds as single lexical units in terminology.

### Active voice → light-verb choice, plus شدن caution
- **[verified 3-0]** The active/passive distinction in compound verbs is carried by the light verb: کردن → active, شدن → passive. An "active voice only" rule must be operationalized as **prefer کردن-type over شدن-type**, not as an English-style voice transformation. (UT Austin)
- **[verified 3-0]** Persian forms the syntactic passive as past participle + شدن (parallel to English be-passive) — but شدن is **polysemous**: also a main verb ("become") and a passive-or-active compound former. Its presence alone does not signal passive; a mechanical "avoid شدن" rule would wrongly flag active compounds. ([ccsenet.org](https://ccsenet.org/journal/index.php/ass/article/view/60916)) Persian also expresses passive meaning morphologically (transitivity alternation), so a شدن-only passive detector under-detects.

### Noun clusters → ezafe chains (تتابع اضافات)
- **[verified 3-0]** The ezafe enclitic -e/-ye is **usually not written** (optional kasra) — most noun-modifier links are invisible in print, an inherent parsing-ambiguity source. ([Encyclopædia Iranica, "Ezafe"](https://www.iranicaonline.org/articles/ezafa/))
- **[verified 3-0]** Persian permits recursively nested ezafe chains (تتابع اضافات) — the direct analog of English noun clusters; STE's ≤3 noun-cluster cap translates to a cap on consecutive ezafe links. (Iranica)
- **[verified 3-0]** Persian noun modification is **right-branching** (modifiers follow the head), so the English pre-nominal cluster rule cannot transfer literally — reformulate for post-nominal ezafe sequences. (Iranica)
- **[single-source]** One ezafe surface form encodes many relations (Lazard: 5 broad categories; Asir: 14 types) — chains are multiply ambiguous in a way English of-phrases are not. Ezafe also serves as Persian's nominalization mechanism (کشتنِ شیر) — relevant to the verb-over-nominalization rule. Ezafe-dropping (فکّ اضافه) is a spoken-register feature; formal docs keep the marker.

### Nominalization → the اداری (bureaucratic) wrapper
- **[single-source, Microsoft fa-IR]** Replace classic formal constructions with plain equivalents: «مورد استفاده قرار دادن» → «استفاده کردن»؛ «می‌باشد» → «است»؛ «ذیل» → «زیر». The Persian analog of STE's verb-over-nominalization and plain-word rules. Persian Wikipedia's MoS likewise bans می‌باشد and Arabic-syntax calques (مربوطه → مربوط). **[single-source, fa.wikipedia MoS]**

### No semicolons → a genuine conflict with native convention
- **[verified 3-0]** Persian editorial practice **actively prescribes** the Persian semicolon (؛) between independent clauses in long sentences and before explanatory phrases — the opposite of STE's ban. A Persian controlled-language standard must explicitly decide to override this convention (strict mode) or permit it sparingly (flavored mode). (WikiShia style manual)

## 5. New Persian-only rules (no STE counterpart)

### Half-space / ZWNJ (نیم‌فاصله)
- **[verified 2-1]** Traditional Persian style resources rarely address ZWNJ, and where they do, they use vague labels (جدا، جدانویسی، عدم فاصله) that fail to distinguish ZWNJ from a full space — **no standard, unambiguous ZWNJ rule set exists in legacy style guides**. ([nf.apll.ir](https://nf.apll.ir/article_196773.html))
- **[verified 3-0]** A uniform stylesheet for the half-space is an unmet, important need in contemporary typed Persian — direct justification for explicit ZWNJ do/don't rules. (nf.apll.ir)
- **[verified 3-0]** ZWNJ frequency varies sharply by part of speech: very high in nouns/adjectives, considerable in particles, low in verbs/adverbs/pronouns — target ZWNJ rules primarily at noun and adjective compounds. (nf.apll.ir)
- **[verified 3-0]** WikiShia mandates half-space for the می verb prefix and plural ها — ZWNJ is codified at rule level in working Persian editorial standards. (WikiShia)
- **[single-source, Virastaran]** The checkable binary: inside one word a full space is forbidden (ZWNJ where needed); between two words exactly one full space, ZWNJ forbidden. می/نمی always half-spaced; تر/ترین half-spaced (exceptions بهتر، کمتر، بیشتر). ZWNJ obligatory after silent ه before suffixes (خانه‌ها). (virastaran.net, go2tr.com, zoorna.org)
- **[single-source]** ZWNJ (U+200C) is a modern typographic layer originating with software designers, not classical grammar — standards must codify it explicitly. Real-world usage is inconsistent (BBC Persian reportedly never uses it) — consistency is the differentiator.

### Character-level normalization
- **[single-source, fa.wikipedia MoS + editing practice]** Persian ی (U+06CC) and ک (U+06A9), never Arabic ي (U+064A) / ك (U+0643) — the codepoints differ and break search/sorting. Avoid tanwin on Persian words. *(The Persian-Wikipedia verification votes for this claim all errored on the usage limit; the rule is corroborated by three independent fetched sources.)*

### Digits, numbers, dates
- **[single-source, fa.wikipedia MoS]** Persian digits ۰–۹ in prose (not Latin 0–9, not Arabic ٠–٩); thousands separator ٬ (U+066C); decimal ممیز ٫ (U+066B) — Iranian academic practice also writes decimals with a slash (۲۱/۷۷). Persian ٪ in technical text, «درصد» in general prose. Solar Hijri calendar for Iranian audiences, format «۲۲ خرداد ۱۳۹۶» (numeric day + month name + year; «۱۳۸۸/۳/۲۲» incorrect in prose); ordinals in words (هشتم not ۸ام). Gregorian month names differ by locale: ژانویه (Iran) vs جنوری (Afghanistan) — a standard must declare its target locale.
- **[single-source, Microsoft fa-IR]** Nouns after numerals and units stay singular: «۲ کتاب» not «۲ کتاب‌ها». Guillemets «» are the approved quotation marks (Iran National Standard, 2011) even around embedded English; no hyphenation; parentheses over em dashes; no mid-sentence ellipsis or colon because the Persian verb must end the sentence.
- **[single-source, Virastaran]** Punctuation spacing: pause marks take no space before, one space after; paired marks no space toward content, one space outside; numeral + counted noun separated by a full space (۲۵ تومان); compound numeric modifiers half-spaced (۲۵تومانی، سی‌ساله).

### Grammar-level rules
- **[single-source, fa.wikipedia MoS]** Formal standard Persian (زبان معیار) only — می‌رود correct, می‌ره banned. Object marker را immediately after its object, not after a relative clause: «کتابی را که آورده بود، برد» not «کتابی که آورده بود را برد».

### RTL/bidi mixing
- **[single-source, W3C](https://www.w3.org/International/articles/inline-bidi-markup/)** Bidi display breaks when opposite-direction inline runs (English terms, code, numbers) are unmarked — failure cases: runs starting/ending with neutral characters, adjacent numbers, consecutive LTR phrases. Fix: wrap each LTR run in `dir="ltr"` markup; `dir="auto"`/`<bdi>` for unknown-direction content; markup preferred over invisible Unicode controls (U+2066/2067/2069 reserved for attribute/title contexts). Code blocks in RTL docs: `<pre dir="ltr"><code>`. Icons mirror in RTL; logos, code, URLs, media controls never mirror. Arabic translations must not be reused for Persian audiences.

## 6. Terminology management

- **[single-source, terminology.apll.ir]** Farhangestan requires approved equivalents to be **inflectable and productive** within Persian word-formation. Every approved term is classified: برگزیده (existing word selected) / نوگزیده (obsolete word repurposed) / نوساخته (newly coined). English is the explicit pivot language of the terminology program. ~20,000 approved terms across ~50 fields (as of early 2009); approved sets become legally binding for government institutions after presidential confirmation. Priority tiers by audience: عمومی (public) → پایه (school) → مشترک (undergraduate, cross-field) → تخصصی (specialist) — general-audience docs should use approved equivalents; narrow specialist terms are lower priority.
- **[single-source, jut.samt.ac.ir]** Content analysis of 1,510 Persian LIS terms: 77.2% rendered as multiword syntactic (ezafe-linked) phrases, 18.1% derivation, only 3.0% loanwords. Documented defects to legislate against: redundancy (حشو), broken head-dependent structure, **inconsistent term families** (خوشهٔ واژگانی), excessive calquing (گرده‌برداری افراطی).
- **[single-source, ArvanCloud docs]** The working dual strategy in Iranian tech docs: Persian coinages as product/category names (فضای ابری، شبکهٔ توزیع محتوا) + established Latin-script terms inline (API, DNS, CDN, SSD, CLI), pairing Persian term with English original in parentheses on first use. ArvanCloud publishes an in-house style guide («آروانی نوشتن») and writes ezafe after silent ه as ZWNJ+ی (نسخه‌ی) — a live example of a house style diverging from دستور خط's هٔ, which is why the skill mandates picking one form per document.

## 7. Readability and validation

- **[refuted 0-3]** ~~"The only established readability measure for Persian was the Flesch-Dayani formula"~~ — killed in verification; do not cite.
- **[refuted 0-3]** ~~"Surface features sufficed for an SVM to classify Persian readability at F1 0.9, validating sentence-length caps"~~ — killed in verification; the STE-inherited length caps in the skill are design decisions, not Persian-validated metrics.
- **[single-source]** English readability formulas (Flesch-Kincaid, FOG, Fry) applied unmodified to Persian systematically misrate texts; adaptation requires recalibrated coefficients or Persian-specific indices. Persian readability research is underdeveloped (rich morphology, productive compounding, clitics blurring word boundaries, no capitalization). A transformer model (AHT-Read) reached F1 ≈ 0.98 on 5-level Persian readability — machine-scored validation of controlled-Persian output is feasible. Technical/scientific Persian is already more uniform than humanities prose — amenable to controlled-language rules.
- **[single-source, MultiCochrane/EMNLP 2023]** Direct automated simplification **into** Farsi is currently weak: models performed far worse in Farsi than English, and even human-reference Farsi plain-language summaries rated worst of four languages (oversimplified, less fluent). A simplify-in-English-then-translate pipeline currently matches or beats direct Farsi simplification — relevant if the skill is used in a translation workflow: apply English STE first, then translate, then run this skill's Persian pass.

## 8. Claims left unverified (usage-limit failures — treat as probable but uncorroborated)

1. Microsoft fa-IR guide prescribes a conversational, everyday register over formal technical Persian (1 supporting vote, 2 errored).
2. Microsoft fa-IR: simple present as default tense; literal future = odd Persian (1 supporting vote, 2 errored).
3. Microsoft fa-IR: ZWNJ mandate for ها/می/اند/اید/ام; compound nouns ZWNJ or non-breaking space (0 valid votes).
4. Microsoft fa-IR: Persian comma، guillemets، no hyphenation، no mid-sentence ellipsis (0 valid votes).
5. fa.wikipedia MoS: mandatory Persian ی/ک codepoints (0 valid votes).
6. fa.wikipedia MoS: half-space rules incl. خانه‌ها، هم‌شکل؛ ـمند attaches (0 valid votes).

Each is consistent with at least two other fetched sources, which is why the corresponding rules stayed in the skill — but they did not pass the adversarial gate.

## Sources (22 fetched; quality as graded by extraction agents)

| Source | Quality | Role |
|---|---|---|
| apll.ir (دستور خطّ فارسی, 1401 ed.) | primary | Official orthography standard |
| nf.apll.ir article 196773 (ZWNJ study, نامهٔ فرهنگستان 2024) | primary | ZWNJ linguistics |
| terminology.apll.ir (روش کار واژه‌گزینی) | primary | Farhangestan terminology method |
| Microsoft fas-irn Style Guide (PDF) | primary | Practitioner localization rules |
| fa.wikipedia.org شیوه‌نامه + تاریخ‌ها و اعداد | primary/secondary | Community editorial standard |
| fa.wikishia.net شیوه‌نامهٔ ویرایشی | primary | Working KB style manual |
| docs.arvancloud.ir | primary | Live Iranian tech-docs practice |
| virastaran.net/khat | secondary | Professional editing rules |
| iranicaonline.org "Ezafe" | primary | Ezafe grammar |
| sites.la.utexas.edu (Persian compound verbs) | primary | Light-verb grammar |
| ccsenet.org (shodan/passive study) | primary | Passive voice analysis |
| arxiv.org/1810.06639 (Persian readability) | primary | Readability features |
| W3C inline-bidi-markup | primary | Bidi rules |
| en.wikipedia.org Controlled_natural_language | secondary | CNL landscape |
| Technical Communication 46(2) (GIFAS Rationalized French) | primary (abstract) | Cross-language STE precedent |
| jut.samt.ac.ir article 34741 (term-formation analysis) | primary | Terminology defects |
| sciencepublishinggroup.com (SOV/SVO comparison) | primary | Word-order transfer |
| MultiCochrane (EMNLP 2023) | primary | Farsi simplification benchmarks |
| zoorna.org ZWNJ.pdf | secondary | ZWNJ mechanics |
| go2tr.com/orthography, vokalapress.ir | blog | Corroboration |
| academia.edu, ingentaconnect (paywalled) | unreliable | Excluded from claims |
