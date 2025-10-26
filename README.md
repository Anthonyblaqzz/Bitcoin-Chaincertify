# CarbonTrack - Carbon Credits NFT Platform

A transparent blockchain-based platform for tracking, trading, and retiring carbon credits as NFTs on the Stacks blockchain.

## Overview

CarbonTrack is a Clarity smart contract that enables the creation, management, and trading of carbon credits as Non-Fungible Tokens (NFTs). The platform provides a transparent marketplace for carbon credits with built-in verification, certification, and retirement mechanisms.

## Features

- **NFT-Based Carbon Credits**: Each carbon credit is represented as a unique NFT with verifiable data
- **Certification System**: Only verified certification bodies can mint credits
- **Transparent Marketplace**: Built-in buying and selling functionality with platform fees
- **Credit Retirement**: Permanent retirement of carbon credits with proof mechanism
- **User Statistics**: Track ownership, sales, retirements, and purchases
- **Environmental Impact Tracking**: Monitor total minted, retired, and sold carbon credits

## Project Structure

```
.
├── contracts/
│   └── carbon-track-contract.clar    # Main smart contract
├── tests/
│   └── carbon-track-contract.test.ts # Test suite
├── settings/
│   ├── Devnet.toml                   # Development network config
│   ├── Mainnet.toml                  # Mainnet configuration
│   └── Testnet.toml                  # Testnet configuration
├── Clarinet.toml                     # Clarinet project configuration
├── package.json                      # Node.js dependencies
├── tsconfig.json                     # TypeScript configuration
└── vitest.config.js                  # Vitest test configuration
```

## Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) v2.0+
- [Node.js](https://nodejs.org/) v18+
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd bitcoin-chancertify
```

2. Install dependencies:
```bash
npm install
```

## Usage

### Running Tests

Run all tests:
```bash
npm test
```

Run tests with coverage and cost reports:
```bash
npm run test:report
```

Watch mode for development:
```bash
npm run test:watch
```

### Contract Functions

#### Admin Functions

**Verify Certification Body**
```clarity
(verify-certification-body "VeraCert" true)
```

**Set Platform Fee Collector**
```clarity
(set-platform-fee-collector 'ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM)
```

#### Core Functions

**Mint Carbon Credit**
```clarity
(mint-carbon-credit 
    u1000                           ;; 1000 kg CO2
    "Solar Farm Project"            ;; project name
    u"Clean energy initiative"      ;; description
    "VeraCert"                      ;; certification body
    "California, USA"               ;; location
    "Renewable Energy")             ;; project type
```

**Transfer Carbon Credit**
```clarity
(transfer-carbon-credit u1 'ST1SJ3DTE5DN7X54YDH5D64R3BCB6A2AG2ZQ8YPD5)
```

**Retire Carbon Credit**
```clarity
(retire-carbon-credit u1 u"Retired for corporate sustainability goals 2024")
```

**List Carbon Credit for Sale**
```clarity
(list-carbon-credit u1 u1000000)  ;; List for 1 STX
```

**Buy Carbon Credit**
```clarity
(buy-carbon-credit u1)
```

**Unlist Carbon Credit**
```clarity
(unlist-carbon-credit u1)
```

#### Read-Only Functions

```clarity
(get-carbon-nft u1)                    ;; Get NFT details
(get-nft-owner-readonly u1)            ;; Get NFT owner
(get-marketplace-listing u1)           ;; Get listing details
(get-user-stats 'ST1PQHQKV...)        ;; Get user statistics
(get-certification-body "VeraCert")    ;; Get certification body info
(get-total-carbon-minted)              ;; Total carbon minted
(get-total-carbon-retired)             ;; Total carbon retired
(get-total-carbon-sold)                ;; Total carbon sold
(get-total-platform-fees)              ;; Total platform fees
(get-platform-fee-collector)           ;; Fee collector address
(get-nft-counter)                      ;; Current NFT counter
```

## Contract Details

### Constants

- **Error Codes**: u3001-u3012 for various error conditions
- **MIN-CARBON-AMOUNT**: 1 kg CO2 minimum per credit
- **MAX-CARBON-AMOUNT**: 1 billion kg CO2 maximum per credit
- **MIN-LISTING-PRICE**: 0.001 STX minimum listing price
- **MAX-LISTING-PRICE**: 1,000,000 STX maximum listing price
- **PLATFORM-FEE-PERCENTAGE**: 1% (100 basis points)

### Data Structures

The contract uses several maps to store data:

- `carbon-nfts`: NFT details including owner, amount, project info, and retirement status
- `nft-owners`: Quick ownership lookup
- `marketplace-listings`: Active marketplace listings
- `user-stats`: Per-user statistics (owned, sold, retired, purchased)
- `certified-bodies`: Verified certification body registry
- `carbon-transactions`: Transaction history

## Development

### Local Development with Clarinet

Check contracts for errors:
```bash
clarinet check
```

Start a local devnet:
```bash
clarinet devnet start
```

Open Clarinet console:
```bash
clarinet console
```

### Testing

The test suite is located in [tests/carbon-track-contract.test.ts](tests/carbon-track-contract.test.ts) and uses Vitest with the Clarinet SDK.

Example test structure:
```typescript
import { describe, expect, it } from "vitest";

describe("carbon credit tests", () => {
  it("should mint a carbon credit", () => {
    // Test implementation
  });
});
```

## Platform Fees

The platform charges a 1% fee on all marketplace transactions. The fee is automatically deducted from the sale price and transferred to the platform fee collector address.

**Example**:
- Sale Price: 100 STX
- Platform Fee (1%): 1 STX
- Seller Receives: 99 STX

## Security Considerations

- Only verified certification bodies can mint carbon credits
- Carbon credits cannot be transferred or listed once retired
- Only the NFT owner can transfer, list, or retire their credits
- Only the platform fee collector can verify certification bodies
- All transactions are recorded on-chain for transparency

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

ISC

## Contact

For questions and support, please open an issue in the repository.

## Acknowledgments

- Built with [Clarinet](https://github.com/hirosystems/clarinet)
- Powered by [Stacks Blockchain](https://www.stacks.co/)
- Testing with [Vitest](https://vitest.dev/)