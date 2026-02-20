# 📋 Agent Guidelines

[🇯🇵 日本語版](docs/AGENTS.ja.md)

## 🎯 Introduction

Always prefer simplicity over pathological correctness. YAGNI, KISS, DRY. No backward-compat shims or fallback paths unless they come free without adding cyclomatic complexity.

## 📁 Project Overview

openclaw-ops is the configuration and operations repository for OpenClaw. It manages CI/CD workflows, linting configurations, and development tooling.

## 🔧 Development Commands

| Command | Description |
| --- | --- |
| `prek run -a` | ✅ Run all CI checks |
| `pre-commit run --all-files` | ✅ Run all pre-commit hooks locally |

## 📂 Directory Structure

```text
/
├── .github/
│   ├── workflows/          # GitHub Actions workflows
│   ├── CODEOWNERS
│   ├── PULL_REQUEST_TEMPLATE.md
│   ├── auto_assign.yml     # Auto-assign reviewers
│   ├── copilot-instructions.md
│   └── labeler.yml         # PR auto-labeling rules
├── docs/
│   ├── AGENTS.ja.md            # Agent guidelines (Japanese)
│   ├── README.ja.md            # Project introduction (Japanese)
│   ├── docker-setup.md         # Docker/Podman setup guide
│   └── docker-setup.ja.md      # Docker/Podman setup guide (Japanese)
├── AGENTS.md                   # Agent guidelines (English)
├── CLAUDE.md                   # Claude Code instructions
├── README.md                   # Project introduction (English)
├── docker-compose.yml          # Docker Compose configuration
├── .env.example                # Environment variable template
├── biome.json                  # Biome config
├── cspell.json                 # Spell checker dictionary
├── renovate.json5              # Dependency update config
├── .markdownlint.json          # Markdown lint rules
├── .pre-commit-config.yaml     # Pre-commit hooks
├── .textlintrc                 # Japanese text lint rules
└── .gitignore
```

## 🔒 GitHub Secrets

| Secret | Workflow | Description |
| --- | --- | --- |
| `OPENAI_API_KEY` | generate-pr-description | OpenAI API key for PR title/description generation |
| `GHA_APP_ID` | update-license-year | GitHub App ID for automated commits |
| `GHA_APP_PRIVATE_KEY` | update-license-year | GitHub App private key for automated commits |

## ⚡ Key Technical Decisions

| Category | Tool |
| --- | --- |
| CI/CD | prek |
| Code Formatting | Biome (JSON), Prettier (YAML) |
| Markdown Lint | markdownlint-cli2 |
| Japanese Text Lint | textlint with SmartHR preset |
| Spell Check | cspell |
| Shell Lint | ShellCheck |
| Pre-commit Hooks | pre-commit |
| Dependency Updates | Renovate |
| PR Description | OpenAI GPT-4o |
