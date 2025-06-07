# Copilot Agent Instructions — Simple Portfolio

## 0. TL;DR
- **最小構成**: `index.html` と `style.css` の 2 ファイルのみ  
- **目的**: 個人ポートフォリオ（自己紹介・作品リンク）の公開  
- **重要**: 公開 OSS と連続 30 token 以上の一致を避け、オリジナルコードを維持する  

---

## 1. 禁止・回避事項（Public-Code Avoidance）
1. **OSS サンプルをそのまま貼り付け**ない。コピペ候補は必ず名称・構造をリファクタすること。  
2. 外部テンプレートを使う場合でも **一致スコア 0.25 未満** に抑える。  
3. MIT/Apache-2.0 以外のライセンス部分は提案しない。  
4. 著作権表記入りコメントは削除するか、自動生成した旨を記載して置換。  
5. `detect-public-source("index.html", "style.css")` でスコア >0.25 の場合、自動で**変数名・レイアウト構造を変更**してからコミット。

---

## 2. ファイルガイド
<repo>/
├─ index.html # ルート直下 / GitHub Pages の公開対象
└─ style.css # 外部 CSS。クラス命名は BEM / Utility どちらでも可


### index.html に必須
- `<!doctype html>` から始まる HTML5
- `<meta charset="utf-8">`, `<meta name="viewport" ...>`  
- OGP 用 `<meta property="og:...">` を 3 つ以上（title, type, image）
- `<header>` / `<main>` / `<footer>` のセマンティック要素
- 作品サムネは **画像タグの代替テキスト**を必ず入れる

### style.css 指針
- リセットは独自 20 行程度の最小スタイルに留める  
- 可読性を優先し、コメントでセクション区切りを書く  
- メディアクエリは `@media (min-width: 768px)` 1 箇所で OK  
- カラーパレットは HSL で定義し `:root { --c-primary: hsl(...); }` を推奨

---

## 3. UI / UX ルール
1. **ロードサイズ ≤ 50 KB（gzip）** を目標  
2. ダークモード対応（`prefers-color-scheme`）: `body.dark` トグルで実装  
3. キーボード操作: `:focus-visible` にカスタムアウトライン  
4. レスポンシブ確認: DevTools の iPhone SE / Pixel 5 幅で崩れないこと

---
