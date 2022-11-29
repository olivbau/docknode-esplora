# Docknode BTC

## Metrics

* `https://yourdomain.com:9100/metrics`
* `https://yourdomain.com:9102/metrics`


## Install 

0. VPS config (optional)
```bash
apt update
apt upgrade
apt install git
# install docker https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository
```

1. Clone the repository and
```bash
git clone https://github.com/olivbau/docknode-btc.git
cd docknode-btc
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
ufw allow ssh
ufw deny 8080
ufw enable
```

4. Run
```bash
curl -o ./aptos/genesis.blob https://raw.githubusercontent.com/aptos-labs/aptos-networks/main/mainnet/genesis.blob
curl -o ./aptos/waypoint.txt https://raw.githubusercontent.com/aptos-labs/aptos-networks/main/mainnet/waypoint.txt
docker compose up -d --pull always
docker logs -f fullnode --since 1m
docker compose down
```