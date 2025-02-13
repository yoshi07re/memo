https://codepen.io/yopida_re/pen/YPzPGMo
https://b-moon.net/responsive-font-size-with-clamp-and-custom-properties/
https://lopan.jp/css-custom-properties/variables/


*,
::before,
::after {
  --clamp-root-font-size: 16;
  --clamp-slope: calc((var(--clamp-max) - var(--clamp-min)) / (var(--clamp-viewport-max) - var(--clamp-viewport-min)));
  --clamp-y-axis-intersection: calc(var(--clamp-min) - (var(--clamp-slope) * var(--clamp-viewport-min)));
  --clamp-preffered-value: calc(
    var(--clamp-y-axis-intersection) * (1rem / var(--clamp-root-font-size)) + (var(--clamp-slope) * 100vi)
  );
  --clamp: clamp(
    calc(var(--clamp-min) * (1rem / var(--clamp-root-font-size))),
    var(--clamp-preffered-value),
    calc(var(--clamp-max) * (1rem / var(--clamp-root-font-size)))
  );

  font-size: var(--clamp);
}

/* bodyにデフォルト値を設定する */
body {
  --clamp-viewport-min: 375;
  --clamp-viewport-max: 1200;
  --clamp-min: 14;
  --clamp-max: 16;
}


* {
   /* font-size: calc(var(--size) * var(--px-to-rem)); */
  --to-rem: calc(var(--size, 16) / 16 * 1rem);
}

/* 使用時 */
p {
  --size: 14;
  font-size: var(--to-rem);
}
