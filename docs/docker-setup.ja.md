# Docker / Podman セットアップ

[🇺🇸 English](docker-setup.md)

## 前提条件

- **Docker Engine 24 以上**（Docker Compose v2 同梱）、または
- **Podman 4 以上** と `podman-compose`

## クイックスタート

<!-- textlint-disable -->

```bash
# Clone the repository
git clone https://github.com/tqer39/openclaw-ops.git
cd openclaw-ops

# Copy the example environment file
cp .env.example .env

# Edit .env and set your API keys
vi .env

# Start the gateway
docker compose up -d
```

<!-- textlint-enable -->

## Linux Mint での Podman セットアップ

### Podman と podman-compose のインストール

<!-- textlint-disable -->

```bash
sudo apt update
sudo apt install -y podman podman-compose
```

<!-- textlint-enable -->

### Rootless 設定

<!-- textlint-disable -->

```bash
# Verify subuid/subgid entries exist for your user
grep "$USER" /etc/subuid
grep "$USER" /etc/subgid

# Enable lingering so containers survive logout
loginctl enable-linger "$USER"
```

<!-- textlint-enable -->

### Podman で起動

<!-- textlint-disable -->

```bash
podman-compose up -d
```

<!-- textlint-enable -->

## ソースからのビルド

OpenClaw イメージをローカルでビルドする場合は以下の手順で行います。

<!-- textlint-disable -->

```bash
# Clone the main OpenClaw repository
git clone https://github.com/openclaw/openclaw.git
cd openclaw

# Build the image
docker build -t openclaw:local .

# Return to openclaw-ops and start services
cd ../openclaw-ops
docker compose up -d
```

<!-- textlint-enable -->

## CLI セットアップ（オンボーディング）

CLI プロファイルを使ってオンボーディングウィザードを実行します。

<!-- textlint-disable -->

```bash
docker compose run --rm openclaw-cli
```

<!-- textlint-enable -->

## サービスの停止

<!-- textlint-disable -->

```bash
docker compose down
```

<!-- textlint-enable -->

## トラブルシューティング

### ポートが使用中の場合

`.env` でポートマッピングを変更してください。

<!-- textlint-disable -->

```bash
OPENCLAW_GATEWAY_PORT=28789
OPENCLAW_BRIDGE_PORT=28790
```

<!-- textlint-enable -->

### ボリュームのパーミッションエラー

マウント先のディレクトリが存在し、書き込み可能であることを確認してください。

<!-- textlint-disable -->

```bash
mkdir -p .openclaw workspace
```

<!-- textlint-enable -->

### Podman: Rootless コンテナが起動しない場合

<!-- textlint-disable -->

subuid/subgid の設定を確認してください。

```bash
podman system migrate
podman info --format '{{.Host.IDMappings}}'
```

<!-- textlint-enable -->
