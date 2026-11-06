# The Warning Flicker — agent brief

A static, clickable prototype of a long-form article, "The Warning Flicker", about climate flickering
before tipping points. The illustrations are made of text fragments and animate on hover. Built for
GitHub Pages.

## Source of truth

- Figma: https://www.figma.com/design/AknCsAtZgqhsDL1OmKLwVb, frame "Desktop - 1" `1:2` (1440 × 5014).
  It is desktop only; there is no mobile design.
- **Never edit the Figma file.** Read only.
- Copy is verbatim, including its typos ("millenia", "may in some cases by headed", "one of more of").

## Files

```
index.html   the whole page: HTML + <style> + <script>, no build, no dependencies besides Google Fonts
assets/      title.svg (exported title artwork) + WebP conversions of the Figma image fills
.nojekyll    tells GitHub Pages to serve files as-is
```

Run it with `python3 -m http.server` from this folder.

## How it works

- **Scaled frame.** `.page` is 1440 × 5014 and uses `zoom: var(--z)`. `fit()` in `<head>` sets `--z` to the
  viewport width ÷ 1440. Every px value in the CSS is a Figma coordinate. On narrow screens the page simply
  scales down.
- **Title.** "The Warning Flicker" (node `105:209`) is around 300 masked text fragments in Figma, so it is
  exported as one SVG (`assets/title.svg`, positioned at left 20, top 0). The export's two white background
  rects were removed. The rect inside `<clipPath id="clip0_0_1">` must stay, or nothing renders.
- **Rotated layers** use `.pc` with `--cx --cy` (centre), `--w --h` (unrotated size) and `--r` (rotation),
  all taken from the Figma codegen. Image crops use `.ph` with `--iw --ih --il --it` percentages.
- **Interactive frames** are `[data-fx]`, one per Figma component set. A mouse entering `.hit` runs
  `data-steps` in order with `data-delays` ms between them, and leaving resets to `data-state="1"`. On
  touch screens a tap toggles. The CSS keys off `[data-state]`.
  - Frame 4 `105:186`, the map: flickers through piece opacities (V2 → V3 → V4, 0.3s ease-in;
    delay 825 = 525 + 300, then 615 = 315 + 300).
  - Frame 2 `70:1757`, the dunes: blowing sand fades in (1.4s gentle).
  - Frame 3 `95:160`, the two land pieces: they drift and rotate apart and a fragment stream appears
    (1.4s gentle).
  - Frame 5 `107:609`: pieces stack up, 0.8s apart.
- **Pointer handling.** Art frames have `pointer-events: none` except their `.hit` box. The article column
  sits above them (z-index 3), with pointer events only on non-empty paragraphs, so text and links stay
  usable. The `.hit` boxes were placed to avoid the text column.
- `.tail` is "test part 2 3" (`113:669`), the scattered fragments at the foot of the page. It is rotated
  −36.42° about its top-left corner and cropped with the fill's `imageTransform`.
