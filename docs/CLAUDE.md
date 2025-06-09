# CLAUDE.md

このファイルは Claude AI がプロジェクトを理解し、効率的に作業するための設定とガイドラインです。

## プロジェクト概要

**DMiyamo3のポートフォリオサイト**
- VR/AR技術、3Dプログラミング、数学をテーマにした制作活動のポートフォリオ
- GitHub Pagesでホスティングされる静的サイト
- レスポンシブデザイン、ダークモード対応

## ファイル構成

```
├── index.html          # メインページ（ポートフォリオ）
├── reflex.html         # Reflex Tapゲーム
├── prime-cascade.html  # Prime Cascadeゲーム
├── style.css           # 全体のスタイルシート
└── README.md           # プロジェクト説明
```

## 技術仕様

### フロントエンド
- **HTML5** - セマンティックマークアップ
- **CSS3** - カスタムプロパティ、Grid、Flexbox使用
- **Vanilla JavaScript** - フレームワーク不使用

### デザインシステム
- **カラーパレット**: HSLベースの統一カラーシステム
- **テーマ**: ライト/ダークモード対応
- **レスポンシブ**: モバイルファーストアプローチ

### 主要機能
- ダークモードトグル（ローカルストレージ対応）
- 作品カテゴリごとの色分け表示
- ミニゲーム集（反射神経測定・素数連鎖ゲーム）

## コーディング規約

### HTML
- セマンティックなタグを使用
- アクセシビリティ属性（aria-label等）を適切に設定
- Open Graphメタタグで適切な共有設定

### CSS
- カスタムプロパティ（CSS変数）でカラーパレット管理
- BEM的な命名規則（.works-category, .work-item等）
- レスポンシブはmin-widthベースのメディアクエリ

### JavaScript
- Vanilla JavaScript使用（フレームワーク不使用）
- ES6+記法を活用
- DOM操作は最小限に抑制

## デザインガイドライン

### カラーシステム
```css
--c-primary: hsl(220, 85%, 58%)      # メインカラー（青）
--c-featured: hsl(280, 70%, 58%)     # 代表作品（紫）
--c-vr: hsl(210, 75%, 55%)           # VR/AR（青系）
--c-display: hsl(150, 65%, 50%)      # 立体視技術（緑）
--c-tool: hsl(35, 80%, 55%)          # ツール（オレンジ）
```

### 作品表示
- 各カテゴリに専用色を設定
- 画像は最大320px幅で統一
- メタ情報はバッジ形式で表示

## 一般的なタスク

### 新しい作品を追加する場合
1. `index.html`の適切なカテゴリセクションに作品項目を追加
2. 画像URLと説明文を設定
3. 適切な`work-meta`クラスで展示情報を追加

### スタイル調整
1. `style.css`のカスタムプロパティを使用
2. ダークモード対応も同時に確認
3. モバイル表示の確認も必須

### ゲーム機能の修正・追加
1. **Reflex Tap**: `reflex.html`内のインラインJavaScript
   - 反射神経測定ゲーム
   - 3回の平均反応時間を計測

2. **Prime Cascade**: `prime-cascade.html`
   - 素数連鎖消去ゲーム
   - Canvas 2D + 物理演算システム
   - ローカルストレージでスコア保存
   - Claude Codeとの協力により作成

## サイト構成とデザインのベストプラクティス

### 情報アーキテクチャ設計指針

#### 1. 階層化されたコンテンツ構造
```
Hero Section (3-5作品)
├── 代表作品のみ大きく表示
├── 訪問者の興味を即座に引く
└── CTAでより多くの作品へ誘導

Category Navigation
├── タブ形式またはフィルター機能
├── VR/AR、立体視、ツール、数学の分類
└── 「すべて表示」オプション

Detailed Works Archive
├── ページネーションまたは無限スクロール
├── 検索・フィルタリング機能
└── 外部詳細ページへのリンク
```

#### 2. 視覚的階層の明確化
- **Hero作品**: 大きな画像 + 詳細説明
- **Featured作品**: 中サイズ画像 + 概要
- **Archive作品**: 小画像 + タイトルのみ
- **ナビゲーション**: 固定ヘッダーで素早いアクセス

### UX/UI改善指針

#### モバイルファースト設計
```css
/* 推奨ブレークポイント */
--mobile: 320px-767px     /* 作品を1列表示 */
--tablet: 768px-1023px    /* 作品を2列表示 */
--desktop: 1024px+        /* 作品を3列表示 */
```

#### インタラクション設計
- **ホバーエフェクト**: 控えめなトランジション（0.2s）
- **フォーカス管理**: キーボードナビゲーション対応
- **読み込み状態**: スケルトンUIまたはプログレッシブ画像読み込み

### パフォーマンス最適化戦略

#### 画像最適化
```html
<!-- 重要作品は WebP + fallback -->
<picture>
  <source srcset="hero-image.webp" type="image/webp">
  <img src="hero-image.jpg" alt="作品説明" loading="lazy">
</picture>

<!-- IntersectionObserver による遅延読み込み -->
<img data-src="work-image.jpg" class="lazy-load" alt="作品説明">
```

#### CSS設計原則
```css
/* コンポーネント指向のCSS */
.work-card { /* 基本スタイル */ }
.work-card--featured { /* バリエーション */ }
.work-card--archive { /* バリエーション */ }

/* カスタムプロパティでテーマ管理 */
.work-card {
  background: var(--surface-color);
  border: 1px solid var(--border-color);
  transition: var(--hover-transition);
}
```

#### JavaScript設計パターン
```javascript
// モジュールパターンで機能分割
const PortfolioApp = {
  navigation: NavigationModule,
  filtering: FilterModule,
  lazyLoading: LazyLoadModule,
  darkMode: ThemeModule
};
```

### アクセシビリティ指針

#### キーボードナビゲーション
- Tab順序の論理的配置
- Skip linkの実装
- フォーカストラップ（モーダル使用時）

#### スクリーンリーダー対応
```html
<section aria-labelledby="works-heading">
  <h2 id="works-heading">Featured Works</h2>
  <div role="grid" aria-label="作品一覧">
    <article role="gridcell" aria-describedby="work-1-desc">
      <h3>作品タイトル</h3>
      <p id="work-1-desc">作品説明</p>
    </article>
  </div>
</section>
```

### SEO・メタデータ戦略

#### 構造化データ
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "DMiyamo3",
  "jobTitle": "VR/AR Developer",
  "knowsAbout": ["Virtual Reality", "Augmented Reality", "3D Programming"]
}
</script>
```

#### Open Graph最適化
```html
<meta property="og:title" content="作品名 | Miyamo's Portfolio">
<meta property="og:description" content="作品の詳細説明">
<meta property="og:image" content="作品の代表画像URL">
<meta property="og:type" content="website">
```

### 推奨ファイル構造（将来的な拡張時）

```
├── index.html              # ランディングページ
├── works/
│   ├── index.html         # 全作品一覧
│   ├── vr-ar.html         # VR/AR作品
│   ├── display.html       # 立体視技術
│   └── tools.html         # ツール・ユーティリティ
├── games/
│   ├── reflex.html        # ゲーム集約
│   └── [other-games].html
├── about.html              # 詳細なAboutページ
├── assets/
│   ├── images/           # ローカル画像
│   ├── css/             # CSS分割
│   └── js/              # JavaScript分割
└── data/
    └── works.json        # 作品データ（将来的なCMS化）
```

## 注意事項

- 外部依存関係なし（CDNライブラリ等使用しない）
- GitHub Pagesの制約内での静的サイト運用
- 画像は外部URL使用（主にTwitter、GitHub）※重要作品はローカル化推奨
- SEO対応（meta description、Open Graph等）
- アクセシビリティ対応（focus-visible、aria属性等）
- Core Web Vitals指標を意識したパフォーマンス設計

## テストコマンド

### ローカル開発
```bash
# 簡易HTTPサーバー起動（Python）
python -m http.server 8000
# または（Node.js）
npx serve .
```

### チェック項目
- [ ] レスポンシブ表示確認
- [ ] ダークモード動作確認
- [ ] 全リンクの動作確認
- [ ] 画像読み込み確認
- [ ] Reflexゲーム動作確認
- [ ] Prime Cascadeゲーム動作確認
- [ ] ローカルストレージの最高記録保存確認

### 本番デプロイ
GitHub Pagesで自動デプロイ。`main`ブランチへのpushで更新される。

## ゲーム機能詳細

### Prime Cascade仕様
- **ゲーム性**: 素数をタップして割り切れる合成数を消去
- **物理演算**: 重力・バウンス・衝突判定を実装
- **制限時間**: 30秒
- **スコア保存**: `localStorage['primeCascadeBest']`
- **技術**: Canvas 2D、Vanilla JavaScript
- **UI**: インゲームオーバーレイ、アニメーション効果

### ゲーム追加時の手順
1. 新しいHTMLファイルを作成（単一ファイル構成）
2. `index.html`のMini Gamesセクションにリンク追加
3. レスポンシブ対応とダークモード考慮
4. CLAUDE.mdのチェック項目に追加