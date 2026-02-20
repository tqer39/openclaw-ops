# 📋 エージェントガイドライン

[🇺🇸 English](../AGENTS.md)

## 🎯 はじめに

<!-- textlint-disable -->

Always prefer simplicity over pathological correctness. YAGNI, KISS, DRY. No backward-compat shims or fallback paths unless they come free without adding cyclomatic complexity.

<!-- textlint-enable -->

## 📁 プロジェクト概要

openclaw-ops は OpenClaw の構成・運用リポジトリです。CI/CD ワークフロー、リンター設定、開発ツールを管理しています。

## 🔧 開発コマンド

| コマンド | 説明 |
| --- | --- |
| `prek run -a` | ✅ すべての CI チェックを実行 |
| `pre-commit run --all-files` | ✅ すべての pre-commit フックをローカルで実行 |

## 📂 ディレクトリ構成

```text
/
├── .github/
│   ├── workflows/          # GitHub Actions ワークフロー
│   ├── CODEOWNERS
│   ├── PULL_REQUEST_TEMPLATE.md
│   ├── auto_assign.yml     # レビュワー自動アサイン
│   ├── copilot-instructions.md
│   └── labeler.yml         # PR 自動ラベル付けルール
├── docs/
│   ├── AGENTS.ja.md            # エージェントガイドライン（日本語）
│   ├── README.ja.md            # プロジェクト紹介（日本語）
│   ├── docker-setup.md         # Docker/Podman セットアップガイド
│   └── docker-setup.ja.md      # Docker/Podman セットアップガイド（日本語）
├── AGENTS.md                   # エージェントガイドライン（英語）
├── CLAUDE.md                   # Claude Code 設定
├── README.md                   # プロジェクト紹介（英語）
├── docker-compose.yml          # Docker Compose 設定
├── .env.example                # 環境変数テンプレート
├── biome.json                  # Biome 設定
├── cspell.json                 # スペルチェッカー辞書
├── renovate.json5              # 依存関係更新設定
├── .markdownlint.json          # Markdown リントルール
├── .pre-commit-config.yaml     # pre-commit フック
├── .textlintrc                 # 日本語テキストリントルール
└── .gitignore
```

## 🔒 GitHub Secrets

| シークレット | ワークフロー | 説明 |
| --- | --- | --- |
| `OPENAI_API_KEY` | generate-pr-description | PR タイトル・説明文生成用の OpenAI API キー |
| `GHA_APP_ID` | update-license-year | 自動コミット用の GitHub App ID |
| `GHA_APP_PRIVATE_KEY` | update-license-year | 自動コミット用の GitHub App 秘密鍵 |

## ⚡ 主要な技術選定

| カテゴリ | ツール |
| --- | --- |
| CI/CD | prek |
| コードフォーマッタ | Biome（JSON）、Prettier（YAML） |
| Markdown リント | markdownlint-cli2 |
| 日本語テキストリント | textlint（SmartHR プリセット） |
| スペルチェック | cspell |
| シェルリント | ShellCheck |
| pre-commit フック | pre-commit |
| 依存関係更新 | Renovate |
| PR 説明文生成 | OpenAI GPT-4o |
