# Visual Direction: Coolaboratory.com

**From:** Grant (Senior UX Designer & Marketing Strategist)
**For:** Shauna (build)
**Status:** Round three — refinements against the built three-column page (masthead height, sticky header, single accent color replacing purple/rust). Structure from round two stands; this pass edits it in place rather than rewriting it.
**Grounding:** 2026-08-09 brief + design-state.md + ruth-copy.md (round six) + 2009 manifesto (`Team Inbox/Coolaboratory`) + logo pixel-sampled palette (`Team Inbox/CoolaboratoryLogo.png`)

**What changed and why this doc looks different now:** Andrew asked for a structural rebuild — three columns instead of six stacked sections, present in both header and body, so the practical/utility information (status, contact, the milmoe.com link) stays visible the whole time instead of living at the bottom of a long scroll, and so the professional work narrative and the Make:SF story read as two separate, parallel accounts rather than one merged history. This is not a patch to the old two-column §3 spec — that's gone. Everything still locked from before carries forward unchanged: Bitter (never Fraunces), the palette, the white masthead band matching the logo, no motion, real accessibility work throughout. Everything about the page's overall shape is new.

---

## 0. What this page is actually for

One audience: a recruiter or conference contact who just got handed `andrew@coolaboratory.com` and is doing a 15-second legitimacy check before they take it seriously. They are not being sold anything. They're confirming a real person with real history is behind this, then either emailing him or clicking through to milmoe.com. Every decision below is in service of that read, not of winning a portfolio award. If a choice makes the page look "designed" at the expense of looking real, it's the wrong choice.

---

## 1. Typography

**Pairing: Bitter (headings + narrative body) / JetBrains Mono (Column 1's entire rail + photo captions) — unchanged from the prior round, Fraunces remains permanently off the table.**

- **Bitter** — a slab serif, sturdy and workshop-adjacent rather than soft and craft-branded. Full weight range on Google Fonts; this page uses 400 and 700 only, no italic, nothing on the page calls for it.
- **JetBrains Mono** — its job just got bigger. In the six-section version, mono was reserved for the email and the milmoe.com link, two technical strings sitting inside otherwise-serif prose. Now that Column 1 is a self-contained utility rail (status, contact, CTA, all three lines), the whole rail is set in JetBrains Mono, not just the two links. That's a real upgrade to what the font pairing is doing: it's no longer marking two isolated words, it's marking an entire zone of the page as functionally different from the two narrative columns beside it. Photo captions in Column 3 stay mono too, same logic — functional label, not prose.

**Scale (desktop / mobile):**

| Role | Font | Size | Weight | Notes |
|---|---|---|---|---|
| Column heading | Bitter | 30px / 22px | 700 | `--accent` (see §2 — changed this round from `--purple`). Used exactly twice now — Column 2's "Interactive product design, on screen and off" and Column 3's "Make:SF" — identical treatment for both, deliberately: they're peer stories, not a primary and a secondary. Apply `text-wrap: balance` to both; Column 2's heading is seven words and will wrap to two lines at this column width, `balance` keeps the break from stranding one word alone on the second line. |
| Narrative body copy (Columns 2 & 3) | Bitter | 18px / 17px | 400 | Line-height 1.65 / 1.6. |
| Identity paragraph (spans Columns 2+3) | Bitter | 18px | 400 | Same size as narrative body — it doesn't get a size bump for sitting in a wide spanning band, see §3. |
| Column 1 rail (status, contact, CTA) | JetBrains Mono | 15px / 14px | 400 | Line-height 1.6 — mono needs more breathing room than serif at the same size or it reads cramped. `--ink`, except the two real links (email, milmoe.com) which take link styling per §5. |
| Photo captions (Column 3) | JetBrains Mono | 12px | 400 | `--ink` at ~70% opacity |

Visually-hidden `<h1>` with real text ("Coolaboratory: Makers of Fine Experience") sits behind the logo image for screen reader users — the logo PNG's alt text carries the same string. Colon, not em-dash, per Ruth's house-style correction.

---

## 2. Color Palette

**Purple and rust are both retired this round, replaced by a single new accent sourced from milmoe.com.** Andrew didn't like either the heading purple or the link rust. Rather than picking two new colors, he asked for one: milmoe.com's own accent token (`#BF6B69`, a dusty rose/light maroon, used there for links/hover/CTAs) applied to both the headings and the links here. That's a real, deliberate point of connection between Andrew's two properties — everywhere else on this page is built specifically to read as *distinct* from milmoe.com (different type system, different palette family, different register), so a single shared accent color is worth calling out as the one intentional thread tying them together, not an inconsistency.

One color, two verified applications — the exact hex passes AA for one use and not the other, so it ships as two tokens from the same source value rather than one:

| Token | Hex | Source | Use | Contrast |
|---|---|---|---|---|
| `--accent` | `#BF6B69` | exact milmoe.com accent, unmodified | Column 2 and Column 3 headings (30px/22px, weight 700 — qualifies as "large text" under WCAG, 3:1 threshold applies, not 4.5:1) | 3.4:1 on `--bg`, 3.8:1 on `--bg-header`. Passes the large-text AA threshold with real (if not huge) margin. Shipped exactly as-is, unmodified, matching milmoe.com precisely — this is the one case where the exact value clears the bar it needs to clear. |
| `--accent-link` | `#9C4E4C` | darkened from `#BF6B69` | Link default color (email, milmoe.com link) — small mono text (15px/14px), does not qualify as large text, needs the full 4.5:1. Both links live in Column 1, so the relevant background is `--bg-column1`, not `--bg` | 5.2:1 on `--bg`, 5.4:1 on `--bg-column1` (re-verified against the updated tint value below — still clears with real margin). The exact accent value fails badly here (3.4:1 on `--bg`, well under 4.5:1) — this is a genuine AA failure, not a close call, so a darkened variant is required, not optional. |
| `--accent-link-hover` | `#844240` | darkened further from `--accent-link` | Link hover/active/focus | 6.6:1 on `--bg`, 6.9:1 on `--bg-column1`. Clearly distinguishable from the default link state by more than hue alone. |
| `--bg-header` | `#FFFFFF` | exact logo match | Masthead band — full-bleed white, holds only the logo. |
| `--bg` | `#F6F1E7` | warm cream | Page background below the masthead, Columns 2 and 3. |
| `--bg-column1` | `#F6F6F9` | pixel-sampled from the logo's "Coo" letters, see below | Column 1's background, at every breakpoint (see §3 and §4) — replaces the vertical rule. |
| `--ink` | `#241A30` | derived from logo indigo/purple | Body text. 16.6:1 on `--bg-header`, 14.7:1 on `--bg`, 15.4:1 on `--bg-column1` — all comfortably clear AA. |
| `--green` | `#1F3A1E` | darkened from logo tagline green | Reserve token, still undocumented use on the current page — kept because it's a real sampled hue, not deleted for tidiness. |

**Retired this round:** `--purple` (`#54225A`) and `--rust`/`--rust-hover` (`#AA3429`/`#8F2C22`) — remove from the stylesheet entirely, don't leave them as dead unused tokens. Everywhere they were previously referenced (headings, links) now points at `--accent`/`--accent-link`/`--accent-link-hover` per the table above. **`--bg-alt` (`#EDE4D3`) is also retired this round** — it had exactly one job, marking Column 1's mobile footer band, and that job now belongs to `--bg-column1` instead (see §3/§4). Same reasoning as retiring purple/rust: don't leave a token in the stylesheet once the thing it did has a real successor.

**`--bg-column1` derivation — moved closer to the actual logo ink, not an abstract "cool gray."** The first pass was reasoned from first principles: lighter and colder than `--bg`, hue borrowed from the logo's indigo end. Andrew went further and pixel-sampled the actual "Coo" letters in the wordmark directly: average `#585A82`, HSL(237°, 19%, 43%) — a real measurement, not an estimate, and reassuringly close to the hue the first-pass tint had already landed on by inference. He wants the tint to read as a bit lighter and a bit more blue than *that first pass*, which in practice means: keep the hue essentially where it was (237–238°, already matching the sampled ink), move saturation up from the first pass's ~10–12% partway toward the ink sample's 19% (not all the way — this stays a pale background, not a mid-tone chip), and nudge lightness up rather than down (a paler tint reads "more blue" from added saturation, it doesn't need to get darker or approach the ink's own 43% lightness to do that). Landed on **hue 238°, saturation ~18%, lightness ~97%** → `#F6F6F9`. Confirmed lighter than the first-pass tint by relative luminance (0.923 vs. 0.906) and visibly more saturated side by side, while staying legitimately pale.

**Masthead band matches the logo exactly.** The logo file is flat/opaque, no alpha channel — it always renders as a white rectangle. `--bg-header` gives it a full-bleed white band to sit in so there's no seam against the cream body. A 1px hairline rule (`--ink` at 12% opacity) closes the band at its bottom edge — this rule is now the *only* rule on the page; it no longer repeats at Column 1 (see §3).

**Optional dark mode** — token set updated for the new accent and the new Column 1 tint: `--bg-dark #17111F`, `--ink-dark #F1E9D8`, `--green-dark #6FA96C` unchanged; `--purple-dark`/`--rust-dark` retired along with their light-mode counterparts, replaced by a single `--accent-dark: #BF6B69` — the exact milmoe hex, unmodified, works for **both** headings and links on the dark background (4.9:1 against `--bg-dark`, clearing even the stricter 4.5:1 body-text threshold, not just the 3:1 large-text one). No separate darkened link variant needed in dark mode — light backgrounds and this particular rose hue don't have much contrast headroom, dark backgrounds do. `--bg-column1-dark` updated this round to **`#161727`** (hue 239°, saturation ~27%, lightness ~12%) — same "closer to the logo ink, a touch lighter and more blue" logic applied from an already-cool dark base: a modest nudge up from the previous value's hue 240°/lightness 11.5%/saturation 25%, keeping the dark-mode hue in the same family as the light-mode tint's 238° rather than letting the two drift apart. `--ink-dark` stays legible at 14.7:1; `--accent-dark` (used for links in dark mode) holds at 4.7:1 — re-verified after the nudge, still clears with real margin, not a close call. Still the one genuinely optional item; the masthead stays white even in dark mode regardless.

---

## 3. Page Structure: The Three-Column Grid

This is the core of the round-two revision, edited this round for masthead height and header stickiness. Read this section before touching CSS.

### Masthead height — reduced ~20%, and now defined explicitly

The prior round's document never actually restated a masthead padding number for the three-column structure (an oversight, not a decision) — Shauna's build didn't have a spec'd height to work from either. Defining it properly now, at the already-reduced target: the logo itself doesn't change size (still capped at 240px wide / ~66px tall, deliberately matched to Column 1's track width, see below — shrinking the logo wasn't part of this ask, only the header's overall height was, so the padding around the logo is the lever, not the logo itself).

- **Desktop:** 57px top/bottom padding around the logo → total masthead height **180px** (down from an implied 226px baseline of 80px padding — a 20.4% reduction).
- **Mobile:** 32px top/bottom padding → total masthead height **130px** (down from an implied 162px baseline of 48px padding — a 19.8% reduction).

Both numbers matter beyond just "shorter header" — the desktop figure (180px) is now load-bearing for the sticky-header/sticky-Column-1 coordination below. If the masthead's height ever changes again, Column 1's sticky offset has to change with it; they're coupled values now, not independent ones.

### Desktop grid

- **Container: max-width 1160px, centered.**
- **Columns:** `grid-template-columns: 240px minmax(0, 1fr) 332px;` with a 48px column gap.
  - **Column 1 (240px):** the persistent rail. Narrow on purpose — it's holding short administrative statements, not prose, and reads more like a margin note than a fourth story if it stays tight.
  - **Column 2 (fluid, ~245–444px depending on viewport, hard-capped at 444px):** the work narrative. This is the column that absorbs viewport width changes between the 960px collapse point and the 1160px container cap. **Correction, round twelve:** the figure previously written here (~512–560px) was never checked against the actual grid math and didn't match it — working it through against the shipped `240px minmax(0,1fr) 332px` columns, 48px gaps, and 1160px max-width container (all border-box, so padding is included in that cap): content width = 1160 − 48px gutters = 1112px; minus 96px of column gaps and the two fixed columns (240 + 332) leaves 444px, which is the width at *any* viewport ≥ 1160px — i.e., the overwhelming majority of real desktop widths, since the grid box stops growing past its own max-width. Only viewports between 961–1159px see it narrower, shrinking to ~245px right at the 960px collapse point. Verified this round because Ruth's longer Chicago/industrial-IoT paragraph (round eleven) needed checking against the real number, not the stale one — see the reading-measure note below.
  
  **Reading measure check, round twelve (no width change made):** at 444px and 18px Bitter, the line measure works out to roughly 45–46 characters per line — the low end of the comfortable 45–75cpl range, but comfortable, and consistent with this column's deliberate editorial/magazine-narrow feel next to Column 3. A longer paragraph doesn't change that measure; it only adds more wrapped lines within it; the second Chicago paragraph going from ~165 to ~320 characters turns roughly 4 lines into roughly 8, not a single wider or narrower line anywhere. Column 3 stays taller than Column 2 regardless (its three stacked photos dominate its height far more than either column's text does), so the extra height in Column 2 doesn't introduce a new imbalance beyond the one already pre-authorized below ("don't force their total heights to match"). No layout change was needed for the longer paragraph; this note exists so a future pass doesn't have to re-derive the same math.
  - **Column 3 (332px, fixed):** Make:SF, text and photos. Deliberately close to the old two-column spec's ~331px rail width — Shauna already re-exported and cropped all three photos at 660×440 (2× that width) for the prior structure. Keeping Column 3 at essentially the same width means those exports are still correct and don't need redoing.
- **Breakpoint: 960px.** Below that viewport width, the grid collapses to a single column (see "Mobile" below). Chosen deliberately below typical tablet-portrait widths (768–834px would already be uncomfortably tight for a 512px middle column plus two side columns) so tablets in portrait get the simpler mobile treatment rather than a cramped three-up squeeze.

### The header is sticky now too, and Column 1 has to coordinate with it

Round two made Column 1 sticky. This round, Andrew wants the masthead sticky as well — pinned to the very top of the viewport permanently — with Column 1 sitting statically below it, and Columns 2/3 scrolling up underneath both. Two sticky elements stacked on top of each other need to be coordinated deliberately or they'll fight each other; here's the mechanism.

**The header:** `position: sticky; top: 0; z-index: 20;` on the `<header class="masthead">` element itself (the whole band, not an inner wrapper — there's nothing else in the header competing for space the way Column 1 has the tall grid-row/sticky-inner split). It needs an opaque background (`--bg-header`, already spec'd) because it's the one element on the page with genuine visual masking duty: as Columns 2 and 3 scroll up, their content passes underneath the header across the full page width, and the header has to paint over it, not let it show through.

**Column 1's sticky offset changes from 24px to 180px.** Shauna's build picked `top: 24px` for Column 1's sticky inner wrapper as a reasonable judgment call when the header wasn't sticky — 24px was just "a little clearance from the top of the viewport." Now that the header is *always* occupying the top 180px of the viewport (per the height figure above), `top: 24px` would be wrong — it would try to lock Column 1's content at 24px from the viewport edge, which is underneath/behind the now-permanent header. Column 1's sticky `top` must equal the header's height exactly: **180px**. That way Column 1 locks flush against the header's bottom edge, not overlapping it.

**This is a different number from, and independent of, the 96px content-rhythm gap.** Shauna's build also gave `.identity` and `.col1-sticky` their own `margin-top: 96px` so Column 1's outer box (and its vertical rule) would start flush at the top of the body grid while the visible text still got breathing room — that 96px is a spacing-rhythm choice (the same token used for cross-section gaps elsewhere on the page) and has nothing to do with header height. It doesn't change this round. Don't conflate the two numbers: 180px is "where sticky content locks relative to the sticky header," 96px is "how much air sits above the content before it gets there." Both are real and both stay in the CSS, they just answer different questions.

**Z-index stack, top to bottom:** header (`z-index: 20`) above Column 1 (`z-index: 10`) above Columns 2/3 (no explicit z-index needed, default stacking). In practice Column 1 and Columns 2/3 never actually overlap — they sit at different x-positions in the grid and don't compete for the same pixels — so the meaningful stacking relationship is really just "header above everything," and Column 1's z-index is there mostly as a defensive default so the layer order is unambiguous in the code, not because a real visual conflict would otherwise occur. Column 1's own background (`--bg-column1`, see below) is opaque, but for a different reason than the header's — it's not masking anything scrolling underneath it (nothing does), it's the color-based separation device that replaces this round's retired vertical rule.

**One nice consequence, not extra work:** with Column 1's background now tinted (see below) instead of marked by a rule, the sticky header's white band and Column 1's cool-gray tint sit directly adjacent at all times during scroll — two distinct, deliberate colors meeting at a clean edge, doing the same "this is a structural boundary, not a mistake" job the old flush-corner rule detail used to do, just through color instead of a line. Nothing extra to build for this; it's a consequence of the two backgrounds already being different values.

**This still isn't "motion."** Same reasoning as round two, just now applying to two elements instead of one: nothing animates or transitions, two elements simply stop scrolling with the page at different, coordinated thresholds.

**Mobile:** the header stays sticky there too (`position: sticky; top: 0`) — simple and standalone, since Column 1 isn't sticky on mobile (it collapses to a normal-flow footer block, see below), so there's no second element to coordinate against. No z-index conflict to think through on mobile either, for the same reason.

Implementation shape for Column 1 (unchanged from round two apart from the `top` value): the outer grid item spans the full height of the body grid (`grid-row: 1 / -1`), so its box is exactly as tall as whichever of Columns 2/3 is taller. The actual visible content — logo header row plus the three rail lines — sits in an inner wrapper with `position: sticky; top: 180px;` inside that tall box, so it stays pinned until the bottom of its own (tall) containing box is reached, then releases naturally, the standard sticky-sidebar pattern.

**One dependency worth stating explicitly, since it already broke once:** `grid-row: 1 / -1` only resolves correctly if `.page-grid` has explicit row tracks declared (`grid-template-rows`, not just `grid-template-columns`) — without them, `-1` has no explicit grid to count back from and collapses to nearly nothing, sizing Column 1's box to the identity band alone instead of the full page, which leaves the sticky inner content no room to travel and it scrolls off like anything else. Confirm `grid-template-rows` is declared on `.page-grid` any time this structure gets touched.

### Column 1's background tint — replaces the vertical rule

The rule is gone. Andrew wants Column 1 separated by color instead of a line — a background tint, a shade lighter and a shade colder than the page's cream, pixel-sampled from the logo itself. `--bg-column1` (`#F6F6F9`, derivation and contrast numbers in §2) fills Column 1's entire box.

**Applies to the full outer grid box, not just the visible sticky content.** Column 1's outer grid item still spans the full body height (`grid-row: 1 / -1`, same box that used to carry the rule) — the tint goes on that outer box, not on the small inner wrapper that holds the sticky logo/rail text. This matters: if the tint only filled the compact sticky content area, it would read as a colored card floating in a track of plain cream page background — exactly the "card" language this page has rejected everywhere else (no boxes, no borders, no drop shadows, see §3's "no cards" principle and the identical call made for Column 2/3 in the last round). Filling the whole column-height box instead makes it a structural zone of the page, not a callout — a lane of consistent color running top to bottom, which is what "persistent rail" is supposed to look like. The tint doesn't need to be sticky itself; it's painted on the same tall, non-sticky outer box that was always there, so it's simply present for the full scrollable height regardless of where the reader has scrolled to.

**Desktop only, one more round: the tint now bleeds past Column 1's own box on both sides.** Andrew wants it running from the actual left edge of the browser window — past the container's own gutter, not stopping at the grid's edge — to roughly the midpoint of the 48px gap toward Column 2, about 24px past Column 1's current right edge. `.col1-rail` lives inside the 1160px max-width container, which can't natively bleed past itself, so this needs a dedicated background layer sized independently of the container.

Implementation: a `::before` pseudo-element on `.col1-rail` (not a real `<div>` — this is purely decorative, and a pseudo-element is invisible to the accessibility tree by construction, no `aria-hidden` needed the way an empty real element would require). `.col1-rail` needs `position: relative` to anchor it (safe to add — it's already the tall, non-sticky outer box, this doesn't interact with the inner sticky wrapper's own positioning).

```css
.col1-rail {
  position: relative;
}
.col1-rail::before {
  content: "";
  position: absolute;
  top: 0;
  bottom: 0;
  left: calc(-1 * max(0px, (100vw - 1160px) / 2));
  right: -24px;
  background: var(--bg-column1);
  z-index: 0;
}
.col1-sticky {
  position: relative;
  z-index: 1;
}
```

Two things to understand about that `left` value, not just copy: `(100vw - 1160px) / 2` is the standard distance from the viewport edge to the container's edge once the viewport is wider than the 1160px container cap — at exactly 1160px viewport width that distance is 0, and it grows as the viewport widens further. `max(0px, ...)` clamps it at 0 for any viewport narrower than 1160px, where the container (assuming no side padding of its own) already touches the viewport edge and there's nothing left to bleed past — one formula correctly handles both cases without a separate media query. `right: -24px` is simple by comparison since it's relative to `.col1-rail`'s own right edge, which doesn't depend on viewport width at all.

Since this pseudo-element replaces the plain `background-color` that would otherwise sit directly on `.col1-rail`, move the color there instead of on `.col1-rail` itself — one background layer, not two overlapping ones. Stacking: the pseudo-element sits at `z-index: 0` (behind), the sticky text wrapper gets an explicit `z-index: 1` (in front) — both are children within `.col1-rail`'s own stacking context (already `z-index: 10` relative to the rest of the page, see above), so this doesn't touch the page-level stacking order at all, it's purely about making sure the tint paints behind the text rather than relying on implicit DOM-order paint rules.

**Mobile doesn't need this.** The mobile footer band is already a normal full-width block with no side container to bleed past — it's naturally edge-to-edge already (per §3's mobile section below). The `calc()` breakout technique above is a desktop-only concern, specific to escaping the centered max-width container.

**No rule anywhere on Column 1 anymore.** The masthead's horizontal hairline rule (§2) is now the only rule left on the page — deliberately not extended to a second location this round, since the tint is doing the separation job that rule used to do at Column 1's edge.

**A note on `text-align: right` on Column 1's desktop text — the reasoning changes, the behavior doesn't.** Between rounds, Andrew asked for Column 1's rail text to be right-aligned on desktop, and it was implemented as "flush against Column 1's vertical hairline rule" (per design-state.md). That justification no longer applies now that the rule is gone. Keep the right-alignment anyway — it holds up on its own merits independent of the rule it was originally described against: right-aligning short marginalia text so it faces *into* the main columns, rather than out toward the page's outer edge, is a real print convention (think captions and margin notes set flush to the inner margin, not the outer one). It reads as Column 1 addressing Columns 2/3, which is arguably a better fit for "utility rail commenting on the main content" than the original line-based justification was. Mobile stays left-aligned, unchanged — that reasoning (nothing to justify against in a full-width footer block) was never about the rule specifically and still holds.

### Row structure

- **Row 1 (identity band):** spans Columns 2+3 as one wide grid area, sitting directly below the masthead. The identity paragraph goes here — see §5.
- **Row 2 (the two stories):** Column 2 and Column 3 each start here, at the same y-position, so their headings align horizontally — a deliberate outcome, not an accident of the grid. Don't force their total heights to match; Column 3 (which carries three photos) will almost certainly run longer than Column 2, and that's fine — two columns ending at different points is normal editorial layout, not a bug to fix.

### Mobile: single column, and the ordering question

Below 960px, everything collapses to one column, fluid width, 24px side gutters — consistent with every other mobile treatment on this page.

**The stacking order is not the desktop visual order.** DOM order (and therefore mobile order) is: masthead → identity paragraph → Column 2 (the work) → Column 3 (Make:SF + photos) → Column 1's rail content (status, contact, CTA), last. On desktop, CSS Grid explicit placement pulls Column 1's block to the visual left without changing where it sits in the DOM.

Two things drove that specific call:

1. **Content order.** The original brief locked a content sequence: logo → identity/services → history → status → contact → milmoe.com link. That's "prove the thing, then give the exit doors" — establish who Coolaboratory is and show the work before offering the practical closing details. A mobile visitor who hasn't read anything yet shouldn't see "not taking contract work" and a redirect to a different site as the first thing after the logo — that reads defensive, not credible, and it's not what the desktop layout does either (Column 1 is visually present the whole time on desktop, but a first-time reader's eye still lands on the identity paragraph and the two stories first; Column 1 is peripheral, not primary, even though it's persistent).
2. **This is also the more defensible accessibility call, not just the better narrative one.** Columns 2 and 3 contain zero interactive elements — pure headings and paragraphs, no links, images aren't tab stops. The only two focusable things on the entire page (the email link and the milmoe.com link) both live inside Column 1's block, together, regardless of where that block sits in the DOM. That means putting Column 1 last in DOM order creates no keyboard tab-order hazard — there's nothing else to tab through in between that a reordering could scramble. And for a screen reader linearizing the page front to back, "here's who we are, here's the work, here's Make:SF, here's how to reach us and where else to go" is a genuinely meaningful sequence (WCAG 1.3.2), arguably more meaningful than utility information leading a page whose whole job is to establish legitimacy first. Desktop's CSS Grid placement (explicit `grid-column`/`grid-row`, not the `order` property) repositions Column 1 visually without touching DOM order — same category of technique as `order` in terms of visual/DOM divergence, but used here where that divergence causes no real harm, unlike the `order` property, which I'm still avoiding on principle for anything that risks it.

On mobile, Column 1's rail is no longer sticky (nothing to stick to once it's not running alongside taller siblings) — it just becomes the last stacked block, functioning like a footer. Give it a full-bleed `--bg-column1` band (edge to edge, matching the masthead's device), covering all three lines as one group. **This is the same token used for Column 1's desktop tint, not a separate mobile-only color** — Column 1 is one semantic unit regardless of viewport, and now that its identity is carried by color rather than a line, that color should mean the same thing everywhere it shows up. (This replaces the six-section-era `--bg-alt` device, now retired — see §2.)

### Logo alignment — changed from the prior round

Previously the logo was centered across the full page width. That's wrong now: Column 1 is a real, present structural element with its own left edge (reinforced by its background tint, see below), and the logo needs to sit directly above it, not centered independently of it. **Logo is left-aligned to the content edge at every breakpoint** — on desktop that's Column 1's left edge, on mobile it's the single column's left edge. One rule, no breakpoint-specific override needed.

Cap the logo at Column 1's track width: **240px**, down from the prior round's 320px cap. Two things follow from this, both good: it now aligns exactly with the rail beneath it, and 240px is closer to the logo's native 299×82px than 320px was — less upscaling, not more, so it should render slightly sharper than before despite being smaller on screen.

---

## 4. Column 1: The Persistent Rail

**Landmark: `<aside aria-label="Contact and status">`**, wrapping the rail's body content (not the logo — the logo stays with the masthead). This is new, and deliberately different from the six-section build's choice to skip landmarks on unlabeled content. Back then, four generic `<section>` regions with nothing to distinguish them would have been landmark noise. Column 1 is a different situation: it's one functionally distinct, structurally separate part of the page that persists through scroll and holds both of the page's interactive elements — exactly the case `<aside>` exists for. It gives screen reader users a real shortcut straight to contact information without reading through both narrative columns first.

**Content, in order — three single-statement lines, no headings. Locked final wording (superseded twice since round two, per design-state.md — quoting the current, final versions here so this doc doesn't drift):**

> Email for availability.

> andrew@coolaboratory.com.

> For full-time roles, visit Milmoe.com

(Capital-M "Milmoe.com," no trailing period on the CTA line — both intentional exceptions to the page's own conventions, not typos, see design-state.md decisions log if this gets "corrected" by mistake in a future pass.)

The email is rendered via the JS-decode approach Shauna's already been briefed on separately — treat it as a normal text/link element for layout purposes, same visual treatment as any other link on the page (`--accent-link`, underlined, `--accent-link-hover` on hover/focus, no button styling — see §2 for why this is a darkened variant of the heading accent rather than the exact milmoe hex). Same for the milmoe.com link. The status line is plain text, no link.

All three lines: JetBrains Mono, per §1. **The gap between the three lines is no longer uniform.** Status-to-email stays **16px** — tighter than the narrative paragraph gap elsewhere on the page, appropriate for a rail of short administrative statements rather than flowing prose. Email-to-CTA gets **32px** — a deliberate, larger break, not a rhythm inconsistency: Andrew wants a real editorial pause between "how to reach me" (status + email, one unit) and "or go here instead" (the milmoe.com CTA, a different kind of line entirely — it's not about Coolaboratory, it's a pointer away from it). 32px isn't an invented number; it's the same token already used elsewhere on the page for exactly this kind of "same general area, but a genuine beat" transition (Column 3's prose-to-photos gap in §7 uses the same value for the same reason). Reusing it here instead of picking a new number keeps the page's spacing vocabulary from growing without cause.

---

## 5. Identity Band (spans Columns 2+3)

One sentence, per Ruth's round-six cut:

> Coolaboratory is Andrew G Milmoe's independent practice: user experience design, physical AI, frontier AI model training, and support for the maker community.

Sits in Row 1, spanning the full width of Columns 2+3 combined (~890–940px depending on viewport). **Don't let the text itself stretch that wide** — cap the paragraph's own max-width at ~680px (the same comfortable prose measure used throughout the rest of this system), left-aligned within the spanning band so it starts flush with Column 2's left edge. The grid area is wide; the text measure isn't. A single sentence stretched across a 900px line would be a bad reading experience regardless of how much room the layout offers it.

No heading, no kicker, same size as narrative body copy (18px Bitter 400) — the sentence's own first four words ("Coolaboratory is Andrew G Milmoe's...") do the identifying work, consistent with the no-kicker system established earlier and still in force.

---

## 6. Column 2: The Work

**Heading:** Interactive product design, on screen and off

**Body (two paragraphs):**

> Coolaboratory started in the Oakland Bay Area: information architecture and user experience design for global brands, by way of local digital agencies.

> That same discipline carried it to Chicago: user experience design and physical AI for hardware startups, taking the work out of the browser and into real machines.

**Landmark: `<section aria-labelledby="col2-heading">`** — legitimate now in a way it wasn't in the six-section build, because Column 2 and Column 3 both carry real, distinct headings this round, consistently. Two matched, meaningfully-labeled landmarks, not one outlier among five unlabeled sections.

Paragraph gap: 24px, same token used everywhere else on the page. Heading-to-first-paragraph gap: 16px.

---

## 7. Column 3: Make:SF

**Heading:** Make:SF

**Body (one paragraph, four sentences):**

> A Bay Area maker community, founded by Andrew in November 2007. Over the next decade it grew to 3,000 active members and produced more than 200 workshops, all of it hands-on: at the workbench, at Maker Faire, teaching and building alongside people who cared more about figuring it out than showing off. He moved on in May 2018.

**Landmark: `<section aria-labelledby="col3-heading">`**, same reasoning as Column 2.

**Then, below the paragraph (32px gap — slightly more than the 24px used between paragraphs, since this is a real content-type transition from prose to photos, but still less than the 96px cross-column gap since it's the same story continuing):** the three photos, stacked vertically, one per row, 20px gap between them. This carries forward from the prior round's photo spec essentially unchanged — same photos, same crop, same captions, same alt text, just living in Column 3 of a three-column grid instead of a rail beside a single wide column.

**Assets (already built and shipped by Shauna, reuse as-is):**

| File | Caption | Native/export size |
|---|---|---|
| `images/make-sf-booth.jpg` | "Make:SF booth, Maker Faire Bay Area" | 660×440, 3:2, ~109KB |
| `images/sensor-glove.jpg` | "Members collaborate on sensor glove" | 660×440, 3:2, ~113KB |
| `images/whiteboard-demo.jpg` | "Member demo at TechShop" | 660×440, 3:2, ~113KB, hand-cropped offset (top-heavy) |

**Alt text (unchanged, still evidentiary, distinct from the captions above):**
- Photo 1: `"Make:SF / TheBayMakers booth at a Bay Area maker faire, with adults and children soldering and building at a shared table."`
- Photo 2: `"Closeup of a wired sensor glove prototype during a wearable-tech demo, with a small group gathered around open laptops."`
- Photo 3: `"A presenter at a whiteboard walks a seated and standing group through an electronics build laid out on a workshop table."`

**Treatment, unchanged:** no frames, no drop shadows, no rounded corners, no filters or duotone. `object-fit: cover`, `aspect-ratio: 3/2`. **Keep the `height: auto` fix on `.photo-item img`** — Shauna already found and fixed the bug where the HTML `width`/`height` attributes (kept for layout-shift prevention) fight the CSS `aspect-ratio` if there's no explicit `height: auto` override; don't let that regress in the rebuild.

Column width (332px) means the images render close to their exported display size already — no new export work needed, see §3.

---

## 8. Interaction / Hover Notes

Minimal, per the credibility-not-persuasion principle.

- **Links** (email, milmoe.com — both now living in Column 1 only): underlined by default, `--accent-link`. Hover/focus: `--accent-link-hover`, underline offset increases 2px.
- **Focus states:** visible 2px solid outline in `--ink`, offset 2px, on both links. No `outline: none`.
- **No scroll animation, no fade-ins, no parallax.** Sticky positioning on Column 1 (§3) is the one place this page's layout responds to scroll at all, and it's explicitly not an animation — see that section for why it doesn't conflict with this rule.

---

## 9. Tone-in-Visuals — Tying Back to the Manifesto

Unchanged from prior rounds, still the governing logic:

- **No generic system-font fallback flash.** `font-display: swap`, sized fallback stack (Georgia for Bitter, ui-monospace for JetBrains Mono) so nothing jumps on load.
- **No stock icons, no illustration, no hero image.** The content is the credibility.
- **Consistent baseline grid, not "close enough."** At this page's scale, inconsistency is always visible even when it can't be named.
- **The email and milmoe.com link get the same visual weight as any other text on the page** — not a button, not a highlighted box, even now that they live in a persistent, always-visible rail. Persistent visibility was Andrew's practical ask (make it easy to find), not a request to make it louder. The page still isn't asking for anything.

---

## Decision Moments

**On the column proportions:** "240 / fluid / 332 wasn't an aesthetic split, it came from working backward from two real constraints: Column 1 only needs to hold short administrative sentences, so it can stay narrow without cramping; and Column 3 needed to land close to the ~331px width the photos were already exported for in the previous round, so Shauna's crop and compression work carries forward instead of getting redone for a few pixels of difference. The middle column just absorbs whatever's left. Efficient proportions and defensible proportions turned out to be the same numbers here, which doesn't always happen."

**On Column 1 going sticky:** "Andrew was explicit that Column 1 should stay visible at all times, so this wasn't really a judgment call, it was almost a spec. The part that needed real thought was making sure 'stays visible while you scroll' didn't read as a violation of the no-motion rule I've held to everywhere else on this page. It's not — nothing animates, nothing eases in, an element just stops scrolling relative to the viewport the way a fixed sidebar always has. If anything it's the opposite of motion: it's the one thing on the page that deliberately doesn't move while everything around it does."

**On reordering Column 1 to last in the DOM instead of first:** "The instinct on a lot of responsive rebuilds is to make mobile order match desktop visual order as closely as possible, so I almost put Column 1 first in the DOM to match where it sits on the far left of the desktop grid. I'm glad I checked the accessibility angle before doing that, because it would have been the wrong call twice over: narratively, leading a mobile visitor with 'we're not taking contract work, here's a different site' before they've read a word about what Coolaboratory even is undercuts the whole 'prove it, don't sell it' premise. And it turns out there's no accessibility cost to putting it last, since Columns 2 and 3 have zero interactive elements between them, there's nothing for a keyboard user to lose track of. Content order and correctness pointed the same direction for once."

**On replacing the rule with a tint:** "I'd defended the vertical rule pretty specifically last round — reused the masthead's exact rule token, walked through why a line was justified here when I'd killed one between Section 3's two columns earlier. Andrew's call to drop it for a color tint instead isn't a reversal of that reasoning, it's a different, equally valid way to solve the same problem: mark Column 1 as its own thing. A line says 'boundary.' A tint says 'this whole area is a different zone.' For a column that's meant to feel like a persistent, ambient utility rail rather than a bordered panel, color is arguably the more honest device of the two — it doesn't need a hard edge to read as separate, it just needs to look like a slightly different kind of light."

**On deriving the tint color instead of picking one:** "Andrew's brief was specific enough to work from: lighter, colder, grounded in the existing palette rather than an arbitrary gray. The logo's own gradient runs indigo to rust, and everything else on this page had already drawn from the rust end — the accent, the links, the old purple. Nothing had touched the indigo end. So 'colder' wasn't just 'add some blue,' it was 'finally use the other half of the one asset this whole palette is built from.' That's a more defensible answer than eyeballing a pleasant gray, and it keeps the tint from feeling like an unrelated color dropped in from outside the system."

**On filling the full column height, not just the sticky content box:** "The instinct-speed version of this was to just tint the little sticky block of logo-and-three-lines, since that's the part anyone actually looks at. I caught myself before doing that — a compact tinted box sitting in a track of plain page background is a card, and cards are exactly the visual language this page has been refusing to speak since round one. Filling the whole tall grid box instead, the same box that used to carry the rule, makes it a zone of the page rather than a highlighted element on the page. Small distinction, but it's the difference between 'persistent rail' and 'sidebar widget.'"

**On defining the masthead height instead of just shrinking it:** "Andrew's ask was simple, shrink the header 20 percent, but I couldn't actually do that cleanly because the round-two doc never wrote down a real height for the three-column masthead in the first place — that was a genuine gap, not a hidden number I was reducing from. So this round does two things at once: it defines the masthead height for the first time and lands it already 20 percent below the last number that was ever written down, back in round one. Worth being honest about in the doc rather than quietly pretending there was always a precise figure being adjusted."

**On making the header sticky alongside Column 1:** "The part of this that actually took thought wasn't 'make the header sticky,' that's one CSS property. It's that Column 1 was already sticky from last round with its own offset, and stacking a second sticky element on top of it without updating that offset would've made Column 1's content try to lock in place behind the now-permanent header, invisible. The fix is one number, Column 1's sticky `top` has to equal the header's height exactly, but it's a number that will silently go wrong again if anyone changes the header height later without remembering the two are now coupled. I flagged that dependency explicitly in the doc rather than just fixing today's instance of it."

**On the color change:** "Andrew asked for one color to replace two, milmoe's accent for both the headings and the links, and said to only adjust it if contrast genuinely failed. It genuinely failed, but only for one of the two uses — the exact hex clears the bar for the big bold headings (large text only needs 3:1) and misses it badly for the small link text (which needs 4.5:1). So it ships as one source color with two names, not two colors: `--accent` unmodified where it passes, `--accent-link` darkened only as far as required where it doesn't. That's not a workaround, it's exactly the conditional Andrew already gave me — I just had to find out empirically which branch of it applied where."

**On the full-bleed tint:** "The lazy version of this would've been to just widen `.col1-rail`'s own grid track, but that changes the grid's actual math — Column 2's width, the sticky offset math, everything downstream assumes Column 1 is 240px. What Andrew wants is purely visual: the *color* reaches further than the *content* does. That's exactly what a background layer, sized independently of the box it's decorating, is for — the grid stays 240px, the paint bleeds past it. Worth being precise about the calc() rather than hand-waving 'make it full width,' because the same formula has to correctly produce zero bleed once the viewport gets narrow enough that there's nothing to bleed past in the first place."

**On the second color pass:** "The first tint was reasoned from principles — lighter, colder, borrow from the logo's indigo end. Andrew went and actually sampled the logo's ink directly, which is a better source than my inference was. What's interesting is the first pass landed on almost the same hue anyway (237–238° both times) — the reasoning held up, it just needed real saturation to read as confidently blue instead of a hint of one. 'Lighter and more blue at the same time' sounds like a contradiction until you remember saturation and lightness are separate dials — you can make something read more colorful without making it darker, which is exactly what a pale tint needs if it's going to stay a background and not become a chip."

**On the line-gap break:** "Three lines in a tight rail, and Andrew wants a bigger pause before exactly one of them — the CTA. That's not a spacing preference, it's an editorial one: two of these lines are about reaching Andrew, the third is about going somewhere else entirely. Reusing the 32px token that's already doing the same 'related but distinct beat' job in Column 3 rather than picking a fresh number keeps this from becoming a one-off exception nobody remembers the reasoning for later."

**On re-aligning the logo:** "Centering the logo made sense when the page was one column and the logo was the only thing in a wide masthead. It stopped making sense the moment Column 1 became a real, present structural element with its own left edge — a centered logo floating independently above an asymmetric rail below it would read like a mistake. Left-aligning it to Column 1's edge fixes that, and dropping the display cap from 320px to 240px to match the rail's width happens to get the logo closer to its native resolution in the process, which I'll take."

---

**Handoff note for Shauna:** three changes this round, all in §3/§4 of this doc:

1. **Tint color updated:** `--bg-column1` is now `#F6F6F9` (was `#F4F4F6`), `--bg-column1-dark` is now `#161727` (was `#161625`) — both pixel-derived from the actual logo ink this time, full reasoning and contrast numbers in §2. If you already shipped the previous values, this is a find-and-replace on those two hex strings, nothing structural changes.
2. **The tint now bleeds past `.col1-rail`'s own box** — full CSS in §3's "Column 1's background tint" section: a `::before` pseudo-element with `left: calc(-1 * max(0px, (100vw - 1160px) / 2))` and `right: -24px`, `position: relative` added to `.col1-rail`, explicit `z-index: 1` on `.col1-sticky` so the text stays above the new background layer. Move the background color off `.col1-rail` itself and onto this pseudo-element — don't leave two overlapping background declarations. Desktop only; mobile's footer band is already naturally edge-to-edge.
3. **Line spacing inside Column 1 is no longer uniform:** status→email stays 16px, email→CTA becomes 32px (reusing the same token as Column 3's prose-to-photos gap, not a new number). Only that one gap changes.

Nothing else from the last handoff changed — masthead height, sticky header, `--accent`/`--accent-link` tokens, and the `text-align: right` reasoning update are all still current, see §2/§3 above.
