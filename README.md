# BSC Lottery System

A decentralized lottery smart contract deployed on Binance Smart Chain (BSC). This contract enables transparent and trustless lottery functionality where participants can enter by sending BNB, and winners are selected through a verifiable random process.

## Overview

The Lottery contract implements a simple yet secure lottery mechanism on BSC. Players contribute BNB to enter the lottery pool, and the contract manager can trigger a winner selection that distributes the entire pool to a randomly selected participant.

## Features

- **Transparent Operations**: All lottery entries and winner selections are recorded on-chain
- **Secure Random Selection**: Winner selection uses on-chain randomness based on block properties
- **Manager Controls**: Designated manager can initiate winner selection
- **Minimum Entry**: Enforces a minimum entry amount (0.01 BNB) to prevent spam
- **Automatic Pool Management**: Winner receives the entire pool balance automatically

## Contract Details

### State Variables

- `manager`: Address of the contract owner who can pick winners
- `players`: Array of addresses that have entered the current lottery round

### Functions

- `enter()`: Allows users to enter the lottery by sending BNB (minimum 0.01 BNB)
- `pickWinner()`: Manager-only function that selects a random winner and transfers the pool
- `getPlayers()`: Returns the list of all current participants
- `balanceInPool()`: Returns the current balance of the lottery pool

## Prerequisites

- Node.js (v12 or higher)
- npm or yarn
- Truffle framework
- A BSC-compatible wallet (MetaMask recommended)
- BNB for deployment and testing (testnet BNB for testnet deployment)

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd BSC-lottery-system
```

2. Install dependencies:
```bash
npm install
```

3. Configure your deployment settings in `truffle-config.js`:
   - Add your mnemonic phrase (keep this secure!)
   - Adjust network settings if needed

## Deployment

### Local Development

1. Start a local blockchain (Ganache or similar):
```bash
# Using Ganache CLI
ganache-cli
```

2. Deploy to local network:
```bash
truffle migrate --network development
```

### BSC Testnet

1. Ensure your wallet has testnet BNB from the [BSC Testnet Faucet](https://testnet.binance.org/faucet-smart)

2. Deploy to testnet:
```bash
truffle migrate --network testnet
```

### BSC Mainnet

⚠️ **Warning**: Only deploy to mainnet after thorough testing. Ensure you have sufficient BNB for gas fees.

```bash
truffle migrate --network bsc
```

## Usage

### Interacting with the Contract

After deployment, you'll receive the contract address. You can interact with it using:

1. **Truffle Console**:
```bash
truffle console --network testnet
```

2. **Web3.js or Ethers.js** in your frontend application

3. **Remix IDE** (connect to BSC via MetaMask)

### Example Interactions

**Enter the lottery:**
```javascript
// Send transaction with at least 0.01 BNB
await lottery.enter({ value: web3.utils.toWei('0.02', 'ether') });
```

**Check pool balance:**
```javascript
const balance = await lottery.balanceInPool();
console.log(web3.utils.fromWei(balance, 'ether'), 'BNB');
```

**Get all players:**
```javascript
const players = await lottery.getPlayers();
console.log('Current players:', players);
```

**Pick winner (manager only):**
```javascript
await lottery.pickWinner();
```

## Security Considerations

- The random number generation uses block properties which can be somewhat predictable. For production use, consider integrating Chainlink VRF for true randomness.
- The manager has sole control over winner selection. Ensure the manager address is secure and trusted.
- Always test thoroughly on testnet before mainnet deployment.
- Review and audit the contract code before handling significant funds.

## Network Configuration

The project is configured for:
- **Development**: Local blockchain (port 8545)
- **Testnet**: BSC Testnet (network ID: 97)
- **Mainnet**: BSC Mainnet (network ID: 56)

## Project Structure

```
BSC-lottery-system/
├── contracts/
│   ├── Lottery.sol          # Main lottery contract
│   └── Migrations.sol        # Truffle migration contract
├── migrations/
│   ├── 1_initial_migration.js
│   └── 2_deployed_contracts.js
├── build/                    # Compiled contracts (auto-generated)
├── truffle-config.js         # Truffle configuration
└── package.json
```

## Development

### Compiling Contracts

```bash
truffle compile
```

### Running Tests

Currently, no test suite is configured. To add tests:

1. Create test files in the `test/` directory
2. Use Truffle's testing framework or Mocha/Chai
3. Run tests with: `truffle test`

## License

ISC

## Author

bilal kilnaz

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## Disclaimer

This software is provided as-is. Use at your own risk. Always conduct thorough testing and security audits before deploying to mainnet with real funds.

