[
  {
    "slug": "20260201",
    "title": "サイトメンテナンスのお知らせ",
    "body": "2/1 02:00〜04:00 にメンテナンスを行います。\n期間中、一時的に表示が不安定になる場合があります。\nご迷惑をおかけしますが、ご了承ください。",
    "category": "maintenance",
    "publishedAt": "2026-02-01T09:00:00+09:00"
  },
  {
    "slug": "20260203",
    "title": "新機能：お問い合わせフォームの改善",
    "body": "スパム対策を強化し、送信完了までの導線を短縮しました。\nスマホでの入力体験も改善しています。",
    "category": "update",
    "publishedAt": "2026-02-03T12:30:00+09:00"
  },
  {
    "slug": "20260205",
    "title": "お知らせ一覧ページの表示速度を改善しました",
    "body": "キャッシュ戦略を見直し、初回表示と再訪問時の体感速度を改善しました。\nあわせて画像の最適化も実施しています。",
    "category": "performance",
    "publishedAt": "2026-02-05T18:10:00+09:00"
  },
  {
    "slug": "20260206",
    "title": "障害発生と復旧のご報告",
    "body": "本日 10:12〜10:28 の間、一部ページが表示できない状態が発生しました。\n原因はCDN設定の切り替え時の不整合で、現在は復旧済みです。\n再発防止としてデプロイ手順を更新しました。",
    "category": "incident",
    "publishedAt": "2026-02-06T11:00:00+09:00"
  },
  {
    "slug": "20260210",
    "title": "採用情報を更新しました",
    "body": "Web制作・運用ポジションの募集要項を更新しました。\n詳細は採用ページをご確認ください。",
    "category": "recruit",
    "publishedAt": "2026-02-10T09:00:00+09:00"
  }
]



<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>JSON → HTML Generator</title>
  <style>
    body { font-family: system-ui, -apple-system, sans-serif; padding: 16px; }
    button, input { padding: 10px; }
    .log { white-space: pre-wrap; background: #f5f5f5; padding: 12px; margin-top: 12px; }
  </style>
</head>
<body>
  <h1>JSON → 1レコード = 1ページ HTML生成</h1>

  <p>
    JSONファイル：
    <input id="jsonPath" value="./data.json" size="30" />
  </p>

  <p>
    サイトURL：
    <input id="siteOrigin" value="https://example.com" size="30" />
  </p>

  <button id="run">ZIPでダウンロード</button>

  <div id="log" class="log"></div>

  <script src="https://cdn.jsdelivr.net/npm/jszip@3.10.1/dist/jszip.min.js"></script>
  <script>
    const log = (msg) => document.getElementById("log").textContent = msg;

    const escapeHtml = (s) =>
      String(s ?? "")
        .replaceAll("&", "&amp;")
        .replaceAll("<", "&lt;")
        .replaceAll(">", "&gt;");

    const formatDate = (iso) => {
      if (!iso) return "";
      const d = new Date(iso);
      return `${d.getFullYear()}.${String(d.getMonth()+1).padStart(2,"0")}.${String(d.getDate()).padStart(2,"0")}`;
    };

    function buildHtml(item, siteOrigin) {
      const url = `${siteOrigin}/news/${item.slug}/`;
      const body = escapeHtml(item.body).replaceAll("\n", "<br>");

      return `<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>${escapeHtml(item.title)}</title>
  <meta name="description" content="${escapeHtml(item.body.slice(0,120))}">
  <meta property="og:type" content="article">
  <meta property="og:url" content="${url}">
</head>
<body>
  <main style="max-width:720px;margin:40px auto;font-family:system-ui">
    <time datetime="${item.publishedAt}">
      ${formatDate(item.publishedAt)}
    </time>
    <h1>${escapeHtml(item.title)}</h1>
    <p>${body}</p>
    <p><a href="/news/">← 一覧へ</a></p>
  </main>
</body>
</html>`;
    }

    document.getElementById("run").onclick = async () => {
      try {
        const jsonPath = document.getElementById("jsonPath").value;
        const siteOrigin = document.getElementById("siteOrigin").value.replace(/\/$/, "");

        const res = await fetch(jsonPath);
        if (!res.ok) throw new Error("JSONが読み込めません");

        const data = await res.json();
        if (!Array.isArray(data)) throw new Error("JSONは配列である必要があります");

        const zip = new JSZip();

        for (const item of data) {
          if (!item.slug) continue;
          zip.file(`${item.slug}/index.html`, buildHtml(item, siteOrigin));
        }

        const blob = await zip.generateAsync({ type: "blob" });
        const a = document.createElement("a");
        a.href = URL.createObjectURL(blob);
        a.download = "pages.zip";
        a.click();

        log(`OK: ${data.length}件からHTMLを生成しました`);
      } catch (e) {
        log("Error: " + e.message);
      }
    };
  </script>
</body>
</html>



