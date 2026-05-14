<div align="center">
  <a href="https://particle.network/">
    <img src="https://i.imgur.com/xmdzXU4.png" />
  </a>
  <h3>
    Particle Connect — Solana Demo
  </h3>
</div>

This example demonstrates integrating social and Web3 wallet logins on the **Solana mainnet** using [Particle Connect](https://developers.particle.network/api-reference/connect/desktop/web). Once connected, users can view their balances, send SOL and USDC, sign messages, and browse their recent transaction history.

## Features

- Connect via social logins (Google, Twitter, etc.) or injected wallets (Phantom, OKX, Coinbase, Trust, BitKeep)
- Display wallet address, chain ID, SOL balance, and mainnet USDC balance
- Send SOL (`SystemProgram.transfer` with compute budget priority fee)
- Send USDC (SPL token transfer; automatically creates the recipient's Associated Token Account if it doesn't exist)
- Sign an arbitrary message
- View the last 10 transaction signatures with timestamps and Solana Explorer links

## Built with

- [Particle Connect](https://developers.particle.network/api-reference/connect/desktop/web) (`@particle-network/connectkit` v2)
- [Next.js 14](https://nextjs.org/) (App Router) + React 18 + TypeScript
- [`@solana/web3.js`](https://solana-labs.github.io/solana-web3.js/) + [`@solana/spl-token`](https://spl.solana.com/token)
- [Tailwind CSS](https://tailwindcss.com/) + shadcn/ui component primitives

> **Note:** The app connects to **Solana mainnet** by default. Real funds are used for any transactions you send.

## About Particle Connect

**Particle Connect** provides a unified modal that handles both social logins (via Particle Auth) and standard Web3 wallet connections. It is an all-in-one SDK for end-to-end onboarding and wallet management, making Web3 equally accessible to crypto-native users and newcomers.

Learn more: [Particle Connect docs](https://developers.particle.network/api-reference/connect/desktop/web) | [particle.network](https://particle.network)

## Prerequisites

- **Node.js** v18 or later
- **Yarn** or **npm**
- A [Particle Network dashboard](https://dashboard.particle.network/#/applications) account with a project configured for Solana
- A [WalletConnect Cloud](https://cloud.walletconnect.com/) project ID
- A Solana RPC endpoint (e.g. from [Helius](https://helius.dev/), [QuickNode](https://www.quicknode.com/), or the public endpoint)

## Quickstart

### 1. Clone the repository

```bash
git clone https://github.com/Particle-Network/connect-solana-demo
cd solana-demo
```

### 2. Install dependencies

```bash
yarn
# or
npm install
```

### 3. Set environment variables

Copy the sample file and fill in your values:

```bash
cp .env.sample .env
```

Open `.env` and set each variable:

| Variable | Description |
|---|---|
| `NEXT_PUBLIC_PROJECT_ID` | Your Particle Network **Project ID** from the [dashboard](https://dashboard.particle.network/#/applications) |
| `NEXT_PUBLIC_CLIENT_KEY` | Your Particle Network **Client Key** from the [dashboard](https://dashboard.particle.network/#/applications) |
| `NEXT_PUBLIC_APP_ID` | Your Particle Network **App ID** from the [dashboard](https://dashboard.particle.network/#/applications) |
| `NEXT_PUBLIC_WALLETCONNECT_PROJECT_ID` | Your [WalletConnect Cloud](https://cloud.walletconnect.com/) project ID |
| `NEXT_PUBLIC_SOLANA_RPC_URL` | Your Solana RPC endpoint URL |

### 4. Run the development server

```bash
npm run dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### 5. Build for production

```bash
npm run build
npm run start
# or
yarn build
yarn start
```

## Project structure

```
src/
├── app/
│   ├── actions.ts        # Server action: fetches transaction history via RPC
│   ├── globals.css       # Global styles
│   ├── layout.tsx        # Root layout with ConnectKit provider
│   └── page.tsx          # Main page: balances, send SOL/USDC, sign message
├── components/
│   ├── CopyButton.tsx    # One-click copy to clipboard
│   ├── ExplorerLink.tsx  # Link to Solana Explorer for a transaction
│   ├── Header.tsx        # App header with ConnectButton
│   └── ui/               # shadcn/ui primitives (Button, Card, Input, Label, DropdownMenu)
├── connectkit.tsx         # Particle Connect provider configuration (chains, wallets, RPC)
└── lib/
    └── utils.ts           # Tailwind class merge utility
```

## Deployment

The project deploys to [Vercel](https://vercel.com/) without any additional configuration. After importing the repository, add the same five `NEXT_PUBLIC_*` environment variables in the Vercel project settings before deploying.
