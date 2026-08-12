# Garage Eight layout catalog

53 layout families, grouped by purpose. Each has a `family` id ("1.1", "7.2", etc.) used in `slide_specs`. The exact slot names and their example/default text live in `scripts/layouts_manifest.json` — always look a family up there before filling it in, since slot names are specific (e.g. `column_1_item_3_value`, not `value3`) and this catalog only gives the gist.

Every family works in both `"light"` and `"dark"` theme — same content, same slot names, just different generated colors.

## Covers (family 1.x) — use ONE of these for the very first slide

- **1.1** — eyebrow + title + author name/role. The standard opening cover.
- **1.2** — same as 1.1, plus a "drivers" row listing up to 3 people/names below (e.g. project stakeholders).
- **1.3, 1.4, 1.5** — visual variants of a cover (title + author name/role, no eyebrow, no drivers row). Different photo/graphic treatment, same content shape as 1.1 minus the eyebrow and drivers.

## Section dividers (family 2.x) — use to introduce a new part of the deck

- **2.1, 2.2, 2.5, 2.6** — big section name + a short description paragraph. Use between major parts of a long deck ("Часть 2: Результаты", etc).
- **2.3, 2.4** — section name + "next speaker" kicker/name, for decks with multiple presenters handing off to each other.

## Agenda (family 3.x)

- **3.1** — the only agenda layout: title + up to 4 numbered agenda items, each with a title and one-line subtitle.

## Charts (family 4.x) — quantitative/visual data

- **4.1** — title + subtitle + a 5-category bar chart (label + value pairs).
- **4.2** — title + subtitle + 2 large highlighted numbers side by side, each with a caption (good for "before vs after" or two headline KPIs).
- **4.3** — title + subtitle + a donut/status breakdown: 3 status rows (label+value) plus a center value+label for the donut itself.
- **4.4** — title + subtitle + a node/network diagram: 1 center node name + up to 8 surrounding node names (org chart, ecosystem map, etc).
- **4.5** — one huge headline stat/percentage + a 5-point year timeline below it (trend over time headline).
- **4.6** — title + subtitle + 3 labeled progress bars (each with 2 values, e.g. before/after) + 2 extra small metric callouts.

## Diagrams / process (family 5.x)

- **5.1** — roadmap with 3 "phase" chips (each: a small label like "PHASE 1", an optional date range, and a title) laid out as a curved timeline.
- **5.2** — 3-month plan: each month gets a label ("МЕСЯЦ 1"), a title, and a short description.
- **5.3** — a 4-step staircase/growth diagram: each step has a number, title, and description, increasing in visual size.
- **5.4** — a Gantt-style timeline: up to 4 activity rows across up to 8 month columns (labels only, no per-cell values — good for high-level roadmaps).
- **5.5** — a ranked list/leaderboard: up to 5 rows, each with a label, a value, and a percent.
- **5.6** — title + 4 feature/benefit cards (title + description each).

## Photo slides (family 6.x) — layouts built around a person's photo or a big portrait-style graphic

- **6.1** — title + subtitle + one big stat callout (value + label), photo on the side. Good for "meet the team" headline stats.
- **6.2** — just 2 metric callouts (value+label each), no title — use as a quick stats aside.
- **6.3** — a person's name + role + a big title/subtitle + 3 numbered points about them. Good for a "spotlight" or team-member profile slide.
- **6.4** — a pull-quote: author name + role + the quote text itself. Use for a testimonial or leadership quote.
- **6.5** — title + subtitle + 3 metric callouts, photo-backed.
- **6.6** — title + one caption + 3 label/value item rows (e.g. hiring funnel stats).
- **6.7** — title + one big stat/value + label, minimal.
- **6.8** — 3 small "kicker + name" cards (e.g. 3 new hires, each with a role kicker and a name) — no title on this layout.
- **6.9** — one headline metric (value+label) + a caption + 3 label/value item rows below.
- **6.10** — 3 labeled progress bars with before/after values, no title.
- **6.11** — title + 3 numbered points + one stat callout (value+label) — good for "what holds the team together"-style culture slides.
- **6.12** — title + subtitle + one stat callout — a simpler variant of 6.1/6.7, often used as a recruiting/CTA slide.

## Text-heavy slides (family 7.x)

- **7.1** — title + a bulleted list (pass the bullet items as one `\n`-joined string in `slide_body_list`, one line per bullet).
- **7.2** — title + TWO columns, each with a column title and up to 6 label/value metric rows, plus a footnote. Great for side-by-side KPI comparisons (e.g. "Finance" vs "Product").
- **7.3** — title + subtitle + 4 metric callouts (value+label) in a row.
- **7.4** — title + subtitle + intro body paragraph + 4 feature cards (title+desc each).
- **7.5** — title + subtitle + intro body + up to 6 numbered step cards (number+title+desc each) — a more detailed process-explainer than 5.3.
- **7.6** — one headline stat + title + subtitle + 3 small label/value items below — a "hero metric" slide.
- **7.7** — title + up to 6 metric callouts (value+label) in a grid — the biggest all-metrics grid available.
- **7.8** — subtitle + 2 intro paragraphs + 3 feature blocks (title+body each), no separate slide_title (this layout's own subtitle IS the heading).
- **7.9** — title + up to 5 cards (title+desc each) — a "who this is for" / audience-segments layout.
- **7.10** — title + up to 4 cards (title+desc each) — an "integrations"/logos-and-descriptions layout.

## Mockup/product-screenshot slides (family 8.x)

- **8.1** — title + subtitle + 3 label/value items, designed to sit next to a product screenshot mockup.
- **8.2** — just title + subtitle, designed to sit next to a large product screenshot (no metric rows).
- **8.3** — 3 captions only, no title — for a triptych of 3 product screenshots.
- **8.4** — title + 2 labeled sections (subtitle+body each) — for comparing two states/scenarios.

## Closing slides (family 9.x) — use ONE of these for the very last slide

- **9.1** — "Thank you" + 2 call-to-action card labels (e.g. "Мы в соцсетях" / "Открытые вакансии") + presenter name/role.
- **9.2, 9.3** — same as 9.1, plus a subtitle line (e.g. restating the deck's title/topic).

## Choosing layouts for a user's content

Match the SHAPE of what the user describes to a family, not the literal wording:
- A short list of 3-6 numeric KPIs → 7.3, 7.6, 7.7, or 6.2/6.5 depending on count and whether there's a title.
- Two groups of KPIs to compare → 7.2.
- A timeline/roadmap with phases or dates → 5.1, 5.2, or 5.4.
- A quote or testimonial → 6.4.
- A person/team spotlight → 6.3, 6.8.
- A step-by-step process → 5.3, 5.5, 7.5.
- Free-flowing paragraphs with no clear structure → 7.4, 7.8, or a divider (2.x) if it's really just a section intro.
- Don't force every user request into a layout that doesn't fit — if nothing matches well, say so and ask what they'd like instead of stuffing content into the wrong slot count.
