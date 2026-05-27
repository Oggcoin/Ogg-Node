# 🪨 OGG Node — Linux Binary Setup

Native Linux node. No Docker needed. Just download, extract, and run.

Good for solo miners, exchanges, validators, and custom deployments.

**Package includes:**
- `egem` — Oggchain node binary
- `genesis.json` — Genesis block
- `static-nodes.json` — Bootnodes (auto-connect)
- `start.sh` — Startup script

---

## 📋 Requirements

| Requirement | Minimum |
|---|---|
| OS | Ubuntu 20.04 / 22.04 / 24.04 |
| RAM | 4 GB |
| CPU | 2 cores |
| Disk | 100 GB SSD |
| Ports | 18545 (RPC), 30303 (P2P) |

---

## 1️⃣ Download Package

Get the latest release directly on your server:

```bash
wget https://github.com/Oggcoin/Ogg-Node/releases/latest/download/ogg-node-linux-amd64.tar.gz
```

Or with curl:
```bash
curl -L -O https://github.com/Oggcoin/Ogg-Node/releases/latest/download/ogg-node-linux-amd64.tar.gz
```

---

## 2️⃣ Extract Package

```bash
tar -xzf ogg-node-linux-amd64.tar.gz
cd ogg-release
chmod +x egem start.sh
```

---

## 3️⃣ Start Node

### Solo Miner

Set your wallet address and start:

```bash
export WALLET=0xYourWalletAddress
./start.sh
```

Mining rewards go directly to your wallet. No pool needed.

### Full Node / Exchange (No Mining)

Start without setting a wallet:

```bash
./start.sh
```

Node will sync and expose RPC on port `18545`. No mining will run.

---

## 4️⃣ Run in Background

To keep node running after closing terminal:

```bash
export WALLET=0xYourWalletAddress
nohup ./start.sh > ogg-node.log 2>&1 &
echo $! > ogg-node.pid
```

View logs:
```bash
tail -f ogg-node.log
```

Stop background node:
```bash
kill $(cat ogg-node.pid)
```

---

## 5️⃣ Check Sync Status

```bash
curl -s -X POST http://localhost:18545 \
  -H "Content-Type: application/json" \
  --data '{"jsonrpc":"2.0","method":"eth_syncing","params":[],"id":1}'
```

Returns `false` when fully synced.

---

## 6️⃣ Check Block Number

```bash
curl -s -X POST http://localhost:18545 \
  -H "Content-Type: application/json" \
  --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'
```

---

## 7️⃣ Check Connected Peers

```bash
curl -s -X POST http://localhost:18545 \
  -H "Content-Type: application/json" \
  --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":1}'
```

`0x2` means 2 peers connected. Node is healthy.

---

## ✅ Node Ready Checklist

```
Package downloaded      ✓
Binary extracted        ✓
WALLET set (if mining)  ✓
Node running            ✓
RPC alive               ✓
Peers connected         ✓
Chain syncing           ✓
```

---

## 🪨 Useful Commands

| Action | Command |
|---|---|
| Start with mining | `export WALLET=0xYour... && ./start.sh` |
| Start full node | `./start.sh` |
| View logs | `tail -f ogg-node.log` |
| Check peers | `curl -s -X POST http://localhost:18545 -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":1}'` |
| Check block | `curl -s -X POST http://localhost:18545 -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'` |
| Stop node | `kill $(cat ogg-node.pid)` |

---

## 🔗 Links

| | |
|---|---|
| 🌐 Website | https://oggcoin.org |
| 📖 Docs | https://oggcoin.gitbook.io/the-book-of-ogg |
| ⛏️ Mining Pool | https://pool.oggcoin.org |
| 💬 Telegram | https://t.me/proveyouogg |
| 🐦 Twitter/X | https://x.com/oggchain |
| 🎮 Discord | https://discord.gg/VrBQz7upZb |

---

🪨 **Node running. Chain syncing. Cave connected.**
