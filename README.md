[🇺🇸 English](#english) · [🇨🇳 中文](#chinese)

---

<a name="english"></a>

# ETH Payment

> Generate EIP-681 Ethereum payment links and QR codes for any EVM chain. Zero configuration, instant setup.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)

## Overview

ETH Payment is an OpenClaw skill that generates **EIP-681 compliant payment links** compatible with MetaMask and other Ethereum wallets. No API keys, no servers, no configuration required.

**Perfect for:**
- Payment requests and invoices
- Donation links
- Mobile-friendly checkout
- Any on-chain payment collection

**Supported Networks:** Base · Ethereum · Arbitrum · Optimism · Polygon

## Installation

```bash
openclaw skill install https://github.com/AntalphaAI/eth-payment
```

### Install via ClawHub

```bash
clawhub install evm-payment
```

### Prerequisites

- **Python 3.8+**
- **pip packages** (installed automatically on first use):

```bash
pip install qrcode==1.7.0 pillow==10.3.0
```

## Quick Start

```bash
# Basic ETH payment on Base
eth-payment create --to 0xYourAddress --amount 0.1

# USDC payment with QR code
eth-payment create --to 0xYourAddress --amount 100 --token USDC --qr payment.png

# Specify network
eth-payment create --to 0xYourAddress --amount 10 --token USDC --network ethereum --qr qr.png
```

Or just tell the AI agent:

> "Generate a payment link for 100 USDC on Base to 0x1F3A9A450428BbF161C4C33f10bd7AA1b2599a3e"

## Commands

### `create` — Generate Payment Link

```bash
eth-payment create --to <address> --amount <number> [options]

Required:
  --to <address>      Recipient address (0x...)
  --amount <number>   Amount to request

Options:
  --token <symbol>    Token symbol (default: ETH)
  --network <name>    base | ethereum | arbitrum | optimism | polygon (default: base)
  --qr <path>         Save QR code to file
  --json              Output as JSON
```

### `chains` — List Supported Networks

```bash
eth-payment chains
eth-payment chains --json
```

### `tokens` — List Tokens for a Network

```bash
eth-payment tokens --network base
eth-payment tokens --network ethereum --json
```

### `validate` — Validate Address

```bash
eth-payment validate 0x...
```

## Supported Networks

| Network   | Chain ID | Native Token | ERC-20 Tokens          |
|-----------|----------|--------------|------------------------|
| base      | 8453     | ETH          | USDC, USDT, WETH       |
| ethereum  | 1        | ETH          | USDC, USDT, WETH, DAI  |
| arbitrum  | 42161    | ETH          | USDC, USDT, ARB        |
| optimism  | 10       | ETH          | USDC, OP               |
| polygon   | 137      | MATIC        | USDC, USDT, WETH       |

## Example: Invoice with QR Code

```bash
eth-payment create \
  --to 0x1F3A9A450428BbF161C4C33f10bd7AA1b2599a3e \
  --amount 100 \
  --token USDC \
  --network base \
  --qr invoice_qr.png
```

**JSON output:**

```json
{
  "success": true,
  "network": "base",
  "chain_id": 8453,
  "token": "USDC",
  "recipient": "0x1F3A9A...",
  "amount": "100",
  "links": {
    "eip681": "ethereum:0x833...@8453/transfer?address=0x...&uint256=100000000",
    "metamask": "https://metamask.app.link/send/..."
  }
}
```

## Extending Chains

Add a new EVM chain by editing `config/chains.json`:

```json
{
  "chains": {
    "new-chain": {
      "name": "New Chain",
      "chain_id": 12345,
      "native_token": "NATIVE",
      "tokens": {
        "USDC": {
          "address": "0x...",
          "decimals": 6
        }
      }
    }
  }
}
```

## Security Notes

- This skill **only generates** payment links — it cannot execute transactions
- No private keys or secrets required
- All processing happens locally
- Always verify the recipient address before sharing

## License

MIT — Antalpha AI Team

---

<a name="chinese"></a>

# ETH Payment（以太坊收款）

> 为任意 EVM 链生成符合 EIP-681 标准的以太坊收款链接和二维码。零配置，即装即用。

## 简介

ETH Payment 是一个 OpenClaw 技能，用于生成兼容 MetaMask 和其他以太坊钱包的 **EIP-681 标准收款链接**。无需 API Key，无需服务器，无需任何配置。

**适用场景：**
- 收款请求与发票
- 捐款链接
- 移动端友好的结账流程
- 任何链上收款需求

**支持网络：** Base · Ethereum · Arbitrum · Optimism · Polygon

## 安装

```bash
openclaw skill install https://github.com/AntalphaAI/eth-payment
```

### 通过 ClawHub 安装

```bash
clawhub install evm-payment
```

### 前置依赖

- **Python 3.8+**
- **pip 依赖包**（首次使用时安装）：

```bash
pip install qrcode==1.7.0 pillow==10.3.0
```

## 快速上手

```bash
# 在 Base 网络发起 ETH 收款
eth-payment create --to 0x你的地址 --amount 0.1

# USDC 收款并生成二维码
eth-payment create --to 0x你的地址 --amount 100 --token USDC --qr payment.png

# 指定网络
eth-payment create --to 0x你的地址 --amount 10 --token USDC --network ethereum --qr qr.png
```

也可以直接用自然语言告诉 AI：

> "帮我生成一个收款链接，收 100 USDC，Base 网络，收款地址 0x1F3A9A450428BbF161C4C33f10bd7AA1b2599a3e"

## 命令说明

### `create` — 生成收款链接

```bash
eth-payment create --to <地址> --amount <金额> [选项]

必填参数：
  --to <地址>         收款地址（0x...）
  --amount <金额>     收款金额

可选参数：
  --token <代币>      代币符号（默认：ETH）
  --network <网络>    base | ethereum | arbitrum | optimism | polygon（默认：base）
  --qr <路径>         生成二维码并保存到指定路径
  --json              以 JSON 格式输出
```

### `chains` — 查看支持的网络

```bash
eth-payment chains
eth-payment chains --json
```

### `tokens` — 查看某网络支持的代币

```bash
eth-payment tokens --network base
eth-payment tokens --network ethereum --json
```

### `validate` — 验证地址格式

```bash
eth-payment validate 0x...
```

## 支持网络一览

| 网络      | Chain ID | 原生代币 | 支持的 ERC-20            |
|-----------|----------|----------|--------------------------|
| base      | 8453     | ETH      | USDC, USDT, WETH         |
| ethereum  | 1        | ETH      | USDC, USDT, WETH, DAI    |
| arbitrum  | 42161    | ETH      | USDC, USDT, ARB          |
| optimism  | 10       | ETH      | USDC, OP                 |
| polygon   | 137      | MATIC    | USDC, USDT, WETH         |

## 示例：生成带二维码的发票

```bash
eth-payment create \
  --to 0x1F3A9A450428BbF161C4C33f10bd7AA1b2599a3e \
  --amount 100 \
  --token USDC \
  --network base \
  --qr invoice_qr.png
```

**JSON 输出示例：**

```json
{
  "success": true,
  "network": "base",
  "chain_id": 8453,
  "token": "USDC",
  "recipient": "0x1F3A9A...",
  "amount": "100",
  "links": {
    "eip681": "ethereum:0x833...@8453/transfer?address=0x...&uint256=100000000",
    "metamask": "https://metamask.app.link/send/..."
  }
}
```

## 扩展自定义链

编辑 `config/chains.json` 即可新增任意 EVM 链：

```json
{
  "chains": {
    "new-chain": {
      "name": "New Chain",
      "chain_id": 12345,
      "native_token": "NATIVE",
      "tokens": {
        "USDC": {
          "address": "0x...",
          "decimals": 6
        }
      }
    }
  }
}
```

## 安全说明

- 本技能**仅生成**收款链接，不会执行任何链上交易
- 无需私钥或任何密钥
- 全程本地处理，无数据上传
- 分享前请务必核对收款地址

## License

MIT — Antalpha AI Team
