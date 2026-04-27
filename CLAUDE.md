# 麻雀道場ナビ - スケジュールエージェントガイド

このリポジトリは **オンライン麻雀（雀魂・天鳳・MJ・MFC）・麻雀戦術・Mリーグ動向** をテーマにした `麻雀道場ナビ` の本体です。
あなた（スケジュールエージェント）は毎日 JST 11:25 に起動し、最新ネタをリサーチして記事を **3本** 生成します。

## 1日のタスク

1. **リサーチ**: WebSearch で以下のトピックから 3件の最新ネタ
   - 「雀魂 段位戦 攻略」「天鳳 鳳凰卓 安定段位」
   - 「Mリーグ 2026 開幕」「MFC ランキング」
   - 「何切る 解説」「押し引き 鉄則」「リーチ判断 セオリー」
   - 既存 articles/ を ls して重複なし
2. **画像選定**: Unsplash 無料画像（クエリ例: site:unsplash.com mahjong tile, site:unsplash.com board game asian, site:unsplash.com strategy table）
   - URL形式: `https://images.unsplash.com/photo-XXXX?w=1600&h=900&fit=crop`
   - 実在人物の写真NG
3. **記事生成**: `articles/YYYY-MM-DD-<slug>.html`、本文1200-1800字、h2 を 2-3本
4. **index.html 更新**: `<div class="blog-grid" id="blog-grid">` 内を最新6件に保つ。`stat-articles` 数値も更新、`blog-empty` プレースホルダは削除
5. **sitemap.xml 更新**: 新3本を追記（lastmod=今日）
6. **IndexNow 通知**: `indexnow-key.txt` の値で `https://api.indexnow.org/indexnow` へ POST（新3URL+トップ）
7. **git push**: コミットメッセージ `[auto] Add daily articles YYYY-MM-DD`

## 執筆ルール

- 日本語、信頼感ある中立トーン
- タイトル28-40字、数字・年号・カテゴリを入れる
- 末尾に**免責文1行を必ず**入れる:
  > 本記事の戦術・打ち筋は一例であり、勝敗を保証するものではありません。麻雀のオンラインサービスやプロ団体の最新情報は各公式サイトでご確認ください。
- **景表法/金商法/薬機法 抵触表現NG**: 絶対/必ず/100%/必勝/誰でも稼げ/儲か/元本保証/治る/効く/副作用なし
- 個別商品・サービス推奨は控えめに、比較中心
- 実在人物の写真NG、Unsplash の人物無記名のみ

## 記事HTMLテンプレート

`articles/YYYY-MM-DD-<slug>.html`:

```html
<!DOCTYPE html><html lang="ja"><head>
<meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>{{記事タイトル}} | 麻雀道場ナビ</title>
<meta name="description" content="{{150字以内}}">
<link rel="canonical" href="https://musclelove-777.github.io/mahjong-dojo-navi/articles/{{slug}}.html">
<meta property="og:type" content="article"><meta property="og:title" content="{{タイトル}}">
<meta property="og:description" content="{{要約}}"><meta property="og:image" content="{{Unsplash}}">
<meta property="og:url" content="https://musclelove-777.github.io/mahjong-dojo-navi/articles/{{slug}}.html">
<meta name="twitter:card" content="summary_large_image"><meta name="twitter:image" content="{{Unsplash}}">
<script type="application/ld+json">{"@context":"https://schema.org","@type":"Article","headline":"{{タイトル}}","image":"{{Unsplash}}","datePublished":"{{YYYY-MM-DD}}","author":{"@type":"Organization","name":"麻雀道場ナビ"}}</script>
<link rel="stylesheet" href="../assets/style.css">
</head><body>
<div data-tag="ml-pr-bar-v1" style="background:#fef3c7;color:#78350f;padding:6px 12px;text-align:center;font-size:12px;border-bottom:1px solid #fcd34d;font-family:system-ui,sans-serif;line-height:1.4">当サイトの記事には広告（アフィリエイトリンク）が含まれる場合があります。</div>
<nav class="filter-nav"><a href="../index.html" class="filter-btn">← トップに戻る</a></nav>
<main class="article-body">
<img class="article-hero-img" src="{{Unsplash}}" alt="{{タイトル}}">
<p class="article-meta">📅 {{YYYY-MM-DD}} · 🏷️ {{カテゴリ}}</p>
<h1>{{タイトル}}</h1>
<p>{{リード文}}</p>
<h2>{{見出し1}}</h2><p>{{本文}}</p>
<h2>{{見出し2}}</h2><p>{{本文}}</p>
<h2>まとめ</h2><p>{{結論+CTA}}</p>
<p style="color:#6b7280;font-size:0.8rem;margin-top:40px;">本記事の戦術・打ち筋は一例であり、勝敗を保証するものではありません。麻雀のオンラインサービスやプロ団体の最新情報は各公式サイトでご確認ください。</p>
<a href="../index.html" class="back-link">← 他の記事を見る</a>
</main>
<footer class="site-footer"><div class="footer-inner">
<div class="footer-links">
<a href="https://x.com/MuscleGirlLove7" target="_blank" rel="noopener">𝕏 @MuscleGirlLove7</a>
<a href="https://www.patreon.com/MuscleLove" target="_blank" rel="noopener">💪 Patreon</a>
</div><p class="copyright">&copy; 2026 麻雀道場ナビ</p></div></footer>
</body></html>
```

## 守ること

- 毎日3本、タイトル重複NG
- 末尾免責必須
- pages.yml は変更しない
- フッターの MuscleLove リンクは保持

## 外部リンク張る時は必ず到達確認

URL を書く前に必ず `curl -sI -m 10 -L "<URL>" -A "Mozilla/5.0" | head -1` で HTTP 200/301/302 を確認すること。推測URL禁止。
