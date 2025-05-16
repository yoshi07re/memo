<ul>
  <li class="card">
  <a class="link" href="https://example.com/">
    <h2 class="title">タイトルタイトルタイトルタイトルタイトルタイトルタイトルタイトルタイトル</h2>
    <p class="description">本文テキスト</p>
  </a>
  <p class="tags">
    <a href="https://example.com/hello/">#hello</a>
    <a href="https://example.com/world/">#world</a>
  </p>
</li>
<li class="card">
  <a class="link" href="https://example.com/">
    <h2 class="title">タイトル</h2>
    <p class="description">本文テキスト本文テキスト本文テキスト本文テキスト本文テキスト本文テキスト本文テキスト本文テキスト本文テキスト本文テキスト本文テキスト本文テキスト本文テキスト本文テキスト</p>
  </a>
  <p class="tags">
    <a href="https://example.com/hello/">#hello</a>
      <a href="https://example.com/hello/">#hello</a>
      <a href="https://example.com/hello/">#hello</a>
    <a href="https://example.com/hello/">#hello</a>
    <a href="https://example.com/hello/">#hello</a>
    <a href="https://example.com/hello/">#hello</a>
    <a href="https://example.com/world/">#world</a>
  </p>
</li>
</ul>



.card {
  display: grid;
  grid-template-rows: subgrid;
  grid-row: span 3;
}

.link {
  display: grid;
  grid-template-rows: subgrid;
  grid-row: 1 / 4;
  grid-column: 1;
}

.tags {
  grid-row: 3 / 4;
  grid-column: 1;
  align-self: start;
}
ul {
  max-width: 600px;
  display: grid;
  grid-template-columns: 1fr 1fr;
}
