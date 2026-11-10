# Client logo grid spec

**Owner** Grant (layout). **Build** Shauna. **Approved by** Andrew G Milmoe. **Last updated** 2026-11-10.

**Scope** A 2 x 5 logo grid in `section.col2` of index.html, with nine logos in an order set by Andrew. The tenth cell is left empty on purpose. This spec describes the design that is live on coolaboratory.com.

## Logo order

Andrew's order, read left to right and top to bottom.

| Row | Left | Right |
|-----|------|-------|
| 1 | Razorfish | AKQA |
| 2 | Mercor | PG&E |
| 3 | mHub | Exploratorium |
| 4 | eveo | Kyte |
| 5 | The Fly | (empty) |

## Source audit

Sources live in `Team Inbox/Coolaboratory/Icons/`. Every source is black on white or has a transparent background, so every tile is white.

| Logo | Source file | Source px | Background | Notes |
|------|-------------|-----------|------------|-------|
| Razorfish | razorfish.png | 1000x250 | Transparent, flattened onto white | Andrew's higher-res replacement for the old lime JPG |
| AKQA | akqa.png | 600x600 | White | Black serif wordmark |
| Mercor | Mercor.png | 1980x686 | Transparent, flattened onto white | |
| PG&E | pg-e.png | 300x80 | Semi-transparent, flattened onto white | Kept at native size |
| mHub | mHub.png | 554x554 | White | Stacked mark, the squarest logo |
| Exploratorium | Exploratorium.jpg | 1200x340 | White | Andrew's black-on-white replacement for the old white-on-black JPG |
| eveo | eveo.jpg | 400x175 | White | Andrew's higher-res black-on-white replacement for the old 200px black tile |
| Kyte | Kyte.jpg | 670x335 | White | Orange wordmark in the source |
| The Fly | TheFly.jpeg | 192x128 | White | Kept at native size |

## 1. Placement

After the existing col2 content, directly below the second paragraph and still inside `section.col2`.

Why. Col2 is the work narrative. The two paragraphs make the claim (global brands by way of agencies, then hardware startups), and the logos are the proof, so they come after the claim. Column 3 does the same with its photo rail after its paragraph. This also keeps the col2 and col3 headings aligned, which the layout depends on.

## 2. Title

- **Text** `Partial list of Coolaboratory&nbsp;clients` in the HTML, with no colon and no trailing punctuation. The `&nbsp;` keeps "Coolaboratory clients" together so "clients" never sits alone on a line.
- **Element** `h3`, a subsection of the col2 `h2`, so the outline stays correct.
- **Style** Reuses `.mono-line` (JetBrains Mono, 15px desktop and 14px mobile, weight 400, line-height 1.6, `--ink`). It reads as a label in the same voice as the Column 1 rail and the photo captions, and keeps the col2 `h2` as the only accent-colored heading in the column.
- **Spacing** `margin: 32px 0 16px;` on `.client-logos-heading`. The 32px top reuses the col3 prose-to-photos spacing.
- **Wrapping** `text-wrap: balance`, set in the shared no-widows rule alongside the col2 and col3 `h2`. The `&nbsp;` is the fallback for browsers without `text-wrap` support.

## 3. Tile ratio and export size

- **Tile ratio** 2:1 (width to height), the same for every logo.
- **Export canvas** 480 x 240 px PNG, white background, no alpha. The tile renders at most 216 x 108 CSS px, so 480 x 240 covers 2x retina at full size.
- **Logo placement** Fit the logo's ink inside a centered 364 x 140 px content box, preserving proportions, and fill the rest of the canvas with white. Never crop the ink.
- **Scale down only** Logos are scaled down to fit the content box, never up. A logo whose ink is already smaller than the box stays at its native size, centered. PG&E and The Fly are the two that stay native, so they read smaller than their neighbors, which is accepted.
- **Transparent sources** (Razorfish, Mercor, PG&E) are flattened onto #FFFFFF.
- **File names** `images/clients/razorfish.png`, `akqa.png`, `mercor.png`, `pge.png`, `mhub.png`, `exploratorium.png`, `eveo.png`, `kyte.png`, `the-fly.png`.

## 4. Grid CSS

```css
.client-logos-heading {
  margin: 32px 0 16px;
}

.client-logos {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 1px;
  padding: 0;
  margin: 0;
  list-style: none;
  background: transparent;
  max-width: 444px; /* desktop col2 width; stops tiles ballooning on tablets */
}

.client-logos li { margin: 0; }

.client-logos img {
  display: block;
  width: 100%;
  height: auto;          /* keep, same reason as the photo-rail note in styles.css */
  aspect-ratio: 2 / 1;
  filter: grayscale(1);
}
```

- **Scaling** Tiles are fluid (`1fr` each) and the 2:1 ratio holds at every width. Desktop col2 is 444px, so each tile is about 221 x 111.
- **Phone width** Stays at 2 columns, as Andrew asked for 2 x 5. At a 375px viewport each tile is still about 162 x 81.
- **Background** The grid has no background and no outer padding. The page color shows through the 1px gaps, and the tile edges line up with the column text above.
- **Grayscale** `filter: grayscale(1)` is applied to every logo by Andrew's choice. The PNGs themselves keep their original colors. Andrew is fine with Kyte, PG&E, The Fly and Mercor reading faint in grayscale, so don't boost their contrast or swap them out.
- No border, radius, shadow or hover on tiles. The logos are not links.

## 5. The empty 10th cell

Bottom row, right side, left empty on purpose.

- Don't add a 10th `li`. Auto-placement leaves the cell empty, and since the grid has no background, the empty cell simply doesn't show. The page continues behind it.
- No placeholder, text, border, icon or "more" label.
- This keeps the screen reader count honest at nine items.

## 6. Accessibility

```html
<h3 class="mono-line client-logos-heading" id="clients-heading">Partial list of Coolaboratory&nbsp;clients</h3>
<ul class="client-logos" role="list" aria-labelledby="clients-heading">
  <li><img src="images/clients/razorfish.png" alt="Razorfish" width="480" height="240" loading="lazy" decoding="async"></li>
  <li><img src="images/clients/akqa.png" alt="AKQA" ...></li>
  <li><img src="images/clients/mercor.png" alt="Mercor" ...></li>
  <li><img src="images/clients/pge.png" alt="PG&amp;E" ...></li>
  <li><img src="images/clients/mhub.png" alt="mHub" ...></li>
  <li><img src="images/clients/exploratorium.png" alt="Exploratorium" ...></li>
  <li><img src="images/clients/eveo.png" alt="eveo" ...></li>
  <li><img src="images/clients/kyte.png" alt="Kyte" ...></li>
  <li><img src="images/clients/the-fly.png" alt="The Fly" ...></li>
</ul>
```

- Alt text is the company name only, with no "logo" suffix.
- `role="list"` is there because Safari and VoiceOver drop list semantics when `list-style: none` is set.
- Reading order matches visual order (left to right, top to bottom), which is Andrew's order.

## 7. Theme notes

- **Dark theme** Nine white tiles sit on the dark `--bg` with 1px dark gaps between them. The white blocks echo the white masthead band at the top of the page, so they have a precedent.
- **Light theme** The white tiles sit on the cream `--bg`, and the 1px cream gaps separate them.
- **Faint logos** With grayscale on, Kyte, PG&E, The Fly and Mercor are lighter than the rest. Andrew has seen this and accepts it.

## Revision history

**2026-11-10** Updated to match the live design.
- **Order** Changed to Andrew's custom order, with Razorfish, AKQA / Mercor, PG&E / mHub, Exploratorium / eveo, Kyte / The Fly, and the 10th cell empty.
- **Tiles** All nine are now white. eveo, Razorfish and Exploratorium use Andrew's higher-res black-on-white or transparent sources, so the black tiles and the lime Razorfish tile are gone. Logos are scaled down only, never up, and PG&E and The Fly stay at native size.
- **Grid** Removed the `--logo-frame` token. The background is transparent, the outer padding is 0 and the gap is 1px, so the empty 10th cell doesn't show.
- **Grayscale** Added `filter: grayscale(1)` on the logos at Andrew's request.
- **Heading** Margin changed to 32px 0 16px. Added `text-wrap: balance` and a `&nbsp;` in "Coolaboratory&nbsp;clients".
