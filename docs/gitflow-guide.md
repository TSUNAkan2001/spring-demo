# 開発フローガイド（Git Flow運用）

このプロジェクトでは **Git Flow** をベースにしたブランチ運用を採用します。  
目的は「安定したリリース」と「開発中の変更を安全に管理」することです。

---

## 🚀 ブランチ構成

| ブランチ名 | 用途 | 作成タイミング |
|-------------|------|----------------|
| `main` | 本番リリース済みコード | リリース時のみマージ |
| `develop` | 開発中の最新コード | 常に存在（基幹開発ブランチ） |
| `feature/*` | 新機能・改修用ブランチ | 機能ごとに `develop` から作成 |
| `release/*` | リリース準備用ブランチ | リリース前に `develop` から作成 |
| `hotfix/*` | 緊急修正用ブランチ | 本番障害発生時に `main` から作成 |

---

## 🧩 ブランチ命名ルール

| 種別 | 命名例 | 内容 |
|------|---------|------|
| feature | `feature/login-api` | ログインAPI機能の追加 |
| fix | `fix/user-validation` | ユーザバリデーション修正 |
| release | `release/v1.0.0` | バージョン1.0.0のリリース準備 |
| hotfix | `hotfix/typo` | 緊急修正（例：タイプミス） |

---

## 💻 開発の流れ

1. **developからブランチ作成**
   ```bash
   git checkout develop
   git pull
   git checkout -b feature/〇〇
ローカルで開発・コミット

bash
コードをコピーする
git add .
git commit -m "add: 機能概要を記述"
リモートにブランチをプッシュ

bash
コードをコピーする
git push -u origin feature/〇〇
Pull Requestを作成

feature/〇〇 → develop へPRを出す

レビューを通してマージ

リリース準備時

bash
コードをコピーする
git checkout develop
git checkout -b release/v1.0.0
git push -u origin release/v1.0.0
テスト・ドキュメント整備完了後、main にマージ。

本番リリース後

main → develop にもマージして整合性を保つ。

🧱 コミットメッセージ規則（推奨）
プレフィックス	意味
add:	新規機能追加
fix:	バグ修正
update:	機能改善・仕様変更
remove:	不要コード削除
docs:	ドキュメント修正
refactor:	リファクタリング

例：

bash
コードをコピーする
git commit -m "add: ユーザ登録APIを実装"
git commit -m "fix: バリデーションロジック修正"
🧹 その他運用ルール
直接 main にコミットしない

コードレビューは最低1名以上が担当

バージョンタグは vX.Y.Z 形式で付与

必要に応じて README や CHANGELOG を更新

📦 コマンド早見表
操作	コマンド例
新機能ブランチ作成	git checkout -b feature/〇〇 develop
ブランチ一覧	git branch -a
最新を反映	git pull origin develop
ブランチ削除	git branch -d feature/〇〇
リモートブランチ削除	git push origin --delete feature/〇〇