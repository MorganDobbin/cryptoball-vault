# CryptoBall Vault - Anonymous Price Prediction Market

A privacy-preserving crypto price prediction market built with FHEVM. Users can submit encrypted price predictions for BTC/ETH, and results are only revealed after the prediction period ends.

## Features

- **FHE Encryption**: All price predictions are encrypted using Fully Homomorphic Encryption
- **Privacy-Preserving**: Individual predictions remain private until finalization
- **On-Chain Aggregation**: Encrypted predictions are aggregated on-chain without decryption
- **Fair Competition**: No copying or cheating - predictions are locked until reveal

## Quick Start

### Prerequisites

- **Node.js**: Version 20 or higher
- **npm**: Package manager

### Installation

1. **Install dependencies**

   ```bash
   npm install
   cd ui && npm install
   ```

2. **Set up environment variables**

   ```bash
   npx hardhat vars set MNEMONIC

   # Set your Infura API key for network access
   npx hardhat vars set INFURA_API_KEY

   # Optional: Set Etherscan API key for contract verification
   npx hardhat vars set ETHERSCAN_API_KEY
   ```

3. **Compile contracts**

   ```bash
   npm run compile
   ```

4. **Run tests**

   ```bash
   # Test on local network (mock FHEVM)
   npm run test

   # Test on Sepolia (after deployment)
   npm run test:sepolia
   ```

5. **Deploy to local network**

   ```bash
   # Terminal 1: Start a local FHEVM-ready node
   npx hardhat node

   # Terminal 2: Deploy to local network
   npx hardhat deploy --network localhost

   # Update contract address in ui/src/abi/CryptoPriceGuessAddresses.ts
   # Set the address for chainId 31337
   ```

6. **Start frontend**

   ```bash
   cd ui
   npm run dev
   ```

7. **Deploy to Sepolia Testnet** (after local testing)

   ```bash
   # Deploy to Sepolia
   npx hardhat deploy --network sepolia

   # Update contract address in ui/src/abi/CryptoPriceGuessAddresses.ts
   # Set the address for chainId 11155111

   # Verify contract on Etherscan
   npx hardhat verify --network sepolia <CONTRACT_ADDRESS>
   ```

## 📁 Project Structure

```
cryptoball-vault/
├── contracts/
│   ├── CryptoPriceGuess.sol  # Main prediction market contract
│   └── FHECounter.sol        # Example FHE counter contract
├── deploy/                    # Deployment scripts
├── test/                      # Test files
│   ├── CryptoPriceGuess.ts   # Local network tests
│   └── CryptoPriceGuessSepolia.ts  # Sepolia testnet tests
├── ui/                        # Frontend React application
│   ├── src/
│   │   ├── abi/               # Contract addresses
│   │   ├── components/        # React components
│   │   ├── hooks/             # Custom hooks (useCryptoPriceGuess)
│   │   └── lib/               # Utilities (wagmi config)
│   └── package.json
├── hardhat.config.ts          # Hardhat configuration
└── package.json               # Dependencies and scripts
```

## 📜 Available Scripts

| Script             | Description              |
| ------------------ | ------------------------ |
| `npm run compile`  | Compile all contracts    |
| `npm run test`     | Run all tests (local)    |
| `npm run test:sepolia` | Run tests on Sepolia  |
| `npm run coverage` | Generate coverage report |
| `npm run lint`     | Run linting checks       |
| `npm run clean`    | Clean build artifacts    |

## 🔐 Contract Functions

### For Users
- `createPredictionEvent()`: Create a new prediction event (admin)
- `submitPrediction()`: Submit an encrypted price prediction
- `getPredictionEvent()`: Get event details
- `hasUserPredicted()`: Check if user has submitted a prediction

### For Admins
- `endPredictionEvent()`: End the prediction period
- `setActualPrice()`: Set the actual price after target date
- `finalizePredictionEvent()`: Decrypt and finalize results

## 🚀 Next Steps

1. **Complete FHE Encryption**: Implement full FHE encryption in the frontend using `@zama-fhe/relayer-sdk`
   - Reference: `quiet-key-cast/frontend/fhevm/useFhevm.tsx`
   - Create `useFhevm` hook similar to reference implementation
   - Integrate encryption in `PredictionModal` component

2. **Update Contract Address**: After deployment, update `ui/src/abi/CryptoPriceGuessAddresses.ts`

3. **Add ABI**: Copy the compiled ABI from `artifacts/contracts/CryptoPriceGuess.sol/CryptoPriceGuess.json` to frontend

4. **Test End-to-End**: 
   - Create a prediction event
   - Submit encrypted predictions
   - End event and finalize results

## 📚 Documentation

- [FHEVM Documentation](https://docs.zama.ai/fhevm)
- [FHEVM Hardhat Setup Guide](https://docs.zama.ai/protocol/solidity-guides/getting-started/setup)
- [FHEVM Testing Guide](https://docs.zama.ai/protocol/solidity-guides/development-guide/hardhat/write_test)
- [FHEVM Hardhat Plugin](https://docs.zama.ai/protocol/solidity-guides/development-guide/hardhat)

## 📄 License

This project is licensed under the BSD-3-Clause-Clear License. See the [LICENSE](LICENSE) file for details.

## 🆘 Support

- **GitHub Issues**: [Report bugs or request features](https://github.com/zama-ai/fhevm/issues)
- **Documentation**: [FHEVM Docs](https://docs.zama.ai)
- **Community**: [Zama Discord](https://discord.gg/zama)

---

**Built with ❤️ by the Zama team**
