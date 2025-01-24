.visual {
  --_translate: 200px;

  inline-size: 100%;
  block-size: calc(100% + var(--_translate));
  object-fit: cover;
  animation: parallax linear both;
  animation-timeline: scroll(root);
}

.decorations {
  position: relative;
  z-index: -1;
}

.decorations > * {
  position: absolute;
  inset-block-start: calc(var(--_offset-y) * 1dvb);
  inset-inline-start: calc(var(--_offset-x) * 1dvi);
  clip-path: var(--_shape);
  inline-size: max(calc(160 * var(--fluid-ratio)), 80px);
  aspect-ratio: 1;
  background-color: var(--_accent);
  animation: parallax linear both;
  animation-timeline: scroll(root);
}

.decorations > :nth-child(1) {
  --_translate: -100px;
  --_accent: red;
  --_offset-x: 5;
  --_offset-y: 40;
  --_shape: circle(50% at 50% 50%);
}

.decorations > :nth-child(2) {
  --_translate: 100px;
  --_accent: gold;
  --_offset-x: 72;
  --_offset-y: 12;
  --_shape: polygon(
    50% 0%,
    61% 35%,
    98% 35%,
    68% 57%,
    79% 91%,
    50% 70%,
    21% 91%,
    32% 57%,
    2% 35%,
    39% 35%
  );
}

.decorations > :nth-child(3) {
  --_translate: -200px;
  --_accent: blue;
  --_offset-x: 15;
  --_offset-y: 60;
  --_shape: polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%);
}

@keyframes parallax {
  from {
    translate: 0 calc(var(--_translate) * -1) 0;
  }

  to {
    translate: 0 var(--_translate) 0;
  }
}

:root {
  --color-light: #f7f8f8;
  --color-dark: #434a56;
  --layout-width: 1280;
  --fluid-ratio: calc(1 / var(--layout-width) * 100dvi);

  background-color: var(--color-light);
  color: var(--color-dark);
}

header {
  --_text-safe-area: calc(120 * var(--fluid-ratio));
  --_padding: max(calc(32 * var(--fluid-ratio)), 32px);

  display: block grid;
  grid-template-columns:
    var(--_padding) [text-start] var(--_text-safe-area)
    [image-start] 1fr [image-end text-end];
  block-size: max(100svb, 480px);
  padding-block: var(--_padding);

  &::after {
    content: "";

    /* 画像のオーバーレイ */
    grid-column: image;
    grid-row: 1;
    background-image: linear-gradient(rgb(0 0 0 / 10%), rgb(0 0 0));
  }
}

header > * {
  grid-row: 1;
}

h1 {
  z-index: 1;
  grid-column: text;
  align-self: center;
  background-image: linear-gradient(
    90deg,
    var(--color-dark) 0% var(--_text-safe-area),
    var(--color-light) var(--_text-safe-area) 100%
  );
  background-clip: text;
  color: transparent;
  font-family: Cinzel, serif;
  font-size: clamp(1.25rem, 0.071rem + 5.24cqi, 4rem);
  font-weight: 400;
}

.image {
  contain: strict;
  z-index: -1;
  grid-column: image;
}

section {
  display: block grid;
  row-gap: 1rlh;
  align-content: center;
  min-block-size: 100svb;
  padding-block: 64px;
  padding-inline: max(5svi, 20px);
}

h2 {
  font-size: clamp(1rem, 0.636rem + 1.82dvi, 2rem);
  text-align: center;
  text-wrap: balance;
}

p {
  max-inline-size: 60rem;
  margin-inline: auto;
}
