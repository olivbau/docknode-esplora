# Docknode Esplora

## Metrics

- Esplora: `https://mydomain.com`
- Nodeexporter endpoint: `https://mydomain.com:9100/metrics`

## Install

0. VPS config (optional)

```bash
apt update
apt upgrade -y
apt install -y git ufw
# apt update && apt upgrade -y && apt install -y git
# Install docker: https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository
```

1. Clone the repository

```bash
git clone https://github.com/olivbau/docknode-esplora.git
cd docknode-esplora
```

2. Configure environement variables

```bash
cp .env.example .env

# Generate users passwords for basic auth
docker run --rm caddy:2-alpine caddy hash-password --plaintext 'password'

# Set users and passwords for basic auth
# Set the host
nano .env
```

3. Setup UFW

```bash
sudo ufw allow ssh && sudo ufw allow 8333 && sudo ufw allow https
sudo systemctl enable --now ufw
sudo systemctl status ufw
```

4. Run

```bash
docker compose pull
docker compose up -d
docker logs -f docknode-btc-caddy-1 --since 5m
docker logs -f docknode-btc-esplora-1 --since 5m
docker compose down
```
