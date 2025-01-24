<style is:global>
  :root {
    --accent: 136, 58, 234;
    --accent-light: 224, 204, 250;
    --accent-dark: 49, 10, 101;
    --accent-gradient: linear-gradient(45deg, rgb(var(--accent)), rgb(var(--accent-light)) 30%, white 60%);
  }

  *::-webkit-scrollbar {
    width: 6px;
    background: #444647;
  }

  ::-webkit-scrollbar-thumb {
    background: #333435;
    border-radius: 999px;
  }

  html {
    background: #13151a;
    background-size: 224px;
    scroll-behavior: initial;

    --base-vw: 375;
  }

  body {
    position: relative;
    min-height: 100%;
    overflow-x: hidden;
    font-family: 'Noto Sans JP', 'Hiragino Sans', 'Hiragino Kaku Gothic ProN', Meiryo, sans-serif;
    font-size: 0.9375rem;
    font-feature-settings: 'palt';
    line-height: 1;
    letter-spacing: 0.1em;
    word-break: normal;
    overflow-wrap: anywhere;
    line-break: strict;
  }

  li {
    list-style: none;
  }

  address {
    font-style: normal;
  }

  :focus:not(:focus-visible) {
    outline: none;
  }

  :focus-visible {
    outline-style: double;
    outline-color: #ffd34e;
  }

  main[tabindex='-1'] {
    outline: none;
  }

  /* lenis */
  html.lenis,
  html.lenis body {
    height: auto;
  }

  .lenis.lenis-smooth {
    scroll-behavior: auto !important;
  }

  .lenis.lenis-smooth [data-lenis-prevent] {
    overscroll-behavior: contain;
  }

  .lenis.lenis-stopped {
    /* overflow: hidden; */
    overflow: auto;
  }

  .lenis.lenis-scrolling iframe {
    pointer-events: none;
  }

  /* html.is-changing .transition-main {
    transition: opacity 250ms ease-in-out;
  }

  html.is-animating .transition-main {
    opacity: 0;
  } */
</style>
