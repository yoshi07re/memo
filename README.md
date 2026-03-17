# BEM Element が増えすぎる問題への実務対策

## 対策A：Element は「アンカーだけ」付ける

全部に `__` を付けない。スタイルの起点（アンカー）になる要素だけ BEM クラスを持たせて、細部は要素セレクタやユーティリティで処理する。

```html
<section class="lp-hero">
  <div class="lp-hero__body">
    <h1>タイトル</h1>
    <p>リードテキスト</p>
  </div>
</section>
```

```css
.lp-hero__body > h1 { /* タイトル */ }
.lp-hero__body > p  { /* リード */ }
```

- ✅ BEM は「構造の要点」だけ
- ✅ 子要素が増えてもクラスが増えない
- ⚠️ `>` 前提なので DOM 変更が多い場所では使いすぎ注意（次の対策と併用）

---

## 対策B：繰り返しは"子コンポーネント化"して BEM を分割

子要素が多い場所は、だいたい「繰り返しブロック」。その部分だけ独立 Block に切ると、命名も CSS も分散して短くなる。

```html
<!-- 事例セクション -->
<section class="lp-case">
  <div class="lp-case__list">
    <!-- 事例カード（独立Block） -->
    <article class="case-card">
      <h3 class="case-card__title">事例タイトル</h3>
      <p class="case-card__desc">説明文</p>
    </article>
  </div>
</section>
```

- ✅ `lp-case__item__title__...` みたいな地獄を回避
- ✅ CSS も責務分離できる

---

## 対策C：「意味が薄い小物」は Utility に寄せる

`__text` `__desc` `__note` `__label` が増えるのは、見た目上の差分が理由なことが多い。そこは Utility で済ませるのが現実的。

```html
<p class="text-sm text-muted">補足テキスト</p>
<span class="font-bold text-accent">ラベル</span>
```

- ✅ BEM の Element を増やさず見た目調整できる
- ✅ 命名が短くなる

---

## 対策D：Element 命名のパターンを固定して増殖を抑える

Element 名が増えると破綻するので、有限の語彙で回すのがコツ。

### おすすめ固定セット

| Element 名 | 用途 |
|------------|------|
| `__inner` | 内側ラッパー |
| `__body` | メインコンテンツ領域 |
| `__head` | ヘッダー部 |
| `__foot` | フッター部 |
| `__title` | 見出し |
| `__lead` | リード文 |
| `__list` | リストコンテナ |
| `__item` | リスト項目 |
| `__cta` | CTA ボタン |
| `__actions` | 操作ボタン群 |
| `__media` | メディア領域 |
| `__img` | 画像 |
| `__icon` | アイコン |

```html
<!-- 比較表の例 -->
<section class="lp-compare">
  <div class="lp-compare__head">
    <h2 class="lp-compare__title">プラン比較</h2>
    <p class="lp-compare__lead">最適なプランをお選びください</p>
  </div>
  <div class="lp-compare__body">
    <div class="lp-compare__list">...</div>
  </div>
  <div class="lp-compare__foot">
    <a class="lp-compare__cta">お問い合わせ</a>
  </div>
</section>
```

これで「細かい名前を考える回数」が減る。

---

## 対策E：`data-*` を "JS フック専用" にしてクラス数を減らす

子要素が増える理由が「JS 用クラス」だとさらに増える。JS は `data-ui` に逃がすと、BEM は純粋に見た目だけにできる。

```html
<button class="lp-hero__cta" data-ui="open-modal">お申し込み</button>
```

```js
document.querySelector('[data-ui="open-modal"]')
```

- ✅ 見た目クラスと挙動フックを分離
- ✅ 命名衝突も減る

---

@theme {
  /* FontFamily */
  --font-jp:
    'Noto Sans JP', 'Hiragino Sans', 'Hiragino Kaku Gothic ProN', 'Meiryo',
    'sans-serif';
  --font-en: 'Google Sans Flex', sans-serif;

  /* Fontsize */
  --text-xs: 0.64rem;
  --text-sm: 0.8rem;
  --text-base: 0.9375rem;
  --text-lg: clamp(1.0625rem, 0.932rem + 0.552vw, 1.25rem);
  --text-xl: clamp(1.172rem, 1.01rem + 0.691vw, 1.563rem);
  --text-2xl: clamp(1.465rem, 1.262rem + 0.863vw, 1.953rem);
  --text-3xl: clamp(1.831rem, 1.578rem + 1.079vw, 2.441rem);
  --text-4xl: clamp(2.289rem, 1.973rem + 1.349vw, 3.052rem);
  --text-5xl: clamp(2.861rem, 2.466rem + 1.686vw, 3.815rem);
  --text-6xl: clamp(3.576rem, 3.083rem + 2.107vw, 4.768rem);
  --text-7xl: clamp(4.47rem, 3.854rem + 2.633vw, 5.96rem);
  --text-8xl: clamp(5.588rem, 4.818rem + 3.291vw, 7.45rem);
  --text-9xl: clamp(6.985rem, 6.022rem + 4.114vw, 9.313rem);
  --text-10xl: clamp(8.731rem, 7.528rem + 5.143vw, 11.641rem);

  /* LineHeight */
  --text-xs--line-height: 1.3;
  --text-sm--line-height: 1.5;
  --text-base--line-height: 1.75;
  --text-lg--line-height: 1.3;
  --text-xl--line-height: 1.3;
  --text-2xl--line-height: 1.3;
  --text-3xl--line-height: 1.3;
  --text-4xl--line-height: 1.3;
  --text-5xl--line-height: 1.2;
  --text-6xl--line-height: 1.2;
  --text-7xl--line-height: 1.2;
  --text-8xl--line-height: 1.2;
  --text-9xl--line-height: 1.2;
  --text-10xl--line-height: 1.2;

  /* Colors */
  --color-white-pure: #fff;
  --color-white: #f3efef;
  --color-black: #484848;
  --color-gray: #696969;
  --color-accent: #ffd34f;
  --color-line: #d4d4d1;

  /* Width */
  --max-content-width: 96rem;
  --max-small-width: 50rem;

  /* Spacing */
  --spacing-inner: clamp(
    1rem,
    calc(0.3784530386740331rem + 2.6519337016574585vw),
    2.5rem
  );
  --about-modal-max-height: calc(100dvh - 4rem);

  /* Z-Index */
  --z-canvas: 0;
  --z-ghost: 10;
  --z-ui: 20;
  --z-header: 100;
  --z-side: 200;
  --z-overlay: 999;
}

@layer base {
  :where(body) {
    position: relative;
    overflow-inline: clip;
    min-block-size: 100dvh;
  }

  :where(h1, h2, h3, h4, h5, h6):lang(ja) {
    font-feature-settings: 'palt';
    word-break: auto-phrase;
  }

  :where(p) {
    hyphens: auto;
  }

  :where(p):lang(ja) {
    font-kerning: normal;
  }

  :where(p):lang(en) {
    font-kerning: normal;
    text-wrap: pretty;
  }

  :where(pre, time, input, textarea, [contenteditable]) {
    text-autospace: no-autospace;
  }

  :where(address) {
    font-style: normal;
  }

  :where(img, svg) {
    width: 100%;
  }

  :focus:not(:focus-visible) {
    outline: none;
  }

  :focus-visible {
    outline-style: double;
    outline: 2px solid var(--color-accent);
    outline-offset: 2px;
  }

  main[tabindex='-1'] {
    outline: none;
  }

  * {
    min-inline-size: 0;
  }

  html {
    scroll-behavior: initial;
    scrollbar-gutter: stable;
    --base-vw: 375;
  }

  body {
    background-color: var(--color-white);
    color: var(--color-black);
    font-family: var(--font-jp);
    font-size: var(--text-base);
    letter-spacing: 0.08em;
    text-spacing-trim: trim-start;
    text-autospace: normal;
    line-break: strict;
    overflow-wrap: anywhere;
    color-scheme: dark;
  }

  @media not (width >= 375px) {
    html {
      font-size: calc(100 / var(--base-vw) * 1 * 16vw);
    }
  }

  @media (width >= 640px) and (width <= 767.98px) {
    html {
      --base-vw: 640;
      font-size: calc(100 / var(--base-vw) * 1 * 16vw);
    }
  }

  @media (width >= 1920px) {
    html {
      --base-vw: 1920;
      font-size: calc(100 / var(--base-vw) * 1 * 16vw);
    }
  }

  main[tabindex='-1'] {
    outline: none;
  }

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

  .lenis.lenis-scrolling iframe {
    pointer-events: none;
  }

  html.tw-about-modal-open,
  html.tw-about-modal-open body {
    overscroll-behavior: none;
  }
}

@layer utilities {
  *::-webkit-scrollbar {
    width: 6px;
    background-color: #444647;
  }

  *::-webkit-scrollbar-thumb {
    background-color: #333435;
    border-radius: 999px;
  }

  [data-about-scroll] {
    -ms-overflow-style: none;
    scrollbar-width: none;
  }

  [data-about-scroll]::-webkit-scrollbar {
    display: none;
    width: 0;
    height: 0;
    background-color: transparent;
  }

  .tw-wbr {
    word-break: keep-all;
    overflow-wrap: anywhere;
  }
}
