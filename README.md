# TakumiPay Smart Contracts — Monad Metropolis Hackathon 2026

> **Treasury, Settlement & Merchant Payment Contracts for Monad (EVM)**  
> *Production-grade UUPS proxy architecture supporting Agora AUSD remittance and sub-second merchant settlements.*

- **Team:** Planckify Labs
- **Track Entered:** Track 02 — Consumer Products & Payments
- **Primary Contracts:** `evm/src/TakumiPay.sol` (UUPS Proxy 2.1.0), `evm/src/MockAUSD.sol`
- **License:** [GNU General Public License v3.0 (GPLv3)](./LICENSE)

---

## Monad On-Chain Deployments

TakumiPay contracts are deployed and configured on both **Monad Mainnet** (real Agora AUSD settlement) and **Monad Testnet** (open-mint MockAUSD for merchant verification).

### 1. Monad Mainnet (`chainId: 143`) — Production Remittance Rail

| Contract / Role | Address / Hash | Explorer |
|---|---|---|
| **TakumiPay Proxy (UUPS)** | [`0x479B0843C3e0627f36551660506dEd5b349Fa968`](https://monadvision.com/address/0x479B0843C3e0627f36551660506dEd5b349Fa968) | [View on MonadVision](https://monadvision.com/address/0x479B0843C3e0627f36551660506dEd5b349Fa968) |
| **Implementation** | `0x1aC593085Fa34c651E805085da4b2cabAC676F99` | Implementation Logic |
| **Proxy Deploy Tx** | `0x0c50d974055f91c9b093d45026d4ab214f7b0f67e30627976f8bc66f6128f8c7` | Verified broadcast |
| **Implementation Deploy Tx** | `0x051d16f8b67b71945231f82550060a565496883a02f95404e5c4152b01f83525` | Verified broadcast |
| **Allowed Payment Token** | Agora AUSD: [`0x00000000eFE302BEAA2b3e6e1b18d08D69a9012a`](https://monadvision.com/address/0x00000000eFE302BEAA2b3e6e1b18d08D69a9012a) | Real AUSD (6 decimals) |
| **Enable AUSD Tx** | `0x8d12ec7d42afd22e9f436a0832fb1814ea047f7e7cf9dbcdd7b6feafbc37d0a2` | `addAllowedPaymentToken` |
| **Backend Signer** | `0x299E4E56e9F05A21414A62479DA1514C20aA61e8` | Quote signature verification |
| **Withdrawal Delay** | `86400` seconds (24h) | Timelocked treasury defense |

Deployment record: [`evm/deployments/143.json`](./evm/deployments/143.json)

---

### 2. Monad Testnet (`chainId: 10143`) — QRIS Merchant Spend Verification Rail

| Contract / Role | Address / Hash | Explorer |
|---|---|---|
| **TakumiPay Proxy (UUPS)** | [`0x9EEC5aD4FC092fD468A8114007e541238F4Ba5ee`](https://testnet.monadvision.com/address/0x9EEC5aD4FC092fD468A8114007e541238F4Ba5ee) | [View on Testnet Explorer](https://testnet.monadvision.com/address/0x9EEC5aD4FC092fD468A8114007e541238F4Ba5ee) |
| **Implementation** | `0xbB074ED383dA5C99756D72b62f7Fdff97A8c9022` | Implementation Logic |
| **Proxy Deploy Tx** | `0x6eed45f5b5bac2652706f8f7bd765887dd278d8df0a54edd1476f8578b4386d6` | Verified broadcast |
| **Implementation Deploy Tx** | `0x76b3f2c44af2fd9ba31cb9d81eb2f79eb316d2effbc5e2d04649c718c3234e0e` | Verified broadcast |
| **Open-Mint MockAUSD** | [`0x1aC593085Fa34c651E805085da4b2cabAC676F99`](https://testnet.monadvision.com/address/0x1aC593085Fa34c651E805085da4b2cabAC676F99) | Stand-in (6 decimals) |
| **MockAUSD Deploy Tx** | `0xdca51260a5709ccbadbd39f86dbd2e7ef6046647d9ff2e3a64882dacf1f4aa01` | Deploy Mock token |
| **MockAUSD Initial Mint Tx**| `0x2f1fc4a16acd3deca75e40f3695421799a46bb807d2b52fa028398f434726605` | 1M AUSD demo mint |

Deployment record: [`evm/deployments/10143.json`](./evm/deployments/10143.json)

---

## Repository Layout

- **`evm/` (Monad Focus):** Solidity implementation built with Foundry. Contains UUPS upgradeable proxies, EIP-712 merchant quote verification, `MockAUSD.sol`, Foundry scripts, and test suites.
- **`solana/`, `stellar/`, `sui/`:** Counterpart implementations retained to document TakumiPay's multi-chain architecture without modifying original commit history.

---

## Originality & Build Window Disclosure (Section 4.1 #4)

- **Pre-Existing Foundation (Prior to September 1, 2026):** Multi-chain contract architecture and core payment interface specifications.
- **Built & Deployed During Hackathon (September 16 – September 19, 2026):**
  - EVM Foundry configuration and Monad RPC endpoint integration (`evm/foundry.toml`).
  - `MockAUSD.sol` open-mint testnet token to allow unconstrained consumer payment testing on Monad Testnet (`evm/src/MockAUSD.sol`, `evm/script/DeployMockAUSD.s.sol`).
  - Deployments of TakumiPay 2.1.0 to Monad Mainnet (`143`) and Monad Testnet (`10143`) with AUSD allowlisting and sweep cap governance.
- **AI Tools Disclosure:** Contract tests and documentation drafted with the assistance of Claude and Gemini.

---

## Verification & Testing (Foundry)

```bash
cd evm

# Install Foundry dependencies
forge install

# Run all unit and integration tests
forge test

# Run tests with gas report
forge test --gas-report
```

---

## License

This project is licensed under the [GNU General Public License v3.0 (GPLv3)](./LICENSE).
