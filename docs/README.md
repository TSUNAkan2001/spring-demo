# 🌿 Git Flow 運用ルール（Spring Boot プロジェクト）

## 🚀 ブランチ構成



main
├─ develop
│ ├─ feature/xxxx # 新機能追加
│ ├─ fix/xxxx # 不具合修正
│ ├─ refactor/xxxx # リファクタリング
│ └─ docs/xxxx # ドキュメント更新
├─ release/xxxx # リリース準備
└─ hotfix/xxxx # 緊急修正


---

## 🧩 各ブランチの役割

| ブランチ名 | 役割 | 作成元 | マージ先 |
|:--|:--|:--|:--|
| **main** | 本番リリース済みコード（安定版） | release / hotfix | - |
| **develop** | 開発統合ブランチ（最新の開発状態） | main | main |
| **feature/*** | 新機能開発用 | develop | develop |
| **fix/*** | バグ修正用（開発中） | develop | develop |
| **release/*** | リリース直前テスト用 | develop | main |
| **hotfix/*** | 本番緊急修正 | main | main / develop |

---

## 🧭 開発の流れ

### ① 新機能追加
```bash
git checkout develop
git pull
git checkout -b feature/add-login
# コード修正
git add .
git commit -m "Add login feature"
git push -u origin feature/add-login


→ GitHubでPR（Pull Request）を作成し、developへマージ。

② リリース準備
git checkout develop
git pull
git checkout -b release/v1.0.0
# テストやバージョン更新
git add .
git commit -m "Prepare release v1.0.0"
git push -u origin release/v1.0.0


→ GitHubでrelease/v1.0.0 → mainへPR
→ マージ後にリリースタグを作成。

③ 緊急修正（本番環境の不具合対応）
git checkout main
git pull
git checkout -b hotfix/fix-login-bug
# 修正
git add .
git commit -m "Fix login bug"
git push -u origin hotfix/fix-login-bug


→ GitHubでhotfix → mainとdevelopにマージ。

📘 命名規則
種別	命名例	意味
feature	feature/add-user-api	新機能追加
fix	fix/user-validation	バグ修正
refactor	refactor/db-layer	構造改善
docs	docs/readme-update	ドキュメント更新
release	release/v1.0.0	リリース準備
hotfix	hotfix/fix-login-error	緊急修正
🔖 コミットメッセージ規則（任意）
[カテゴリ] 内容


例：

[add] implement user registration API
[fix] correct null pointer on login
[refactor] split controller into service layer
[docs] update project README

🧠 Tips

develop ブランチは常に最新の開発状態を保つ

main には「本番リリース済み」コードのみを置く

feature/fix ブランチは作業が終わったら削除

タグ（v1.0.0など） をリリース時に付けると管理が楽

💬 よく使うコマンド一覧
操作	コマンド
ブランチ一覧	git branch -a
新規ブランチ作成	git checkout -b feature/xxxx
現在のブランチ確認	git status
リモート反映	git push -u origin feature/xxxx
マージ（例: developへ）	git checkout develop && git merge feature/xxxx
不要ブランチ削除	git branch -d feature/xxxx
リモートブランチ削除	git push origin --delete feature/xxxx
✅ 運用ポイント

PR（Pull Request）でレビューを必ず通す

main への直接 push は禁止（PR経由でのみ反映）

バージョン番号は release/vX.Y.Z 形式で管理

コミットメッセージは英語 or 一貫した書式で統一


---

## 🧩 手順③：GitHubに反映

保存したらターミナルで👇：

```bash
git add README.md
git commit -m "Add Git Flow README"
git push


更新日:2025-10-19