# 🪨 OGG Node — TAR Package Setup

Portable cave package. Everything included. No Docker Hub needed.

Good for exchanges, validators, private infrastructure, airgapped setups, and custom deployments.

**Package includes:**
- Docker setup
- Genesis block
- Bootnodes
- Startup scripts
- RPC configuration

---

## 📋 Requirements

| Requirement | Minimum |
|---|---|
| OS | Ubuntu 20.04 / 22.04 / 24.04 |
| RAM | 8 GB |
| CPU | 4 cores |
| Disk | 100 GB SSD |
| Docker | 20.x or higher |

---

## 1️⃣ Download Package

Get the latest release directly on your server.

**Browse all releases:**
```
https://github.com/Oggcoin/Ogg-Node/releases/latest
```

**Download with wget:**
```bash
wget https://github.com/Oggcoin/Ogg-Node/releases/latest/download/ogg-node-docker.tar.gz
```

**Or with curl:**
```bash
curl -L -O https://github.com/Oggcoin/Ogg-Node/releases/latest/download/ogg-node-docker.tar.gz
```

**Or upload manually from your machine:**
```bash
# SCP
scp ogg-node-docker.tar.gz root@YOUR_SERVER_IP:/root/

# Windows users — WinSCP or FileZilla works fine
```

---

## 2️⃣ Extract Package

```bash
cd /root
tar -xzf ogg-node-docker.tar.gz
cd ogg-node
```

Cave unpacked. Ready to build.

---

## 3️⃣ Install Docker

If Docker is not yet on your server:

```bash
sudo apt update
sudo apt install -y docker.io docker-compose-plugin
sudo systemctl enable docker
sudo systemctl start docker
```

Verify Docker is running:

```bash
docker --version
```

---

## 4️⃣ Build Ogg Node Image

Build local Docker image from the package files:

```bash
docker compose build
```

> First build takes a few minutes. Ogg preparing the tools.

---

## 5️⃣ Start Ogg Full Node

Run node in background:

```bash
docker compose up -d
```

Node alive. Cave open.

---

## 6️⃣ Check Logs

```bash
docker logs -f ogg-node
```

Healthy startup looks like this:

```
genesis initialized
RPC opened on 18545
peers connected
blocks syncing
```

> Press `CTRL + C` to exit log view. Node keeps running.

---

## 7️⃣ Check RPC

Confirm RPC is alive and responding:

```bash
curl -s http://127.0.0.1:18545 \
-H "Content-Type: application/json" \
--data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'
```

Expected response:

```json
{"jsonrpc":"2.0","id":1,"result":"0xf8"}
```

JSON response means RPC is working. Node is ready.

---

## 8️⃣ Check Peers and Sync

Open node console:

```bash
docker exec -it ogg-node /app/ogg-node attach http://127.0.0.1:18545
```

Run inside console:

```javascript
net.peerCount
eth.blockNumber
eth.syncing
```

**Healthy node:**

| Check | Expected |
|---|---|
| `net.peerCount` | `> 0` — peers found |
| `eth.blockNumber` | `> 0` — blocks arriving |
| `eth.syncing` | `false` — fully synced |

> If `eth.syncing` still shows progress — node is catching up. Let it finish.

Exit console:

```javascript
exit
```

---

## 9️⃣ Stop / Start / Restart

```bash
# Stop
docker compose down

# Start
docker compose up -d

# Restart
docker compose restart
```

---

## 🔄 Rebuild After Update

When a new package version is released:

```bash
docker compose down
docker compose build --no-cache
docker compose up -d
```

---

## 🪨 Useful Commands

| Action | Command |
|---|---|
| View logs | `docker logs -f ogg-node` |
| Running containers | `docker ps` |
| Check RPC | `curl http://127.0.0.1:18545` |
| Stop node | `docker compose down` |
| Restart node | `docker compose restart` |
| Rebuild image | `docker compose build --no-cache` |

---

## ✅ Node Ready Checklist

```
Package downloaded      ✓
Docker installed        ✓
Image built             ✓
Node running            ✓
RPC alive               ✓
Peers connected         ✓
Chain syncing           ✓
```

Cave connected. Rock is ready.

---

## 🔗 Links

| | |
|---|---|
| 🌐 Website | https://oggcoin.org |
| 📖 Docs | https://oggcoin.gitbook.io/the-book-of-ogg |
| ⛏️ Mining Pool | https://pool.oggcoin.org |
| 💬 Telegram | https://t.me/proveyouogg |
| 🐦 Twitter/X | https://x.com/oggcave |
| 🎮 Discord | https://discord.gg/VrBQz7upZb |

---

🪨 **Node running. Chain syncing. Cave connected.**
