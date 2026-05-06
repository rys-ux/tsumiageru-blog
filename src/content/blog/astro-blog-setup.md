---
title: 'AstroでZenn風ブログを作った話'
description: '静的サイトジェネレーターのAstroを使って、Zennライクなデザインのブログを構築しました。その構成と工夫したポイントを紹介します。'
pubDate: '2026-05-04'
tags: ['Astro', 'ブログ', 'フロントエンド']
emoji: '🛸'
---

## なぜ Astro を選んだのか

ブログを作るにあたって、いくつかのフレームワークを検討しました。

| フレームワーク | 特徴 |
|---|---|
| Next.js | React 製・多機能だが複雑 |
| Gatsby | GraphQL が必要で学習コスト高 |
| **Astro** | シンプル・高速・Markdown 対応が強力 |

Astro を選んだ理由は主に3つです：

1. **デフォルトでゼロ JavaScript** — 不要な JS を送らないので高速
2. **Markdown/MDX が強力** — Content Collections で型安全に管理できる
3. **シンプルな構文** — `.astro` ファイルが直感的でわかりやすい

## プロジェクト構成

```
src/
├── content/
│   ├── config.ts        # コレクションのスキーマ定義
│   └── blog/            # Markdown 記事ファイル
│       └── *.md
├── layouts/
│   ├── BaseLayout.astro  # 共通レイアウト
│   └── BlogPostLayout.astro  # 記事ページ用
├── components/
│   ├── Header.astro
│   └── Footer.astro
├── pages/
│   ├── index.astro      # トップ（記事一覧）
│   ├── about.astro      # このブログについて
│   └── blog/
│       └── [slug].astro # 記事詳細（動的ルート）
└── styles/
    └── global.css
```

## Content Collections とは

Astro の Content Collections は、Markdown ファイルを型安全に管理できる機能です。

`src/content/config.ts` でスキーマを定義するだけで、フロントマターの型チェックが自動で行われます。

```typescript
import { defineCollection, z } from 'astro:content';

const blog = defineCollection({
  type: 'content',
  schema: z.object({
    title: z.string(),
    description: z.string(),
    pubDate: z.coerce.date(),
    tags: z.array(z.string()).default([]),
    emoji: z.string().default('📝'),
  }),
});

export const collections = { blog };
```

## デザインのポイント

Zenn 風のデザインで意識したことは：

- **余白を十分に取る** — 読みやすさを最優先
- **アクセントカラー** — `#3EA8FF` のブルーをメインに
- **カードUI** — 記事一覧をカードで表示してホバーエフェクト
- **絵文字アイコン** — 記事ごとに絵文字を設定してビジュアルにメリハリ

## まとめ

Astro は本当にシンプルで、ブログ用途には最適だと感じました。

記事を書くのに集中できる環境が整ったので、あとはコンテンツを積み上げるだけです！
