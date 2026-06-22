# Design System Loop — Handoff

## What this is

Run an agentic loop (following the scaffold below) that:
1. Extracts a design system from the existing HTML wireframes
2. Pauses for human approval of the design tokens
3. Redesigns all wireframes using the design system

## Repository

`moxie-moss/super-duper-octo-palm-tree` — branch `claude/agentic-scaffold-test-xbmu5q`

9 standalone HTML wireframes for a workwear e-commerce site (Dovetail Workwear):
- `homepage.html`, `pdp.html`, `collection.html`, `cart.html`, `minicart.html`
- `cart-upsells-compare.html`, `account.html`, `blog-article.html`, `blog-index.html`
- `404.html`, `search.html`

All CSS is inline within each file (no external stylesheet). The wireframes are already
visually representative of the live site at dovetailworkwear.com.

## Prior work on this branch

- PR #1 is open (draft): fixed missing/empty `alt` attributes across 3 files (10 images)
- That work is complete and committed — don't re-do it

## The task

### Phase 1 — Extraction (iterations 1–N)
Scan every HTML file and extract:
- **Colors**: all hex/rgb/hsl values from inline styles and `<style>` blocks
- **Typography**: font families, sizes, weights, line heights
- **Spacing**: padding, margin, gap values (build a scale)
- **Border radius**: all values in use
- **Shadows**: all box-shadow/text-shadow values
- **Component patterns**: buttons, cards, nav, forms, badges

Produce a `design-system.css` file at the repo root with CSS custom properties
for all tokens, organized by category.

### Phase 2 — Human checkpoint (required)
Stop and show the user:
- The extracted color palette (hex values + where each appears)
- The type scale
- Any inconsistencies or gaps found

Do NOT proceed to Phase 3 without explicit user approval. Ask if they want to
adjust or evolve any tokens before applying.

### Phase 3 — Application (one file per iteration)
Update each HTML file to reference `design-system.css` and use the CSS custom
properties instead of hardcoded values. Verify each file after editing before
moving to the next.

### Termination
All 9+ files updated, no todos remaining, design-system.css committed.

## Agentic loop scaffold to follow

Use this structure for every iteration:

```
1. INTENT: State what you are about to do and why.
2. ACTION: Execute the tool call.
3. RESULT: Capture and interpret the output.
4. STATE UPDATE: Update todos, compress context if needed.
5. TERMINATION CHECK: Pending tool calls, todos, or subagents? If no: exit. If yes: continue.
```

**Tool call failure:** capture error + recovery path, inject into next context, continue loop.

**Repetition detection:** if the same tool call with same parameters has been issued twice,
do not repeat — try an alternative approach.

**Context compression:** summarize completed iterations into a state block once the todo
list grows long. Retain: what was accomplished, what remains, any errors, current intent.

**Human checkpoint:** the Phase 2 pause above is mandatory. Use it.

## Notes

- The live site (dovetailworkwear.com) returns 403 for automated fetches — work from the local HTML files only
- The Shopify theme repo (moxie-moss/shopify-theme) requires session scope to be added via the repo selector below the chat input — not needed if working from local files
- minicart.html line 712 has `<img id="qsThumbImg" src="" alt="">` — this is a JS-populated placeholder, leave it alone
