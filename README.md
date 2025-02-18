https://codepen.io/yopida_re/pen/YPzPGMo
https://b-moon.net/responsive-font-size-with-clamp-and-custom-properties/
https://lopan.jp/css-custom-properties/variables/

// スクロールバーの幅を計算する関数
const getScrollbarWidth = () =>
  window.innerWidth - document.documentElement.clientWidth;

// スムーススクロール関数
const smoothScroll = () => {
  // スクロールリンク取得
  const targets = document.querySelectorAll('a[href^="#"]');
  if (targets.length === 0) {
    return;
  }

  function easing(t, b, c, d) {
    return c * (0.5 - Math.cos((t / d) * Math.PI) / 2) + b;
  }

  // スクロール速度
  const animeSpeed = 600;
  const scrollBusyClass = "is-scroll-busy";
  const bodyElm = document.body;

  // クリックイベント設定
  targets.forEach((target) => {
    target.addEventListener("click", (event) => {
      event.preventDefault();

      // スクロールイベント重複防止
      if (bodyElm.classList.contains(scrollBusyClass)) {
        return;
      }
      bodyElm.classList.add(scrollBusyClass);

      // hrefから遷移先を取得
      const href = target.getAttribute("href");
      const scrollStopTarget = document.querySelector(
        href === "#" || href === "" ? "html" : href
      );

      // 遷移先が存在しない場合は処理しない
      if (!scrollStopTarget) {
        bodyElm.classList.remove(scrollBusyClass);
        return;
      }

      // ヘッダーの高さ分をオフセット（存在しない場合は0）
      const header = document.querySelector("header");
      const headerHeight = header ? header.offsetHeight : 0;

      // 移動先の位置を算出
      const targetRectTop = scrollStopTarget.getBoundingClientRect().top;
      const currentScroll = window.pageYOffset || document.documentElement.scrollTop;
      const targetPosition = currentScroll + targetRectTop - headerHeight;

      // アニメーション開始時間
      let start;

      // スクロールアニメーション関数
      function mainAnime(timestamp) {
        if (start === undefined) {
          start = timestamp;
        }
        const elapsedTime = timestamp - start;
        if (elapsedTime > animeSpeed) {
          window.scrollTo(0, targetPosition);
          bodyElm.classList.remove(scrollBusyClass);
          return;
        }
        window.scrollTo(
          0,
          easing(elapsedTime, currentScroll, targetPosition - currentScroll, animeSpeed)
        );
        requestAnimationFrame(mainAnime);
      }

      // アニメーション初回呼び出し
      requestAnimationFrame(mainAnime);
    });
  });
};

// スムーススクロール関数呼び出し
smoothScroll();
