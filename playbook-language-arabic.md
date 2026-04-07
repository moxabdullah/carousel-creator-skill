# Arabic Language Playbook

Read this file ONLY when the carousel is in Arabic. Skip it for English.

Arabic is not a translation problem. It's a writing problem with a different cultural and rhetorical operating system. The biggest mistake you can make is writing the carousel in English first and then translating. The result reads stiff, foreign, and obviously machine-generated. Write Arabic *natively* from the research scratchpad, not from English copy.

## What the language layer handles automatically

The template's language layer flips these things when you call `applyLanguage('ar')`:

- `dir="rtl"` on the document and all slides
- Arrow characters: → becomes ← in bottom bars
- Big background numerals move from bottom-right to bottom-left
- Dot spacing in top bars mirrors (margin-right becomes margin-left)
- Font swaps: Inter Tight → IBM Plex Sans Arabic, Instrument Serif → Amiri, Inter → Cairo
- Page numbers stay LTR (Western numerals "01 / 10" still read left-to-right inside the RTL flow)

You don't need to do anything for these. The layer handles them.

## What you DO need to handle

The skill cannot automate good Arabic writing. That's your job. This file teaches the writing.

## Modern Standard Arabic, not dialect

Always write in **Modern Standard Arabic (MSA / الفصحى).** Do not use Egyptian, Khaleeji, Levantine, or any other dialect.

Reasons:
- MSA is universally readable across the Arab world. A carousel in Egyptian Arabic excludes Khaleeji audiences and vice versa.
- MSA reads as professional and trustworthy. Dialect can read as casual to the point of unprofessional in certain contexts.
- The visual themes we built (Tech, Editorial, Modern) all carry a polished register that pairs with MSA, not dialect.

The exception: if the user explicitly asks for a specific dialect, write in that dialect. Don't second-guess them.

## Writing Arabic that doesn't sound translated

These are the patterns that distinguish native Arabic writing from translated English.

### 1. Use Arabic rhetorical structures, not English ones

English viral copy loves the "X isn't about Y. It's about Z" reframe. Arabic prefers:

- **Parallelism (السجع / التوازي):** repeating sentence structures with subtle variation. "ليس عن X، بل عن Y" works, but Arabic loves it more when the parallel is rhythmic: "ليس البطء عيباً، بل البطء حكمة."
- **Rhetorical questions (الاستفهام البلاغي):** "هل تظن أن X؟" lands harder in Arabic than the English equivalent.
- **Emphatic constructions (التوكيد):** Arabic uses particles like "إنّ" and "قد" for emphasis where English uses italics or bold. "إنّ الحقيقة أبسط مما تظن" carries weight that "الحقيقة أبسط مما تظن" doesn't.

### 2. Lean into Arabic's love of metaphor

English viral copy is direct and literal. Arabic readers expect and enjoy figurative language even in casual content. Where English would say "Claude is the AI pros use to win," Arabic naturally extends to "Claude هو السلاح الذي يستخدمه المحترفون بصمت ليتفوّقوا على الجميع." The weapon metaphor lands harder in Arabic than literal translation would.

Don't overdo it — one well-placed metaphor per slide is plenty. But don't strip them out for fear of being "too poetic." Arabic carries metaphor better than English does.

### 3. Diacritics (التشكيل) for emphasis

Arabic doesn't have italics. The closest equivalent is selective diacritics on key words. Where English would italicize "*think*," Arabic can write "يُفكِّر" with full diacritics on the verb. The visual weight of the marks signals "this word matters."

Use sparingly — once per slide maximum. Diacritics on every word makes text look like a textbook, not a carousel.

### 4. Sentence length

Arabic sentences are naturally longer than English sentences for the same idea. Don't fight this. A 12-word English headline often becomes a 15-word Arabic headline that reads naturally.

That said, the viral formula still demands punch. Cut filler ruthlessly: drop "إن" when not needed for emphasis, cut "هذا" before nouns when context is clear, and avoid stacking prepositional phrases.

### 5. Avoid English word order traps

English subject-verb-object often becomes Arabic verb-subject-object. "ChatGPT users are switching" translates literally to "مستخدمو ChatGPT يتحولون" but reads more naturally as "يهاجر مستخدمو ChatGPT" — verb first, more dynamic.

Other traps:
- English passive voice → use Arabic active voice. "The study found X" → "وجدت الدراسة X" not "وُجد X في الدراسة."
- English "you should" → Arabic imperative directly. "ينبغي عليك أن تجرّب" → just "جرّب."
- English "there is/are" → drop in Arabic. "There is a study" → "ثمة دراسة" or just start with the noun.

## Numerals — Western or Arabic-Indic?

The system defaults to **Western numerals (1, 2, 3)** for the giant background numerals and page numbers. This was a deliberate choice — Western numerals look cleaner at huge display sizes and are universally readable across Arabic-speaking regions.

**Inside body text, use Arabic-Indic numerals (١، ٢، ٣).** This is the natural form for Arabic prose. "10× smarter" becomes "١٠ أضعاف ذكاءً" or "أذكى بـ١٠ مرّات." A carousel that uses Western numerals in the design system but Arabic-Indic numerals in prose feels native — it mirrors how Arabic publications actually mix the two.

**Exception:** if the topic involves Western brand names with numbers (e.g., "GPT-4," "iOS 18"), keep them in Western numerals. Mixing GPT-٤ looks wrong.

## Footer and label translations

The English template uses footer phrases like "Swipe," "Keep going," "Yep," "Now you know." Don't translate these literally. Use Arabic equivalents that have the same energy:

| English | Arabic |
|---|---|
| Swipe | اسحب |
| Keep going | تابع |
| Yep | بالضبط |
| By Anthropic | من Anthropic |
| Finally | أخيراً |
| In seconds | في ثوانٍ |
| All of it | كلّ ذلك |
| Now you know | الآن تعرف |
| Free to start | مجّاناً |
| Save | احفظ |
| End | النهاية |

For top bar labels (the "Why Claude / The Claim / Sound Familiar" mini-titles), translate the *intent* not the words. "Sound Familiar" becomes "هل يبدو مألوفاً؟" with the question mark for emphasis.

## Theme-specific Arabic font choices

The template loads these Arabic fonts. Each theme uses a specific pairing:

- **Tech** (Arabic): IBM Plex Sans Arabic (heading) + Cairo (body). Geometric, modern, matches the Tech theme's confident grotesque feel.
- **Editorial** (Arabic): Amiri (heading) + IBM Plex Sans Arabic (body). Amiri is a classical Naskh-style serif — the closest Arabic equivalent to Instrument Serif's editorial vibe.
- **Modern** (Arabic): IBM Plex Sans Arabic (heading + body, different weights). Matches the Swiss/Minimalist restraint of the English Modern theme.

Don't mix and match. The pairings are tuned.

## Per-slide considerations

### Slide 1 (Hook)
Arabic hooks land harder when they're rhythmic. Aim for sentences that have internal balance. Example: "يهاجر المستخدمون بصمت. والسبب صادم." — two short clauses, parallel rhythm.

### Slide 3 (Pain)
The "sound familiar?" rhetorical question is even more effective in Arabic than English. End the pain slide with "هل يبدو مألوفاً؟" or "هل عشت هذا؟" — direct address questions hit hard.

### Slide 7 (Stack)
Category labels in the stack should be 1-2 words in Arabic, just like English. The challenge is that some Arabic concepts need more words. Pick the shortest possible expression. "Coding" → "البرمجة" works. "Project management" → "إدارة المشاريع" is borderline; consider just "إدارة" if context makes it clear.

### Slide 8 (Turning Point)
Arabic loves the reframe structure but expresses it differently. Instead of "X isn't about Y, it's about Z," use "X ليس [Y]، إنّه [Z]" with the إنّ for emphasis. Or use the more poetic structure "ليس X مجرّد Y، بل هو Z" (X is not merely Y, rather it is Z).

### Slide 10 (CTA)
Arabic CTAs work best with imperative verbs. "احفظ" (save) is stronger than "يمكنك حفظ" (you can save). The comment ask: "اكتب 'CLAUDE' في التعليقات" — keep the keyword in Latin letters since users will type it that way.

## Brand and product names

Keep brand names, product names, and Latin acronyms in their original Latin script inside Arabic text:
- ChatGPT → ChatGPT (not "تشات جي بي تي")
- Claude → Claude (not "كلود")
- PDF → PDF (not "بي دي إف")
- iOS → iOS
- Anthropic → Anthropic

This is standard in Arabic tech writing. Transliteration looks dated and unprofessional in 2026.

URLs stay in Latin: claude.ai, not كلود.اي.

## Punctuation

Use Arabic punctuation marks where they exist:
- `،` (Arabic comma) instead of `,`
- `؛` (Arabic semicolon) instead of `;`
- `؟` (Arabic question mark) instead of `?`

Periods and exclamation marks are the same character as English (`.` and `!`).

Quotation marks: use either `«guillemets»` or English `"quotes"`. Both are acceptable in modern Arabic. Pick one and stay consistent within a single carousel.

## Failure modes specific to Arabic

**Translating instead of writing.** If your Arabic carousel started its life as English copy, the reader will feel it. Write from the research scratchpad directly into Arabic.

**Using dialect when MSA was needed.** Casual Arabic dialect on a Tech-themed business carousel reads as unprofessional. Stick to MSA unless the user specifies otherwise.

**Stripping metaphor.** Arabic readers expect richer figurative language than English readers. Don't reduce it to plain literal copy.

**Forgetting Arabic-Indic numerals in body text.** Western numerals belong in the design system (giant background numbers, page numbers). Inside Arabic prose, use Arabic-Indic numerals.

**Awkward word order.** Arabic verb-first constructions are more dynamic than subject-first. Use them where they fit.

**Translating brand names.** Keep ChatGPT, Claude, GPT-4, iOS, etc. in Latin script.

**Diacritic overload.** One emphatic word per slide gets full diacritics. Not every word.

**Translating footer/label phrases literally.** "Keep going" is "تابع," not "استمر في الذهاب."
