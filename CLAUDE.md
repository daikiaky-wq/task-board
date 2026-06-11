# CLAUDE.md — Task Board Project

## プロジェクト概要

Vite + React で構築したタスク管理ボードアプリケーション。

### デプロイ先

**https://daikiaky-wq.github.io/task-board/**

`main` ブランチへの push で GitHub Actions が自動ビルド＆デプロイする。

### 技術スタック

| 種別 | 技術 | バージョン |
|------|------|-----------|
| UI ライブラリ | React | 18 |
| ビルドツール | Vite | 8 |
| スタイリング | CSS (vanilla) | — |
| CI/CD | GitHub Actions | — |
| ホスティング | GitHub Pages | — |
| 状態永続化 | localStorage | ブラウザ標準 |

### 起動方法
```
npm install
npm run dev   # 開発サーバー (http://localhost:5173)
npm run build # プロダクションビルド → dist/
npm run preview # ビルド成果物をローカルでプレビュー
```

### ファイル構成

```
src/
  main.jsx      # エントリーポイント
  App.jsx       # ルートコンポーネント（状態管理・ロジック）
  App.css       # App コンポーネントのスタイル
  index.css     # グローバルスタイル（body, リセット）
.github/
  workflows/
    deploy.yml  # GitHub Pages 自動デプロイワークフロー
```

### コンポーネント命名規約

- **コンポーネントファイル名・関数名**: PascalCase（例: `TaskItem.jsx`, `export default function TaskItem`）
- **CSS クラス名**: kebab-case（例: `.task-item`, `.add-btn`, `.delete-btn`）
- **props・変数名**: camelCase（例: `onToggle`, `isCompleted`）
- **定数**: UPPER_SNAKE_CASE（例: `STORAGE_KEY`）
- **コンポーネントは 1 ファイル 1 コンポーネント** を原則とする
- **ファイル配置**: `src/components/` 配下にコンポーネントを置く（現在は App.jsx に集約）

---

## Git 運用ルール

### コード変更のたびに GitHub へプッシュする

コードを変更した場合、以下の手順を **必ず毎回** 実行すること。

1. 変更内容を確認する
   ```
   git status
   git diff
   ```
2. 関連ファイルをステージングする（機密ファイルを含めないこと）
   ```
   git add <対象ファイル>
   ```
3. 変更内容を端的に表すコミットメッセージでコミットする
   ```
   git commit -m "変更内容の説明"
   ```
4. GitHub へプッシュする
   ```
   git push origin <ブランチ名>
   ```

> コード変更後にプッシュを省略することは禁止。必ず push まで完了させること。

### ブランチ戦略

- `main` ブランチは常にデプロイ可能な状態を維持する
- 機能追加・バグ修正は feature ブランチで作業し、PR を通じて `main` へマージする
  - ブランチ名例: `feature/add-task-filter`, `fix/drag-drop-bug`
- `main` への直接プッシュは原則禁止

### コミットメッセージ規則

- 日本語・英語どちらでもよい
- 変更の「何を」「なぜ」が伝わる内容にする
- 形式例:
  - `feat: タスクのドラッグ&ドロップ機能を追加`
  - `fix: 完了タスクが消えないバグを修正`
  - `refactor: タスクカードコンポーネントを分割`

---

## コーディング規則

- コメントは WHY が自明でない箇所のみ記載する（WHAT の説明は不要）
- 不要な後方互換コードや未使用変数は削除する
- セキュリティ上の脆弱性（XSS, SQLインジェクション等）を導入しない

---

## 作業フロー

1. タスクを着手前に明確にする
2. 実装 → テスト → コミット → **プッシュ** の順で進める
3. UI 変更はブラウザで動作確認してから完了とする
