# carousel-creator

My Claude skill for making 10-slide social carousels.

## What's in here

- `SKILL.md` — the orchestrator. Claude reads this first.
- `playbook-research.md` — when/how to search before writing
- `playbook-copywriting.md` — viral formula, tone matrix, slide-by-slide rules
- `playbook-themes.md` — Tech / Editorial / Modern, when to pick each
- `playbook-language-arabic.md` — read only for Arabic carousels
- `template.html` — master template, has 3 themes + EN/AR language layer + PDF export

## How it works

Ask Claude for a carousel about anything. The skill makes Claude:
1. Detect language (EN or AR from your message)
2. Research the topic (2-4 web searches)
3. Share a 2-3 sentence findings note
4. Propose 2 themes, wait for me to pick
5. Generate 10 slides using the viral formula
6. Build the HTML file, save to outputs
7. Patch in place when I ask for edits

## Themes

- **Tech** — dark, bold, orange. AI/productivity/business/careers.
- **Editorial** — serif, NYT-ish, deep red. Culture/opinion/ideas.
- **Modern** — Swiss minimalist, deep blue. Wellness/lifestyle/sensitive topics.

## Languages

EN and AR. Arabic is written natively in MSA, not translated. RTL/fonts/numerals handled automatically.

## Output

Single HTML file. Open in any browser, click ↓ Download PDF. The PDF button doesn't work inside Claude's artifact viewer — needs a real browser tab.

## To update

Edit any file, commit, push. The SKILL.md is the contract — if I want to change behavior, edit that first.

## Notes to self

- The 3 themes are deliberately non-overlapping. Don't add a 4th unless it covers ground none of the existing 3 do.
- Tone calibration matters more than theme choice. A wellness carousel in punchy tone is worse than no carousel.
- Always 10 slides. Don't loosen this without rethinking the whole formula.
- Brand layer was deliberately skipped in v1. Add later if I get tired of generic CTAs.
- Arabic font sizes are smaller than English on purpose — Arabic glyphs are visually denser.
