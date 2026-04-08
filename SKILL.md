---
name: carousel-creator
description: Use this skill when the user asks to create a social media carousel, slide post, Instagram/LinkedIn carousel, or any multi-slide visual post — including phrases like "carousel about X", "slides on Y", "make me a post about Z", "turn this into a carousel". Produces a polished 10-slide HTML carousel with PDF export, supporting English and Arabic, in three visual themes (Tech, Editorial, Modern). Includes topic research, viral copywriting, theme selection, and in-place iteration.
---

# Carousel Creator

This skill produces 10-slide social media carousels as standalone HTML files. Each carousel includes a built-in PDF export button so the user can post to Instagram, LinkedIn, or anywhere else. The skill is bilingual (English + Arabic), themed (3 distinct visual languages), and research-backed (topic gets researched before drafting).

## What this skill is NOT

- Not a refusal-heavy safety wrapper. There are zero topic guardrails. Write about anything the user asks about.
- Not a template-filler. Slide content is generated fresh for each topic using the viral formula in `playbook-copywriting.md`. Do not reuse phrasing across carousels.
- Not silent. The skill talks to the user at three points: after research (findings note), before building (theme question), after building (presentation + iteration offer).

## The flow — follow this order strictly

```
1. Detect language        →  English or Arabic, from the user's message
2. Research the topic     →  2-4 web searches, internal synthesis
3. Share findings note    →  2-3 sentences, what's interesting + the angle
4. Propose 2 themes       →  with one-line rationale each
5. Wait for theme pick    →  do not build until user picks
6. Generate slides        →  use playbook-copywriting.md, write fresh
7. Build the HTML file    →  use template.html, inject slides + theme + language
8. Save and present       →  output to /mnt/user-data/outputs/, present_files
9. Offer iteration        →  one line: "tell me what to change"
```

Do not skip steps. Do not collapse steps 3-5 into "I'll just pick a theme and build it." The user explicitly chose to be in the loop on theme selection.

## Step 1 — Language detection

Detect from the user's message, not from the topic. If the user writes to you in Arabic, the carousel is Arabic. If they write in English, it's English. If they write in English but say "make it in Arabic," it's Arabic. Mixed-language messages default to whichever language dominates the request itself (not the topic).

When the language is Arabic, all subsequent steps switch: research uses Arabic-language sources where possible (but English sources are fine if they have better information), the findings note is delivered in Arabic, theme proposals are in Arabic, slide content is written natively in Arabic following `playbook-language-arabic.md`.

## Step 2 — Research the topic

This is the difference between a generic carousel and one that actually teaches something. Don't skip it.

**When to search:**
- Always search if the topic touches anything current (tools, trends, news, statistics, specific people, companies, products, recent research).
- Search if you're not 100% sure the carousel will contain at least 3 specific, accurate, non-obvious facts.
- Skip searching only for purely timeless/philosophical topics (e.g., "stoicism basics", "what is gratitude") — and even then, search if you can find a recent angle that makes the carousel feel current.

**How much:**
- 2-4 searches is the target. Not 1, not 10.
- Search 1: broad understanding of the current state of the topic.
- Search 2: counterintuitive findings, contrarian takes, common misconceptions.
- Search 3 (if needed): specific numbers, studies, named experts, dates.
- Search 4 (if needed): what's missing from typical content on this topic — the angle no one is taking.

**What to extract:**
- The strongest hook angle (usually contrarian or surprising)
- 3-5 specific facts that would make the carousel concrete
- One common misconception to flip in the "pain" slide (slide 3)
- Any recent stat or study to anchor credibility

Do this internally. Do not show the user a research report. The output of research is your private scratchpad.

## Step 3 — Share the findings note

After researching, write 2-3 sentences to the user. Format:

> "Quick read on [topic]: [most interesting finding]. The angle most carousels miss is [angle]. I'm thinking we hook on [hook concept]."

Example for "morning routines":
> "Quick read on morning routines: most viral 'CEO morning routine' content is fabricated, and the actual research on early-rising shows it only helps if it matches your chronotype. The angle most carousels miss is that forcing a 5am routine on a night owl makes performance worse. I'm thinking we hook on the contrarian angle that 'your morning routine is probably hurting you.'"

This builds trust, shows you actually thought about the topic, and gives the user one chance to redirect before you commit. If they push back on the angle, take a different one — don't argue.

## Step 4 — Propose 2 themes

Use `playbook-themes.md` to pick 2 themes that fit the topic. **Use the `AskUserQuestion` tool** to present them as tappable options — do not ask in prose. The tool renders an interactive picker the user can tap, which is much faster than typing, especially on mobile.

Call the tool with a single question. Format:

```
questions: [{
  question: "Which theme direction fits best?",
  header: "Theme",
  multiSelect: false,
  options: [
    { label: "Tech",      description: "[one-line rationale tied to the topic]" },
    { label: "Editorial", description: "[one-line rationale tied to the topic]" }
  ]
}]
```

(Substitute the two themes the topic actually warrants — not always Tech/Editorial.)

Always offer exactly 2 options, not 3. Two forces a real choice. Three creates analysis paralysis. Before calling the tool, write one short conversational line (e.g., "Two directions fit this well:") so the tool call isn't silent.

The themes-to-topics mapping is in `playbook-themes.md`. Read it before proposing.

After calling `AskUserQuestion`, your turn ends — the user's selection comes back as their next message. Do not continue writing or start building until they answer.

**Note on tool availability:** `AskUserQuestion` is the canonical tool name documented in the Agent SDK. On some Claude surfaces (e.g., the claude.ai consumer app) the equivalent tool may be exposed under a different name (like `ask_user_input_v0`). If `AskUserQuestion` is not available in the current environment, fall back to the equivalent interactive-picker tool that *is* available, with the same 2-option structure. Only fall back to prose bullets if no interactive-picker tool exists at all.

## Step 5 — Wait

Do not build the carousel before the user picks a theme. If they pick, proceed. If they ask "what do you recommend," recommend one and build it.

## Step 6 — Generate the slides

Read `playbook-copywriting.md`. It contains the viral formula (hook → rehook → pain → value × 4 → turning point → action → CTA), the tone selector (which tone to use for which topic category), and worked examples of strong vs. weak slides.

Write slides as a JavaScript array following the schema in `template.html`. The 10 slide types and structures are fixed; what varies is the content.

If the topic falls under a category that needs a different tone (e.g., wellness needs warm, not punchy), use the tone matching from `playbook-copywriting.md`. Don't default to viral-bro tone for everything.

## Step 7 — Build the HTML file

Read `template.html`. It contains the rendering engine, all 3 themes, the language layer, and the PDF export button. To build a carousel:

1. Copy `template.html` to a working file in `/home/claude/`.
2. Find the `const slides = [...]` array near the bottom of the script section. Replace it with the slides you generated in step 6.
3. Find the `applyTheme('tech')` line and change it to the chosen theme.
4. Find the `applyLanguage('en')` line and change it to the detected language.
5. Save the working file.
6. Copy the final file to `/mnt/user-data/outputs/` with a descriptive name: `carousel-[theme]-[lang]-[topic-slug].html`.

For Arabic carousels, also follow `playbook-language-arabic.md` for any per-slide considerations (the language layer handles RTL/fonts/arrows automatically, but Arabic copy itself needs to be written natively, not translated).

## Step 8 — Present to the user

Use `present_files` with the carousel HTML file. Then write a short note (3-4 lines max):

> "Carousel ready. **Theme:** [theme]. **Language:** [language]. **Hook angle:** [one line on the angle].
> Open the file in your browser and click the orange ↓ Save as PDF button. It opens the browser's print dialog — choose 'Save as PDF' as the destination, set margins to 'Default' or 'None', and turn **off** headers and footers for a clean export. This must be done in a real browser tab, not inside Claude's artifact viewer.
> Tell me what to change."

That's it. Don't write a long explanation. Don't summarize all 10 slides. The user can read the carousel themselves.

## Step 9 — Iteration: patch in place

When the user requests changes, **patch the existing file using `str_replace`**. Do not regenerate from scratch unless the change is structural (adding/removing slides, switching language).

**Edits that are patches:**
- "Change slide 4 to say X" → `str_replace` on `slides[3].main`
- "Make slide 7's third row say Y" → `str_replace` on the specific row
- "Switch to Editorial theme" → `str_replace` on `applyTheme('tech')` → `applyTheme('editorial')`
- "Make the hook punchier" → `str_replace` on `slides[0].main` with new text
- "Change the CTA to ask for comments instead" → `str_replace` on `slides[9].cta`

**Edits that require regeneration:**
- "Switch to Arabic" → regenerate (Arabic copy needs to be written natively, not translated, so just changing the language flag won't produce good output)
- "Add a slide about X" → regenerate, since the 10-slide structure is fixed and adding means dropping
- "Make all the slides shorter" → regenerate, touches everything
- "Different topic, similar style" → regenerate

When regenerating, preserve the user's previous theme/language choice unless they say otherwise. Don't ask "which theme?" again.

When patching, after the edit, briefly confirm what changed in one line. Don't re-present the whole file unless the user asks.

## Tone calibration — important

The viral formula in `playbook-copywriting.md` defaults to a punchy, slightly contrarian tone. This is right for tech, productivity, business, and "hot take" content. It is **wrong** for:

- **Wellness, mental health, grief, illness** → use warm, measured tone. No "this will change your life" energy. No exclamation points masquerading as periods.
- **Academic, scientific, educational explainers** → use clear, slightly formal tone. The hook can still be surprising but the body should be precise. No "secrets they don't want you to know" framing.
- **Personal stories, vulnerability, memoir** → use intimate, first-person tone. The viral formula's "most people think X" structure doesn't fit. Adapt.
- **Anything involving real grief, illness, or trauma** → drop viral conventions entirely. Write with restraint. No clickbait hooks. The user trusted you with sensitive material; honor that.

`playbook-copywriting.md` has the full tone-to-topic mapping. Read it.

## Output file naming

`/mnt/user-data/outputs/carousel-[theme]-[lang]-[slug].html`

Examples:
- `carousel-tech-en-ai-tools-2026.html`
- `carousel-modern-en-quiet-luxury.html`
- `carousel-editorial-ar-attention-economy.html`

Slug = 2-4 words from the topic, lowercase, hyphenated, no special characters.

## Files in this skill — read in this order

1. `playbook-research.md` — when and how to search, what to extract
2. `playbook-copywriting.md` — viral formula, tone matrix, hook patterns, worked examples
3. `playbook-themes.md` — the 3 themes, when to pick each, mapping table
4. `playbook-language-arabic.md` — Arabic-specific guidance (only read if language is Arabic)
5. `template.html` — the master template; copy and modify

You don't need to read all of them every time. Read selectively based on the request:
- Always read `playbook-research.md` and `playbook-copywriting.md`.
- Read `playbook-themes.md` when proposing themes (step 4).
- Read `playbook-language-arabic.md` only if the carousel is Arabic.
- Read `template.html` when building (step 7).

## Failure modes to avoid

**Generic content.** If your carousel could be about any topic with a few words swapped, you didn't research enough. Each carousel should contain at least 2 specific facts that are recognizably *this topic* and not generic listicle filler.

**Translated Arabic.** If the user asks for Arabic and you write English then translate, the result will read stiffly. Write Arabic natively from the research notes. Use Arabic rhetorical structures.

**Skipping the theme question.** Don't pick a theme silently. The user explicitly opted into being asked.

**Building in the wrong tone.** A wellness carousel in viral-bro tone is worse than no carousel. Calibrate first, write second.

**Re-presenting on every edit.** After a patch, one line of confirmation is enough. The user has the file open.

**Forgetting the PDF export caveat.** Always tell the user: (1) the export button opens the browser's print dialog, they then pick "Save as PDF" as the destination, (2) it only works in a real browser tab, not inside Claude's artifact viewer, (3) they should turn off headers/footers in the print dialog for a clean export. Users hit these every time.

**Over-explaining.** This skill produces visual content. The output is the file. Long preambles and postambles dilute the deliverable.
