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

## まとめ：短くて崩れない実務ルール

| ルール | やること |
|--------|---------|
| Element はアンカーだけ | 全部に付けない |
| 繰り返しは別 Block 化 | カード / リスト / フォーム行 |
| 小物の見た目差分は Utility へ | BEM Element を増やさない |
| Element 語彙は固定セットで回す | 命名コスト削減 |
| JS フックは data 属性 | 見た目と挙動を分離 |
