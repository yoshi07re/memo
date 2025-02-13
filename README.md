https://codepen.io/yopida_re/pen/YPzPGMo
https://b-moon.net/responsive-font-size-with-clamp-and-custom-properties/


:root {
  --font-size: 100;
  --rF: calc(16 * var(--font-size) / 100); /* root font size 16 */
  --minW: 375; /* viewport width at the minimum font size */
  --maxW: 1200; /* viewport width at the max font size */
}

.html {
  font-size: calc(var(--font-size) * 1%); /* 16px */
}

body {
  --minF: 14; /* minimum font size 14px */
  --maxF: 16; /* max font size 16px */
  font-size: clamp(calc(var(--minF) / 16 * 1rem), 
                   calc(var(--minF) / 16 * 1rem + 
                   (var(--maxF) - var(--minF)) / (var(--maxW) - var(--minW)) * 
                   (100vw - var(--minW) * 1px) * var(--rF)), 
                   calc(var(--maxF) / 16 * 1rem));
}

h1 {
  --minF: 24; /* minimum font size 24px */
  --maxF: 48; /* max font size 48px */
  font-size: clamp(calc(var(--minF) / 16 * 1rem), 
                   calc(var(--minF) / 16 * 1rem + 
                   (var(--maxF) - var(--minF)) / (var(--maxW) - var(--minW)) * 
                   (100vw - var(--minW) * 1px) * var(--rF)), 
                   calc(var(--maxF) / 16 * 1rem));
}
