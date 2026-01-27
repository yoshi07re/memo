<dl class="barGraph barGraph--small barGraph--anchor_03 mt-3 mb-5">

  
  <div class="barGraph__group" style="--rows: 2">
    共通の文章
  </div>

  <div class="barGraph__item">
    <dt>内容</dt>
    <dd><span style="--bg:#0066cb; --size:92.1%">55.25%</span></dd>
  </div>

  <div class="barGraph__item">
    <dt>内容の魅力</dt>
    <dd><span style="--bg:#0066cb; --size:92.1%">55.25%</span></dd>
  </div>

  <div class="barGraph__group" style="--rows: 2">
    共通の文章
  </div><div class="barGraph__item">
    <dt>内容の魅力</dt>
    <dd><span style="--bg:#0066cb; --size:92.1%">55.25%</span></dd>
  </div><div class="barGraph__item">
    <dt>内容の魅力</dt>
    <dd><span style="--bg:#0066cb; --size:92.1%">55.25%</span></dd>
  </div>
  <div class="barGraph__item barGraph__scaleRow">
    <dt aria-hidden="true"></dt>
    <dd style="background:none;border:none;padding-block:0">
      <div class="barGraph-scale">
        <span style="--left:-4px">0</span>
        <span>20</span>
        <span style="--left:2px">40</span>
        <span style="--left:4px">60</span>
      </div>
    </dd>
  </div>
</dl>


.barGraph{
  display:grid;
  /* ①共通列 ②dt列 ③dd列 */
  grid-template-columns:
    minmax(80px, max-content)
    minmax(var(--min-width, 40px), max-content)
    1fr;
  gap: 0 8px;
  align-items: center;
}

/* 各行は “中身をグリッドに直配置” したいので display: contents */
.barGraph__item{ display: contents; }

.barGraph__item dt{
  grid-column: 2;
  font-size: 13px;
  text-align: right;
}

.barGraph__item dd{
  grid-column: 3;
  display: flex;
  font-size: 14px;
  border-right: 1px solid #e0e0e0;
  background-image: repeating-linear-gradient(to right, #e0e0e0 0px, #e0e0e0 1px, transparent 1px, transparent 25%);
  padding-block: 8px;
  margin-bottom: 0;
}

.barGraph--anchor_03 .barGraph__item dd{
  background-image: repeating-linear-gradient(to right, #e0e0e0 0px, #e0e0e0 1px, transparent 1px, transparent 33.333%);
}

.barGraph__item dd > span{
  position: relative;
  display: block;
  width: var(--size);
  padding-block: 8px;
  background-color: var(--bg);
  color: var(--text, #fff);
  text-align: center;
  white-space: nowrap;
}

.barGraph--small .barGraph__item dd > span{ padding-block: 0px; }

/* 共通文章（左列に置いて、行数分だけ縦に伸ばす） */
.barGraph__group{
  grid-column: 1;
  grid-row: span var(--rows);
  align-self: center;          /* 中央寄せ */
  font-size: 12px;
  color: #666;
  white-space: nowrap;
}

/* 目盛り行は共通列を空にしたい（必要なら） */
.barGraph__scaleRow dt{ grid-column: 2; }
.barGraph__scaleRow dd{ grid-column: 3; }
