https://codepen.io/yopida_re/pen/YPzPGMo
https://b-moon.net/responsive-font-size-with-clamp-and-custom-properties/
https://lopan.jp/css-custom-properties/variables/

window.addEventListener("resize", () => {
  if (!isMobile()) {
    // ハンバーガーメニューの状態をリセット
    humberger.classList.remove(CLASS);
    menu.classList.remove(CLASS);
    backgroundFix(false);
    humberger.setAttribute("aria-expanded", "false");
    flg = false;
    
    // アコーディオンの状態をリセット（モバイル用トリガーとコンテンツ）
    document.querySelectorAll(".js-sp-accordion-trigger").forEach((trigger) => {
      trigger.classList.remove(CLASS);
      trigger.setAttribute("aria-expanded", "false");
      // 次の要素がアコーディオンのコンテンツの場合、クラスを除去
      const content = trigger.nextElementSibling;
      if (content && content.classList.contains(CLASS)) {
        content.classList.remove(CLASS);
      }
    });
    
    // デスクトップ用のアコーディオン（もし別途管理している場合）
    document.querySelectorAll(".js-accordion").forEach((content) => {
      content.classList.remove(CLASS);
    });
  }
});
