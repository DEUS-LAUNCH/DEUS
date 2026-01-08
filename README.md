# Token Launchpad

A Solana token launchpad built with Meteora's Dynamic Bonding Curve SDK. Launch tokens with automatic liquidity and fair pricing.

## Features

- 🚀 One-click token creation with bonding curve
- 📈 Real-time price charts via Jupiter/TradingView
- 💱 Multiple quote token support (SOL, ZEC, USD1, etc.)
- 💬 Token chat rooms with WebSocket
- 👤 Wallet profiles and trading history
- 📊 Platform statistics and leaderboards
- 🎨 Modern dark UI with responsive design

## Prerequisites

- Node.js 18+
- Solana wallet with SOL for fees
- Pinata account for IPFS uploads
- Meteora DBC config keys (from Meteora Studio)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/token-launchpad.git
cd token-launchpad
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
```bash
cp .env.example .env
# Edit .env with your values
```

4. Set up configs.json:
```bash
cp configs.example.json configs.json
# Add your Meteora DBC config public keys
```

5. Create required directories:
```bash
mkdir -p uploads vanity image_cache
```

6. Start the server:
```bash
npm start
```

## Configuration

### Environment Variables (.env)

| Variable | Description | Required |
|----------|-------------|----------|
| `PINATA_JWT` | Pinata JWT for IPFS uploads | Yes |
| `WALLET_SECRET` | Base58 encoded wallet private key | Yes |
| `SOLANA_RPC_URL` | Solana RPC endpoint | Yes |
| `ADMIN_WALLET` | Admin wallet public key | No |
| `PORT` | Server port (default: 3000) | No |

### Bonding Curve Configs (configs.json)

Create bonding curve configurations in [Meteora Studio](https://studio.meteora.ag/) and add the config public keys to `configs.json`:

```json
{
    "SOL": "your_sol_config_pubkey",
    "ZEC": "your_zec_config_pubkey"
}
```

### Vanity Keypairs

Pre-generate Solana keypairs and place them in the `vanity/` directory. Each token launch consumes one keypair.

## Project Structure

```
├── server.js          # Express backend
├── public/
│   └── index.html     # Frontend SPA
├── configs.json       # Meteora DBC configs
├── db.json           # LowDB database
├── vanity/           # Pre-generated keypairs
├── uploads/          # Temporary file uploads
└── image_cache/      # Cached token images
```

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/create` | POST | Create new token |
| `/sign-and-send` | POST | Sign and broadcast tx |
| `/all-tokens` | GET | List all tokens |
| `/tokens` | GET | List tokens by deployer |
| `/platform-stats` | GET | Platform statistics |
| `/api/comments/:mint` | GET/POST | Token comments |

## Deployment

### Render.com

1. Create a new Web Service
2. Connect your GitHub repo
3. Set environment variables
4. Add a persistent disk at `/data`
5. Deploy

### Self-hosted

```bash
# Production
NODE_ENV=production npm start

# With PM2
pm2 start server.js --name launchpad
```

## Tech Stack

- **Backend**: Express.js, LowDB, WebSocket
- **Frontend**: Vanilla JS, TailwindCSS-inspired
- **Blockchain**: @solana/web3.js, Meteora DBC SDK
- **Storage**: Pinata IPFS, LowDB JSON
- **Charts**: Lightweight Charts, Jupiter Data API

## License

MIT

## Disclaimer

This software is provided as-is. Always audit smart contracts and test thoroughly on devnet before mainnet deployment. Not financial advice.
