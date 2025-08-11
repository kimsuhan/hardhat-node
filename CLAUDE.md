# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview
This is a comprehensive Ethereum smart contract development template featuring:
- **Backend**: Hardhat with Ignition deployment system
- **Frontend**: Next.js 15 block explorer for local network interaction
- **Full-stack integration**: TypeScript throughout, ethers.js for blockchain interaction

## Development Commands

### Smart Contract Development
- `npm run compile` - Compile smart contracts
- `npm test` - Run all tests
- `npx hardhat test test/Lock.ts` - Run specific test file
- `REPORT_GAS=true npm test` - Run tests with detailed gas reporting
- `npx hardhat coverage` - Generate coverage report

### Local Blockchain
- `npm run node` - Start local Hardhat node (required for frontend)
- `npm run deploy:local` - Deploy all contracts to local network
- `npx hardhat ignition deploy ./ignition/modules/Lock.ts --network localhost` - Deploy specific module

### Frontend Block Explorer
- `cd front-end && npm run dev` - Start Next.js development server (requires running Hardhat node)
- `cd front-end && npm run build` - Build production frontend
- `cd front-end && npm run lint` - Lint frontend code

### Network Operations
- `npx hardhat ignition deploy ./ignition/modules/Lock.ts --network sepolia` - Deploy to testnet
- `npx hardhat verify CONTRACT_ADDRESS --network sepolia` - Verify contract on Etherscan

## Architecture

### Smart Contract Layer (Root Directory)
- **Contracts**: `contracts/Lock.sol` - Sample timelock contract with withdrawal mechanism
- **Tests**: `test/Lock.ts` - Comprehensive test suite using fixtures and time manipulation
- **Deployment**: `ignition/modules/Lock.ts` - Ignition deployment configuration with parameters
- **Types**: `typechain-types/` - Auto-generated TypeScript bindings for type-safe contract interaction

### Frontend Layer (`front-end/`)
Full-featured blockchain explorer built with Next.js 15 and ethers.js:
- **Dashboard**: Real-time network stats, latest blocks, gas prices
- **Block Explorer**: Browse all blocks with pagination, detailed block information
- **Transaction Explorer**: View transaction details, gas usage, status
- **Account Explorer**: Check balances and transaction history
- **Auto-refresh**: Real-time data updates every 10 seconds

### Key Integration Patterns
- **Web3 Connection**: `front-end/src/lib/web3.ts` - Centralized ethers.js provider and utility functions
- **Type Safety**: Shared TypeScript interfaces between contract types and frontend
- **Local Development**: Frontend connects to localhost:8545 (Hardhat node)
- **Error Handling**: Comprehensive error states and retry mechanisms

### Testing Strategy
- **Contract Testing**: Uses `loadFixture` for efficient test setup and state snapshots
- **Time Manipulation**: Advanced testing with `time.increaseTo()` for time-dependent contracts
- **Event Testing**: Verification of emitted events with specific parameters
- **Balance Testing**: ETH transfer validation with `changeEtherBalances`
- **Revert Testing**: Custom error messages and revert conditions

### Deployment Architecture
- **Modular Deployments**: Hardhat Ignition for reproducible deployments
- **Parameter Management**: External parameter configuration support
- **Multi-Network**: Support for local, testnet, and mainnet with environment-based configuration
- **Gas Optimization**: Built-in gas reporting with external API integration

### Network Configuration
- **Local Development**: Hardhat network with 3-second block intervals
- **Local Node**: localhost:8545 with chainId 31337
- **Testnet**: Sepolia configuration with environment variable support
- **Gas Reporting**: Configurable with CoinMarketCap and Etherscan API integration