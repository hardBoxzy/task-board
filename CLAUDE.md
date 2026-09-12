# CLAUDE.md

このファイルは、Claude Code がこのリポジトリで作業する際のガイドラインです。

## プロジェクト概要

React製のシンプルなタスクボードアプリ。

- テキスト入力でタスクを追加
- チェックボックスで完了・未完了を切り替え
- タスクを削除
- 完了済みタスクはグレー表示
- タスクは `localStorage` に保存され、リロードしても消えない

## デプロイ先

https://hardboxzy.github.io/task-board/

- `main` ブランチへの push をトリガーに GitHub Actions（[.github/workflows/deploy.yml](.github/workflows/deploy.yml)）が自動でビルド・デプロイする。
- GitHub リポジトリの Settings > Pages > Source は「GitHub Actions」に設定済み。

## 技術スタック

- React 19
- Vite 8（ビルドツール・開発サーバー）
- プレーンCSS（App.css / index.css、CSSフレームワークは未使用）
- oxlint（Lint）
- TypeScriptは未導入（`.jsx` + `@types/react` による型補完のみ）
- パッケージマネージャ: npm

## コンポーネントの命名規約

- コンポーネントファイルは `PascalCase.jsx`（例: `App.jsx`）。1ファイル1コンポーネントを基本とする。
- 関数・変数は `camelCase`。イベントハンドラは「動詞 + 対象」で命名する（例: `addTask`, `toggleTask`, `deleteTask`）。`handleXxx` のような接頭辞は使わない。
- state は用途がわかる名詞（`tasks`, `text`）、setter はReactの `useState` の慣例通り `setTasks` のように対応させる。
- CSSクラス名は `kebab-case`。BEM風に「ブロック要素」を `-` でつなぐ（例: `task-form`, `task-list`, `task-label`, `task-text`, `delete-button`）。状態は既存クラスに追加するモディファイアクラスで表す（例: 完了済みタスクは `task completed`）。

## Git 運用ルール

- **コードに変更を加えるたびに、変更内容をコミットし、GitHub にプッシュすること。**
  - 作業を溜め込まず、意味のある単位（1つの機能追加・修正など）ごとに commit → push を行う。
  - コミットメッセージは変更内容が分かるように簡潔に記載する。
  - push 前に `git status` で意図しないファイルが含まれていないか確認する。
  - force push（`--force`）や履歴を書き換える操作は、明示的な指示がない限り行わない。

## 開発時の注意事項

- 破壊的な操作（ファイル削除、`git reset --hard` など）を行う前は、必ずユーザーに確認する。
- 秘匿情報（APIキー、パスワードなど）を含むファイルはコミットしない。
