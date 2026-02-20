# Docker / Podman Setup

[🇯🇵 日本語版](docker-setup.ja.md)

## Prerequisites

- **Docker Engine 24+** with Docker Compose v2, or
- **Podman 4+** with `podman-compose`

## Quick Start

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

## Podman on Linux Mint

### Install Podman and podman-compose

```bash
sudo apt update
sudo apt install -y podman podman-compose
```

### Rootless Setup

```bash
# Verify subuid/subgid entries exist for your user
grep "$USER" /etc/subuid
grep "$USER" /etc/subgid

# Enable lingering so containers survive logout
loginctl enable-linger "$USER"
```

### Run with Podman

```bash
podman-compose up -d
```

## Building from Source

If you need to build the OpenClaw image locally:

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

## CLI Setup (Onboarding)

Run the onboarding wizard using the CLI profile:

```bash
docker compose run --rm openclaw-cli
```

## Stopping Services

```bash
docker compose down
```

## Troubleshooting

### Port Already in Use

Change the port mappings in `.env`:

```bash
OPENCLAW_GATEWAY_PORT=28789
OPENCLAW_BRIDGE_PORT=28790
```

### Permission Denied on Volumes

Ensure the mounted directories exist and are writable:

```bash
mkdir -p .openclaw workspace
```

### Podman: Rootless Container Fails to Start

Verify your subuid/subgid configuration:

```bash
podman system migrate
podman info --format '{{.Host.IDMappings}}'
```
