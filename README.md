.grid-container {
  container-type: inline-size;
  inline-size: min(var(--container-size), 100%);
  margin-inline: auto;
}

.grid {
  --_template: "title" "subtitle" "image" "description";

  display: block grid;
  reading-flow: grid-rows;
  grid-template: var(--_template);
  gap: clamp(8px, 2cqi, 16px) clamp(16px, 4cqi, 32px);

  @container (600px <= inline-size) {
    --_template: "image title" "image subtitle" "image description" / 1fr 1fr;
  }

  & [style*="--grid-area:"] {
    grid-area: var(--grid-area);
  }
}

@property --grid-area {
  syntax: "*";
  inherits: false;
  initial-value: auto;
}

.hgroup {
  display: contents;

  & h1 {
    font-size: 1.5rem;
    line-height: 1.25;
  }

  & p {
    font-size: 1.25rem;
    line-height: 1.25;
  }
}

.image {
  position: relative;

  &::before {
    content: "";
    display: block flow;
    aspect-ratio: 16 / 9;
  }

  & img {
    position: absolute;
    inset: 0;
    inline-size: 100%;
    block-size: 100%;
    object-fit: cover;
  }
}

.description {
  display: block grid;
  row-gap: 1em;
  align-self: start;
}

@property --container-size {
  syntax: "<length>";
  inherits: false;
  initial-value: 640px;
}

.controls {
  display: block grid;
  row-gap: 32px;
  inline-size: min(640px, 100%);
  margin-inline: auto;

  & input {
    --_accent: blue;
    --_foreground: oklch(from var(--_accent) calc(l * 1.5) c h);
    --_background: oklch(from var(--_accent) calc(l * 1.8) c h);
    --_border: oklch(from var(--_accent) calc(l * 2) calc(c * 0.3) h);
    --_thumb-size: 16px;

    inline-size: 100%;
    block-size: 12px;
    border: solid 4px var(--_border);
    border-radius: calc(1px / 0);
    background-color: var(--_background);
    appearance: none;
    cursor: pointer;

    &::-webkit-slider-thumb {
      --_thumb-shadow: 0px 3px 6px 0px rgb(0 0 0 / 15%);

      inline-size: var(--_thumb-size);
      aspect-ratio: 1;
      border-radius: calc(1px / 0);
      box-shadow: var(--_thumb-shadow);
      background-color: var(--_foreground);
      appearance: none;
    }

    &:active::-webkit-slider-thumb {
      --_thumb-shadow: 0px 3px 6px 0px rgb(0 0 0 / 15%);
    }

    &::-moz-range-thumb {
      --_thumb-shadow: 0px 3px 6px 0px rgb(0 0 0 / 15%);

      inline-size: var(--_thumb-size);
      aspect-ratio: 1;
      border-radius: calc(1px / 0);
      box-shadow: var(--_thumb-shadow);
      background-color: var(--_foreground);
      appearance: none;
    }

    &::-moz-focus-outer {
      border: unset;
    }
  }

  & p {
    justify-self: center;
  }
}

:root {
  background-color: #fcfcfc;
  font-family: "open sans", sans-serif;
}

body {
  display: block grid;
  row-gap: 64px;
  align-content: start;
  padding: max(20px, 5dvi);
}
