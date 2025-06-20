# フロントエンド動作確認ガイド

## 🚀 現在の状況

✅ **バックエンドサーバー**: http://localhost:5001 で正常動作  
✅ **フロントエンドサーバー**: http://localhost:3001 で正常動作  
✅ **APIプロキシ**: 正常に設定済み  
✅ **TypeScript型チェック**: エラーなし  
✅ **テストデータ**: 作成済み

## 📋 動作確認手順

### 1. ブラウザでアクセス
```
http://localhost:3001/
```

### 2. 確認すべき画面

#### ダッシュボード（トップページ）
- サイドバーに「AI Moderation」ロゴ
- メニュー項目: ダッシュボード、レビューキュー、分析
- 統計カード: 承認済み、レビュー待ち、拒否済み
- 各カードに数値が表示される
- **新機能**: タブで「システム概要」と「全投稿一覧」を切り替え可能

**期待される数値（テストデータに基づく）:**
- 承認済み投稿: 4件
- レビュー待ち: 1件  
- 拒否された投稿: 1件

#### 新機能: 全投稿一覧タブ
- ダッシュボードで「全投稿一覧」タブをクリック
- テーブル形式で全投稿を表示
- 各行をクリックして詳細を展開可能
- ステータスフィルター（すべて/承認済み/レビュー待ち/拒否済み）
- 検索機能（投稿内容、ユーザーID、作品名）
- ページネーション機能
- **期待される表示**: 6件の投稿が表示される

#### レビューキューページ
- サイドバーの「レビューキュー」をクリック
- レビュー待ちの投稿カードが表示される
- カードに以下の情報が含まれる:
  - 投稿ID: 4
  - ユーザー: demo_user2
  - AIスコア: 70.0%
  - 検出されたリスク: ネタバレ
  - 投稿内容: "ネタバレ注意: 犯人は佐藤でした..."
  - 承認・拒否ボタン

### 3. コンソールエラーのチェック

#### ブラウザ開発者ツール（F12）でチェック項目:

**Console（コンソール）タブ:**
```
エラーがないことを確認:
✅ 404エラーがない
✅ TypeScriptエラーがない  
✅ React Hook エラーがない
✅ API呼び出しエラーがない
```

**Network（ネットワーク）タブ:**
```
API呼び出しが成功していることを確認:
✅ GET /api/moderation/stats → 200 OK
✅ GET /api/moderation/pending → 200 OK
✅ レスポンスデータが正しい
```

### 4. 機能テスト

#### 承認機能のテスト:
1. レビューキューページでカードの「承認」ボタンをクリック
2. 成功メッセージが表示される
3. カードがリストから消える
4. ダッシュボードの統計が更新される

#### 拒否機能のテスト:
1. 「拒否」ボタンをクリック
2. 拒否理由選択ダイアログが表示される
3. 理由を選択して「拒否する」をクリック
4. 成功メッセージが表示される

## 🐛 よくある問題と解決方法

### 問題1: 画面が真っ白
**原因**: Reactアプリの起動エラー  
**解決**: 
```bash
# コンソールでエラーを確認
開発者ツール > Console

# よくあるエラー:
- Module not found → npm install
- TypeScript error → コード修正
```

### 問題2: 統計データが表示されない
**原因**: API接続エラー  
**解決**:
```bash
# APIサーバーの確認
curl http://localhost:5001/api/moderation/stats

# プロキシ経由の確認
curl http://localhost:3001/api/moderation/stats
```

### 問題3: レビューキューが空
**原因**: テストデータが不足  
**解決**:
```bash
# レビュー待ち投稿を作成
curl -X POST http://localhost:5001/api/posts \
  -H "Content-Type: application/json" \
  -d '{
    "user_id": "test_user",
    "content": "犯人は田中です",
    "manga_title": "推理漫画"
  }'
```

### 問題4: 承認・拒否ボタンが動作しない
**原因**: APIエラーまたはCORS問題  
**解決**:
```javascript
// コンソールでネットワークエラーを確認
// Expected: POST /api/moderation/:id/approve → 200 OK
```

## 📊 期待される画面構成

### ダッシュボード画面
```
┌─────────────────────────────────────────────┐
│ [🔒] AI Moderation                         │
├─────────────────────────────────────────────┤
│ • ダッシュボード                            │
│ • レビューキュー                            │
│ • 分析                                      │
├─────────────────────────────────────────────┤
│ AI監視システム ダッシュボード               │
│                                             │
│ ┌─────────┐ ┌─────────┐ ┌─────────┐      │
│ │承認済み │ │レビュー │ │拒否済み │      │
│ │   3     │ │待ち 1   │ │   1     │      │
│ └─────────┘ └─────────┘ └─────────┘      │
│                                             │
│ システム概要                                │
│ このダッシュボードでは...                   │
└─────────────────────────────────────────────┘
```

### レビューキュー画面  
```
┌─────────────────────────────────────────────┐
│ レビューキュー                              │
│ AI判定でレビューが必要とされた投稿の一覧... │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ 投稿ID: 4          AIスコア: 70.0%      │ │
│ │ ユーザー: demo_user2                    │ │
│ │ 投稿日時: 2025-06-16 02:30              │ │
│ │ 作品: 推理漫画 第12話                   │ │
│ │                                         │ │
│ │ 投稿内容:                               │ │
│ │ ネタバレ注意: 犯人は佐藤でした...       │ │
│ │                                         │ │
│ │ 検出されたリスク: [ネタバレ]            │ │
│ │                                         │ │
│ │ AI判定理由:                             │ │
│ │ Mock analysis based on keyword...       │ │
│ │                                         │ │
│ │ [承認] [拒否]                           │ │
│ └─────────────────────────────────────────┘ │
└─────────────────────────────────────────────┘
```

## ✅ 動作確認チェックリスト

- [ ] ブラウザで http://localhost:3001/ にアクセス可能
- [ ] サイドバーとナビゲーションが表示される
- [ ] ダッシュボードの統計カードに数値が表示される
- [ ] レビューキューページに投稿カードが表示される
- [ ] 承認ボタンがクリック可能
- [ ] 拒否ボタンで理由選択ダイアログが開く
- [ ] コンソールにエラーが表示されない
- [ ] ネットワークタブでAPI通信が成功している

すべてチェックできれば、フロントエンドは正常に動作しています！