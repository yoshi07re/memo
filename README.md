.flex {
  --breakpoint: 640px;
  max-width: 1280px;
  display: block flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-inline: auto;
  padding-block: 120px;
}

.flex > * {
  flex-grow: 1;
  flex-basis: calc((var(--breakpoint) - 100%) * 9999);
}

.block {
  display: block grid;
  row-gap: 24px;
  grid-auto-columns: 1fr;
  align-content: center;
  justify-items: center;
}

.button {
  --_base-size: calc(400 * 1em / 16);
  --_foreground: #fff;
  --_background: #333;
  --_duration: 0.3s;
  --_padding: calc(24 * 1em / 16);

  display: inline grid;
  grid-template-columns: 1fr auto 1fr;
  column-gap: calc(8 * 1em / 16);
  align-items: center;
  inline-size: min(var(--_base-size), 100%);
  padding-block: calc(var(--_padding) + var(--leading-trim));
  padding-inline: var(--_padding);
  border-radius: 4px;
  background-color: color-mix(
    in sRGB,
    var(--_background),
    white var(--_lighten, 0%)
  );
  color: var(--_foreground);
  transition: background-color var(--_duration);

  &::before {
    content: "";
  }

  &::after {
    content: "";
    justify-self: end;
    inline-size: calc(8 * 1em / 16);
    aspect-ratio: 1;
    border-block-start: 1px solid;
    border-inline-end: 1px solid;
    translate: var(--_translate, 0);
    rotate: 45deg;
    transition: translate var(--_duration);
  }

  &:any-link:hover {
    @media (any-hover: hover) {
      --_lighten: 20%;
      --_translate: 4px;
    }
  }

  &:focus-visible {
    --_lighten: 20%;
    --_translate: 4px;
  }
}
