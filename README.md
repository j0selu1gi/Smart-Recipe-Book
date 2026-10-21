# Recipe Book

**▶ Live demo: https://j0selu1gi.github.io/Smart-Recipe-Book/**

A personal recipe book that lives as a single HTML file. Browse your recipes, scale
servings up or down, cook step-by-step with a checklist, keep a list of pantry
staples, and build a shopping list — every change is saved automatically.

Built as a widget for the [Kimi Work](https://www.kimi.com/) dashboard; it also runs
standalone in any browser (see *Running it* below).

## What it does, in plain terms

- **Recipes tab** — all your recipes as cards. Search and filter by tag
  (dinner, quick, vegetarian…). Click a card to open the full recipe: ingredients on
  the left, numbered steps on the right.
- **Add / edit / delete recipes** — a built-in editor for the title, timing, tags,
  ingredients (quantity, unit, name, notes) and cooking steps.
- **Servings stepper** — a recipe written for 4 people but you're feeding 6? Tap `+`
  and every ingredient quantity is recalculated automatically.
- **Cook mode** — add recipes to the cook list and check off steps as you go, so a
  phone or laptop next to the stove replaces a printed recipe.
- **Pantry staples tab** — the ingredients you almost always have at home. When you
  build a shopping list from a recipe, anything already in your pantry is left off.
- **Shopping list tab** — pick which cook-list recipes you're shopping for and get a
  combined, de-duplicated list of what you actually need to buy. (Designed to feed the
  H-E-B cart agent in Kimi Work.)

## How it works (technical, but simple)

- **One file, no build step.** Everything — markup, styles, and logic — is in
  `index.html`. No dependencies, no `npm install`.
- **Data model.** A recipe is a plain object: title, tags, prep/cook minutes,
  servings, an ingredients array, and a steps array. All recipes live in one JSON
  state: `{ recipes, staples, cookList }`.
- **Autosave.** Inside Kimi Work, every edit is written through the widget host
  (`window.DaimonWidget.files.writeText`) to `data/recipe-book-state.json`, with a
  "Saved" / "Saving…" indicator in the header. Standalone, changes are kept in memory
  for the session (the app starts from the embedded sample recipes).
- **Scaling.** Quantities are stored as `{qty, unit}`; scaling multiplies `qty` by
  `newServings / originalServings` and tidies fractions for display.
- **Theming.** The UI uses Kimi's design tokens (CSS custom properties like
  `--kimi-color-text-primary`). `kimi-standalone.css` supplies equivalent values when
  the app is opened outside Kimi Work.

## Running it

- **In Kimi Work:** place `index.html` in a Widget workspace — it picks up the host
  theme and autosaves automatically.
- **Standalone:** just open `index.html` in a browser (double-click it, or serve the
  folder with any static server). `kimi-standalone.css` provides the fallback theme.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole app (UI + logic) |
| `kimi-standalone.css` | Fallback theme/variables for standalone use |
| `data/recipe-book-state.json` | The autosaved state from the author's dashboard (sample data) |

## License

MIT — free to use, copy, modify, and share. See [LICENSE](LICENSE).
