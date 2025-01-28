  @media not (width >= 375px) {
    html {
      font-size: calc(100 / var(--base-vw) * 1 * 16vw);
    }
  }

  @media (width >= 640px) and (width <= 767.98px) {
    html {
      font-size: calc(100 / var(--base-vw) * 1 * 16vw);

      --base-vw: 640;
    }
  }

  @media (width >= 1920px) {
    html {
      font-size: calc(100 / var(--base-vw) * 1 * 16vw);

      --base-vw: 1920;
    }
  }
