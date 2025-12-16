# OrpheusVPN
![OrpheusVPN CI](https://github.com/SUM-Soft/OrpheusVPN/actions/workflows/ci.yml/badge.svg)

It's a **clean, production-ready VLESS server setup using Docker**, with **automatic updates via Watchtower**.
This setup uses **Xray-core** (recommended for VLESS) and supports **TCP + Reality** (most common today). You can adapt it to WS/TLS if needed.

---

## Prerequisites

* Linux VPS (Ubuntu 20.04+ recommended)
* A domain name (optional but recommended)
* Docker & Docker Compose installed
```bash
curl -fsSL https://get.docker.com | sh
apt install docker-compose -y
```

## Directory Structure
```bash
mkdir -p /opt/orpheus-vpn/logs
cd /opt/orpheus-vpn
```

## Generate UUID & Reality Keys
```bash
docker run --rm teddysun/xray xray uuid
docker run --rm teddysun/xray xray x25519
```
Replace in .env file:
* `your-unique-uuid-here`
* `your-reality-private-key-here`

## Start the Server
```bash
docker-compose up -d
```

## Client VLESS Example (Reality)
```
vless://UUID@SERVER_IP:443?
encryption=none
&flow=xtls-rprx-vision
&security=reality
&sni=SERVER_NAME
&fp=chrome
&pbk=PASSWORD
&sid=a1b2c3
&type=tcp
```

## Firewall (Important)
```bash
ufw allow 443/tcp
ufw allow ssh
ufw enable
```
