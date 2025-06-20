# 新規投稿作成機能 - 使用ガイド

## 🎯 機能概要

新規投稿作成機能は、ユーザー投稿をシミュレートしてAI監視システムの動作を確認できる機能です。テスト目的、デモンストレーション、システム動作確認に使用します。

## 🚀 アクセス方法

**URL**: http://localhost:3001/create-post

サイドバーの「新規投稿作成」メニューからアクセスできます。

## 📋 使用方法

### 1. 基本的な投稿作成手順

1. **ユーザー情報入力**
   - ユーザーID: 例「manga_fan_123」（必須）
   - コンテンツタイプ: テキスト/画像

2. **作品情報入力（任意）**
   - 漫画タイトル: 例「ワンピース」
   - 話数: 例「1001」

3. **投稿内容入力**
   - 投稿内容を入力欄に記入（必須）
   - またはサンプルコメントをクリックして自動入力

4. **投稿作成**
   - 「投稿作成」ボタンをクリック
   - 即座に結果が表示されます

5. **結果確認**
   - 投稿ID、ステータス、メッセージを確認
   - 投稿履歴に自動追加

### 2. 画面構成

```
┌─────────────────────────────────────────────────────┐
│ 新規投稿作成                                        │
├─────────────────────────────────────────────────────┤
│ ┌─────────────────────────────┐  ┌───────────────────┐│
│ │ 投稿情報                    │  │ 投稿履歴          ││
│ │                             │  │ ┌───────────────┐ ││
│ │ ユーザーID [_____________]  │  │ │🟢 ID:9 承認済み │ ││
│ │ タイプ [テキスト ▼]        │  │ │ test_user       │ ││
│ │                             │  │ │ 12:34           │ ││
│ │ サンプルユーザー:           │  │ └───────────────┘ ││
│ │ [test_user_001] [manga_fan] │  │ ┌───────────────┐ ││
│ │                             │  │ │🟡 ID:8 待機中  │ ││
│ │ ───────────────────────────  │  │ │ spoiler_user    │ ││
│ │                             │  │ │ 12:30           │ ││
│ │ 作品情報（任意）            │  │ └───────────────┘ ││
│ │ 漫画タイトル [____________] │  │                   ││
│ │ 話数 [____]                 │  │ 使用方法          ││
│ │                             │  │ 1. ユーザーID入力 ││
│ │ 人気漫画:                   │  │ 2. 作品情報入力   ││
│ │ [ワンピース] [進撃の巨人]   │  │ 3. 投稿内容入力   ││
│ │                             │  │ 4. 投稿作成実行   ││
│ │ ───────────────────────────  │  │ 5. 結果確認       ││
│ │                             │  │                   ││
│ │ 投稿内容                    │  │ 期待される動作:   ││
│ │ [_____________________]     │  │ 通常→自動承認     ││
│ │ [_____________________]     │  │ ネタバレ→待機     ││
│ │ [_____________________]     │  │ 違反→自動拒否     ││
│ │                             │  │                   ││
│ │ サンプルコメント:           │  │                   ││
│ │ 通常    ネタバレ  不適切    │  │                   ││
│ │ [面白い] [犯人は] [クソ]    │  │                   ││
│ │ [楽しみ] [死ぬ]   [無駄]    │  │                   ││
│ │                             │  │                   ││
│ │ [投稿作成] [クリア]         │  │                   ││
│ │                             │  │                   ││
│ │ ✅ 投稿が正常に作成されました！│  │                   ││
│ │ 投稿ID: 9 | ステータス: 承認済み│  │                   ││
│ └─────────────────────────────┘  └───────────────────┘│
└─────────────────────────────────────────────────────┘
```

## 📊 サンプルデータ

### プリセットされたサンプル

#### ユーザーID
```
test_user_001
manga_fan_123  
review_writer
casual_reader
spoiler_user
```

#### 人気漫画タイトル
```
ワンピース
進撃の巨人
鬼滅の刃
呪術廻戦
僕のヒーローアカデミア
ドラゴンボール
ナルト
銀魂
```

#### サンプルコメント

**通常コメント（自動承認予定）:**
```
この漫画本当に面白いです！
作画がとても綺麗ですね
キャラクターがみんな魅力的
次回が楽しみです
おすすめの漫画教えてください
```

**ネタバレコメント（レビュー待ち予定）:**
```
犯人は○○でした
最終回で主人公が死ぬ
ラスボスの正体は○○
次回で重要キャラが退場
隠されていた秘密が明らかに
```

**不適切コメント（レビュー待ち/拒否予定）:**
```
この作者の作品はクソつまらない
時間の無駄だった
こんな漫画読むやつの気が知れない
作者は才能がない
最悪の展開
```

**スパムコメント（レビュー待ち予定）:**
```
私のサイトをチェックしてください http://example.com
格安で漫画売ります。連絡ください
フォロバします！
相互フォローお願いします
私のYouTubeチャンネル登録してください
```

## 🔄 AIシステムの判定パターン

### 期待される自動判定結果

| コメントタイプ | AIスコア | 予想ステータス | 理由 |
|---------------|---------|---------------|------|
| 通常・ポジティブ | 0.0-0.2 | 自動承認 | リスクなし |
| 軽微な批判 | 0.2-0.4 | 自動承認 | 低リスク |
| ネタバレ | 0.5-0.8 | レビュー待ち | 中リスク |
| 誹謗中傷 | 0.5-0.8 | レビュー待ち | 中リスク |
| 個人情報 | 0.8-1.0 | 自動拒否 | 高リスク |
| 重度の違反 | 0.8-1.0 | 自動拒否 | 高リスク |

### リスク検出例

#### ネタバレ検出
```
入力: "犯人は田中先生でした"
期待結果:
- AIスコア: ~70%
- 検出リスク: spoiler
- ステータス: pending (レビュー待ち)
```

#### 誹謗中傷検出
```
入力: "この作者の作品はクソつまらない"
期待結果:
- AIスコア: ~60%
- 検出リスク: harassment, brand_damage  
- ステータス: pending (レビュー待ち)
```

#### 個人情報検出
```
入力: "連絡先: 090-1234-5678"
期待結果:
- AIスコア: ~90%
- 検出リスク: personal_info
- ステータス: rejected (自動拒否)
```

## 🎯 使用場面

### 1. システムテスト
```
新機能リリース前の動作確認
→ 各タイプのコメントでAI判定をテスト
→ 期待通りの結果が得られるか検証
```

### 2. デモンストレーション
```
クライアント向けのシステム紹介
→ リアルタイムでAI判定の様子を実演
→ 各機能の有効性をアピール
```

### 3. トレーニング・教育
```
新人スタッフの研修
→ 様々なコメントパターンを体験
→ AI判定とモデレーションの流れを理解
```

### 4. パフォーマンステスト
```
システム負荷テスト
→ 大量の投稿を短時間で作成
→ レスポンス時間や安定性を確認
```

## 📈 投稿履歴機能

### 履歴表示内容
- **投稿ID**: システム内での一意識別子
- **ユーザーID**: 投稿者名
- **ステータス**: AI判定結果（承認済み/レビュー待ち/拒否済み）
- **作品情報**: 漫画タイトル・話数（入力した場合）
- **投稿時刻**: 作成タイムスタンプ
- **投稿内容**: 先頭部分のプレビュー

### ステータス表示
- 🟢 **承認済み**: 自動承認された安全な投稿
- 🟡 **レビュー待ち**: 人間のレビューが必要な投稿  
- 🔴 **拒否済み**: 自動拒否された問題のある投稿

### データ連携
- ダッシュボードの統計数値に即座に反映
- 全投稿一覧に新しい投稿として表示
- レビュー待ちの場合はレビューキューに追加

## 🔧 高度な使用方法

### バッチテスト
```javascript
// 複数のテストケースを順次実行
const testCases = [
  { user: "test_001", content: "面白い漫画ですね" },
  { user: "test_002", content: "犯人は田中です" },
  { user: "test_003", content: "クソつまらない作品" }
];

// 各ケースを順番に投稿してAI判定を確認
```

### カスタムテストケース
```
特定の作品や状況に応じたテストケースを作成:
- 作品固有の専門用語
- ファンコミュニティ特有の表現
- 季節イベント関連のコメント
```

### A/Bテスト
```
同様の内容で表現を変えて判定結果を比較:
- "犯人は田中です" vs "田中が犯人でした"
- "つまらない" vs "面白くない" vs "退屈"
```

## ⚠️ 注意事項

### 制限事項
- 作成された投稿は実際のシステムに保存される
- テスト用投稿が多くなると統計データに影響する
- 投稿履歴はセッション中のみ保持（ページリロードで消失）

### ベストプラクティス
- テスト前に現在の統計データをメモしておく
- 大量のテスト投稿後はデータベースのクリーンアップを検討
- 本番環境では使用を控える
- 実際のユーザー名や個人情報は使用しない

### セキュリティ
- 機密情報やセンシティブな内容のテストは避ける
- 実在の人物名や企業名は使用しない
- テスト用であることが明確なユーザーIDを使用

## 🔄 今後の改善予定

- [ ] バルク投稿機能（CSVアップロード）
- [ ] テストケース保存・読み込み機能
- [ ] 投稿履歴の永続化
- [ ] より詳細なAI分析結果表示
- [ ] 画像投稿のシミュレーション機能

## 💡 効果的な活用方法

### 定期的なシステム確認
```
週次/月次でのルーチンチェック:
1. 各リスクカテゴリのサンプルを投稿
2. AI判定結果が期待値と一致するか確認
3. 異常があれば早期発見・対応
```

### 新機能テスト
```
AI判定ロジック更新時:
1. 既存のテストケースで回帰テスト
2. 新しいパターンでの動作確認
3. 判定精度の向上を確認
```

この機能により、管理者はシステムの動作を包括的に確認し、AI監視機能の信頼性を継続的に検証できます。