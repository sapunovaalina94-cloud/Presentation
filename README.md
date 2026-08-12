[SKILL.md](https://github.com/user-attachments/files/30984873/SKILL.md)
---
name: garage8-presentation-generator
description: Generates on-brand Garage Eight PowerPoint presentations from a person's own content. Use this skill whenever anyone asks to create, build, generate, or put together a presentation, deck, slides, or pitch for Garage Eight (or just says "make me a presentation about X" in a Garage Eight / G8 context) — even if they don't mention branding, a template, or PowerPoint explicitly. Also trigger on requests to add a slide to an existing Garage Eight deck, or to redo/restyle a deck "in our template" / "in the G8 style". Do NOT use this for generic presentation advice, unbranded slides, or requests to edit an arbitrary .pptx that has nothing to do with Garage Eight's own template.
---

# Garage Eight presentation generator

This skill turns a person's plain description of their content into a real, on-brand Garage Eight `.pptx` file — no PowerPoint editing, no knowledge of the template's internals required from them. It works by cloning real slides out of the master deck in `assets/decks/` (which already contains every approved layout) and filling in the text.

**This package only supports the dark theme.** The light-theme master deck isn't bundled here (kept as a separate skill package to stay under the upload size limit) — always generate with `dark`, don't ask the user to choose a theme.

## Why this exists, and what "on-brand" actually means here

The master deck in `assets/decks/` is the real, designer-approved Garage Eight template — not a generic PowerPoint theme. Every layout in it was individually reviewed and pixel-tuned (font sizes, spacing, alignment) by the design team over many rounds. Your job is to reuse those exact slides as-is and swap in the user's words — never redraw a layout from scratch, never invent new fonts/colors/spacing, and never hand-edit the .pptx directly with your own shape-positioning guesses. If a layout doesn't quite fit what someone wants, pick the closest real layout rather than trying to build a new one - the whole value of this skill is that every output slide already looks right.

## Workflow

### 1. Understand what the user wants

Ask (briefly, don't interrogate) for:
- The topic/purpose of the deck and roughly how many slides / what sections it needs.
- Whatever content they already have in mind — bullet points, a rough outline, numbers, names, quotes, whatever they've got. It's fine if it's messy or incomplete; you'll shape it into slides.

You don't need them to know layout names or slot names — that's your job to figure out.

### 2. Map their content onto real layouts

Read `references/layout_catalog.md` for a human-readable summary of all 53 layout families, grouped by purpose (covers, dividers, agenda, charts, diagrams, photo slides, text slides, mockups, closings). Pick families that match the SHAPE of what the user described — a list of 4 KPIs fits a metrics-grid layout, a timeline fits a roadmap/phase diagram, a testimonial fits the quote layout, etc.

Every deck should normally open with a cover (family `1.x`) and close with a closing slide (family `9.x`) unless the user explicitly wants something else (e.g. "just give me 3 slides to drop into an existing deck").

**Once you've picked a family, look it up in `scripts/layouts_manifest.json`** to get its exact slot names and see the original placeholder/example text (which hints at the intended tone and length for that slot — e.g. if the example is a two-word label, don't write a full sentence there). Slot names are specific and must be copied exactly (e.g. `column_1_item_3_value`, not `col1_item3_val` or `value_3`) — the generator does not fuzzy-match slot names, only slide content.

### 3. Write real content for every slot

Fill in every slot for every chosen family with the user's actual content, in their language, matching the tone/length implied by that slot's example text in the manifest. Don't leave placeholder text in — if the user hasn't given you enough for a particular slot, either ask them or write something reasonable and flag it as a draft you made up, rather than shipping the manifest's own filler text ("Заголовок", "Lorem Ipsum...", etc.) in a real deck.

Slots you don't set are simply left at the template's own default (for chrome-like elements this is fine and expected) — you don't need to fill every single decorative slot on every slide, only the ones that carry real content the user cares about.

### 4. Build the slide_specs and generate

Construct a JSON array, one object per slide, in the order they should appear:

```json
[
  {"family": "1.1", "values": {"slide_eyebrow": "Ежеквартальный отчёт", "slide_title": "...", "author_name": "...", "author_role": "..."}},
  {"family": "7.2", "values": {"slide_title": "...", "column_1_title": "...", "column_1_item_1_label": "...", "column_1_item_1_value": "..."}},
  {"family": "9.1", "values": {"slide_title": "Спасибо за внимание!", "card_1_label": "...", "card_2_label": "...", "author_name": "...", "author_role": "..."}}
]
```

Write this to a temp JSON file, then run:

```bash
python3 scripts/build_presentation.py dark /tmp/slide_specs.json /tmp/output.pptx
```

Always pass `dark` as the theme — this package only has the dark master deck bundled. Run this from inside the skill's own directory (or pass full paths) so the script's relative imports/asset paths resolve correctly.

### 5. Check the report before handing the file over

The script prints a JSON report to stdout — for every slide, `applied_slots` (what got filled) and `missing_slots` (slot names that didn't match anything real on that slide). **A non-empty `missing_slots` is always a bug in the slide_specs, not a template limitation** — it means a slot name was typo'd or doesn't exist for that family. Fix the slot name against `layouts_manifest.json` and rerun rather than shipping a slide with content silently missing.

If everything applied cleanly, hand the `.pptx` back to the user. Mention which layouts you used for which slides in a sentence or two, since they may want to swap one for a different variant.

### 6. Iterating

If the user wants changes — different content, a different layout for a slide, reordering — just rebuild the `slide_specs` and rerun. Don't try to hand-edit a previously generated `.pptx`'s XML directly; regenerating from the source decks is what keeps every slide pixel-correct.

## Things this skill does NOT do

- It does not invent new layouts or move/resize shapes beyond what's already baked into the master decks (that tuning work is done; don't redo it).
- It does not support arbitrary images/logos beyond what's already in the template chrome — if a user wants to insert their own photo into a photo-layout slide (family `6.x`), tell them the current version doesn't support swapping the photo itself, only the surrounding text.
- It does not merge with or edit a deck the user already has open elsewhere — it only produces a fresh `.pptx` from the two master decks.
